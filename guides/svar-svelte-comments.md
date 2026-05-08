# svar-svelte — comments

_Generated 2026-05-08T13:35:37.017Z_

## Contents

- [`comments/index.md`](#file-comments-index-md)
- [`locales.md`](#file-locales-md)
- [`themes.md`](#file-themes-md)


## File: comments/index.md

> Source: `comments/index.md`

Use when building, configuring, styling, localizing, or integrating SVAR Svelte Comments / @svar-ui/svelte-comments components

#### Package

```js
import { Comments, Willow, WillowDark } from "@svar-ui/svelte-comments";
```

Top-level exports:

- `Comments` - comments list with add, edit, delete, async data loading, built-in message layouts, and text/markdown rendering
- `Willow`, `WillowDark` - theme wrappers that forward to `@svar-ui/svelte-core` themes and add comments CSS variables

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
- `value` is not `$bindable`; keep parent state or backend state synchronized from `onchange`

##### Rendering Modes

- `render="flow"` is the default layout
- `render="bubbles"` uses chat-style bubbles
- custom `render` component receives `owned`, `edit`, `author`, `date`, and a `children` snippet from source
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
import type { Component } from "svelte";

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

- root list: `.wx-comments-list` is `height: 100%`
- scroll body: `.wx-list` is flex column
- message stack: `.wx-messages`
- flow layout: `.wx-flow`, `.wx-flow.wx-owned`, `.wx-flow-toolbar`, `.wx-message`, `.wx-menu-icon`, `.wx-comment-date`
- bubble layout: `.wx-bubble`, `.wx-bubble.wx-owned`, `.wx-bubble-wrapper`, `.wx-main-bubble`, `.wx-agent-message`, `.wx-avatar`, `.wx-message`
- shared message hooks: `.wx-author-name`, `.wx-menu-icon`, `.wx-comment-date`, `.wx-owned`
- composer hooks: `.wx-comments-textarea`, `.wx-comments-textarea.wx-flow`, `.wx-textarea-wrapper`, `.wx-textarea-avatar`, `.wx-textarea-bottombar`
- avatar hooks: `.wx-user`, `.wx-user.wx-small`, `.wx-user.wx-normal`, `.wx-border`, `.wx-comments-avatar-color-light`, `.wx-comments-avatar-color-dark`
- edit/delete menu is rendered by `@svar-ui/svelte-menu`
- package CSS variables: `--wx-comments-msg-background`, `--wx-comments-msg-background-agent`, `--wx-avatar-color-dark`

```svelte
<div class="comments-pane">
	<Comments value={comments} {users} activeUser={1} />
</div>

<style>
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

```svelte
<script>
	import { Comments } from "@svar-ui/svelte-comments";

	let comments = $state([
		{ id: 1, user: 1, content: "First comment", date: new Date() },
	]);

	const users = [
		{ id: 1, name: "Alice Smith", avatar: "/avatars/alice.png" },
		{ id: 2, name: "Marta Kowalska", color: "#e23a43" },
	];
</script>

<Comments value={comments} {users} activeUser={1} focus={true} />
```

##### Persist Changes

```svelte
<script>
	import { Comments } from "@svar-ui/svelte-comments";

	let comments = $state([]);
	const activeUser = { id: 1, name: "Alice Smith" };

	async function saveChange(ev) {
		comments = ev.value;

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

<Comments value={comments} onchange={saveChange} activeUser={activeUser} />
```

##### Load By External Key

```svelte
<script>
	import { Comments } from "@svar-ui/svelte-comments";

	let pageId = $state(1);
	const users = [{ id: 1, name: "Alice Smith" }];

	function loadComments(id) {
		return api.getComments(id);
	}

	function saveComment({ action, comment, id, originalValue }) {
		return api.forPage(originalValue).save(action, comment, id);
	}
</script>

<Comments
	value={pageId}
	ondata={loadComments}
	onchange={saveComment}
	{users}
	activeUser={1}
/>
```

##### Switch Layout Or Markdown

```svelte
<script>
	import { Comments } from "@svar-ui/svelte-comments";

	let render = $state("flow");
	const comments = [
		{ id: 1, user: 1, content: "### Title\n\n**Markdown** text" },
	];
	const users = [{ id: 1, name: "Alice Smith" }];
</script>

<Comments
	value={comments}
	{users}
	activeUser={1}
	{render}
	format="markdown"
/>
```

##### Custom Message And Content Renderers

```svelte
<!-- MessageRenderer.svelte -->
<script>
	let { owned, author, date, children } = $props();
</script>

<div class:owned style="padding-left: 8px">
	<b>{author.name}</b>
	<span>{date.toLocaleString()}</span>
	{@render children()}
</div>
```

```svelte
<!-- ContentRenderer.svelte -->
<script>
	let { content } = $props();
</script>

<span class="content">{content.toUpperCase()}</span>
```

```svelte
<script>
	import { Comments } from "@svar-ui/svelte-comments";
	import MessageRenderer from "./MessageRenderer.svelte";
	import ContentRenderer from "./ContentRenderer.svelte";

	const users = [{ id: 1, name: "Alice Smith" }];
	const comments = [{ id: 1, user: 1, content: "Hello", date: new Date() }];
</script>

<Comments
	value={comments}
	users={users}
	activeUser={1}
	render={MessageRenderer}
	format={ContentRenderer}
/>
```

#### Implementation Notes

- there is no public item registration API; custom renderers are passed directly through `render` and `format`


## File: locales.md

> Source: `locales.md`

i18n patterns common to all SVAR Svelte components - Locale wrapper, bundled language packs, extending words and formats

### Localizing SVAR Svelte Components

All `@svar-ui/svelte-*` widgets read locale data from a single Svelte context (`wx-i18n`). The mechanics live in `@svar-ui/svelte-core`; every other package consumes them.

#### Locale Wrapper

Wrap the subtree you want to localize. With no wrapper, widgets fall back to English.

```svelte
<script>
    import { Calendar, Locale } from "@svar-ui/svelte-core";
    import { de } from "@svar-ui/core-locales";
</script>

<Locale words={de}>
    <Calendar value={new Date(2025, 4, 1)} />
</Locale>
```

Wrap the smallest subtree that needs the alternative locale - nested `Locale` blocks let different parts of the app render in different languages.

`Locale` does not render any DOM wrapper; it only mutates context, so it never affects layout.

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

If you see English fallbacks in a localized UI, the missing terms come from the package's own locale module - merge them in via `Locale words={...}`.

To localize a standalone widget, merge the matching package locale with the core locale:

```svelte
<script>
    import { Gantt } from "@svar-ui/svelte-gantt";
    import { Locale } from "@svar-ui/svelte-core";
    import { cn } from "@svar-ui/gantt-locales";
    import { cn as cnCore } from "@svar-ui/core-locales";
</script>

<Locale words={{ ...cn, ...cnCore }}>
    <Gantt {...settings} />
</Locale>
```

#### Extending Or Overriding Words

`Locale words` accepts a partial pack and extends the current context. Spread an existing pack to keep its formats and override only what you need:

```svelte
<script>
    import { Calendar, Locale } from "@svar-ui/svelte-core";
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

<Locale {words}>
    <Calendar value={new Date(2025, 4, 1)} />
</Locale>
```

Pass `optional={true}` to make merged terms additive fallbacks rather than overrides - useful for layering app-specific strings on top of a full pack.

#### Affected Surfaces

Locale changes calendar labels, date/time formats, modal buttons, pager strings, empty-list text, notice/modal helpers, color-board select text - any widget that displays static strings or formats values reads them through this context.

#### Direct Helper

For non-component code, use the `locale` helper to build a translator:

```js
import { en, locale } from "@svar-ui/svelte-core";

const i18n = locale(en).extend(
    { core: { "Rows per page": "Rows" } },
    true
);
const _ = i18n.getGroup("core");
_("Rows per page"); // "Rows"
```


## File: themes.md

> Source: `themes.md`

### Styling SVAR Svelte Components

All `@svar-ui/svelte-*` widgets share the same theming pipeline. The mechanics live in `@svar-ui/svelte-core`; every other package consumes them.

#### Theme Wrapper

Wrap the part of the app that uses SVAR widgets in a theme component from `@svar-ui/svelte-core`:

```svelte
<script>
    import { Willow } from "@svar-ui/svelte-core";
</script>

<Willow>
    <App />
</Willow>
```

Available themes: `Willow`, `WillowDark`. The wrapper:

- sets the Svelte context `wx-theme`
- renders `.wx-theme.wx-{name}-theme` with `height:100%`
- loads Open Sans + the `wxi` icon CSS by default; pass `fonts={false}` to skip when the host app manages fonts itself

Without a theme wrapper widgets still render but lose theme variables and font/icon CSS.

#### Per-widget Willow / WillowDark themes

Several widgets ship their **own** `Willow` / `WillowDark` components on top of the core base. The widget version wraps the core theme and layers in widget-specific CSS variables (bar colors, grid borders, timescale fonts, etc.). When using such a widget, import the theme from the widget package - not from core - so both layers apply.

Widgets that expose custom `Willow` / `WillowDark` themes:

- `@svar-ui/svelte-core` - base
- `@svar-ui/svelte-gantt`
- `@svar-ui/svelte-grid`
- `@svar-ui/svelte-editor`
- `@svar-ui/svelte-filter`
- `@svar-ui/svelte-filemanager`
- `@svar-ui/svelte-comments`
- `@svar-ui/svelte-kanban`

The widget theme delegates to core and adds extra rules scoped to `.wx-willow-theme` (or `.wx-willow-dark-theme`):

```svelte
<script>
    import { Willow } from "@svar-ui/svelte-core";
    let { fonts = true, children } = $props();
</script>

{#if children}
    <Willow {fonts}>{@render children()}</Willow>
{:else}
    <Willow {fonts} />
{/if}

<style>
    :global(.wx-willow-theme) {
        --wx-gantt-border-color: #e6e6e6;
        --wx-gantt-task-color: #3983eb;
        /* ...widget-specific overrides... */
    }
</style>
```

Mount the widget's own theme once at the app root. The wrapper internally renders the core `Willow`, so a separate core import is not needed:

```svelte
<script>
    import { Willow } from "@svar-ui/svelte-gantt";
    import { Gantt } from "@svar-ui/svelte-gantt";
</script>

<Willow />
<Gantt {...settings} />
```

#### CSS Variables

Theme styling is variable-driven. Override variables on the theme wrapper or on any ancestor of the widgets you want to restyle - overrides cascade to every SVAR widget in the subtree.

```svelte
<Willow>
    <div class="brand">
        <App />
    </div>
</Willow>

<style>
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

```svelte
<Toolbar css="my-toolbar" {items} />

<style>
    .my-toolbar {
        padding: 8px 12px;
    }
</style>
```

Composite widgets often expose secondary css props for nested popups (`menuCss` on `Toolbar`/`MenuBar`, etc.). Check the per-component file for the exact set.

#### Class Hooks

The per-component file lists the exact selectors that widget exposes.

#### Custom CSS class overrides

When writing custom rules to override widget styles, always use **at least two selectors** (e.g. `.a .b {}`). Svelte scopes its component styles by appending a hash class which has higher specificity than a plain `.b`. A two-selector rule (`.a .b`) matches or beats that specificity and wins.

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
