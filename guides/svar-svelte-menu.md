# svar-svelte — menu

_Generated 2026-05-08T13:35:37.017Z_

## Contents

- [`menu/index.md`](#file-menu-index-md)
- [`locales.md`](#file-locales-md)
- [`themes.md`](#file-themes-md)


## File: menu/index.md

> Source: `menu/index.md`

Use when UI of app requires Menu, MenuBar, DropDownMenu, ContextMenu, or ActionMenu / @svar-ui/svelte-menu components

#### Package

```js
import {
	Menu,
	MenuBar,
	DropDownMenu,
	ContextMenu,
	ActionMenu,
	registerMenuItem,
} from "@svar-ui/svelte-menu";
```

#### Components

- `Menu` - low-level popup menu positioned from `parent` or `left`/`top`
- `DropDownMenu` - wraps trigger content, opens a menu on click
- `ContextMenu` - wraps content, opens an action menu on `contextmenu`
- `ActionMenu` - reusable menu controller; wraps clickable content or opened with `bind:this` and `show(ev, obj)`
- `MenuBar` - horizontal menu bar; top-level items with `data` open submenus through an internal `ActionMenu`

#### Supported functionality

##### Events

- option `handler`, component `onclick`
- leaf click order: `option.handler(pack)` first, then component `onclick(pack)`, where `pack` is `{ context, option, event }`
- submenu parent options do not fire `onclick`; hover/click opens the child menu
- clicking outside an open menu calls `onclick({ action: null, option: null })`

##### Positioning

`at` defaults to `"bottom"` and is passed to `calculatePosition` from `@svar-ui/lib-dom`

- options: `bottom`, `right`, `left`, `top`, `bottom-right`, `bottom-left`, `bottom-fit`, `point`
- submenus internally use `at="right-overlap"`

##### Context resolution (ContextMenu, ActionMenu)

- `ActionMenu.show(ev, obj)` opens from event target, sets cursor coordinates from `ev.clientX/Y`, uses `obj` as `context`
- without `obj`, locates context from a data attribute derived from `dataKey`; default `dataKey="contextId"` means `data-context-id`
- `resolver(item, event)` can replace or reject context; falsy return prevents menu opening
- `filter(option, item)` hides leaf options for a context; groups remain only when filtered children remain

##### Option's properties

- `comp` - component name; built-in is `separator`; can also be a registered string renderer or a Svelte component
- `id` - stable key returned in callbacks and used by keyed rendering; missing ids generated during normalization
- `text`, `subtext` - default label and right-side helper text
- `icon` - appended to `wx-icon`, e.g. `"wxi wxi-content-copy"`
- `data` - creates nested submenu options
- `disabled` - adds `wx-disabled`, blocks pointer interaction
- `css` - appended to option wrapper `.wx-option`
- `handler` - per-option click handler
- deprecated `type` is copied to `comp`
- custom item components receive `option` object with all configured props

##### Common option configurations

```js
{ id: "edit", text: "Edit", icon: "wxi wxi-edit" }
{ id: "delete", text: "Delete", disabled: true }
{ id: "copy", text: "Copy", subtext: "Ctrl+C" }
{ id: "add", text: "Add", data: [/* submenu options */] }
{ comp: "separator" }
```

Custom renderers can be registered with `registerMenuItem("user", UserMenuItem)` and referenced as `comp: "user"`, or `comp` can be set to a Svelte component directly.

#### Public Types

```ts
import type { Component } from "svelte";

export interface IMenuOption {
	id?: string | number;
	text?: string;
	subtext?: string;
	handler?: (ev: IMenuOptionClick) => void;
	data?: IMenuOption[];
	css?: string;
	icon?: string;
	disabled?: boolean;
	comp?: string | Component<any>;
}

export interface IMenuOptionClick {
	context?: any;
	option: IMenuOption;
	event?: MouseEvent;
}

export declare const Menu: Component<{
	options?: IMenuOption[];
	left?: number;
	top?: number;
	at?: string;
	parent?: HTMLElement;
	mount?: (callback: () => void) => void;
	context?: any;
	css?: string;
	onclick?: (ev: IMenuOptionClick) => void;
}>;

export declare const MenuBar: Component<{
	css?: string;
	menuCss?: string;
	options?: IMenuOption[];
	onclick?: (ev: IMenuOptionClick) => void;
}>;

export declare const DropDownMenu: Component<{
	options?: IMenuOption[];
	at?: string;
	css?: string;
	children?: () => any;
	onclick?: (ev: IMenuOptionClick) => void;
}>;

export declare const ContextMenu: Component<{
	options?: IMenuOption[];
	at?: string;
	resolver?: (item: any, event: MouseEvent) => any;
	dataKey?: string;
	filter?: (option: IMenuOption, item: any) => boolean;
	css?: string;
	children?: () => any;
	onclick?: (ev: IMenuOptionClick) => void;
}>;

export declare const ActionMenu: Component<{
	options?: IMenuOption[];
	at?: string;
	resolver?: (item: any, event: MouseEvent) => any;
	dataKey?: string;
	filter?: (option: IMenuOption, item: any) => boolean;
	css?: string;
	children?: () => any;
	onclick?: (ev: IMenuOptionClick) => void;
}>;

export declare function registerMenuItem(
	type: string,
	handler: Component<{ option?: any }>
): void;
```

#### Styling

- for `Menu`/`DropDownMenu`/`ContextMenu`/`ActionMenu` - `css` is appended to `.wx-menu`; use it as the parent styling hook for the popup
- for `MenuBar` - `css` is appended to `.wx-menubar`; `menuCss` is passed to its popup `.wx-menu`
- `option.css` is appended to the option wrapper `.wx-option`

- menu container: `.wx-menu`
- menubar container: `.wx-menubar`
- option wrapper: `.wx-option`
- separator: `.wx-separator` and `.wx-separator-menu` (full width, `--wx-border-medium`)
- icons inside options: `.wx-icon`, `.wx-sub-icon`
- text parts: `.wx-value`, `.wx-subtext`
- state hooks: `.wx-active`, `.wx-disabled`
- `DropDownMenu`/`ActionMenu`/`ContextMenu` render through `Portal`; `css` targets the menu, not the trigger wrapper - style trigger child markup directly


```css
/* widen popup */
.app-menu {
	min-width: 200px;
}
```

#### Recipes

##### Dropdown With Click Handler

```svelte
<script>
	import { DropDownMenu } from "@svar-ui/svelte-menu";

	const options = [
		{
			id: "add",
			text: "Add",
			icon: "wxi wxi-plus",
			data: [
				{ id: "add-child", text: "Child task" },
				{ id: "add-below", text: "Task below" },
			],
		},
		{ comp: "separator" },
		{ id: "edit", text: "Edit", icon: "wxi wxi-edit" },
		{ id: "delete", text: "Delete", disabled: true },
	];

	function clicked(ev) {
		if (!ev.option) return;
		console.log(ev.option.id);
	}
</script>

<DropDownMenu {options} onclick={clicked} at="bottom-fit">
	<button>Open</button>
</DropDownMenu>
```

##### Low-Level Menu Anchored To An Element

```svelte
<script>
	import { Menu } from "@svar-ui/svelte-menu";

	const options = [{ id: "copy", text: "Copy" }];
	let parent = $state(null);

	function clicked() {
		parent = null;
	}
</script>

<button onclick={ev => (parent = ev.currentTarget)}>Open</button>

{#if parent}
	<Menu {options} {parent} at="right" onclick={clicked} />
{/if}
```

##### Menu Bar With Submenus

```svelte
<script>
	import { MenuBar } from "@svar-ui/svelte-menu";

	const options = [
		{
			id: "file",
			text: "File",
			data: [
				{ id: "new", text: "New document" },
				{ id: "print", text: "Print", icon: "wxi-empty" },
			],
		},
		{ id: "help", text: "Help", data: [{ id: "hotkeys", text: "Hotkeys" }] },
		{ id: "about", text: "About" },
	];
</script>

<MenuBar
	{options}
	css="app-menubar"
	menuCss="app-menu"
	onclick={ev => console.log(ev.option?.id)}
/>
```

##### Context Menu With Resolver And Filter

```svelte
<script>
	import { ContextMenu } from "@svar-ui/svelte-menu";

	const rows = [
		{ id: 1, kind: "project", name: "Project A" },
		{ id: 2, kind: "task", name: "Task 1" },
	];

	const options = [
		{ id: "add", text: "Add task" },
		{ id: "edit", text: "Edit" },
		{ id: "delete", text: "Delete" },
	];

	function resolver(id) {
		return rows.find(row => row.id == id);
	}

	function filter(option, row) {
		return row.kind !== "project" || option.id === "add";
	}
</script>

<ContextMenu
	{options}
	at="point"
	{resolver}
	{filter}
	onclick={ev => console.log(ev.context, ev.option?.id)}
>
	{#each rows as row (row.id)}
		<div data-context-id={row.id}>{row.name}</div>
	{/each}
</ContextMenu>
```

##### Programmatic Action Menu

```svelte
<script>
	import { ActionMenu } from "@svar-ui/svelte-menu";

	const options = [
		{ id: "a", text: "Project A" },
		{ id: "b", text: "Project B" },
	];

	let selected = $state(["a", "b"]);
	let menu = $state();

	function markSelected(option, index) {
		option.icon = option.id === selected[index] ? "wxi-check" : "wxi-empty";
		return true;
	}

	function clicked(ev) {
		if (ev.option) selected[ev.context] = ev.option.id;
	}
</script>

<ActionMenu {options} filter={markSelected} onclick={clicked} bind:this={menu} />

{#each selected as value, index}
	<button onclick={ev => menu.show(ev, index)}>{value}</button>
{/each}
```

##### Custom Menu Item Renderer

```svelte
<!-- UserMenuItem.svelte -->
<script>
	let { option } = $props();
</script>

<div class="user-option">{option.name}</div>
```

```svelte
<script>
	import { DropDownMenu, registerMenuItem } from "@svar-ui/svelte-menu";
	import AddUserItem from "./AddUserItem.svelte";
	import UserMenuItem from "./UserMenuItem.svelte";

	registerMenuItem("user", UserMenuItem);

	const options = [
		{ id: "u1", comp: "user", name: "Alex Wolensy" },
		{ id: "add", comp: AddUserItem, name: "Add New" },
	];
</script>

<DropDownMenu {options}>
	<button>Select user</button>
</DropDownMenu>
```

#### Implementation Notes

- `ActionMenu` and `ContextMenu` ignore events whose target has `data-menu-ignore`
- `dataKey` is converted from camelCase to kebab-case for DOM attribute lookup
- `ActionMenu.show(null)` closes the active menu
- `onclick` can receive `{ option: null }`
- runtime options can carry extra fields for custom renderers


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
