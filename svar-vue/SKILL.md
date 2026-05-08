---
name: svar-vue
description: Use when building, configuring, styling, or modifying any SVAR Vue UI component from the @svar-ui/vue-* packages - widgets, layouts, menus, toolbars, calendars, popups, themes, and locales
---

SVAR Vue ships as a family of `@svar-ui/vue-*` packages. This file routes to the per-package entry; each child file is standalone and contains the imports, public types, styling hooks, and recipes for its components.

Open the matching file for the package you are using. If the component you need is not listed in the routing table below, default to `core/index.md`

## Component Routing

| File | Package | Components |
| ---------------------- | ------------------------ | ------------------------------------------------------------------------------------------- |
| `core/index.md` | `@svar-ui/vue-core` | buttons, inputs, selectors, calendars, dropdowns, popups, modals, themes, locale (40+ widgets) |
| `menu/index.md` | `@svar-ui/vue-menu` | `Menu`, `MenuBar`, `DropDownMenu`, `ContextMenu`, `ActionMenu` |
| `toolbar/index.md` | `@svar-ui/vue-toolbar` | `Toolbar` |
| `layout/index.md` | `@svar-ui/vue-layout` | `Layout`, `Cell`, `Panel` |
| `grid/index.md` | `@svar-ui/vue-grid` | `Grid`, `HeaderMenu`, `Tooltip`, `ContextMenu`, `Toolbar` |
| `editor/index.md` | `@svar-ui/vue-editor` | `Editor` |
| `filter/index.md` | `@svar-ui/vue-filter` | `FilterBuilder`, `FilterEditor`, `FilterBar`, `FilterQuery` |
| `gantt/index.md` | `@svar-ui/vue-gantt` | `Gantt`, `Toolbar`, `ContextMenu`, `Editor`, `Tooltip`, `HeaderMenu` |
| `tasklist/index.md` | `@svar-ui/vue-tasklist` | `Tasklist` |
| `comments/index.md` | `@svar-ui/vue-comments` | `Comments` |
| `filemanager/index.md` | `@svar-ui/vue-filemanager` | `Filemanager` |

## Common Techniques

These apply to every `@svar-ui/vue-*` package:

- `themes.md` - theme wrappers, CSS variables, the `css` prop convention, class hooks
- `locales.md` - locale context, bundled language packs, extending words and formats

The widget hierarchy need to be wrapped in a theme component to ensure proper styling
Some widgets (grid,gantt,filemanager, etc) exports their own theme components that delegate to core theme and add their own variables
