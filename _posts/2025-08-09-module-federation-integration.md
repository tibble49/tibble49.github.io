# ⚙️ Module Federation: Dynamic Integration for Micro Frontends

> *If micro frontends are the architecture, Module Federation is the mechanism. This post dives into what Webpack Module Federation is, why it’s a game-changer for micro frontends, and how to use it without tying yourself in knots.*

---

## 🧠 What Is Module Federation?

[Webpack Module Federation](https://webpack.js.org/concepts/module-federation/) is a feature introduced in Webpack 5 that allows multiple applications to **share and consume JavaScript modules at runtime** — without needing to bundle them together during build.

It enables:
- **Independent deployment** of each micro frontend
- **Runtime loading** of components and services
- **Shared dependencies** that are cached and reused

Think of it like a package manager — but for the browser, in real time.

---

## 🔗 Host and Remote — The Core Concepts

Module Federation is built around two roles:

| Role   | Purpose                               |
|--------|----------------------------------------|
| **Host**   | The container application that loads others |
| **Remote** | The micro frontend that exposes modules     |

Each remote exposes components or utilities, and the host imports them dynamically at runtime.

---

## 🧩 Example: Basic Webpack Configuration

In a typical setup, your **remote** app defines what it’s exposing in `webpack.config.js`:

```js
// Remote MFE: webpack.config.js
new ModuleFederationPlugin({
  name: 'mfeUser',
  filename: 'remoteEntry.js',
  exposes: {
    './UserCard': './src/UserCard',
  },
  shared: ['react', 'react-dom']
});
```

Then your **host** consumes that remote:

```js
// Host/Container: webpack.config.js
new ModuleFederationPlugin({
  remotes: {
    mfeUser: 'mfeUser@https://mfe-user.example.com/remoteEntry.js',
  },
  shared: ['react', 'react-dom']
});
```

Then in code:

```js
import UserCard from 'mfeUser/UserCard';
```

Boom — runtime-loaded micro frontend.

---

## ⚙️ What If You're Using Vite?

Module Federation can be used in Vite via [`vite-plugin-federation`](https://github.com/originjs/vite-plugin-federation) or [`module-federation/vite`](https://github.com/module-federation/vite).

Here’s a quick look at how to set it up.

### Remote App (exposes components)
```js
// vite.config.js
import federation from "@originjs/vite-plugin-federation";

export default {
  plugins: [
    federation({
      name: 'mfe-user',
      filename: 'remoteEntry.js',
      exposes: {
        './UserCard': './src/components/UserCard.vue'
      },
      shared: ['vue']
    })
  ],
  build: {
    target: 'esnext',
    minify: false
  }
}
```

### Host App (loads remotes)
```js
// vite.config.js
import federation from "@originjs/vite-plugin-federation";

export default {
  plugins: [
    federation({
      remotes: {
        'mfe-user': 'http://localhost:5001/assets/remoteEntry.js'
      },
      shared: ['vue']
    })
  ],
  build: {
    target: 'esnext',
    minify: false
  }
}
```

In your Vue/React/JS code, you can now import components just like you would in Webpack:

```js
import UserCard from 'mfe-user/UserCard';
```

Note: Ensure CORS is handled correctly and both apps are served via dev/prod servers that support dynamic loading.

---

## ⚖️ Benefits of Module Federation

✅ **Runtime decoupling**  
No more rebuilding the container to pull in updates from MFEs.

✅ **Shared dependencies**  
Avoid shipping React (or other libs) multiple times — share them via the container.

✅ **Flexible versioning**  
Each MFE can use its own compatible versions of shared libs, or enforce singletons.

✅ **Framework-aware orchestration**  
Works seamlessly with React, Angular, Vue, etc.

✅ **Lazy loading**  
Only load the MFE code when it’s needed — great for performance.

---

## ⚠️ Gotchas and Things to Watch Out For

🚨 **Version conflicts**  
If two MFEs depend on different versions of React, you can hit runtime errors.  
Use `singleton: true` in `shared` to enforce a single version.

🚨 **Eager loading**  
Don’t preload every remote — load them only when needed to keep bundles lean.

🚨 **Remote unavailability**  
If a remote is down or fails to load, your container must handle the fallback. Build in error boundaries or dynamic loading safeguards.

🚨 **Runtime configuration**  
You may need to set `publicPath: 'auto'` and load `remoteEntry.js` dynamically based on environment or tenant.

---

## 🏗️ How Module Federation Fits Micro Frontends

Module Federation works especially well when:
- You want **independent team deployments**.
- You’re using a **shared router or container** to orchestrate MFEs.
- You want **shared utilities or design systems** without duplicating them across apps.
- You have a consistent framework across teams (e.g., all React).

This makes it ideal for scaling frontend development in large organizations — without tightly coupling teams or forcing lockstep releases.

---

## 🔄 Module Federation vs Web Components

If you're wondering how Module Federation compares to Web Components (another valid MFE path):

| Feature                        | Module Federation        | Web Components             |
|-------------------------------|--------------------------|----------------------------|
| Integration Style             | Application-level        | Component-level            |
| Dependency Sharing            | ✅ Yes (via `shared`)     | ❌ No (must bundle or dedupe manually) |
| Framework Agnostic            | ⚠️ Limited (depends on build config) | ✅ Fully                   |
| Shadow DOM & Encapsulation    | ❌ No                     | ✅ Yes                     |
| Best For                      | Team-scale orchestration | Portability and framework diversity |

👉 For more on this comparison, check out [Post 3](https://tibble49.github.io/integration-styles-for-micro-frontends/).

---

## 🧭 Coming Up Next

Next time, we’ll explore **Web Components** — what they offer, when they shine, and how to ship them as micro frontends in a runtime container.


