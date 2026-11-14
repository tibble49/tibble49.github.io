---
title: "Your Architecture Diagram Can't Stop an AI Agent. A Unit Test Can."
date: 2026-11-09
categories: [architecture, software]
tags: [architecture, software, testing, governance, ci-cd]
series:
author: Lindsey Tibbitts
author_profile: true
excerpt: "With AI coding agents in the loop, an architecture rule that isn't an executable test is only a suggestion. Here's why architecture unit tests belong in your build."
---

## A pull request that looks fine

Picture a pull request from your coding agent. It compiles. The unit tests pass. The feature does what the ticket asked for.

Buried in the diff, a controller now calls the database directly. It skips the service layer that every other controller in the codebase goes through.

Nothing about that change is broken. Plenty of systems are built that way. As Graziano puts it in his [harness guide](https://ainativesoftware.engineering/harness), "None of that is wrong in the abstract, but it's wrong for your system."

A careful reviewer catches it. A tired reviewer on the fifth agent PR of the afternoon might not. Then the next agent session finds that controller, treats it as a pattern, and copies it.

This isn't hypothetical. My team made a version of this mistake three times.

Our web app has a rule about how new features connect to it. Wire one up the wrong way and every user pays for it on every page load, even if they never open that feature. Over about three months, three features were wired up the wrong way. One left pages hanging for about 40 seconds when a dependency stopped responding. One made a page noticeably slow in production. One caused an error on a page that had nothing to do with it.

After the first, we wrote the lesson into code comments. Nothing enforced those comments, so it happened twice more. What stopped it was a rule that fails the build when someone wires a feature up the old way. A coding agent later wrote one of the fixes.

Every one of those changes looked fine. The existing code supported it, and the tests passed. That is exactly the kind of mistake an agent will repeat as readily as a person.

My argument in this post is simple. With coding agents in the loop, an architecture rule that isn't an executable test is only a suggestion.

## Erosion is old. Agents speed it up.

Architecture erosion is the slow drift between the structure a team designed and the structure that actually exists in the code. It isn't new. In 2010, [Passos and colleagues](https://homepages.dcc.ufmg.br/~mtov/pub/2010_ieeesw.pdf) described its causes in *IEEE Software*: "During a system's implementation and evolution, it's common to observe deviations from the defined architecture because of unawareness by developers, conflicting requirements, technical difficulties, and deadline pressures."

Unawareness comes first on that list. A coding agent is unaware by design. It starts each session without the design review, the hallway conversation, or the reason we split that module two years ago. When [Li and colleagues](https://arxiv.org/abs/2103.11392v1) asked practitioners what causes erosion, one answer was "knowledge vaporization," which they attribute mostly to "developer turnover, and poorly documented architectural knowledge." An agent is the extreme case: every session is a new hire.

What an agent does have is the code in front of it. [Brinkman](https://jdriven.com/blog/2026/10/ArchUnit-in-the-Age-of-Agentic-Development) puts it well: "An agent learns a lot from the code that is already there. Unfortunately, that includes the bad parts." One shortcut becomes a pattern, and the pattern spreads at the speed of generation.

Early research points the same way. A 2026 preprint on ["constraint decay"](https://arxiv.org/abs/2605.06445) found that agents "lose 27.28 points on average in assertion pass rates from baseline to fully specified tasks," as structural requirements were added. [Another preprint](https://arxiv.org/abs/2605.02741v1), by Zhu, Tsantalis and Rigby, found that more capable models produced "increasingly bloated and coupled code," and that "neither functional correctness nor detailed prompting mitigates this decay." Both are early work, not settled findings.

To be fair, the picture isn't all bad. A [study accepted at SEAA 2026](https://arxiv.org/html/2606.13298), a peer-reviewed conference, compared 151 open-source repositories with and without agent adoption. Architectural smell counts were essentially unchanged (+1.1%, not statistically significant), while the code itself grew 12.8%. Agents don't automatically wreck a codebase. But they don't know your rules, and they write a lot of code.

## The idea: make the architecture fail the build

The fix is to stop describing the architecture and start testing it. If a controller must not touch persistence, write a test that fails when one does, and run it on every build.

This idea has a name. Ford, Parsons, Kua and Sadalage define it in [*Building Evolutionary Architectures*](https://www.thoughtworks.com/insights/books/building-evolutionaryarchitectures-second-edition): "An architectural fitness function is any mechanism that provides an objective integrity assessment of some architectural characteristic(s)." They also give a one-line version: "Fitness functions are to architecture characteristics as unit tests are to the domain."

An architecture unit test is one kind of fitness function. It's atomic, triggered, static and automated. It checks the code's structure, runs when your tests run, and needs no human to judge the result.

My teams work in .NET, where the tool for this is [ArchUnitNET](https://archunitnet.readthedocs.io/en/latest/guide/). It lets you write architecture rules as ordinary unit tests that run with the rest of your test suite.

Here's the rule from the opening, written as an ArchUnitNET test with xUnit (adapted from the [ArchUnitNET user guide](https://archunitnet.readthedocs.io/en/latest/guide/)):

```csharp
using ArchUnitNET.Domain;
using ArchUnitNET.Fluent;
using ArchUnitNET.Loader;
using ArchUnitNET.xUnit;
using Xunit;
using static ArchUnitNET.Fluent.ArchRuleDefinition;

public class ArchitectureTests
{
    private static readonly Architecture Architecture =
        new ArchLoader().LoadAssemblies(typeof(Program).Assembly).Build();

    private static readonly IObjectProvider<IType> Controllers =
        Types().That().ResideInNamespaceMatching(@"^MyApp\.Controllers(\.|$)").As("Controllers");

    private static readonly IObjectProvider<IType> Persistence =
        Types().That().ResideInNamespaceMatching(@"^MyApp\.Persistence(\.|$)").As("Persistence");

    [Fact]
    public void Controllers_go_through_services()
    {
        IArchRule rule = Types().That().Are(Controllers)
            .Should().NotDependOnAny(Persistence)
            .Because("controllers go through services; only services touch persistence");

        rule.Check(Architecture);
    }
}
```

It reads close to how you'd draw it on a whiteboard. When an agent adds that direct database call, the build fails. The message names the rule, the reason from the `Because` clause, and each offending type and dependency.

Here's what a real ArchUnitNET failure looks like. This output comes from David Ullrich's [example on Production Ready](https://www.production-ready.de/2023/12/10/architecture-refactoring-with-archunitnet-en.html), where a rule keeps a desktop layer from reaching straight into the data layer:

```text
FailedArchRuleException
"Types that are Desktop layer should not depend on Data layer" failed:
    DesktopModule.ViewModels.ProductListViewModel does depend on
    DataModule.ProductRepository
```

Current versions word it slightly differently, but the parts are the same.

Whoever reads it, a person or an agent, knows which rule broke, which type broke it, and what it reached for. Add a `Because` and the reason shows up in the message too.

The same idea works on the front end. Here's a similar rule for a TypeScript web app, written for [dependency-cruiser](https://github.com/sverweij/dependency-cruiser), a dependency checker for JavaScript and TypeScript. UI components may not import the API client directly; they get data through hooks:

```js
// .dependency-cruiser.js
module.exports = {
  forbidden: [
    {
      name: "components-go-through-hooks",
      comment: "Components get data through hooks in src/hooks; only hooks call the API client.",
      severity: "error",
      from: { path: "^src/components/" },
      to: { path: "^src/api/" },
    },
  ],
};
```

Run it as part of the build with `--output-type err-long`, and a component that imports the API client fails the check. The `comment` plays the same role as `Because`: it tells whoever broke the rule why it exists.

These tools exist for most stacks, front end and back end. In .NET there's ArchUnitNET and [NetArchTest](https://github.com/BenMorris/NetArchTest). TypeScript and JavaScript have dependency-cruiser, [ArchUnitTS](https://github.com/LukasNiessen/ArchUnitTS) and [tsarch](https://www.angulararchitects.io/en/blog/architecture-beyond-layers-tsarch-for-ai-agents/). Python has [Import Linter](https://github.com/seddonym/import-linter) and [PyTestArch](https://github.com/zyskarch/pytestarch), and Kotlin has [Konsist](https://github.com/LemonAppDev/konsist). The syntax differs. The idea is the same everywhere.

Those failure messages matter more than they look. I'll come back to them.

## Where this came from

Checking code against its intended architecture is an old research topic. Knodel and Popescu [compared static architecture compliance checking approaches](https://publica.fraunhofer.de/handle/publica/354324) at WICSA in 2007. Passos and colleagues gave an [illustrative overview of static conformance checking](https://homepages.dcc.ufmg.br/~mtov/pub/2010_ieeesw.pdf) in 2010.

The fitness function framing arrived in 2017 with *Building Evolutionary Architectures*. Its authors were blunt about their preference: "We prefer building unit tests to catch architecture violations over using strict development guidelines (with the attendant bureaucratic scolding)."

ArchUnit made that practical. A rule became an ordinary unit test, in the same repo, run by the same test runner as everything else. Thoughtworks put it on the [Technology Radar](https://www.thoughtworks.com/radar/tools/archunit) in 2018, at Assess in May and Trial in November.

The book even has a pre-AI version of our agent problem. IDEs offer to add a missing import, and accepting it can quietly create a dependency cycle. In the authors' words, "Developers are so accustomed to this affordance that they swat it away as a reflex action, never actually paying attention." Swap the developer for an agent and the reflex becomes the default.

## Why it matters more now

Teams working with coding agents have started calling the setup around the agent a harness: the instructions, tools and checks that shape what it produces. Birgitta Böckeler, writing on [martinfowler.com](https://martinfowler.com/articles/harness-engineering.html), splits harness controls into two kinds. Guides steer the agent before it acts. Sensors check what it produced and feed the result back.

Most teams start with guides. They write an AGENTS.md file, a plain-text file of instructions the agent reads at the start of its work, and list the architecture rules there. That helps. Graziano is clear about the limit, though: "An AGENTS.md boundary makes the right choice more likely, but it is still advice the agent can fail to follow." Our code comments were that kind of advice, and they didn't stop the next two mistakes.

An architecture test is a sensor. It doesn't hope the agent remembered. It checks every time, and it gives the same answer every time. The book says it plainly: "principles without enforcement are aspirational rather than governance."

The second reason is the failure message. A developer reads a failing test and works out what to do. An agent does the same, right away, in the same session. So the message turns into a repair instruction.

OpenAI's team leaned into this on an agent-written codebase of about a million lines, built through roughly 1,500 pull requests over five months. They enforced layers with custom linters and structural tests, and wrote in their [harness engineering post](https://openai.com/index/harness-engineering/): "Because the lints are custom, we write the error messages to inject remediation instructions into agent context."

Böckeler saw the same loop at smaller scale with dependency-cruiser. From her [sensors article](https://martinfowler.com/articles/sensors-for-coding-agents.html): "The agent violated the rules a handful of times after I introduced them, and then self-corrected based on dependency-cruiser feedback, so it did help keep my folder concepts."

The third reason is timing. Strict structure used to be something you could put off. The OpenAI post makes the point: "This is the kind of architecture you usually postpone until you have hundreds of engineers. With coding agents, it's an early prerequisite: the constraints are what allows speed without decay or architectural drift."

None of this takes people out of the loop. It moves them. As Böckeler puts it, "A good harness should not necessarily aim to fully eliminate human input, but to direct it to where our input is most important." I'd rather my architects spend review time on design decisions than on spotting a misplaced import.

That isn't abstract for my teams. In one of our own discussions, a reviewer said they had spent more than three hours in a single day on about eight non-trivial pull requests. Each went through several human and AI review passes, and the AI comments had to be triaged by hand. The reviewer said they were becoming a blocker.

We changed two things. Authors now run an AI-assisted self-review before opening a pull request, so the mechanical findings are fixed first, and peer review rotates. In parallel, we moved the checks that don't need judgment into the build: layer direction, forbidden access paths and banned packages. When we piloted those rules, 6 of 19 controllers already broke a boundary we had documented. That suggests these are the cheapest issues to stop catching by eye.

## What architecture tests can't do

Architecture tests are narrow on purpose. They see static structure: which class depends on which, and what lives in which package. They don't judge design quality, runtime behavior, or dependencies created through reflection. Böckeler names the boundary: "tools like this are limited to what is expressible via imports, file names, and folder structure."

So a clean run doesn't mean a good design. An agent can respect every layer and still put business logic in the wrong service.

For those semantic problems, people are exploring LLM-based review alongside deterministic checks. Su and colleagues have an [early preprint](https://www.arxiv.org/pdf/2602.07609) evaluating LLMs at detecting violations of architectural decisions. Gonzalez Bravo and colleagues published a peer-reviewed [LLM framework for Clean Architecture conformance](https://www.mdpi.com/2073-431X/15/10/657) in *Computers* this year. I see these as complements. The test gives a hard yes or no on structure. A model can weigh in on the rest.

Rules can also over-constrain. A rule written for today's design can block a good change tomorrow. [Podlesniuk](https://dev.to/sasha_podles/from-prompts-to-invariants-re-architecting-systems-with-archunit-and-llms-1n50), who uses ArchUnit rules to steer agents, puts it well: "Poorly designed tests can block valid evolution just as easily as they can prevent drift." Rules need owners and a periodic review, like any other code.

And none of this makes AGENTS.md pointless. Good instructions raise the odds the agent gets it right the first time. The test catches it when it doesn't. You want both.

## The open question

Here's what I can't tell you: that architecture tests measurably improve AI-written code. No study I've found compares agents working with and without them. The practitioner reports are encouraging, and Böckeler's self-correcting agent is a good sign. But a few reports aren't evidence.

Two 2026 preprints come close without answering it. In [SmellBench](https://arxiv.org/abs/2605.07001), agents asked to fix architectural smells flagged by a detector resolved at most 31 of 65, and the most aggressive one "introduces 140 new smells" along the way. In [another study](https://arxiv.org/abs/2607.14167), agents recovered from far more failures when the feedback named the allowed alternatives, which is a good sign for well-written failure messages. But its tasks were text games, not code. Neither puts architecture rules in a coding agent's loop.

The gap isn't limited to agents. In their [mapping study](https://doi.org/10.1002/smr.2423) on erosion, Li and colleagues wrote: "More empirical studies are required to investigate the practices of detecting and addressing AEr in industrial settings." (AEr is their abbreviation for architecture erosion.)

So I'd like to invite you to try it. Pick a repo and a handful of small tasks. Run your agent once without architecture rules in its loop and once with them. Count the structural violations that make it into the final diff. If you do, I'd like to hear what you find.

## Further reading

- Ford, Parsons, Kua & Sadalage, [*Building Evolutionary Architectures*](https://www.thoughtworks.com/insights/books/building-evolutionaryarchitectures-second-edition), 2nd ed., O'Reilly, © 2023 (Ch. 2 and Ch. 4)
- [ArchUnitNET User Guide](https://archunitnet.readthedocs.io/en/latest/guide/) (.NET) and [dependency-cruiser](https://github.com/sverweij/dependency-cruiser) (JavaScript and TypeScript)
- Böckeler, ["Harness engineering for coding agent users"](https://martinfowler.com/articles/harness-engineering.html) and ["Maintainability sensors for coding agents"](https://martinfowler.com/articles/sensors-for-coding-agents.html)
- Lopopolo, ["Harness engineering: leveraging Codex in an agent-first world,"](https://openai.com/index/harness-engineering/) OpenAI
- Graziano, ["How to build a harness around your repository"](https://ainativesoftware.engineering/harness)
- Brinkman, ["ArchUnit in the Age of Agentic Development,"](https://jdriven.com/blog/2026/10/ArchUnit-in-the-Age-of-Agentic-Development) JDriven
- Passos, Terra, Valente, Diniz & Mendonça, ["Static Architecture-Conformance Checking: An Illustrative Overview,"](https://homepages.dcc.ufmg.br/~mtov/pub/2010_ieeesw.pdf) *IEEE Software* 27(5), 2010
- Knodel & Popescu, ["A Comparison of Static Architecture Compliance Checking Approaches,"](https://publica.fraunhofer.de/handle/publica/354324) WICSA 2007
- Li, Liang, Soliman & Avgeriou, ["Understanding Software Architecture Erosion: A Systematic Mapping Study,"](https://doi.org/10.1002/smr.2423) *Journal of Software: Evolution and Process*, 2022 ([preprint](https://arxiv.org/abs/2112.10934v2)) and ["Understanding Architecture Erosion: The Practitioners' Perceptive,"](https://arxiv.org/abs/2103.11392v1) ICPC 2021
- Larsen & Moghaddam, ["Mining Architectural Quality Under Agentic AI Adoption,"](https://arxiv.org/html/2606.13298) SEAA 2026
- Gonzalez Bravo et al., ["An Evidence-Based LLM Framework for Expert-Validated Clean Architecture Conformance Assessment,"](https://www.mdpi.com/2073-431X/15/10/657) *Computers*, 2026
- Preprints: Dente, Satriani & Papotti, ["Constraint Decay"](https://arxiv.org/abs/2605.06445); Zhu, Tsantalis & Rigby, ["AI-Generated Smells"](https://arxiv.org/abs/2605.02741v1); Su et al., ["Evaluating LLMs for Detecting Architectural Decision Violations"](https://www.arxiv.org/pdf/2602.07609); Dinu, Mihaescu & Rebedea, ["SmellBench"](https://arxiv.org/abs/2605.07001); Ray & Goyal, ["Structured Feedback Improves Repair in an LLM Agent Loop"](https://arxiv.org/abs/2607.14167)
- Podlesniuk, ["From Prompts to Invariants: Re-architecting Systems with ArchUnit and LLMs"](https://dev.to/sasha_podles/from-prompts-to-invariants-re-architecting-systems-with-archunit-and-llms-1n50)
- [Thoughtworks Technology Radar: ArchUnit](https://www.thoughtworks.com/radar/tools/archunit)
