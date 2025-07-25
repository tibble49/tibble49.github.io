---
title: "Navigating Interconnected Decisions: Embracing Variability"
date: 2025-07-01
categories: [architecture, software]
tags: [facilitating-software-architecture, architecture, software, interconnected-decisions, complexity]
series: facilitating-software-architecture
author: Lindsey Tibbitts
author_profile: true
excerpt: "Strategies for managing the complexity of interconnected architectural decisions, understanding how choices ripple through systems and embracing the variability that emerges."
---

Introduction

Chapter 14 of Facilitating Software Architecture dives deep into something every architect wrestles with: the inescapable and often unpredictable variability that emerges from our decisions—and the interconnections between them.

This post is part of my ongoing reflection series on Andrew Harmel-Law’s book. As always, what I share here reflects my own takeaways, experiences, and reactions to the material.

## Key Takeaways

### Variability Isn’t a Flaw—It’s a Feature

Architectural decisions resolve uncertainty—but they also generate new variability. The chapter emphasizes that software architecture isn’t a path to eliminating variability; it’s a practice for working with it intentionally. Unlike manufacturing, where variability is treated like a defect, software thrives on it. It’s what enables flexibility, adaptability, and innovation.

### Spikes Aren’t Just Research—they’re Architecture Tools

Spikes—time-boxed technical investigations—can offer enormous value by helping teams uncover architectural risk early. They don’t ship product, but they do generate something just as valuable: learning. Done well, they replace speculation with concrete insight and often lead directly into an ADR that captures a decision.

This feedback loop—researching, learning, deciding—is a powerful way to manage interconnected decisions without stalling delivery.

### All Architecture Is Interconnected

The chapter outlines four layers of interconnected architectural decisions:

1. Vision and business model (e.g. product focus, funding)
2. Capabilities and responsibilities (e.g. what each system owns)
3. Subsystem design and ownership (e.g. bounded contexts, team boundaries)
4. Detailed technical decisions

Each layer feeds into the others. And while we may want our decisions to be modular and atomic, the reality is: context matters. Our software—and our decisions—are shaped by prior choices, system boundaries, and even team structure.

### Design for Future Decision-Making

One of the most actionable ideas from this chapter is the goal of designing systems so that future decisions can be made as independently as possible. This makes change easier and risk lower—especially early on, when code is light and teams are still flexible.

Event storming, system context diagrams, and collaborative modeling techniques can help clarify those boundaries early. But it’s not just technical: emotional complexity plays a role too. When advice conversations get heated or unclear, it slows everything down and can erode the trust that makes decentralized architecture work.

## Reflection and Application

The idea that decisions are “in conversation” with each other resonated with me. I've definitely seen a single architecture choice cascade through teams in ways that weren’t obvious at the start. When we treat those moments not as missteps but as invitations to reframe or even revisit earlier decisions, we unlock a healthier and more dynamic architecture culture.

I’m also thinking more about reversibility. The more we delay decisions—or stack them on top of unclear foundations—the harder it becomes to unwind them later. But with tools like spikes, smaller decision scopes, and collaborative framing, we can surface interdependencies earlier and reduce that emotional and technical weight.

## Closing Thoughts

This chapter made it clear: there is no such thing as an isolated architectural decision. Variability is the rule, not the exception—and the best thing we can do is lean into it.

By investing in practices that make learning fast, risk safe, and decisions transparent, we’re not just managing complexity—we’re building resilience.

## What’s Next?

The next chapter, The Transition of Power and Accountability, marks the start of Part 4 and turns our attention to the social side of architecture: how decisions, power, and trust intersect when we share responsibility across teams.

---

*Originally published on [LinkedIn](https://www.linkedin.com/pulse/navigating-interconnected-decisions-embracing-lindsey-tibbitts-ls3dc?trackingId=xIJB2iyWT%2BqphheIxwGzOw%3D%3D&lipi=urn%3Ali%3Apage%3Ad_flagship3_profile_view_base_recent_activity_content_view%3Bl3EtK1K6QJud98JNH1YPFQ%3D%3D).* 