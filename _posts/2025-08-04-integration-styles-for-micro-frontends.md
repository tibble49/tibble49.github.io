# 🔄 Integration Styles for Micro Frontends — Build-Time, Runtime, and Beyond

> *Once you’ve defined your micro frontend architecture, the next challenge is figuring out how to stitch those pieces together. There’s no single “right” way — but each integration style comes with tradeoffs you’ll want to understand.*

---

## 🧩 Why Integration Style Matters

Your integration strategy determines:
- **How independently MFEs can be deployed**
- **How tightly or loosely coupled they are**
- **How flexible you are in adopting new technology**
- **Your release cadence**

Pick the wrong one, and you might end up back in monolith land — just with extra steps.

---

## 🛠️ **Build-Time Integration**

**How it works:**  
Each MFE is published as a package (often via NPM). The container app imports it at build time, and the whole product is compiled and deployed together.

**Pros:**
- Simple to set up
- Familiar to most frontend developers
- No runtime orchestration complexity

**Cons:**
- **Lockstep releases** — all MFEs must be rebuilt and redeployed together
- Can reintroduce monolithic dependencies
- Not great for truly independent teams

**Best for:**  
Small teams, low change frequency, or early MFE adoption.

---

## ⚡**Runtime Integration**

**How it works:**  
MFEs are deployed independently and loaded dynamically by the container at runtime. Tools like **Webpack Module Federation** make this possible.

**Pros:**
- Independent deployment and scaling
- No rebuild required to update a single MFE
- Teams can work in different tech stacks

**Cons:**
- More complex setup and infrastructure
- Version mismatches and dependency duplication can cause runtime errors
- Requires careful coordination of shared dependencies

**Best for:**  
Larger teams, high change frequency, long-lived products.

---

## 🌐 **Web Component Integration**

**How it works:**  
MFEs are built as Web Components (Custom Elements, Shadow DOM) and loaded into the container. Any framework — or none — can be used.

**Pros:**
- Framework agnostic
- Strong style and DOM encapsulation
- Easy to drop into any page

**Cons:**
- More boilerplate for state and data passing
- Performance considerations for large apps
- SEO and SSR can be tricky

**Best for:**  
Multi-framework environments or gradual migrations.

---

## 📦 **Iframes (Legacy)**

**How it works:**  
MFEs are embedded as iframes, each fully isolated from the container and each other.

**Pros:**
- Complete isolation — no style or JavaScript conflicts
- Simple to load remote apps

**Cons:**
- Clunky integration
- Limited cross-app communication
- Hard to achieve seamless UX
- Not responsive-friendly

**Best for:**  
Very high-security isolation requirements — otherwise, avoid.

---

## 🗂️ Choosing the Right Integration Style

| Criteria | Build-Time Integration | Runtime (Module Federation) | Web Components | Iframes |
|----------|------------------------|-----------------------------|----------------|---------|
| **Deployment Independence** | ❌ Low — requires rebuild of all MFEs for changes | ✅ High — deploy MFEs individually without container rebuild | ✅ High — deploy components independently | ✅ High — each iframe is fully independent |
| **Performance (Initial Load)** | ✅ Often best — optimized, deduplicated bundles; fast initial load | ✅ Good — lazy-load only what’s needed; shared deps loaded once | ✅ Good — browser-native; encapsulated; small bundles possible | ❌ Poor — loads full external page for each iframe |
| **Performance (Runtime)** | ✅ Predictable | ⚠️ Overhead from dynamic loading; careful dep mgmt needed | ⚠️ Depends on implementation; expensive callbacks can hurt | ❌ Slower due to message passing & rendering overhead |
| **Framework Flexibility** | ❌ Limited — all MFEs must match container’s stack | ✅ High — teams can choose different stacks | ✅ Very high — browser-native, works with any framework | ✅ Very high — complete isolation from host |
| **Isolation** | ❌ Low — styles & scripts can bleed across MFEs | ⚠️ Medium — still need scoped styles | ✅ Strong — Shadow DOM prevents leakage | ✅ Strong — process-level isolation |
| **Complexity** | ✅ Low — simple build pipeline | ⚠️ Medium — requires orchestration tooling & shared dep mgmt | ⚠️ Medium — learning curve for Web Components APIs | ✅ Low — but awkward integration |
| **Best For** | Smaller teams, stable domains, predictable releases | Large teams, frequent releases, mixed stacks | Multi-framework environments, gradual migration | High-security isolation needs only |

---

## 🏎️ Performance Considerations

- **Build-Time Integration**  
  Highly optimized, deduplicated bundles can result in **fast initial load times**. Predictable runtime performance. All MFEs ship together, so bundle size may grow over time if unused code accumulates.

- **Runtime (Module Federation)**  
  Supports **lazy-loading** of MFEs, improving initial load by loading only what’s needed. Shared dependencies can be cached across MFEs. Some **runtime overhead** from dynamic loading; requires careful dependency management to avoid version conflicts.

- **Web Components**  
  Browser-native execution and **Shadow DOM encapsulation** can lead to smaller bundle sizes compared to framework-specific MFEs. Performance can be impacted if **expensive logic** runs inside element lifecycle callbacks. Some features may require polyfills, which can add weight.

- **Iframes**  
  Strong isolation but **slow initial load** due to each iframe loading its own full page and resources. Runtime responsiveness can suffer, and layout integration may cause reflow/repaint overhead.

---

## 💡 My Recommendation

If your goal is **truly independent teams** with **separate deploy cadences**, lean toward **runtime integration** (Module Federation or Web Components).  

If you’re just starting out and want to test the waters, **build-time** might be simpler — just be mindful of the lockstep trap.

---

## 🧭 Coming Up Next

In the next post, we’ll explore **Webpack Module Federation** in depth — including configuration tips, dependency sharing, and avoiding version conflicts.

