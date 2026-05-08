# svar-vue — comments

_Generated 2026-05-08T13:35:37.091Z_

## Contents

- [`comments/index.md`](#file-comments-index-md)
- [`locales.md`](#file-locales-md)
- [`themes.md`](#file-themes-md)


## File: comments/index.md

> Source: `comments/index.md`

Use when building, configuring, styling, localizing, or integrating SVAR Vue Comments / @svar-ui/vue-comments components

#### Package

```js
import { Comments, Willow, WillowDark } from "@svar-ui/vue-comments";
import "@svar-ui/vue-comments/all.css";
```

Top-level exports:

- `Comments` - comments list with add, edit, delete, async data loading, built-in message layouts, and text/markdown rendering
- `Willow`, `WillowDark` - theme wrappers that forward to `@svar-ui/vue-core` themes and add comments CSS variables

#### Supported functionality

##### Data And Users

- `value` is either an `IComment[]` or a truthy key passed to `ondata(value)`
- `ondata(value)` may return `IComment[]` or `Promise<IComment[]>`; while pending, the layout renders with `data=[]`
- `IComment.author` object wins when present; otherwise `IComment.user` is resolved against `users`
- users without `color` get a generated HSL color from `id + name`
- unknown users render as `{ id: 0, name: "Unknown", color: "hsl(0, 0%, 85%)" }`
- `activeUser` can be a user id or an `IUser`; new comments use it for `author` and `user`
- source date formatting uses `comments.dateFormat` or locale specific
-
Common data objects:

```js
const users = [
	{ id: 1, name: "Alice Smith", avatar: "/avatars/alice.png" },
	{ id: 2, name: "Marta Kowalska", color: "#e23a43" },
];

const value = [
	{ id: 1, user: 1, content: "Plain text", date: new Date() },
	{ id: 2, author: users[1], content: "**Markdown**", format: "markdown" },
];
```

##### Change Flow

- add creates `{ id: uid(), content, author, user: author.id, date: new Date() }`
- add/update/delete replace internal data with a new array before calling `onchange`
- add payload: `{ action: "add", value, comment, originalValue }`
- update payload: `{ action: "update", value, id, comment, originalValue }`
- delete payload: `{ action: "delete", value, id, originalValue }`
- if add `onchange` returns an object or promise, returned fields are merged into the newly added comment
- `value` is not two-way bindable; keep parent state or backend state synchronized from `onchange`

##### Rendering Modes

- `render="flow"` is the default layout
- `render="bubbles"` uses chat-style bubbles
- custom `render` component receives `owned`, `edit`, `author`, `date`, and a `children` slot from source
- `format="text"` is the default content renderer
- `format="markdown"` renders markdown content through the bundled Lima renderer
- custom `format` component receives `{ content }`
- per-comment `comment.format` overrides the component-level `format`

Built-ins:

```js
{ render: "flow" }
{ render: "bubbles" }
{ format: "text" }
{ format: "markdown" }
```

##### Editing And Deleting

- owned comments are comments where `message.author.id === active author id`
- only owned comments get the visible menu icon
- internal action menu options are `edit-comment` and `delete-comment`
- edit mode replaces message content with the same textarea component used for posting
- `Ctrl+Enter` or `Cmd+Enter` posts textarea content
- empty textarea content is ignored

#### Public Types

```ts
import type { Component } from "vue";

export interface IUser {
	id: string | number;
	name?: string;
	avatar?: string;
	color?: string;
}

export interface IComment {
	id?: string | number;
	content: string;
	author?: IUser;
	user?: string | number;
	date?: Date;
	format?: "text" | "markdown" | FormatComponent;
}

export interface IChange {
	action: "add" | "update" | "delete";
	id?: string | number;
	comment?: IComment;
	value: IComment[];
	originalValue: IComment[] | string | number;
}

export type FormatComponent = Component<{
	content: string;
}>;

export type RenderComponent = Component<{
	owned?: string | number;
	edit?: string | number;
	author: IUser;
	date: Date;
}>;

export declare const Comments: Component<{
	ondata?: (value: string | number) => Promise<IComment[]> | IComment[];
	onchange?: (ev: IChange) => void;
	value?: IComment[] | string | number;
	readonly?: boolean;
	render?: "bubbles" | "flow" | RenderComponent;
	format?: "text" | "markdown" | FormatComponent;
	users?: IUser[];
	activeUser?: string | number | IUser;
	focus?: boolean;
}>;

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

- root list: `.wx-comments-list` is `height: 100%`
- scroll body: `.wx-list` is flex column
- message stack: `.wx-messages`
- flow layout: `.wx-flow`, `.wx-flow.wx-owned`, `.wx-flow-toolbar`, `.wx-message`, `.wx-menu-icon`, `.wx-comment-date`
- bubble layout: `.wx-bubble`, `.wx-bubble.wx-owned`, `.wx-bubble-wrapper`, `.wx-main-bubble`, `.wx-agent-message`, `.wx-avatar`, `.wx-message`
- shared message hooks: `.wx-author-name`, `.wx-menu-icon`, `.wx-comment-date`, `.wx-owned`
- composer hooks: `.wx-comments-textarea`, `.wx-comments-textarea.wx-flow`, `.wx-textarea-wrapper`, `.wx-textarea-avatar`, `.wx-textarea-bottombar`
- avatar hooks: `.wx-user`, `.wx-user.wx-small`, `.wx-user.wx-normal`, `.wx-border`, `.wx-comments-avatar-color-light`, `.wx-comments-avatar-color-dark`
- edit/delete menu is rendered by `@svar-ui/vue-menu`
- package CSS variables: `--wx-comments-msg-background`, `--wx-comments-msg-background-agent`, `--wx-avatar-color-dark`

```vue
<template>
  <div class="comments-pane">
    <Comments :value="comments" :users="users" :activeUser="1" />
  </div>
</template>

<style scoped>
.comments-pane {
	height: 480px;
	max-width: 760px;
}

.comments-pane .wx-comments-list {
	border: var(--wx-border);
}

.comments-pane .wx-flow {
	padding: 12px 16px;
}

.comments-pane .wx-comments-textarea {
	padding-top: 8px;
}
</style>
```

#### Recipes

##### Basic Comments

```vue
<script setup>
import { ref } from "vue";
import { Comments } from "@svar-ui/vue-comments";

const comments = ref([
	{ id: 1, user: 1, content: "First comment", date: new Date() },
]);

const users = [
	{ id: 1, name: "Alice Smith", avatar: "/avatars/alice.png" },
	{ id: 2, name: "Marta Kowalska", color: "#e23a43" },
];
</script>

<template>
  <Comments :value="comments" :users="users" :activeUser="1" :focus="true" />
</template>
```

##### Persist Changes

```vue
<script setup>
import { ref } from "vue";
import { Comments } from "@svar-ui/vue-comments";

const comments = ref([]);
const activeUser = { id: 1, name: "Alice Smith" };

async function saveChange(ev) {
	comments.value = ev.value;

	if (ev.action === "add") {
		return await api.createComment(ev.comment);
	}

	if (ev.action === "update") {
		await api.updateComment(ev.id, ev.comment);
	}

	if (ev.action === "delete") {
		await api.deleteComment(ev.id);
	}
}
</script>

<template>
  <Comments :value="comments" :onchange="saveChange" :activeUser="activeUser" />
</template>
```

##### Load By External Key

```vue
<script setup>
import { ref } from "vue";
import { Comments } from "@svar-ui/vue-comments";

const pageId = ref(1);
const users = [{ id: 1, name: "Alice Smith" }];

function loadComments(id) {
	return api.getComments(id);
}

function saveComment({ action, comment, id, originalValue }) {
	return api.forPage(originalValue).save(action, comment, id);
}
</script>

<template>
  <Comments
    :value="pageId"
    :ondata="loadComments"
    :onchange="saveComment"
    :users="users"
    :activeUser="1"
  />
</template>
```

##### Switch Layout Or Markdown

```vue
<script setup>
import { ref } from "vue";
import { Comments } from "@svar-ui/vue-comments";

const render = ref("flow");
const comments = [
	{ id: 1, user: 1, content: "### Title\n\n**Markdown** text" },
];
const users = [{ id: 1, name: "Alice Smith" }];
</script>

<template>
  <Comments
    :value="comments"
    :users="users"
    :activeUser="1"
    :render="render"
    format="markdown"
  />
</template>
```

##### Custom Message And Content Renderers

```vue
<!-- MessageRenderer.vue -->
<script setup>
const props = defineProps({
  owned: {},
  author: {},
  date: {},
});
</script>

<template>
  <div :class="{ owned: props.owned }" style="padding-left: 8px">
    <b>{{ props.author.name }}</b>
    <span>{{ props.date.toLocaleString() }}</span>
    <slot />
  </div>
</template>
```

```vue
<!-- ContentRenderer.vue -->
<script setup>
const props = defineProps({ content: {} });
</script>

<template>
  <span class="content">{{ props.content.toUpperCase() }}</span>
</template>
```

```vue
<script setup>
import { Comments } from "@svar-ui/vue-comments";
import MessageRenderer from "./MessageRenderer.vue";
import ContentRenderer from "./ContentRenderer.vue";

const users = [{ id: 1, name: "Alice Smith" }];
const comments = [{ id: 1, user: 1, content: "Hello", date: new Date() }];
</script>

<template>
  <Comments
    :value="comments"
    :users="users"
    :activeUser="1"
    :render="MessageRenderer"
    :format="ContentRenderer"
  />
</template>
```

#### Implementation Notes

- there is no public item registration API; custom renderers are passed directly through `render` and `format`


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
