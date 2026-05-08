# svar-vue — editor

_Generated 2026-05-08T13:35:37.091Z_

## Contents

- [`editor/index.md`](#file-editor-index-md)
- [`locales.md`](#file-locales-md)
- [`themes.md`](#file-themes-md)


## File: editor/index.md

> Source: `editor/index.md`

Use when building, configuring, styling, or modifying SVAR Vue Editor / @svar-ui/vue-editor forms, field items, validation, save flows, panels, toolbars, sections, batches, or custom editor item renderers.

#### Package

```js
import {
	Editor,
	registerEditorItem,
	Willow,
	WillowDark,
} from "@svar-ui/vue-editor";

import "@svar-ui/vue-editor/all.css";
```

#### Supported functionality

##### Components

- `Editor` - main editor shell with inline, sidebar, or modal placement, optional top/bottom toolbars, sections, columns layout, validation, hotkeys, and save flow.
- `registerEditorItem(type, handler)` - registers a Vue component for `item.comp`.
- `Willow`, `WillowDark` - wrappers around matching `@svar-ui/vue-core` themes

##### Built-in item components

- `text` - registered to `Text` from `@svar-ui/vue-core`; default when `comp` is omitted.
- `textarea` - registered to `TextArea` from `@svar-ui/vue-core`.
- `checkbox` - registered to `Checkbox` from `@svar-ui/vue-core`.
- `section` - expandable section header; toggles items whose `section` matches its `key`.
- `readonly` - read-only field renderer used when `readonly={true}`.
- `hidden` - special `comp`; participates in value extraction/diffing but is filtered from rendering.

Common item configurations:

```js
{ comp: "text", key: "name", label: "Name" }
{ comp: "textarea", key: "descr", label: "Description", config: { placeholder: "Add description" } }
{ comp: "checkbox", key: "admin", label: "Is Admin" }
{ comp: "hidden", key: "state" }
{ comp: "section", key: "details", label: "Details", activeSection: true }
{ comp: "text", key: "email", label: "Email", section: "details" }
```

##### External and custom item components

- `item.comp` can be a registered string or a Vue component directly, use `registerEditorItem` to link component to string
- Normal field components receive `value`, `onchange`, `error`, all item fields, and promoted `config` fields; `label` is set to `undefined`
- `section` and `readonly` receives all item fields, and `onclick` for section toggling.
- A custom item must call `onchange({ value })`; it may include `input` to mark input-origin (in-progress) updates.

##### Values and binding

- `values` is an object; each rendered editor reads and writes `values[item.key]`
- String keys containing dots use nested getter/setter functions, for example `key: "user.name"` reads/writes `values.user.name`.
- `config` is shallow-merged into the item before rendering, so `config: { placeholder: "Name" }` becomes a direct prop.
- Custom `getter` and `setter` functions on an item replace the default key access.
- `labelTemplate(value)` replaces the displayed label for normal fields.
- `options` are passed through to item components and are also used by `readonly` to map `value` to `option.label` by matching `option.id`.

##### Events and save flow

- Field change order: child item `onchange({ value, input? })` -> editor `onchange({ key, value, update, input? })` -> diff/validation -> save handling.
- `onchange` can replace `ev.update` to update multiple fields from one field change.
- With `autoSave={true}`, valid changes are written back to the original `values` object and `onsave({ changes, values })` fires immediately.
- With `autoSave={false}`, changed keys stay in `notSaved` until "save" button click ( toolbar item `id: "save"` ) runs validation and save.
- Toolbar action order: internal save or section toggle is handled first, then `onaction({ item, values, changes })` fires.
- Parent code must hide modal/sidebar editors in `onaction`; `cancel`, `close`, and custom actions do not remove the component themselves.
- `onvalidation({ errors, values })` fires when validation result changes; `errors` can be `null`.
- Runtime `changes` is an array of changed keys

##### Validation

- `required: true` fails when `!values[key]`
- `validation(value)` must return truthy for valid values.
- `validationMessage` overrides the displayed error text.
- Required errors use `{ errorType: "required" }`; custom validation errors use `{ errorType: "validation" }`.

##### Sections and batches

- A `section` item toggles all items whose `section` equals the section item `key`.
- `activeSection: true` opens a section initially.
- Normal sections can be toggled independently.
- `sectionMode: "accordion"` opens one section and closes other sections; an open accordion section does not close itself on click.
- `sectionMode: "exclusive"` shows only the active section header and its children.
- `activeBatch` hides every item whose `batch` does not equal `activeBatch`; when `activeBatch` is set, items without a matching `batch` are hidden.

##### Layout, placement, toolbar, and hotkeys

- `placement="inline"` renders `.wx-inline-form`; `placement="sidebar"` renders inside `SideArea`; `placement="modal"` renders inside `ModalArea`.
- `layout="columns"` splits items by `item.column`: `"left"` goes to `.wx-left`, everything else goes to `.wx-right`.
- `topBar` and `bottomBar` accept `false`, `true`, or `{ items: IToolbarItem[] }`; toolbar items are passed to `@svar-ui/vue-toolbar`.
- Automatic default bars are generated only when `topBar === true && bottomBar === true`.
- Automatic manual-save modal uses bottom `{ spacer, save, cancel }`; modal columns use top `{ spacer, save, cancel }`; inline/sidebar manual save uses top `{ spacer, cancel, save }`; auto-save and read-only use top `{ spacer, close }`.
- Toolbar `onchange({ item, value })` is mapped into editor field changes as `{ key: item.key, value }`, so toolbar controls can edit `values`.
- Default hotkeys are enabled unless `hotkeys={false}`: `ctrl+s` triggers save, `escape` triggers cancel/close, and `delete` triggers a `delete` toolbar item when present.
- Custom `hotkeys` are merged with defaults.
- `focus={true}` selects and focuses the first enabled input, textarea, or select after mount.
- Editor `children` render above generated fields inside the content area; demos use this for tabs, segmented controls, and external toolbars.

#### Public Types

```ts
import type { Component } from "vue";
import type { IToolbarItem } from "@svar-ui/vue-toolbar";

export declare const Editor: Component<{
	values?: Record<string, any>;
	items?: {
		comp?: string | Component;
		key?: string;
		label?: string;
		labelTemplate?: (value: any) => string;
		column?: "right" | "left";
		batch?: string | number;
		hidden?: boolean;
		section?: string;
		sectionMode?: "accordion" | "exclusive";
		activeSection?: boolean;
		options?: {
			id?: string | number;
			label?: string;
			[key: string]: any;
		}[];
		required?: boolean;
		validation?: (value: any) => boolean;
		validationMessage?: string;
		config?: {
			[key: string]: any;
		};
		[key: string]: any;
	}[];
	css?: string;
	activeBatch?: string | number;
	topBar?: boolean | { items: IToolbarItem[] };
	bottomBar?: boolean | { items: IToolbarItem[] };
	autoSave?: boolean;
	layout?: "default" | "columns";
	placement?: "inline" | "sidebar" | "modal";
	readonly?: boolean;
	focus?: boolean;
	onchange?: (ev: {
		key: string;
		value: any;
		update: Record<string, any>;
		input?: boolean;
	}) => void;
	onsave?: (ev: {
		changes: string[];
		values: Record<string, any>;
	}) => void;
	onaction?: (ev: {
		item: IToolbarItem;
		values: Record<string, any>;
		changes: string[];
	}) => void;
	onvalidation?: (ev: {
		errors: {
			[key: string]: {
				errorType: "validation" | "required";
			};
		};
		values: Record<string, any>;
	}) => void;
	hotkeys?:
		| false
		| { [key: string]: ((e?: KeyboardEvent) => void) | boolean };
	children?: () => any;
}>;

export declare function registerEditorItem(
	type: string,
	handler: Component<any>
): void;

export declare const Willow: Component<{
	fonts?: boolean;
	children?: () => any;
}>;

export declare const WillowDark: Component<{
	fonts?: boolean;
	children?: () => any;
}>;
```

#### Styling

Import the package CSS before using the component (`all.css` includes dependency styles, `style.css` is this component only)

- `Editor` `css` is appended to the root panel: `.wx-inline-form {css}` for inline placement, `.wx-panel {css}` for modal/sidebar placement.
- Root panel classes: `.wx-inline-form`, `.wx-panel`.
- Content container: `.wx-content`; columns mode adds `.wx-layout-columns`.
- Form body: `.wx-sections` with `--wx-field-width: 600px`.
- Columns layout: `.wx-cols`, `.wx-left`, `.wx-right`; source defaults include `.wx-left { min-width: 640px }`, `.wx-right { width: 364px; background: var(--wx-background-alt) }`.
- Toolbar wrapper: `.wx-editor-toolbar`, `.wx-topbar`, `.wx-bottom`
- Section header: `.wx-section`, `.wx-section-active`, nested `.wx-icon`
- Validation and empty states: `.wx-message`, `.wx-overlay`

```vue
<template>
  <Editor :items="items" :values="values" layout="columns" css="task-editor" />
</template>

<style scoped>
.task-editor .wx-sections {
	--wx-field-width: 520px;
	margin: 8px 16px 0;
}

.task-editor .wx-editor-toolbar {
	padding: 0 16px;
}

.task-editor .wx-cols .wx-left {
	min-width: 520px;
}

.task-editor .wx-cols .wx-right {
	width: 320px;
	margin-left: 20px;
}
</style>
```

#### Recipes

##### Basic Inline Editor

```vue
<script setup>
import { ref } from "vue";
import { Editor } from "@svar-ui/vue-editor";

const items = [
	{ comp: "text", key: "name", label: "Name" },
	{ comp: "checkbox", key: "admin", label: "Is Admin" },
	{ comp: "textarea", key: "descr", label: "Description" },
];

const values = ref({
	name: "John Doe",
	admin: true,
	descr: "Notes",
});
</script>

<template>
  <Editor :items="items" :values="values" :topBar="false" />
</template>
```

##### Manual Save With Validation

```vue
<script setup>
import { ref } from "vue";
import { Editor } from "@svar-ui/vue-editor";

const items = [
	{ comp: "text", key: "firstName", label: "First name", required: true },
	{
		comp: "text",
		key: "email",
		label: "Email",
		validation: value => value.includes("@"),
		validationMessage: "Incorrect email",
	},
];

const values = ref({ firstName: "John", email: "john@example.org" });
const visible = ref(true);

function handleAction({ item, changes }) {
	if (item.id === "save" && changes.length) return;
	visible.value = false;
}

function handleSave({ values: next }) {
	values.value = next;
	visible.value = false;
}
</script>

<template>
  <Editor
    v-if="visible"
    placement="sidebar"
    :autoSave="false"
    :items="items"
    :values="values"
    :onaction="handleAction"
    :onsave="handleSave"
  />
</template>
```

##### Auto Save Sidebar With Custom Toolbar

```vue
<script setup>
import { ref } from "vue";
import { Editor } from "@svar-ui/vue-editor";

const items = [
	{ comp: "text", key: "label", label: "Label" },
	{ comp: "textarea", key: "description", label: "Description" },
];

const values = ref({ id: 1, label: "Task", description: "" });
const open = ref(true);

function handleAction({ item }) {
	if (item.id === "close" || item.id === "delete") open.value = false;
}

function handleSave({ values: next }) {
	values.value = next;
}
</script>

<template>
  <Editor
    v-if="open"
    placement="sidebar"
    :autoSave="true"
    :topBar="{
      items: [
        { comp: 'icon', icon: 'wxi-close', id: 'close' },
        { comp: 'spacer' },
        { comp: 'button', type: 'danger', text: 'Delete', id: 'delete' },
        { comp: 'button', type: 'primary', text: 'Save', id: 'save' },
      ],
    }"
    :items="items"
    :values="values"
    :onaction="handleAction"
    :onsave="handleSave"
  />
</template>
```

##### Update Multiple Values From One Change

```vue
<script setup>
import { ref } from "vue";
import { Editor, registerEditorItem } from "@svar-ui/vue-editor";
import { Combo } from "@svar-ui/vue-core";

registerEditorItem("combo", Combo);

const items = ref([
	{
		comp: "combo",
		key: "country",
		label: "Country",
		options: [
			{ id: "france", label: "France" },
			{ id: "poland", label: "Poland" },
		],
	},
	{ comp: "combo", key: "city", label: "City", disabled: true },
]);

const cities = {
	france: [{ id: "paris", label: "Paris" }],
	poland: [{ id: "warsaw", label: "Warsaw" }],
};

const values = ref({ country: "", city: "" });

function handleChange(ev) {
	if (ev.key !== "country") return;

	items.value[1] = {
		...items.value[1],
		disabled: false,
		options: cities[ev.value],
	};

	ev.update = {
		country: ev.value,
		city: "",
	};
}
</script>

<template>
  <Editor :items="items" :values="values" :onchange="handleChange" :topBar="false" />
</template>
```

##### Register A Custom Item

```vue
<!-- PriorityCombo.vue -->
<script setup>
import { Combo } from "@svar-ui/vue-core";

const props = defineProps({
  value: {},
  options: {},
  onchange: { type: Function },
});
</script>

<template>
  <Combo :value="props.value" :options="props.options" :onchange="props.onchange">
    <template #children="{ option }">
      <span class="priority-dot" :style="{ background: option.color }"></span>
      {{ option.label }}
    </template>
  </Combo>
</template>
```

```vue
<script setup>
import { ref } from "vue";
import { Editor, registerEditorItem } from "@svar-ui/vue-editor";
import PriorityCombo from "./PriorityCombo.vue";

registerEditorItem("priority-combo", PriorityCombo);

const items = [
	{
		comp: "priority-combo",
		key: "priority",
		label: "Priority",
		config: { clearButton: true },
		options: [
			{ id: 1, label: "High", color: "#FE6158" },
			{ id: 2, label: "Low", color: "#77D257" },
		],
	},
];

const values = ref({ priority: 1 });
</script>

<template>
  <Editor :items="items" :values="values" :topBar="false" />
</template>
```

##### Sections And Accordion Panels

```vue
<script setup>
import { ref } from "vue";
import { Editor } from "@svar-ui/vue-editor";

const items = [
	{
		comp: "section",
		key: "personal",
		label: "Personal Info",
		activeSection: true,
		sectionMode: "accordion",
	},
	{ comp: "text", key: "name", label: "Name", section: "personal" },
	{
		comp: "section",
		key: "settings",
		label: "Settings",
		sectionMode: "accordion",
	},
	{ comp: "checkbox", key: "admin", label: "Is admin", section: "settings" },
];

const values = ref({ name: "John", admin: false });
</script>

<template>
  <Editor :items="items" :values="values" :topBar="false" />
</template>
```

##### Batch Switcher In Children

```vue
<script setup>
import { ref } from "vue";
import { Editor } from "@svar-ui/vue-editor";
import { Segmented } from "@svar-ui/vue-core";

const options = [
	{ id: "main", label: "Personal" },
	{ id: "cfg", label: "Settings" },
];

const items = [
	{ comp: "text", key: "name", label: "Name", batch: "main" },
	{ comp: "textarea", key: "descr", label: "Description", batch: "main" },
	{ comp: "checkbox", key: "admin", label: "Is Admin", batch: "cfg" },
];

const values = ref({ name: "John", descr: "", admin: false });
const activeBatch = ref("main");
</script>

<template>
  <Editor :topBar="false" :items="items" :values="values" :activeBatch="activeBatch">
    <Segmented :options="options" v-model:value="activeBatch" />
  </Editor>
</template>
```

##### Modal Columns Layout

```vue
<script setup>
import { ref } from "vue";
import { Editor } from "@svar-ui/vue-editor";

const items = [
	{ comp: "text", key: "name", label: "Name", column: "left" },
	{ comp: "textarea", key: "descr", label: "Description", column: "left" },
	{ comp: "checkbox", key: "admin", label: "Is Admin" },
];

const values = ref({ name: "John", descr: "", admin: false });
const visible = ref(true);
</script>

<template>
  <Editor
    v-if="visible"
    placement="modal"
    layout="columns"
    :autoSave="false"
    :items="items"
    :values="values"
    :onaction="() => (visible = false)"
  />
</template>
```

#### Implementation Notes

- `onvalidation` can receive `errors: null`
- Dot-path keys assume intermediate objects already exist for default getter/setter access.
- `config` is promoted into top-level item props and also remains as `item.config`.
- `readonly={true}` converts every rendered item to the built-in `readonly` renderer.
- `Action` toolbar items with `id: "save"` are special; other IDs are forwarded through `onaction`
- `SideArea` cancel trigger `onaction` with `item.id === "close"`.


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
