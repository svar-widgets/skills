---
name: svar-svelte
description: Use when building, configuring, styling, or modifying any SVAR Svelte UI component from the @svar-ui/svelte-* packages - widgets, layouts, menus, toolbars, calendars, popups, themes, and locales
---

SVAR Svelte ships as a family of `@svar-ui/svelte-*` packages. This file routes to the per-package entry; each child file is standalone and contains the imports, public types, styling hooks, and recipes for its components.

Open the matching file for the package you are using. If the component you need is not listed in the routing table below, default to `core/index.md`

## Component Routing

| File | Package | Components |
| ---------------------- | ------------------------ | ------------------------------------------------------------------------------------------- |
| `core/index.md` | `@svar-ui/svelte-core` | buttons, inputs, selectors, calendars, dropdowns, popups, modals, themes, locale (40+ widgets) |
| `menu/index.md` | `@svar-ui/svelte-menu` | `Menu`, `MenuBar`, `DropDownMenu`, `ContextMenu`, `ActionMenu` |
| `toolbar/index.md` | `@svar-ui/svelte-toolbar` | `Toolbar` |
| `layout/index.md` | `@svar-ui/svelte-layout` | `Layout`, `Cell`, `Panel` |
| `grid/index.md` | `@svar-ui/svelte-grid` | `Grid`, `HeaderMenu`, `Tooltip`, `ContextMenu`, `Toolbar` |
| `editor/index.md` | `@svar-ui/svelte-editor` | `Editor` |
| `filter/index.md` | `@svar-ui/svelte-filter` | `FilterBuilder`, `FilterEditor`, `FilterBar`, `FilterQuery` |
| `gantt/index.md` | `@svar-ui/svelte-gantt` | `Gantt`, `Toolbar`, `ContextMenu`, `Editor`, `Tooltip`, `HeaderMenu` |
| `tasklist/index.md` | `@svar-ui/svelte-tasklist` | `Tasklist` |
| `comments/index.md` | `@svar-ui/svelte-comments` | `Comments` |
| `filemanager/index.md` | `@svar-ui/svelte-filemanager` | `Filemanager` |

## Common Techniques

These apply to every `@svar-ui/svelte-*` package:

- `themes.md` - theme wrappers, CSS variables, the `css` prop convention, class hooks
- `locales.md` - locale context, bundled language packs, extending words and formats

The widget hierarchy need to be wrapped in a theme component to ensure proper styling
Some widgets (grid,gantt,filemanager, etc) exports their own theme components that delegate to core theme and add their own variables