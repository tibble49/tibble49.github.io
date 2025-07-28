# 🏗️ The Building Blocks of Micro Frontend Architecture

> *Once you’ve decided to adopt micro frontends, the next question is: how do you structure them? This post dives into the core architectural elements that make MFEs work — and the decisions you’ll need to make along the way.*

---

## 🧱 Core Components of a Micro Frontend System

A micro frontend architecture typically involves these key players:

### 1. **Container Application (aka “Shell”)**
The container is the glue — it’s responsible for:
- Rendering shared layout (header, nav, footer)
- Handling routing across MFEs
- Managing authentication, global state, or config
- Orchestrating when and where to load each micro frontend

The container can be implemented using a framework like React or Angular, or be completely vanilla JavaScript depending on your setup.

### 2. **Micro Frontend Applications (MFEs)**
Each MFE is an independently built and deployed app that:
- Owns a bounded context or vertical slice of the product
- Handles its own internal routing, UI, and logic
- May use a different tech stack (React, Vue, etc.)

### 3. **Shared Contracts**
To avoid tight coupling, MFEs and the container communicate through:
- Public APIs
- Custom browser events
- Shared routing structures
- Common design tokens or components (when needed)

---

## 🎯 The Importance of Bounded Contexts

Borrowing from Domain-Driven Design (DDD), micro frontends shine when you apply **bounded contexts** effectively. That means:

- Each team owns a domain — like "Billing" or "User Profile"
- The team is responsible for UX, backend APIs, and everything in between
- No accidental shared state or style leaks

Drawing **thicker lines between responsibilities** reduces the risk of inappropriate coupling and makes the system more maintainable.

---

## 👥 Organizing Teams Around Vertical Slices

Instead of separating teams by layer (e.g., “Frontend Team” and “Backend Team”), MFEs encourage forming **full-stack teams** focused on delivering complete features.

For example:

| Team | Domain | Stack |
|------|--------|-------|
| Team A | Account Settings | React + Node.js |
| Team B | Billing | Vue + Go |
| Team C | Dashboard | Svelte + Python |

This structure aligns development with user-facing outcomes — and naturally supports independent releases.

---

## 🧑‍💼 Governance and Team Coordination

Strong architectural governance doesn’t mean heavy-handed control — it means having the right **conversations, constraints, and cadences** in place.

Here’s what that can look like in a micro frontend setup:

- **Clear boundaries**: Enforce clear domain ownership and avoid accidental overlap.
- **Cohesive design**: Invest in visual consistency via shared UX principles or token systems.
- **Robust CI/CD pipelines**: Validate contracts, check for broken integrations, and enforce test coverage.
- **Cross-functional collaboration**: Regular syncs between platform teams and feature teams foster shared ownership and clarity.
- **Platform team as a hub**:
  - Maintains shared infrastructure and design tokens
  - Enforces best practices
  - Provides long-term strategic direction

💬 *Governance works best when it’s not just “someone else’s job” — but a shared responsibility, facilitated by tooling and relationships.*

---

## 🧩 Composition Styles

There are a few different ways to compose MFEs into a working product. We’ll explore them more in the next post, but at a high level:

- **Build-time integration**: all MFEs compiled into the container
- **Runtime integration**: MFEs loaded dynamically via Module Federation or SystemJS
- **Web components**: MFEs exposed as custom elements
- **Iframes**: isolated but limited legacy option

---

## 🛡️ Cross-Cutting Concerns

You’ll need to decide where to centralize vs. distribute common functionality:

- **Auth**: typically handled by the container
- **Routing**: often container-owned, with shared history passed down
- **Design System / UX Consistency**:
  - Maintaining a cohesive UX across independently built apps is hard.
  - Shared component libraries **can help**, but often introduce complexity, ownership tension, or tight coupling.
  - **Alternatives include**:
    - Centralized design systems (owned by platform teams)
    - Well-documented style guides and design tokens
    - Clear communication and ongoing cross-team collaboration

Case studies from **Spotify, IKEA, and DAZN** show that clearly defined boundaries and shared design systems reduce duplication while supporting autonomy.

---

## 📌 Visual Example

![Micro frontend architecture: Shell to MFE](assets/images/shell-to-mfes.png)

---

## 🧠 Takeaways

- MFEs are not just about code — they’re about **team structure and boundaries**
- A clear contract between container and MFEs is crucial
- Start with a vertical slice + a container, and evolve as needed

---

## 🧭 Coming Up Next

In the next post, we’ll look at **integration strategies** — from build-time bundling to runtime orchestration using tools like Webpack Module Federation.

---