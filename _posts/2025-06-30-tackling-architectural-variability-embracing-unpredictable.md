---
title: "Tackling Architectural Variability: Embracing the Unpredictable"
date: 2025-06-30
categories: [architecture, software]
tags: [facilitating-software-architecture, architecture, software, variability, adaptability]
series: facilitating-software-architecture
author: Lindsey Tibbitts
author_profile: true
excerpt: "How to design architectural systems that embrace variability and unpredictability, building resilience and adaptability into your technical decisions and organizational processes."
---

In Chapter 13 of Facilitating Software Architecture, Andrew Harmel-Law digs into one of the core paradoxes of architecture practice: every decision resolves uncertainty—but it also creates more of it. Variability isn’t just a problem to solve. It’s the nature of the work.

> This post is part of a reflection series based on the book Facilitating Software Architecture by Andrew Harmel-Law. The interpretations, examples, and opinions shared here are my own, inspired by my takeaways from the book.

## Architecture Creates and Confronts Variability

Decisions are meant to provide clarity. But in doing so, they open new doors, expose new risks, and shift our understanding of what comes next. That’s not a bug—it’s the essence of software. Unlike manufacturing, where variability is something to eliminate, software depends on it. It’s how we innovate.

But that doesn’t make it easy. Variability increases our cognitive load. It requires constant effort to stay aligned, to communicate across teams, and to adapt as circumstances evolve. The instinct might be to fight it with more planning or tighter design—but that’s a losing battle.

## Smaller Decisions, Faster Feedback

One of the best ways to handle variability is to reduce the size of our decisions. This chapter reinforces that small decisions are easier to validate, easier to course-correct, and easier to learn from.

A few takeaways that hit home for me:

- Walking skeletons (from Steve Freeman): Build the thinnest functional slice and validate early. Catch bad assumptions sooner.
- Small user stories (from Patton and Reinertsen): Reduce variation by making decisions in smaller, right-sized chunks—both from a delivery and business value perspective.
- Batch size matters: The smaller the batch (of decision, of work), the lower the overhead and the higher the clarity.

## Fracture Planes and Decoupling

The chapter also touches on a helpful idea: if a decision feels too big or is blocked, ask “what’s the decision we need to take to be able to take this decision?” That backward step can reveal smaller fracture points—entry paths where work can begin independently or with less risk.

Some fracture planes come from system structure, others from team boundaries or business constraints. Using the advice process to surface these early—especially across teams—helps identify when coordination is needed and when it can be removed altogether.

## Letting Go of Certainty

The drive to make perfect decisions—or to avoid risk—can be paralyzing. But variability means we’ll never be able to guarantee outcomes. The best we can do is shorten the time between making a decision and learning if it worked.

Not every decision will pan out. But when teams are transparent, fast to learn, and supported in updating or walking back decisions, that becomes a strength—not a failure. I appreciate how this chapter reframes architectural missteps as valuable signals rather than embarrassing miscalculations.

## Closing Thoughts

This chapter really made me rethink how I approach architectural decisions. I’ve spent a lot of time trying to "get it right" up front—but that’s rarely how things work out. Software is unpredictable, and that’s not a flaw. It’s just reality.

What matters more is how we handle that unpredictability. If we keep our decisions small, stay open to feedback, and make it easy to adjust course, we give ourselves room to grow without breaking everything in the process. That kind of flexibility feels a lot more valuable than chasing certainty.

## What’s Next?

Chapter 14 continues the theme, exploring Variability and the Interconnectedness of Decisions. It will look at how individual architectural decisions interact and ripple through systems over time.

---

*Originally published on [LinkedIn](https://www.linkedin.com/pulse/tackling-architectural-variability-embracing-lindsey-tibbitts-cpo9c?trackingId=xIJB2iyWT%2BqphheIxwGzOw%3D%3D&lipi=urn%3Ali%3Apage%3Ad_flagship3_profile_view_base_recent_activity_content_view%3Bl3EtK1K6QJud98JNH1YPFQ%3D%3D).* 