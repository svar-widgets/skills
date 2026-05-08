# svar-vue — layout

_Generated 2026-05-08T13:35:37.091Z_

## Contents

- [`layout/index.md`](#file-layout-index-md)
- [`locales.md`](#file-locales-md)
- [`themes.md`](#file-themes-md)


## File: layout/index.md

> Source: `layout/index.md`

Use when building, configuring, styling, or modifying SVAR Vue Layout / @svar-ui/vue-layout components

#### Package

```js
import { Layout, Cell, Panel } from "@svar-ui/vue-layout";

import "@svar-ui/vue-layout/all.css";
```

Top-level exports:

- `Layout` - flex container with direction, spacing presets, padding, and optional drag resizing
- `Cell` - direct layout child with fixed or grow-based sizing and optional header
- `Panel` - collapsible `Cell` variant with an expanded header and collapsed bar

#### Supported functionality

##### Components

- `Layout` renders a full-size flex container with `direction="column"` by default; use `direction="row"` for horizontal panes.
- `Cell` and `Panel` emit `.wx-cell`; only direct `.wx-cell` children of a resizable `Layout` participate in drag resizing

##### Sizing

- `width` or `height` on `Cell`/`Panel` sets a fixed pixel size and `flex:none`.
- Without `width` and `height`, `Cell`/`Panel` uses `flex:{grow}`; `grow` defaults to `1`.
- `minWidth` and `minHeight` set CSS minimums and are read by the resizer to clamp drag ranges.
- In row layouts, fixed `width` is the usual main-axis control; in column layouts, fixed `height` is the usual main-axis control.

##### Layout spacing

- Presets are `clean`, `line`, `wide`, and `space`.
- Preset values in source: `clean` = gap 0/padding 0, `line` = gap 1/padding 0, `wide` = gap 10/padding 0, `space` = gap 10/padding 10.
- `gap` and `padding` override preset values when provided.
- When `resizable` is true, CSS gap is not rendered; 6px `.wx-resizer` elements are injected between direct cells. `padding` still applies.

##### Events and state

- if at least one cell is not flexible, it will have new size set after resizing
- resize between two flexibles cell must be resolved by `oncellresize` handler ( setting new size / flex )
- `Panel` accepts `oncollapse?: (collapsed: boolean) => void`, called after the internal collapsed state toggles.

##### Panel collapse

- Expanded `Panel` always renders `.wx-cell-header` with a toggle button; custom `header` slot replaces label text but not the toggle.
- Collapsed row panels become a vertical bar; collapsed column panels become a horizontal bar.
- Collapsed size is controlled by `--wx-panel-collapsed-size`, default `24px`.
- Collapsed panels can't be resized

#### Public Types

```ts
import { type Slot, type Component } from "vue";

interface ILayoutProps {
	direction?: "column" | "row";
	preset?: "clean" | "line" | "wide" | "space";
	gap?: number;
	padding?: number;
	resizable?: boolean;
	css?: string;
	children: Slot;
	oncellresize?: (sizes: number[]) => void;
}

interface ICellProps {
	label?: string;
	width?: number;
	height?: number;
	minWidth?: number;
	minHeight?: number;
	grow?: number;
	scroll?: boolean;
	css?: string;
	children: Slot;
	header?: Slot;
}

interface IPanelProps {
	label?: string;
	collapsed?: boolean;
	width?: number;
	height?: number;
	minWidth?: number;
	minHeight?: number;
	grow?: number;
	scroll?: boolean;
	css?: string;
	children: Slot;
	header?: Slot;
	oncollapse?: (collapsed: boolean) => void;
}

export declare const Layout: Component<ILayoutProps>;
export declare const Cell: Component<ICellProps>;
export declare const Panel: Component<IPanelProps>;
```

#### Styling

Import the package CSS before using the component (`all.css` includes dependency styles, `style.css` is this component only)

- `css` is appended to the component root: `.wx-layout`, `.wx-cell`, or `.wx-cell.wx-panel`.
- Layout hooks: `.wx-layout`, `.wx-layout-{preset}`, `.wx-column`, `.wx-row`.
- Cell hooks: `.wx-cell`, `.wx-cell-header`, `.wx-cell-body`.
- Panel hooks: `.wx-panel`, `.wx-panel-collapsed`, `.wx-panel-animating`, `.wx-panel-row`, `.wx-panel-column`, `.wx-panel-collapsed-bar`, `.wx-panel-toggle`, `.wx-panel-icon`, `.wx-panel-label`.
- Resizer hooks: `.wx-resizer` is inserted between direct cells; `.wx-resize-overlay` is a temporary fixed overlay during drag.
- global `.wx-scroll` sets `overflow:auto` on the component root.
- global `.wx-border` adds border
- Built-in variables: `--wx-layout-gap-color`, `--wx-layout-line-color`, `--wx-layout-resizer-hover`, `--wx-layout-resizer-active`, `--wx-panel-collapsed-size`.

```vue
<template>
  <Layout direction="row" preset="line" css="app-layout">
    <Cell label="Files" :width="220" css="app-pane">Files</Cell>
    <Cell label="Editor">Editor</Cell>
  </Layout>
</template>

<style scoped>
.app-layout {
	--wx-layout-line-color: #d7dee8;
	--wx-layout-resizer-hover: rgba(40, 95, 170, 0.18);
	--wx-panel-collapsed-size: 30px;
}

.app-pane .wx-cell-header {
	padding: 6px 10px;
}
</style>
```

#### Recipes

##### Basic Fixed And Flexible Panes

```vue
<script setup>
import { Layout, Cell } from "@svar-ui/vue-layout";
</script>

<template>
  <div class="workspace">
    <Layout direction="row" preset="line">
      <Cell label="Sidebar" :width="240" :minWidth="160">
        <nav>Navigation</nav>
      </Cell>
      <Cell label="Main" :grow="3">
        <main>Content</main>
      </Cell>
    </Layout>
  </div>
</template>

<style scoped>
.workspace {
	width: 100%;
	height: 100vh;
}
</style>
```

##### Resizable IDE Layout

```vue
<script setup>
import { ref } from "vue";
import { Layout, Cell, Panel } from "@svar-ui/vue-layout";

const sidebarWidth = ref(220);
</script>

<template>
  <Layout
    direction="row"
    :padding="6"
    resizable
    :oncellresize="sizes => (sidebarWidth = sizes[0])"
  >
    <Panel label="Files" :width="sidebarWidth" :minWidth="120">
      <div>File tree</div>
    </Panel>

    <Cell>
      <Layout preset="line">
        <Cell :grow="3">
          <template #header><span>Editor</span></template>
          <div>Editor area</div>
        </Cell>
        <Panel :grow="1" label="Terminal">
          <div>Terminal</div>
        </Panel>
      </Layout>
    </Cell>
  </Layout>
</template>
```

##### Controlled Panel Collapse

```vue
<script setup>
import { ref } from "vue";
import { Layout, Cell, Panel } from "@svar-ui/vue-layout";

const collapsed = ref(false);
</script>

<template>
  <Layout direction="row" preset="line">
    <Panel
      label="Sidebar"
      :width="220"
      :minWidth="140"
      :collapsed="collapsed"
      :oncollapse="value => (collapsed = value)"
    >
      <div>Sidebar content</div>
    </Panel>
    <Cell>
      <div>Main content</div>
    </Cell>
  </Layout>
</template>
```

##### Custom Header Slot

```vue
<script setup>
import { Layout, Cell } from "@svar-ui/vue-layout";
</script>

<template>
  <Layout>
    <Cell :height="48">
      <template #header>
        <div class="bar">
          <span>Toolbar</span>
          <button>Save</button>
        </div>
      </template>
      <div>Body</div>
    </Cell>
    <Cell scroll>
      <div>Long content</div>
    </Cell>
  </Layout>
</template>
```

##### Presets And Explicit Spacing

```vue
<script setup>
import { Layout, Cell } from "@svar-ui/vue-layout";
</script>

<template>
  <Layout direction="row" preset="space" :gap="12" :padding="16">
    <Cell css="wx-border">Left</Cell>
    <Cell css="wx-border">Right</Cell>
  </Layout>
</template>
```

#### Implementation Notes

- `Cell` renders `.wx-cell-header` and `.wx-cell-body` only when `header` or `label` is provided.
- `Panel` detects row vs column from the parent DOM class `.wx-row`; outside a `Layout`, it behaves as column-oriented.
- Resizable layouts query only `:scope > .wx-cell`, so wrapping a `Cell` or `Panel` in another element prevents it from being resized.
- Drag resizing mutates inline styles on the adjacent cells during the pointer drag. Originally flexible cells are restored after pointer up; originally fixed cells keep their dragged pixel size.


## File: locales.md

> Source: `locales.md`

i18n patterns common to all SVAR Vue components - Locale wrapper, bundled language packs, extending words and formats

### Localizing SVAR Vue Components

All `@svar-ui/vue-*` widgets read locale data from a single Vue inject key (`wx-i18n`). The mechanics live in `@svar-ui/vue-core`; every other package consumes them.

#### Locale Wrapper

Wrap the subtree you want to localize. With no wrapper, widgets fall back to English.

```vue
<script setup>
import { Calendar, Locale } from "@svar-ui/vue-core";
import { de } from "@svar-ui/core-locales";
</script>

<template>
  <Locale :words="de">
    <Calendar :value="new Date(2025, 4, 1)" />
  </Locale>
</template>
```

Wrap the smallest subtree that needs the alternative locale - nested `Locale` blocks let different parts of the app render in different languages.

`Locale` does not render any DOM wrapper; it only mutates the injected context, so it never affects layout.

#### Bundled Language Packs

Core packs ship in `@svar-ui/core-locales`:

```js
import { en, cn, de, es, fr, it, ja, pt, ru } from "@svar-ui/core-locales";
```

Standalone widget packages ship their own dictionaries alongside the core pack - each exports locale objects keyed by language code (`cn`, `de`, `fr`, ...):

- `@svar-ui/core-locales` - core widgets (always include)
- `@svar-ui/editor-locales` - Editor
- `@svar-ui/filter-locales` - Filter
- `@svar-ui/gantt-locales` - Gantt
- `@svar-ui/filemanager-locales` - File Manager
- `@svar-ui/grid-locales` - Grid

If you see English fallbacks in a localized UI, the missing terms come from the package's own locale module - merge them in via `<Locale :words="..." />`.

To localize a standalone widget, merge the matching package locale with the core locale:

```vue
<script setup>
import { Gantt } from "@svar-ui/vue-gantt";
import { Locale } from "@svar-ui/vue-core";
import { cn } from "@svar-ui/gantt-locales";
import { cn as cnCore } from "@svar-ui/core-locales";
</script>

<template>
  <Locale :words="{ ...cn, ...cnCore }">
    <Gantt v-bind="settings" />
  </Locale>
</template>
```

#### Extending Or Overriding Words

`Locale words` accepts a partial pack and extends the current context. Spread an existing pack to keep its formats and override only what you need:

```vue
<script setup>
import { Calendar, Locale } from "@svar-ui/vue-core";
import { cn } from "@svar-ui/core-locales";

const words = {
    ...cn,
    formats: {
        ...cn.formats,
        monthYearFormat: "%Y年%F",
        yearFormat: "%Y年",
    },
};
</script>

<template>
  <Locale :words="words">
    <Calendar :value="new Date(2025, 4, 1)" />
  </Locale>
</template>
```

Pass `:optional="true"` to make merged terms additive fallbacks rather than overrides - useful for layering app-specific strings on top of a full pack.

#### Affected Surfaces

Locale changes calendar labels, date/time formats, modal buttons, pager strings, empty-list text, notice/modal helpers, color-board select text - any widget that displays static strings or formats values reads them through this context.

#### Direct Helper

For non-component code, use the `locale` helper to build a translator:

```js
import { en, locale } from "@svar-ui/vue-core";

const i18n = locale(en).extend(
    { core: { "Rows per page": "Rows" } },
    true
);
const _ = i18n.getGroup("core");
_("Rows per page"); // "Rows"
```


## File: themes.md

> Source: `themes.md`

### Styling SVAR Vue Components

All `@svar-ui/vue-*` widgets share the same theming pipeline. The mechanics live in `@svar-ui/vue-core`; every other package consumes them.

#### Per widget css files

Each package ships `style.css` (this component only) and `all.css` (this component plus all dependencies).

```css
@import "@svar-ui/vue-gantt/style.css";
```

#### Theme Wrapper

Wrap the part of the app that uses SVAR widgets in a theme component from `@svar-ui/vue-core`:

```vue
<script setup>
import { Willow } from "@svar-ui/vue-core";
</script>

<template>
  <Willow>
    <App />
  </Willow>
</template>
```

Available themes: `Willow`, `WillowDark`. The wrapper:

- provides the Vue inject key `wx-theme`
- renders `.wx-theme.wx-{name}-theme` with `height:100%`
- loads Open Sans + the `wxi` icon CSS by default; pass `:fonts="false"` to skip when the host app manages fonts itself

Without a theme wrapper widgets still render but lose theme variables and font/icon CSS.

#### Per-widget Willow / WillowDark themes

Several widgets ship their **own** `Willow` / `WillowDark` components on top of the core base. The widget version wraps the core theme and layers in widget-specific CSS variables (bar colors, grid borders, timescale fonts, etc.). When using such a widget, import the theme from the widget package - not from core - so both layers apply.

Widgets that expose custom `Willow` / `WillowDark` themes:

- `@svar-ui/vue-core` - base
- `@svar-ui/vue-gantt`
- `@svar-ui/vue-grid`
- `@svar-ui/vue-editor`
- `@svar-ui/vue-filter`
- `@svar-ui/vue-filemanager`
- `@svar-ui/vue-comments`
- `@svar-ui/vue-kanban`

The widget theme delegates to core and adds extra rules scoped to `.wx-willow-theme` (or `.wx-willow-dark-theme`):

```vue
<script setup>
import { Willow } from "@svar-ui/vue-core";
defineProps({ fonts: { type: Boolean, default: true } });
</script>

<template>
  <Willow :fonts="fonts">
    <slot v-if="$slots.default" />
  </Willow>
</template>

<style scoped>
:global(.wx-willow-theme) {
    --wx-gantt-border-color: #e6e6e6;
    --wx-gantt-task-color: #3983eb;
    /* ...widget-specific overrides... */
}
</style>
```

Mount the widget's own theme once at the app root. The wrapper internally renders the core `Willow`, so a separate core import is not needed:

```vue
<script setup>
import { Willow, Gantt } from "@svar-ui/vue-gantt";
</script>

<template>
  <Willow />
  <Gantt v-bind="settings" />
</template>
```

#### CSS Variables

Theme styling is variable-driven. Override variables on the theme wrapper or on any ancestor of the widgets you want to restyle - overrides cascade to every SVAR widget in the subtree.

```vue
<template>
  <Willow>
    <div class="brand">
      <App />
    </div>
  </Willow>
</template>

<style scoped>
.brand {
    --wx-color-primary: #0f766e;
    --wx-input-width: 280px;
    --wx-button-border-radius: 4px;
    --wx-calendar-cell-size: 30px;
}
</style>
```

Nest different wrapper blocks for per-section restyling without forking the theme.

#### `css` Prop Convention

Most widgets accept a `css` prop. The string is appended to the widget's root class, so it works as a parent styling hook:

```vue
<template>
  <Toolbar css="my-toolbar" :items="items" />
</template>

<style scoped>
.my-toolbar {
    padding: 8px 12px;
}
</style>
```

Composite widgets often expose secondary css props for nested popups (`menuCss` on `Toolbar`/`MenuBar`, etc.). Check the per-component file for the exact set.

#### Class Hooks

The per-component file lists the exact selectors that widget exposes.

#### Custom CSS class overrides

When writing custom rules to override widget styles, always use **at least two selectors** (e.g. `.a .b {}`). Vue scopes its component styles by appending a hash attribute which has higher specificity than a plain `.b`. A two-selector rule (`.a .b`) matches or beats that specificity and wins.

Convention: the first selector is a container/wrapper of the widget instance, the second is the inner class you want to alter:

```css
.my-gantt-host .wx-bar-task {
    background: #ff8800;
}
```

#### Override Order

Prefer in this order:

1. **CSS variables on a wrapper** - propagates consistently to every widget in the subtree.
2. **`css` prop class** - a stable parent hook that survives internal markup changes.
3. **Direct `.wx-*` selectors** - targeted overrides; tightest coupling to widget internals, use sparingly.

#### Core Vars

##### Base Colors

| Variable | Default | Use for |
|---|---|---|
| `--wx-color-primary` | `#37a9ef` | Primary accent - active states, selected items, links |
| `--wx-color-primary-selected` | `#d5eaf7` | Selected/highlighted row or item background |
| `--wx-color-primary-font` | `#fff` | Text on primary-colored backgrounds |
| `--wx-color-secondary` | `transparent` | Secondary/ghost element background |
| `--wx-color-secondary-hover` | `rgba(55, 169, 239, 0.12)` | Secondary hover background |
| `--wx-color-secondary-font` | `#37a9ef` | Secondary element text |
| `--wx-color-secondary-border` | `#37a9ef` | Secondary element border |
| `--wx-color-success` | `#77d257` | Success indicator |
| `--wx-color-warning` | `#fcba2e` | Warning indicator |
| `--wx-color-info` | `#37a9ef` | Info indicator |
| `--wx-color-danger` | `#fe6158` | Error/destructive state, error borders |
| `--wx-color-disabled` | `#f2f3f7` | Disabled element background |
| `--wx-color-disabled-alt` | `#e9e9e9` | Alternate disabled background |
| `--wx-color-font` | `#2c2f3c` | Primary text |
| `--wx-color-font-alt` | `#9fa1ae` | Secondary/muted text, placeholders |
| `--wx-color-font-disabled` | `#c0c3ce` | Disabled text |
| `--wx-color-link` | `#37a9ef` | Link text |
| `--wx-background` | `#ffffff` | Main surface |
| `--wx-background-alt` | `#f2f3f7` | Alternate surface (cards, tags, odd/even areas) |
| `--wx-background-hover` | `#eaedf5` | Hover state background |

##### Typography

| Variable | Default | Use for |
|---|---|---|
| `--wx-font-family` | `"Open Sans", Arial, Helvetica, sans-serif` | All text |
| `--wx-font-size` | `14px` | Body text |
| `--wx-line-height` | `20px` | Body line height |
| `--wx-font-size-md` | `14px` | Medium text |
| `--wx-line-height-md` | `24px` | Medium line height |
| `--wx-font-size-hd` | `16px` | Headings |
| `--wx-line-height-hd` | `30px` | Heading line height |
| `--wx-font-size-sm` | `12px` | Captions, small text |
| `--wx-line-height-sm` | `16px` | Small line height |
| `--wx-font-weight` | `400` | Normal weight |
| `--wx-font-weight-md` | `600` | Semi-bold (labels, buttons) |
| `--wx-font-weight-b` | `700` | Bold (modal headers) |

##### Icons

| Variable | Default | Use for |
|---|---|---|
| `--wx-icon-color` | `#9fa1ae` | Default icon tint |
| `--wx-icon-size` | `20px` | Icon dimensions |
| `--wx-icon-border-radius` | `2px` | Icon hover-state rounding |

##### Borders, Shadows, Spacing

| Variable | Default | Use for |
|---|---|---|
| `--wx-border` | `1px solid #e6e6e6` | Standard border |
| `--wx-border-radius` | `3px` | Default corner radius |
| `--wx-radius-major` | `6px` | Larger radius (cards, panels) |
| `--wx-border-light` | `none` | Subtle divider |
| `--wx-border-medium` | `1px solid #eaedf5` | Medium divider |
| `--wx-shadow-light` | `0px 3px 10px ...` | Elevated panels (popups, dropdowns) |
| `--wx-shadow-medium` | `0px 4px 20px ...` | High-elevation surfaces (modals) |
| `--wx-padding` | `8px` | Base spacing unit |

##### Layout

| Variable | Default | Use for |
|---|---|---|
| `--wx-field-gutter` | `16px` | Vertical gap between form rows |
| `--wx-field-width` | `400px` | Max width of a form field row |

##### Z-index Scale

| Layer | Value |
|---|---|
| Popups / dropdowns | `100` |
| Modals | `1000` |
| Notices / toasts | `1010` |
