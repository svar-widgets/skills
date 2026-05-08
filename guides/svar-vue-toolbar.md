# svar-vue — toolbar

_Generated 2026-05-08T13:35:37.091Z_

## Contents

- [`toolbar/index.md`](#file-toolbar-index-md)
- [`locales.md`](#file-locales-md)
- [`themes.md`](#file-themes-md)


## File: toolbar/index.md

> Source: `toolbar/index.md`

Use when UI of app requires Toolbar, configuring, or modifying SVAR Vue Toolbar / @svar-ui/vue-toolbar components

#### Package

```js
import { Toolbar, registerToolbarItem } from "@svar-ui/vue-toolbar";

import "@svar-ui/vue-toolbar/all.css";
```

#### Supported functionality

##### Events

- item `handler`, toolbar `onclick`, toolbar `onchange`

##### Value binding

- `values` bag of properties bound to inputs in toolbar by `item.key`, changes tracked by `onchange`

##### Overflow modes

default is `overflow="menu"`

- `menu`: when items no longer fit, trailing top-level items move into a dots menu
    - `menuText` replaces `text` only inside the overflow menu
- `wrap`: wraps to new rows
- `collapse`: never creates a dots menu; it collapses the rightmost open top-level group first, only affects top-level items that have nested `items`; plain buttons do not collapse

##### Item's properties

- `comp` - component name, built in are `button`, `icon`, `label`, `item`, `separator`, `spacer`
- `key` - bind to values by this key
- `text`, `menuText` - content of button in normal and menu modes
- `collapsed`, `layout`, `items` - used to organise groups of buttons ( like ribbons )
- `handler` - per item click handler
- `css` - css class to the button's container
- `spacer` - adds `flex:1` to the button (it takes all space)
- all extra properties passthrough to the Vue components

##### Common elements

Button configurations:

```js
{ comp: "button", text: "Save" }
{ comp: "button", icon: "wxi-search" }
{ comp: "button", icon: "wxi-file", text: "Load" }
{ comp: "button", text: "Apply", type: "primary" }
{ comp: "button", icon: "wxi-delete-outline", disabled: true }
{ comp: "button", icon: "wxi-content-copy", text: "Ctrl+C", menuText: "Copy" }
```

Icon configurations:

```js
{ comp: "icon", icon: "wxi-search" }
{ comp: "icon", icon: "wxi-information-outline", text: "Info" }
{ comp: "icon", icon: "wxi-content-copy", text: "Ctrl+C", menuText: "Copy" }
{ comp: "icon", icon: "wxi-delete-outline", disabled: true }
```

Label, item, separator, spacer configurations:

```js
{ comp: "label", text: "Toolbar title" }
{ comp: "label", key: "name" }
{ comp: "label", key: "name", spacer: true }
{ comp: "item", id: "done", text: "Mark as finished task" }
{ comp: "item", id: "delete", icon: "wxi-delete-outline", text: "Delete item", css: "danger" }
{ comp: "separator" }
{ comp: "spacer" }
```

`item` is a simple clickable row, not a core button, use it for menu/list-style actions, especially inside collapsed groups/header menus.

Widgets from `@svar-ui/vue-core` which can be used as components: Slider, Text, CheckboxGroup, RichSelect, DatePicker, ColorPicker, ColorSelect, Checkbox, Tabs, Pager, Segmented, Switch, TwoState, Combo, MultiCombo.

#### Public Types

```ts
import type { Component } from "vue";

export interface IToolbarItem {
	id?: string | number;
	comp?: string | Component<any>;
	icon?: string;
	css?: string;
	text?: string;
	menuText?: string;
	key?: string;
	spacer?: boolean;
	collapsed?: boolean;
	handler?: (item: IToolbarItem, value?: any) => void;
	layout?: "column";
	items?: IToolbarItem[];
	[key: string]: any;
}

export declare const Toolbar: Component<{
	items?: IToolbarItem[];
	menuCss?: string;
	css?: string;
	values?: { [key: string]: any };
	overflow?: "collapse" | "wrap" | "menu";
	onclick?: (ev: { item: IToolbarItem }) => void;
	onchange?: (ev: { value: any; item: IToolbarItem }) => void;
}>;

export declare function registerToolbarItem(
	type: string,
	handler: Component<any>
): void;
```

#### Styling

Import the package CSS before using the component (`all.css` includes dependency styles, `style.css` is this component only)
- toolbar `css` is appended to `.wx-toolbar`; use it as the parent styling hook
- menu `menuCss` is appended to the overflow `.wx-menu`; item `css` is appended to `.wx-tb-element` or group `.wx-tb-group`

- toolbar container: `.wx-toolbar`
- top-level item wrapper: `.wx-tb-element`
- group wrapper: `.wx-tb-group`, group body: `.wx-tb-body`
- overflow menu container in the toolbar row `.wx-menu`
- content wrapper inside the opened dropdown `wx-drop-menu`
- separator `.wx-separator` and `.wx-separator-menu`
- `layout="column"` on Toolbar makes `.wx-toolbar.wx-column`
- `layout: "column"` on a group makes `.wx-column > .wx-tb-body`
- `comp: "spacer"` renders flex filler; `spacer: true` on normal item makes its wrapper `flex: 1`

```css
/*Gap between toolbar items*/
.my-toolbar .wx-tb-element {
	padding: 2px;
}

/*padding around the whole toolbar*/
.my-toolbar {
	padding: 8px 12px; /* default is 4px */
}

/*padding for groups*/
.my-toolbar .wx-tb-body {
	gap: 4px;
}
```

#### Recipes

##### Basic Toolbar

```vue
<script setup>
import { ref } from "vue";

const message = ref("");
function onClick(item) {
	message.value = `Button '${item.id}' clicked`;
}

const items = [
	{ id: "label", text: "Toolbar with icon buttons" },
	{ comp: "separator" },
	{ id: "search", comp: "button", icon: "wxi-search", handler: onClick },
	{ comp: "spacer" },
	{
		id: "copy",
		comp: "icon",
		icon: "wxi-content-copy",
		handler: onClick,
	},
];
</script>

<template>
  <Toolbar :items="items" />
</template>
```

##### Per-Item Handler

```js
function onClick(item) {
	console.log(item.id);
}

const items = [
	{ id: "edit", comp: "button", icon: "wxi-edit-outline", handler: onClick },
];
```

##### Toolbar Click Handler

```vue
<template>
  <Toolbar
    :items="[
      { id: 'edit', comp: 'button', icon: 'wxi-edit-outline' },
      { id: 'delete', comp: 'button', icon: 'wxi-delete-outline' },
    ]"
    :onclick="ev => console.log(ev.item.id)"
  />
</template>
```

##### Keyed Values

```vue
<script setup>
import { ref } from "vue";
// component must support `value` handler and `onchange` callback to be bound, most vue-core controls fit
import { Slider } from "@svar-ui/vue-core";
const values = ref({ size: 15 });
</script>

<template>
  <Toolbar
    :items="[{ comp: Slider, min: 0, max: 100, key: 'size' }]"
    v-model:values="values"
    :onchange="ev => console.log(ev.item.key, ev.value)"
  />
</template>
```

##### Common core controls

```vue
<script setup>
import { Slider, Segmented, Switch } from "@svar-ui/vue-core";

const options = [
	{ id: 1, label: "One" },
	{ id: 2, label: "Two" },
];
</script>

<template>
  <Toolbar
    css="demo-toolbar"
    :values="{ size: 14, mode: 1, enabled: true }"
    :items="[
      { text: 'Controls' },
      { comp: 'spacer' },
      { comp: Slider, min: 0, max: 100, key: 'size' },
      { comp: Segmented, options, key: 'mode' },
      { comp: Switch, key: 'enabled' },
    ]"
  />
</template>
```

##### Custom Component Contract

```vue
<!-- CustomToolbarItem.vue -->
<script setup>
const props = defineProps({
  value: {},
  onchange: { type: Function },
  onclick: { type: Function },
  menu: {},
  text: { default: "" },
  disabled: { default: false },
});
</script>

<template>
  <button
    :class="{ 'in-menu': props.menu }"
    :disabled="props.disabled"
    :onclick="() => {
      props.onclick?.();
      props.onchange?.({ value: !props.value });
    }"
  >
    {{ props.text }}
  </button>
</template>
```

```js
import CustomToolbarItem from "./CustomToolbarItem.vue";

const items = [{ comp: CustomToolbarItem, key: "flag", text: "Toggle" }];
const values = { flag: false };
```

##### Group

```js
const items = [
	{
		text: "Align",
		items: [
			{ id: "align-left", comp: "button", icon: "wxo-align-left" },
			{ id: "align-center", comp: "button", icon: "wxo-align-center" },
			{ id: "align-right", comp: "button", icon: "wxo-align-right" },
		],
	},
];
```

##### Column Group

```js
const items = [
	{
		layout: "column",
		text: "Font",
		items: [
			{
				items: [
					{
						key: "font-family",
						comp: "richselect",
						options: fontFamilyData,
					},
					{
						key: "font-size",
						comp: "richselect",
						options: fontSizeData,
					},
				],
			},
			{
				items: [
					{ id: "font-bold", comp: "button", icon: "wxo-bold" },
					{ id: "font-italic", comp: "button", icon: "wxo-italic" },
					{
						id: "font-underline",
						comp: "button",
						icon: "wxo-underline",
					},
				],
			},
		],
	},
];
```

##### Ribbon Layout

```js
const items = [
	{
		items: [
			{
				layout: "column",
				items: [
					{
						id: "load",
						css: "bigButton",
						comp: "button",
						icon: "wxi-file",
						text: "Load",
					},
				],
			},
			{
				layout: "column",
				items: [
					{ id: "undo", comp: "button", icon: "wxo-undo" },
					{ id: "redo", comp: "button", icon: "wxo-redo" },
				],
			},
		],
	},
	{ comp: "separator" },
	{
		layout: "column",
		items: [
			{
				items: [
					{
						key: "font-family",
						comp: "richselect",
						options: fontFamilyData,
					},
				],
			},
			{ items: [{ id: "font-bold", comp: "button", icon: "wxo-bold" }] },
		],
	},
];
```

##### Initially-Collapsed Group

```js
const items = [
	{
		text: "Data",
		icon: "wxi-dots-v",
		collapsed: true,
		layout: "column",
		items: [{ id: "load" }, { id: "delete" }],
	},
];
```

##### Header Menu

```vue
<template>
  <Toolbar
    :values="{ name: 'Item X12-A' }"
    :items="[
      { comp: 'label', spacer: true, key: 'name' },
      { comp: 'separator' },
      {
        icon: 'wxi-dots-v',
        collapsed: true,
        layout: 'column',
        items: [
          { id: 'done', comp: 'item', text: 'Mark as finished task' },
          {
            id: 'delete',
            comp: 'item',
            css: 'danger',
            text: 'Delete item',
          },
        ],
      },
    ]"
  />
</template>
```

##### Vertical Toolbar

```vue
<template>
  <Toolbar
    layout="column"
    :items="[
      { id: 'new', comp: 'button', icon: 'wxi-plus' },
      { id: 'edit', comp: 'button', icon: 'wxi-edit-outline' },
      { comp: 'separator' },
      { id: 'delete', comp: 'button', icon: 'wxi-delete-outline' },
    ]"
  />
</template>
```


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
