---
title: "Centralized Architecture Practices in a Decentralized World"
date: 2025-05-13
categories: [architecture, software]
tags: [facilitating-software-architecture, architecture, software, decentralization]
series: facilitating-software-architecture
author: Lindsey Tibbitts
author_profile: true
excerpt: "Exploring how traditional ivory tower and hands-on architecture approaches struggle in modern decentralized environments, and why architects must surrender control to enable team autonomy."
---

This post is part of a reflection series based on the book *Facilitating Software Architecture* by Andrew Harmel-Law. The interpretations, examples, and opinions shared here are my own, inspired by my takeaways from the book.

---

## Introduction

This chapter explores the experiences organizations face when trying to apply traditional architecture practices to modern software engineering. It outlines two common traditional approaches—ivory tower architecture and hands-on architecture—and details the struggles these models face when applied to today’s fast-paced, decentralized environments. It also touches on the impacts of past software revolutions and begins to outline what’s needed from a new architectural approach that meets today’s demands.

As my team navigates this evolving landscape and works to modernize how we operate, I found this chapter especially relevant. It offers both a mirror to the challenges we are experiencing today and a framework for considering the practices we need to build next.

We are living this reality right now. As our teams become increasingly independent and deliver value to users faster, architects are struggling to keep up using traditional methods. This chapter offers timely insights on why that’s happening and what we might do about it.

---

## Key Takeaways

### 1. What Good Architecture Looks Like
- Coherent, cohesive, and aligned with business value.
- Decoupled in the right ways to enable team independence and adaptability.

### 2. The Flaws of Traditional Practices
- Ivory Tower Architecture – Too far removed from the code and real team dynamics.
- Hands-On Architecture – Overly involved with individual teams, missing the system-wide view.
- Both approaches become bottlenecks.

### 3. The Reality of Decentralization
- Decentralization ≠ Distribution – Simply spreading components across servers isn’t enough.
- True decentralization requires surrendering control.
- It introduces more complexity, but that complexity can be bounded and managed.

### 4. Flow Blockers
- Work and permission couplings slow teams down and block delivery flow.

### 5. The Need for Emergent, Feedback-Driven Architecture
- Architecture must evolve in production, not just in plans.
- We must design for emergent behavior—both strong and weak emergence.

---

## Reflections

### The Challenge of Surrendering Control as an Architect

One idea that really challenged me in this chapter is the notion that architects must surrender control in a decentralized system. It’s easy to agree with that concept on paper, but in practice, it’s incredibly uncomfortable.

As architects, we're often expected to be the ones who “know best” or hold the “big picture answers.” Letting go of that expectation feels risky. It can feel like stepping back from the very thing we are supposed to be accountable for. Surrendering control means trusting that the teams closest to the code know more than we do—and they probably do. It means resisting the urge to review or approve every architectural choice. It means focusing on enabling alignment without dictating implementation.

The reality is, trying to hold control actually creates friction. It slows teams down. It turns architects into bottlenecks. It traps knowledge and responsibility in a single role, instead of spreading it across the organization where it belongs.

Letting go of control doesn’t mean abandoning leadership. It means shifting to stewardship—facilitating the right conversations, setting guardrails, and trusting that the people closest to the work are best positioned to make the detailed decisions.

I’ll admit, this is a muscle I’m still building. But this chapter made me realize that the cost of not surrendering control is far higher than the discomfort of loosening my grip.

---

### Supporting Team Independence in a Post-Acquisition World

Another point that really hit home for me is the idea that good architecture must be decoupled to enable team independence and adaptability. This feels especially relevant given the transitions my organization is currently navigating.

We’ve recently acquired two companies, bringing in new teams, new products, and new ways of working. Each team comes with its own culture, workflows, tooling, and delivery practices. Trying to force a single, uniform architecture or process on all of them would likely stifle their ability to deliver value in the ways that work best for them.

Yet, we still need cohesion. Our systems have to work together. We need shared architectural principles—things like security, reliability, and scalability—without over-prescribing how every team achieves those outcomes.

This is where the concept of bounded complexity resonates with me. If we can set clear boundaries—such as defining ownership areas, APIs, or even separating repositories—we can allow teams to operate independently, while still contributing to a cohesive system. Our role as architects isn’t to control every detail, but to enable this balance between alignment and autonomy.

It’s not easy, especially in a constantly shifting environment. But recognizing this need for both cohesion and independence feels like the real architectural challenge we’re facing—not just technically, but organizationally.

---

## Closing Thoughts

This chapter is important because it outlines where we started, where we are now, how we got here, and why we need to change. It traces the evolution from centralized, control-heavy architecture to the complex, decentralized reality most organizations face today. It shows how once-effective methods—like ivory tower design or hyper-involved oversight—simply don’t scale in the face of modern delivery speed and team autonomy.

More importantly, it calls us to adapt. Software delivery isn’t slowing down—it’s accelerating. Teams are more independent than ever. Clinging to outdated ways of working risks turning architecture itself into a bottleneck.

This chapter sets the stage for thinking differently—shifting from controlling to enabling, from predicting to adapting, and from isolated decision-making to learning through real-world feedback. It’s a reminder that architecture isn’t just about designing systems—it’s about helping organizations evolve alongside them.

---

*Originally published on [LinkedIn](https://www.linkedin.com/pulse/centralized-architecture-practices-decentralized-world-tibbitts-4wucc?trackingId=xIJB2iyWT%2BqphheIxwGzOw%3D%3D&lipi=urn%3Ali%3Apage%3Ad_flagship3_profile_view_base_recent_activity_content_view%3Bl3EtK1K6QJud98JNH1YPFQ%3D%3D).* 