---
title: "Using Technology Radar for Collective Insight and Better Tech Decisions"
date: 2025-06-10
categories: [architecture, software]
tags: [facilitating-software-architecture, architecture, software, technology-radar, decision-making]
series: facilitating-software-architecture
author: Lindsey Tibbitts
author_profile: true
excerpt: "Leveraging technology radar as a collaborative tool to align technology choices across teams, reduce decision fatigue, and make better-informed architectural decisions."
---

## Introduction

Chapter 11 introduces a practical tool that supports decentralized decision-making and helps organizations align technology choices without enforcing rigid standards: the Technology Radar. This radar offers a structured but flexible way to track what’s being used, what’s being tried, and what’s emerging—all grounded in real organizational context.

> This post is part of a reflection series based on the book Facilitating Software Architecture by Andrew Harmel-Law. The interpretations, examples, and opinions shared here are my own, inspired by my takeaways from the book.

This chapter really landed for me as a bridge between strategy and day-to-day engineering—a way to make collective insight visible, portable, and actionable.

---

## Key Takeaways

### What Is a Technology Radar?

A Technology Radar is a shared, opinionated view of technology trends inside your organization. It typically maps:

- Techniques
- Tools
- Platforms
- Languages & Frameworks

Blips move across four rings:

1. Hold – Use with caution or avoid
2. Assess – Worth exploring
3. Trial – Worth piloting in controlled environments
4. Adopt – Established best practice or sensible default

It’s not about enforcing conformity—it’s about establishing a shared sense of direction.

---

### Why It Works

- It creates sensible defaults: the go-to technologies unless there’s a good reason to diverge.
- It surfaces organizational insight from actual use—not just theory or hype.
- It helps teams make decisions faster by reducing duplicated research.
- It supports distributed decision-making by showing what’s been tried, what failed, and what might be worth exploring.

> “Our radar should reflect reality. If nothing has changed, there’s no need to move anything.”

---

### Keeping the Radar Alive

- Update it every 6 months—enough time to capture change, but frequent enough to stay relevant.
- Treat it as a living reflection of your tech landscape, not a vision document.
- Include internal solutions and all major versions of technology in use—even those you don’t like.
- Acknowledge that disagreement exists; inclusion doesn’t imply endorsement.

Radar blips should reflect reality first, and guidance second.

---

### Link It to the Advice Process and ADRs

- When making a decision, check the radar first.
- If your ADR deviates from the radar, say so explicitly.
- List the default option and explain why it’s not being chosen.
- This focuses conversation and advice on two questions:

1. Why does this decision require deviation?
2. What’s unsuitable about the current defaults?

> “Our decision contradicts the current blips and their position.”

By making this tension explicit, it encourages real learning and discussion, not just quiet divergence.

---

### How to Build a Radar in Practice

Start asynchronously by sweeping what you’re already using:

- Include everything—not just new tools, but old systems, unpopular tech, and multiple versions.
- Don’t sanitize the radar to reflect only “approved” technology—it must show what actually exists.
- Capture sentiment, context, and lessons learned.

In later rounds:

- Expect more techniques to be added as the concept sinks in.
- Use the “Techniques” quadrant to turn past experience into actionable guidance.

Radar maintenance can also feed back into principles, CFRs, and the advice process. It becomes part of your sociotechnical infrastructure.

---

## Reflection and Application

> I’ve seen teams in my organization waste time and energy evaluating tools someone else had already tried—or quietly adopted without saying anything. This chapter reminded me that visibility is a huge part of operating efficiently at scale.
>
> A radar doesn’t just tell people what’s allowed—it helps them understand what’s been learned. One thing that stood out to me is how helpful the radar could be for highlighting internal tools or solutions we’ve already built. It’s way too easy to spin up something new just because we didn’t realize another team had solved a similar problem.
>
> I also like that it gives space to disagree. If a default doesn’t fit, that’s fine—but what matters is that we talk about it and make the reasoning visible. That kind of open conversation helps build trust and keeps us moving in the same general direction.

---

## Closing Thoughts

A Technology Radar doesn’t enforce decisions—it amplifies awareness. It helps everyone move faster by making organizational knowledge visible, and by creating a safe, shared space for deviation and experimentation.

More than a tool, it becomes a cultural artifact—a sign that your organization is serious about collaborative decision-making, shared defaults, and learning out loud.

---

## What’s Next?

Chapter 11, The Art of Deciding, marks the beginning of Part 3: Finding Your Way Through the Decision Landscape. This next chapter promises to zoom in on the practice of decision-making itself—highlighting the nuances of timing, framing, context, and structure that all come into play when we’re navigating tough architectural calls. I'm looking forward to digging into how this next layer builds on the groundwork of decentralization, advice, and documentation.

---

*Originally published on [LinkedIn](https://www.linkedin.com/pulse/using-technology-radar-collective-insight-better-tech-tibbitts-x0ztc?trackingId=xIJB2iyWT%2BqphheIxwGzOw%3D%3D&lipi=urn%3Ali%3Apage%3Ad_flagship3_profile_view_base_recent_activity_content_view%3Bl3EtK1K6QJud98JNH1YPFQ%3D%3D).* 