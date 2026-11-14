---
title: "Recognizing Architecturally Significant Decisions"
date: 2025-05-15
categories: [architecture, software]
tags: [facilitating-software-architecture, architecture, software, decision-making]
series: facilitating-software-architecture
author: Lindsey Tibbitts
author_profile: true
excerpt: "Understanding the difference between everyday technical decisions and architecturally significant ones that shape the long-term health of our systems, with practical examples and criteria for identification."
---

This post is part of a reflection series based on the book *Facilitating Software Architecture* by Andrew Harmel-Law. The interpretations, examples, and opinions shared here are my own, inspired by my takeaways from the book.

---

## Introduction

This chapter shifts the conversation from architecture as a high-level concept to something much more tangible—decisions. It argues that architecture is really the accumulation of meaningful decisions made over time. Not all decisions carry the same weight, and recognizing which ones matter most is critical to building systems that deliver business value.

As I continue reflecting on how these concepts apply to my own organization, this chapter stood out because it puts language around something we all experience but rarely stop to define—the difference between everyday technical decisions and the architectural ones that shape the long-term health of our systems.

---

## Key Takeaways

### Architecture Is Decision-Making

At its core, practicing software architecture means working with decisions. Not diagrams. Not job titles. Not tooling. Decisions.

It’s critical that everyone involved—not just architects, but also developers, testers, and product owners—has a shared understanding of what makes a decision architecturally significant, and how these decisions actually come about in practice.

### Not All Decisions Are Architectural

The book makes a great distinction:

- All architectural decisions are technical, but
- Not all technical decisions are architectural.

Andrew Harmel-Law draws on Michael Nygard’s definition, which identifies five criteria for architecturally significant decisions:

1. Structure – How the system is organized and how its parts interact.
2. Non-functional characteristics – Qualities like performance, security, scalability, etc.
3. Dependencies – External systems or components the software relies on but doesn’t control.
4. Interfaces – What your system exposes for other systems or users to consume.
5. Construction techniques – How the system is built, deployed, or operated (e.g., deployment strategies).

### Recognizing Significant Decisions

Examples of architecturally significant decisions include:

- Adding or replacing a major dependency or vendor.
- Changing APIs or interfaces in a way that impacts consumers.
- Introducing new deployment techniques like canary releases or blue-green deployments.
- Making structural changes to where core logic resides or switching design patterns.

### Misconceptions About Significance

The chapter also cautions against false signals of significance:

- Who made the decision doesn’t determine its importance.
- How long the decision took doesn’t determine its impact.
- Even unintentional or implicit decisions can be architecturally significant.

### Impact Is Defined at Deployment

Decisions are only truly significant when they impact production—either by changing how the system gets there or by affecting its behavior once it’s running. Shifting your mindset to "How can we ship this right now?" helps focus attention on what actually moves the system forward.

### Feedback Beats Guesswork

Rather than trying to perfectly predict every architectural outcome, teams should deploy sooner, gather real feedback, and adjust. This mindset prioritizes learning over speculation, which is ultimately more valuable for building resilient, adaptable systems.

---

## Examples of Architectural vs. Non-Architectural Decisions

To make this more practical, I’m adding this section to capture examples from my own context. I’ll continue expanding this list over time as I reflect on real decisions my teams face.

### 🏗️ Architectural Decisions

- Migrating from on-premise hosting to a cloud provider like Azure.
- Introducing an event-driven architecture pattern across services.
- Defining service boundaries and APIs for cross-team integration.

### 🛠️ Non-Architectural Decisions

- Choosing between two date formatting libraries for a single microservice.
- Refactoring variable names to improve readability.
- Selecting a code linter or formatting tool.

### 🚦 Architecturally Significant Decisions

- Replacing our identity provider and updating all authentication flows.
- Rolling out a new deployment pipeline with canary releases.
- Introducing a shared library that multiple teams depend on for core business logic.

---

## Reflection and Application

### Recognizing Decision-Making Gaps in My Own Work

One thing this chapter made me reflect on is how easy it is to miss that we’re making architectural decisions all the time—even when they aren’t called out as such.

I’ve seen teams spend weeks debating minor technical details while overlooking major structural or interface decisions that have long-term impact. This chapter is a great reminder that not all decisions deserve equal attention, and part of our job as architects and tech leads is to help teams recognize which ones really matter.

### Shifting Focus Toward Feedback-Driven Architecture

The call to "stop guessing, start deploying, and learn from the feedback" really stood out to me. It challenges the habit of trying to predict all possible outcomes before we ever ship anything. In practice, no architecture is perfect on paper. We need to test, observe, and adapt based on how the system performs in the real world.

This reinforces the idea that architecture isn’t a static design phase—it’s a continuous learning practice that thrives on feedback from real users and real systems.

---

## Closing Thoughts

This chapter pushes us to get serious about recognizing what really matters in architecture: the decisions we make, whether we name them or not.

It challenges us to stop wasting energy on low-impact choices, to focus on architecturally significant decisions, and to ship smaller, faster, and more often so we can learn and improve as we go.

Moving forward, I hope to bring this mindset into my own work—helping teams focus on what matters, deploy with confidence, and adapt based on what we learn in production.

---

## What’s Next?

The next chapter, Decisions at Scale, moves beyond recognizing individual architectural decisions and focuses on the act of deciding itself. It explores the different approaches teams can take to make decisions, especially as the scale of systems, teams, and organizations grows.

I’m looking forward to continuing this series by sharing my takeaways and personal understanding of what it means to facilitate decision-making at scale—not just as a one-time event, but as an ongoing, collaborative practice.

Stay tuned for Chapter 3: Decisions at Scale, coming soon.

---

*Originally published on [LinkedIn](https://www.linkedin.com/pulse/recognizing-architecturally-significant-decisions-lindsey-tibbitts-enccc?trackingId=xIJB2iyWT%2BqphheIxwGzOw%3D%3D&lipi=urn%3Ali%3Apage%3Ad_flagship3_profile_view_base_recent_activity_content_view%3Bl3EtK1K6QJud98JNH1YPFQ%3D%3D).* 