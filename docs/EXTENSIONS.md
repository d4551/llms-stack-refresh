# Extension and Plugin Systems

Canonical deep-dive reference for the plugin, extension, and customization systems of every technology in this stack.

## Why Extension Systems Matter for LLM-Assisted Development

Extension systems are the primary mechanism for adapting each tool to a specific project's needs. LLM coding assistants must understand these systems to generate correct, idiomatic code. This document lists the exact API names, hook names, and configuration points for each tool. Use this file as a reference when generating or reviewing code that customizes any tool in the stack.

## Bun -- Plugin API

**System name**: Bun Plugin API

**Primary API**: `Bun.plugin(pluginObject)` at runtime; `plugins` array in `bunfig.toml` for bundler-level registration

### How it works

A Bun plugin is a JavaScript object with a `name` string and a `setup(build)` function. The `setup` function receives a `build` object and registers callbacks using `build.onLoad()` and `build.onResolve()`.

- `build.onLoad({ filter: /pattern/ }, callback)` -- intercept file loads matching the regex
- `build.onResolve({ filter: /pattern/ }, callback)` -- intercept module resolution

Plugins can return custom `contents` and `loader` values from `onLoad` callbacks. The `loader` value controls how Bun processes the returned content (e.g., `"js"`, `"ts"`, `"json"`, `"text"`).

Plugins registered via `Bun.plugin()` apply to the current Bun process. Plugins listed in `bunfig.toml` under `[bundler] plugins` apply at bundler startup.

### Key hooks and callbacks

- `setup(build)` -- required entry point; receives the `build` object
- `build.onLoad({ filter, namespace? }, callback)` -- intercept file content loading
- `build.onResolve({ filter, namespace? }, callback)` -- intercept module path resolution
- `namespace` -- string identifier for virtual module namespaces (default: `"file"`)

### Supported customizations

- Custom file type loaders (e.g., load `.yaml` files as JavaScript objects)
- Virtual modules (intercept `import "virtual:..."` paths)
- Custom module resolution (rewrite import paths)
- Macros for compile-time JavaScript execution

### Macros

Bun Macros run JavaScript functions at bundle time. Import with the `with { type: "macro" }` import attribute:

```typescript
import { myMacro } from "./macro.ts" with { type: "macro" };
const result = myMacro(); // evaluated at bundle time
```

Macro functions must return a JSON-serializable value or a JSX element.

### Workspaces

Bun supports npm-compatible workspaces via the `workspaces` field in `package.json`:

```json
{
  "workspaces": ["packages/*"]
}
```

Run `bun install` at the repo root to install all workspace packages. Workspace packages can reference each other with `"my-pkg": "workspace:*"`.

### Common patterns

- Register a plugin in a setup file and add it to `bunfig.toml` for automatic loading.
- Use namespaces to avoid collisions between plugins.

### Common anti-patterns

- Do not use `build.onLoad` callbacks that are async unless the Bun version supports async plugins.
- Do not mutate `build` outside of the `setup` function.

### References

- `bun/llms.txt` -- see Plugins, Macros, and Workspaces sections
- Upstream docs: https://bun.sh/docs/bundler/plugins

---

## ElysiaJS -- Plugin System

**System name**: Elysia Plugin System

**Primary API**: `.use(plugin)` method on the Elysia app instance

### How it works

Every Elysia app is itself a valid plugin. Pass any Elysia instance to `.use()` to compose it into the parent app. Elysia deduplicates plugins by object reference, so a plugin shared across multiple files is only registered once.

Plugins can define routes, lifecycle hooks, decorators, and derived state that are scoped or propagated to the parent app.

### Key API points

- `.use(plugin)` -- compose an Elysia instance as a plugin
- `.macro(macroObject)` -- define reusable lifecycle logic with custom properties
- `scoped: true` option in `.use()` -- keep plugin state isolated from parent
- Plugin deduplication: if the same Elysia instance is passed to `.use()` multiple times, it is only applied once

### Official plugins

Install each with `bun add @elysiajs/<name>`:

| Plugin | Package | Purpose |
|--------|---------|---------|
| bearer | `@elysiajs/bearer` | Extract Bearer token from Authorization header |
| cors | `@elysiajs/cors` | CORS headers and preflight handling |
| cron | `@elysiajs/cron` | Cron job scheduling |
| html | `@elysiajs/html` | JSX and HTML response helpers |
| jwt | `@elysiajs/jwt` | JWT sign and verify helpers |
| openapi | `@elysiajs/openapi` | OpenAPI / Swagger documentation generation |
| opentelemetry | `@elysiajs/opentelemetry` | OpenTelemetry tracing integration |
| server-timing | `@elysiajs/server-timing` | Server-Timing response header generation |
| static | `@elysiajs/static` | Static file serving |

### Macros

`.macro()` defines reusable lifecycle properties. A macro can attach `beforeHandle`, `afterHandle`, and other lifecycle hooks based on route configuration values.

```typescript
const authMacro = new Elysia()
  .macro(({ onBeforeHandle }) => ({
    isAuth(value: boolean) {
      if (!value) return;
      onBeforeHandle(({ set }) => {
        set.status = 401;
        return "Unauthorized";
      });
    }
  }));
```

### Community ecosystem

List of community plugins: https://elysiajs.com/plugins/overview

### Common patterns

- Create a shared `plugins/` directory. Export each plugin as a named Elysia instance.
- Use `.macro()` to implement guard patterns (auth checks, rate limiting) applied per-route.

### Common anti-patterns

- Do not instantiate a new Elysia instance inside `.use()` on every request; create the instance once and reuse it for deduplication to work.
- Do not mix scoped and unscoped state without understanding propagation rules.

### References

- `elysiajs/llms.txt` -- see Plugins section
- Upstream plugin docs: https://elysiajs.com/essential/plugin
- Plugin overview: https://elysiajs.com/plugins/overview

---

## htmx -- Extension System

**System name**: htmx Extension API

**Primary API**: `htmx.defineExtension(name, extensionObject)` in JavaScript

**Activation**: `hx-ext="extension-name"` attribute on an HTML element

### How it works

An htmx extension is a JavaScript object that implements one or more hook functions. Register the extension before htmx processes the DOM. Activate an extension on a DOM subtree by adding `hx-ext="name"` to any element; all descendant elements inherit the extension.

### Hook functions

| Hook | Signature | Purpose |
|------|-----------|---------|
| `init` | `(api) => void` | Called once on extension load; receives the htmx internal API |
| `getSelectors` | `() => string[] or null` | Return additional CSS selectors htmx should process |
| `onEvent` | `(name, event) => boolean or void` | Intercept htmx internal events; return `false` to cancel |
| `transformResponse` | `(text, xhr, elt) => string` | Modify raw server response text before htmx processes it |
| `isInlineSwap` | `(swapStyle) => boolean` | Return `true` if this extension handles the given swap style |
| `handleSwap` | `(swapStyle, target, fragment, settleInfo) => boolean or array` | Perform custom DOM swap; return `true` or array of settled elements |
| `encodeParameters` | `(xhr, parameters, elt) => string or FormData or null` | Custom request body encoding |

### Core extensions (shipped with htmx)

| Extension | `hx-ext` value | Purpose |
|-----------|---------------|---------|
| head-support | `head-support` | Merge `<head>` content on page swaps |
| idiomorph | `morph` | DOM morphing swap using the Idiomorph algorithm |
| preload | `preload` | Prefetch content on hover or mousedown |
| response-targets | `response-targets` | Target different elements based on HTTP response status |
| server-sent events | `sse` | Handle Server-Sent Events (SSE) streams |
| WebSockets | `ws` | Handle WebSocket connections |

### Community extensions

Full list: https://htmx.org/extensions/

### Defining an extension

```javascript
htmx.defineExtension("my-extension", {
  onEvent: function(name, event) {
    if (name === "htmx:beforeRequest") {
      // intercept before request
    }
  },
  transformResponse: function(text, xhr, elt) {
    return text.replace("foo", "bar");
  }
});
```

### Common patterns

- Use `transformResponse` to preprocess JSON responses into HTML before htmx processes them.
- Use `onEvent` with `htmx:configRequest` to add custom headers to every request.

### Common anti-patterns

- Do not register extensions after the `DOMContentLoaded` event without also calling `htmx.process(document.body)` to reprocess the DOM.
- Do not use `handleSwap` for simple cases; prefer built-in swap styles.

### References

- `htmx/llms.txt` -- see Core Extensions and Community Extensions sections
- Upstream extension building docs: https://htmx.org/extensions/building/
- Extension list: https://htmx.org/extensions/

---

## Prisma -- Client Extensions

**System name**: Prisma Client Extensions

**Primary API**: `prisma.$extends(extensionObject)` on the PrismaClient instance

### How it works

`$extends` returns a new, extended PrismaClient. The original client is not modified. Extensions add methods, fields, or query interceptors without modifying generated client code.

An extension object has up to four top-level keys, one per component type.

### Extension component types

| Type | Key | Purpose |
|------|-----|---------|
| `client` | `client: { ... }` | Add top-level methods to the client (e.g., `prisma.myMethod()`) |
| `model` | `model: { modelName: { ... } }` | Add model-level static methods (e.g., `prisma.user.myMethod()`) |
| `query` | `query: { modelName: { operation: fn } }` | Intercept and modify queries |
| `result` | `result: { modelName: { fieldName: { ... } } }` | Add computed fields to query results |

### Key API points

- `$extends({ client: { ... } })` -- add methods at `prisma.*` level
- `$extends({ model: { user: { ... } } })` -- add methods at `prisma.user.*` level
- `$extends({ query: { user: { findMany: fn } } })` -- intercept a specific operation
- `$extends({ result: { user: { fullName: { needs: { firstName, lastName }, compute: fn } } } })` -- computed result field
- Use `Prisma.defineExtension()` to create a reusable, shareable extension object

### Shared / reusable extensions

```typescript
import { Prisma } from "@prisma/client";

const softDeleteExtension = Prisma.defineExtension({
  model: {
    $allModels: {
      async softDelete<T>(this: T, id: string) {
        // implementation
      }
    }
  }
});

const prisma = new PrismaClient().$extends(softDeleteExtension);
```

### Observability and tracing

Use `$extends` with the `query` component type to log or trace every query. Alternatively, use the `@prisma/instrumentation` package for OpenTelemetry integration.

### Common patterns

- Define extensions in separate files and compose them with multiple `$extends` calls.
- Use `$allModels` as the model key to apply an extension to all models.

### Common anti-patterns

- Do not mutate the result of `$extends` after creation; create a new extended client for each configuration variation.
- Do not use `result` extensions for data that requires a separate database query; use `model` extensions with explicit method calls instead.

### References

- `prisma/llms.txt` -- see Client Extensions section
- Upstream docs: https://www.prisma.io/docs/orm/prisma-client/client-extensions

---

## Tailwind CSS -- Customization Directives

**System name**: Tailwind CSS v4 CSS-First Customization

**Primary API**: `@plugin`, `@utility`, `@variant`, `@custom-variant`, `@apply`, `@reference`, `@theme` directives in CSS

### How it works

Tailwind CSS v4 uses a CSS-first configuration model. All customization happens in the main CSS file, not in a JavaScript config file. The `@theme` block defines design tokens. Directives like `@utility` and `@variant` extend the framework.

### Directive reference

| Directive | Syntax | Purpose |
|-----------|--------|---------|
| `@theme` | `@theme { --color-brand: #...; }` | Define design tokens (colors, spacing, fonts) |
| `@plugin` | `@plugin "package-name"` | Load a Tailwind CSS plugin |
| `@utility` | `@utility name { ... }` | Define a custom utility class |
| `@variant` | `@variant name { ... }` | Define a custom variant using CSS rules |
| `@custom-variant` | `@custom-variant name selector` | Define a variant from a CSS selector shorthand |
| `@apply` | `@apply class-list` | Apply Tailwind utility classes inside custom CSS rules |
| `@reference` | `@reference "path"` | Import theme tokens without generating CSS output |

### Configuration example

```css
@import "tailwindcss";

@theme {
  --color-brand: #7c3aed;
  --font-display: "Inter", sans-serif;
}

@plugin "@tailwindcss/typography";

@utility card {
  border-radius: 0.5rem;
  padding: 1rem;
  background-color: white;
}

@custom-variant dark (&:where(.dark, .dark *));
```

### Key concepts for v4

- No `tailwind.config.js` required in v4.
- The `@theme` directive replaces the `theme` key in `tailwind.config.js`.
- `@reference` replaces `@config` for token-only imports.
- `@apply` still works for composing utilities inside component CSS.

### Common patterns

- Put all `@theme` token definitions at the top of the main CSS file.
- Use `@utility` for project-specific one-off classes that appear in many components.
- Use `@custom-variant` for selector-based state variants.

### Common anti-patterns

- Do not use `@apply` inside `@utility` definitions for performance reasons; use raw CSS properties instead.
- Do not define `@theme` in multiple files; consolidate tokens in one place.

### References

- `tailwindcss/llms.txt` -- see Customization section
- Upstream docs: https://tailwindcss.com/docs/adding-custom-styles

---

## daisyUI -- Theme and Plugin Configuration

**System name**: daisyUI Tailwind CSS Plugin

**Primary API**: `@plugin "daisyui"` in CSS (v4) or `require("daisyui")` in `tailwind.config.js` (v3)

### How it works

daisyUI is a Tailwind CSS plugin that adds semantic component class names. Configure daisyUI through the plugin options to control which themes are active and how components behave.

### Configuration entry points

**v4 (CSS-first):**

```css
@import "tailwindcss";
@plugin "daisyui";
```

**v3 (tailwind.config.js):**

```javascript
module.exports = {
  plugins: [require("daisyui")],
  daisyui: {
    themes: ["light", "dark", "cupcake"],
  },
};
```

### Theme configuration

- `daisyui.themes` array lists active themes by name.
- Set `daisyui.themes: true` to enable all built-in themes.
- Set `daisyui.themes: false` to disable all themes (use component classes without themes).
- Specify a custom theme object in the array to define a new named theme.

### Custom themes

Define a custom theme with CSS variable overrides:

```javascript
daisyui: {
  themes: [
    {
      mytheme: {
        "primary": "#7c3aed",
        "secondary": "#db2777",
        "accent": "#f59e0b",
        "neutral": "#1f2937",
        "base-100": "#ffffff",
      },
    },
  ],
}
```

### Component customization

Apply Tailwind utility classes alongside daisyUI component classes for per-instance overrides:

```html
<button class="btn btn-primary rounded-full shadow-lg">Custom Button</button>
```

Use CSS variables to override component tokens globally:

```css
:root {
  --btn-focus-scale: 0.98;
}
```

### Common patterns

- List only the themes your project uses in `daisyui.themes` to keep CSS output small.
- Use the `data-theme` HTML attribute to switch themes at runtime.

### Common anti-patterns

- Do not override daisyUI component styles with `!important`; use CSS variable overrides instead.
- Do not mix daisyUI v3 and v4 configuration patterns in the same project.

### References

- `daisyui/llms.txt` -- see Themes and Configuration sections
- Upstream docs: https://daisyui.com/docs/themes/

---

## EasyAuth -- Integration Layer

**System name**: EasyAuth Integration (not a plugin framework)

**Primary API**: Session token validation in Elysia `beforeHandle` lifecycle hook

### How it works

EasyAuth is a managed authentication service, not a plugin system with extension hooks. Integrate EasyAuth by calling its API to validate session tokens, and use Elysia's lifecycle hooks to protect routes.

### Key integration points

**Session validation in Elysia:**

```typescript
app.get("/protected", ({ set, headers }) => {
  // handler
}, {
  beforeHandle: async ({ set, headers }) => {
    const token = headers["x-easyauth-token"];
    const session = await validateEasyAuthToken(token);
    if (!session) {
      set.status = 401;
      return "Unauthorized";
    }
  }
});
```

**HX-Redirect for htmx unauthenticated flows:**

When an htmx request is made by an unauthenticated user, return an `HX-Redirect` response header instead of a 401 status. htmx will redirect the browser to the login URL.

```typescript
beforeHandle: async ({ set, headers, request }) => {
  if (!isAuthenticated) {
    if (request.headers.get("hx-request")) {
      set.headers["HX-Redirect"] = "/login";
      set.status = 200;
    } else {
      set.redirect = "/login";
    }
    return;
  }
}
```

**OAuth provider configuration**: Configure OAuth providers (GitHub, Google, etc.) via the EasyAuth dashboard. No code change is required to switch providers.

### Supported customizations

- Choose which OAuth providers to enable (dashboard configuration).
- Customize session token validation logic in the `beforeHandle` hook.
- Redirect unauthenticated htmx requests using the `HX-Redirect` header.
- Store additional user data by extending the EasyAuth user profile via the dashboard.

### Common patterns

- Create a reusable `authGuard` Elysia plugin that wraps the `beforeHandle` validation logic.
- Use Prisma to store extended user data linked to the EasyAuth user ID.

### Common anti-patterns

- Do not store EasyAuth session tokens in `localStorage`; use `HttpOnly` cookies.
- Do not validate tokens on the client side; always validate server-side in `beforeHandle`.

### References

- `easy-auth/llms.txt` -- see Integration Patterns section
- Upstream docs: https://easyauth.io/docs/
