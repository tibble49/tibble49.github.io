---
title: "Making Better Decisions at Scale"
date: 2025-05-18
categories: [architecture, software]
tags: [facilitating-software-architecture, architecture, software, decision-making, scale]
series: facilitating-software-architecture
author: Lindsey Tibbitts
author_profile: true
excerpt: "How organizations can improve decision-making quality as they scale, focusing on reducing decision fatigue, improving information flow, and creating better decision-making structures."
---

## Introduction

In this chapter, the focus shifts from recognizing architectural decisions to something even more challenging—making decisions at scale. While small decisions can often be made in isolation, architectural decisions in large teams and organizations require coordination, clarity, and intent. This chapter explores the messy reality of group decision-making, different decision-making models, and the trade-offs between speed, ownership, and decentralization.

> This post is part of a reflection series based on the book Facilitating Software Architecture by Andrew Harmel-Law. The interpretations, examples, and opinions shared here are my own, inspired by my takeaways from the book.

As my own organization grows and becomes more distributed, this chapter made me reflect on how our decision-making practices either accelerate or hold back our ability to build and ship software effectively.

---

## Key Takeaways

### The Three-Stage Decision Process

All decisions go through three stages:

1. A Decision Is Required – Recognizing that a choice needs to be made.
2. The Decision Happens – Evaluating options and selecting one.
3. The Decision Is Implemented – Putting the decision into practice.

While this sounds simple, stage one is often overlooked. Many teams don't even realize when they're facing a decision, especially when only one option is presented or the need for a decision is hidden in day-to-day work.

---

### Understanding Option-Making

Effective decision-making starts with option-making—the ability to generate, evaluate, and compare alternatives. This includes:

- Uncharted Territory – When no obvious options exist and significant effort is needed to create them.
- Enumerated Options – When several known solutions can be compared.
- Missed Significance – When only one "obvious" option is considered without exploring others.

Unfortunately, many teams never witness this process, especially when architects make decisions privately. This makes the path to architecture feel invisible or inaccessible to developers.

---

### The Complexity of Group Decision-Making

Software development is a team sport, and scaling decisions across teams is hard. The chapter breaks down six models of group decision-making:

#### 1. Autocratic (Centralized)
- One person makes and takes the decision.
- Fast but risks bottlenecks and low buy-in.

#### 2. Delegated
- One person passes the decision to someone else.
- Can improve relevance if delegated wisely.

#### 3. Consultative
- One person makes the decision after seeking input.
- Input can be ignored, but consultation may improve outcomes.

#### 4. Consent
- One person makes the options and the decision.
- The decision must make it through a group that can block in the form of a veto.
- Open to abuse if a person holds the decision hostage with their veto until they get what they want.

#### 5. Democratic (Voting)
- One person presents options, the group votes.
- Can alienate minorities and reduce ownership.

#### 6. Consensus (Fully Decentralized)
- The whole group collaborates on both options and the final decision.
- Most inclusive, but often slow and prone to compromise.

---

### The Trade-off Between Speed and Decentralization

While decentralization brings more voices and better context, it can also slow down decision-making. The more people involved, the longer it tends to take. However, centralized models risk bottlenecks and disengagement.

The ideal decision process would:

- Involve the right people, not all the people.
- Optimize decision rights—who can initiate, make, and take decisions.
- Prioritize trust over excessive documentation or unnecessary approval steps.

---

### Applying This to My Organization

> In my organization, we’ve experienced both ends of this spectrum. Sometimes, decisions get stuck with one person or one team, slowing us down. Other times, we try to involve everyone, but the process becomes overwhelming and slow.
>
> Currently, our architects tend to be bottlenecks because they follow a more traditional process. Part of reading this book is that we have identified that this process isn't working and are looking for something new to try.

---

## Closing Thoughts

This chapter highlights that decentralization is not the goal on its own—the goal is to make good decisions quickly, with the right people involved.

It reminded me that the speed and quality of decisions depend on how we structure our decision-making process, not just who holds the title of "architect". Whether you’re working in a small team or across a large organization, the real challenge is to balance speed, inclusion, and ownership in a way that moves the system forward.

---

## What’s Next?

The next chapter introduces a decentralized and fast approach to decision-making. It builds on the challenges of making decisions at scale by offering a practical model for empowering teams to make better architectural choices without creating bottlenecks.

I’m looking forward to exploring this process and sharing my takeaways and personal understanding of how it might help us balance speed, inclusion, and autonomy in our own decision-making practices.

Stay tuned for Chapter 4: The Architecture Advice Process, coming soon.

---

*Originally published on [LinkedIn](https://www.linkedin.com/pulse/making-better-decisions-scale-lindsey-tibbitts-u5omc?trackingId=xIJB2iyWT%2BqphheIxwGzOw%3D%3D&lipi=urn%3Ali%3Apage%3Ad_flagship3_profile_view_base_recent_activity_content_view%3Bl3EtK1K6QJud98JNH1YPFQ%3D%3D).* 