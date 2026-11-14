---
title: "Routing in Micro Frontends — Keeping Independent Apps in Sync"
date: 2025-08-18
categories: [frontend, architecture, software]
tags: [routing, urls, micro-frontends, frontend, architecture, software, navigation]
series: micro-frontends
author: Lindsey Tibbitts
author_profile: true
excerpt: "Routing across multiple independently deployed micro frontends is complex. Learn strategies to keep apps in sync, use URLs as contracts, and support deep linking without creating tight coupling."
---

# 🗺️ Routing in Micro Frontends

> *Routing in a single-page app is already a challenge — in a micro frontend architecture, it becomes a coordination exercise between multiple independently deployed applications.*

---

## 🚦 Why Routing Gets Complicated

In a traditional SPA, there’s one router controlling the entire application. In MFEs, multiple applications may need to respond to navigation events. Without coordination, you risk:

- MFEs losing sync with the container’s navigation state.
- Inconsistent URLs for the same views.
- Broken deep links.

---

## 🏠 The Container App as the Routing Source of Truth

A common pattern is for the **container application** to own routing:

1. Container uses a top-level router (e.g., `<BrowserRouter>` in React).
2. It creates a shared `history` object.
3. This `history` is passed down to MFEs so they can integrate with the container’s routing.

This ensures all MFEs navigate in sync, regardless of their framework.

---

## 🔗 Using the URL as a Communication Contract

The URL is one of the most powerful and underutilized communication channels between MFEs.

**Benefits:**
- Well-defined open standard.
- Globally accessible.
- Limited size encourages small, focused data.
- User-facing → encourages clear structure.
- Declarative → avoids imperative API calls.
- Forces MFEs to communicate indirectly → reducing coupling.

When using routes for communication, the **route structure becomes a contract** between MFEs. Changes to this structure should be treated like API changes.

---

## 📍 Deep Linking & Standalone Loading

MFEs should be able to:
- Load directly to a given route (deep linking).
- Handle their own sub-routes when bootstrapped independently.
- Avoid relying on the container to initialize all state before rendering.

This requires coordination between the container and the MFE’s own router configuration.

---

## 🔐 Authentication & Routing

- The container usually owns authentication routes.
- After login, the container routes the user to the appropriate MFE.
- MFEs should be able to handle 401/403 cases gracefully without breaking navigation.

---

## ⚠️ 404s and Unknown Routes

When MFEs are deployed separately, unknown routes may cause issues:
- **Container-owned 404:** Safer; the container decides.
- **MFE-owned 404:** Only for MFE-specific subpaths.

A hybrid approach is common: container handles root-level unknowns, MFEs handle their own.

---

## 🧩 Nested Routing Scenarios

In some cases, an MFE might itself host another MFE. This requires:
- Sub-route isolation.
- Clear boundaries in the URL structure.
- Avoiding route conflicts.

---

## ⚡ Performance Considerations

Routing can trigger MFE loading — lazy-loading MFEs only when their route is active improves performance.

Example (Module Federation + React):
```jsx
<Route path="/cart" element={<RemoteCart />} />
```
The `RemoteCart` MFE is only fetched when the user navigates to `/cart`.

---

## 🛠 Framework Differences

- **React**: Share `history` from `react-router` or use `MemoryRouter` for isolated MFE routing.
- **Vue**: `vue-router` can be synced via custom events or shared state.
- **Angular**: Use the Angular Router in the container; MFEs subscribe via Angular services.
- **Web Components**: No built-in router — often a lightweight custom router or URL pattern matching is used.

---

## 🧭 Key Takeaways

- Make the container app the source of truth for routing.
- Use URLs as a declarative, user-facing communication mechanism.
- Treat route structures as contracts between MFEs.
- Support deep linking for independent MFE loading.
- Plan for 404s, nested routing, and authentication flows.