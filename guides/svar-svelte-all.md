# svar-svelte — full bundle

_Generated 2026-05-08T13:35:37.017Z_

## Contents

- [`SKILL.md`](#file-skill-md)
- [`locales.md`](#file-locales-md)
- [`themes.md`](#file-themes-md)
- [`core/index.md`](#file-core-index-md)
- [`core/avatar.md`](#file-core-avatar-md)
- [`core/button.md`](#file-core-button-md)
- [`core/calendar.md`](#file-core-calendar-md)
- [`core/checkbox.md`](#file-core-checkbox-md)
- [`core/colorboard.md`](#file-core-colorboard-md)
- [`core/colorpicker.md`](#file-core-colorpicker-md)
- [`core/colorselect.md`](#file-core-colorselect-md)
- [`core/combo.md`](#file-core-combo-md)
- [`core/counter.md`](#file-core-counter-md)
- [`core/datepicker.md`](#file-core-datepicker-md)
- [`core/daterangepicker.md`](#file-core-daterangepicker-md)
- [`core/dropdown.md`](#file-core-dropdown-md)
- [`core/field.md`](#file-core-field-md)
- [`core/fullscreen.md`](#file-core-fullscreen-md)
- [`core/globals.md`](#file-core-globals-md)
- [`core/icon.md`](#file-core-icon-md)
- [`core/locale.md`](#file-core-locale-md)
- [`core/modal.md`](#file-core-modal-md)
- [`core/modalarea.md`](#file-core-modalarea-md)
- [`core/month.md`](#file-core-month-md)
- [`core/multicombo.md`](#file-core-multicombo-md)
- [`core/pager.md`](#file-core-pager-md)
- [`core/popup.md`](#file-core-popup-md)
- [`core/portal.md`](#file-core-portal-md)
- [`core/radio.md`](#file-core-radio-md)
- [`core/rangecalendar.md`](#file-core-rangecalendar-md)
- [`core/richselect.md`](#file-core-richselect-md)
- [`core/segmented.md`](#file-core-segmented-md)
- [`core/select.md`](#file-core-select-md)
- [`core/sidearea.md`](#file-core-sidearea-md)
- [`core/slider.md`](#file-core-slider-md)
- [`core/suggest-dropdown.md`](#file-core-suggest-dropdown-md)
- [`core/switch.md`](#file-core-switch-md)
- [`core/tabs.md`](#file-core-tabs-md)
- [`core/text.md`](#file-core-text-md)
- [`core/textarea.md`](#file-core-textarea-md)
- [`core/themes.md`](#file-core-themes-md)
- [`core/timepicker.md`](#file-core-timepicker-md)
- [`core/twostate.md`](#file-core-twostate-md)
- [`menu/index.md`](#file-menu-index-md)
- [`toolbar/index.md`](#file-toolbar-index-md)
- [`layout/index.md`](#file-layout-index-md)
- [`grid/index.md`](#file-grid-index-md)
- [`editor/index.md`](#file-editor-index-md)
- [`filter/index.md`](#file-filter-index-md)
- [`filter/FilterBar.md`](#file-filter-filterbar-md)
- [`filter/FilterBuilder.md`](#file-filter-filterbuilder-md)
- [`filter/FilterEditor.md`](#file-filter-filtereditor-md)
- [`filter/FilterQuery.md`](#file-filter-filterquery-md)
- [`gantt/index.md`](#file-gantt-index-md)
- [`tasklist/index.md`](#file-tasklist-index-md)
- [`comments/index.md`](#file-comments-index-md)
- [`filemanager/index.md`](#file-filemanager-index-md)


## File: SKILL.md

> Source: `SKILL.md`

SVAR Svelte ships as a family of `@svar-ui/svelte-*` packages. This file routes to the per-package entry; each child file is standalone and contains the imports, public types, styling hooks, and recipes for its components.

Open the matching file for the package you are using. If the component you need is not listed in the routing table below, default to `core/index.md`

#### Component Routing

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

#### Common Techniques

These apply to every `@svar-ui/svelte-*` package:

- `themes.md` - theme wrappers, CSS variables, the `css` prop convention, class hooks
- `locales.md` - locale context, bundled language packs, extending words and formats

The widget hierarchy need to be wrapped in a theme component to ensure proper styling
Some widgets (grid,gantt,filemanager, etc) exports their own theme components that delegate to core theme and add their own variables


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


## File: core/index.md

> Source: `core/index.md`

Use when building, configuring, styling, or modifying SVAR Svelte Core / @svar-ui/svelte-core widgets, themes, locale, forms, popups, selectors, calendars, buttons, and display components

This is an index file. Open the focused widget file that matches the component you are using. Each child file is standalone and contain all critical info needed for that widget.

#### Package

```js
import {
	TextArea,
	Button,
	Checkbox,
	CheckboxGroup,
	ColorSelect,
	ColorBoard,
	ColorPicker,
	Combo,
	DatePicker,
	DateRangePicker,
	Fullscreen,
	Avatar,
	Icon,
	MultiCombo,
	Popup,
	Dropdown,
	Pager,
	RadioButton,
	RadioButtonGroup,
	RichSelect,
	Segmented,
	Select,
	Slider,
	Switch,
	Tabs,
	Text,
	Counter,
	Globals,
	Field,
	Calendar,
	Month,
	RangeCalendar,
	TimePicker,
	TwoState,
	Modal,
	ModalArea,
	SideArea,
	Portal,
	Willow,
	WillowDark,
	Locale,
	locale,
	popupContainer,
	SuggestDropdown,
	en,
} from "@svar-ui/svelte-core";
```

#### Widget Index

- `button.md` - `Button`
- `twostate.md` - `TwoState`
- `icon.md` - `Icon`
- `checkbox.md` - `Checkbox`, `CheckboxGroup`
- `radio.md` - `RadioButton`, `RadioButtonGroup`
- `switch.md` - `Switch`
- `segmented.md` - `Segmented`
- `tabs.md` - `Tabs`
- `field.md` - `Field`
- `text.md` - `Text`
- `textarea.md` - `TextArea`
- `counter.md` - `Counter`
- `slider.md` - `Slider`
- `select.md` - `Select`
- `combo.md` - `Combo`
- `multicombo.md` - `MultiCombo`
- `richselect.md` - `RichSelect`
- `suggest-dropdown.md` - `SuggestDropdown`
- `dropdown.md` - `Dropdown`
- `popup.md` - `Popup`
- `portal.md` - `Portal`, `popupContainer`
- `colorselect.md` - `ColorSelect`
- `colorboard.md` - `ColorBoard`
- `colorpicker.md` - `ColorPicker`
- `calendar.md` - `Calendar`
- `month.md` - `Month`
- `rangecalendar.md` - `RangeCalendar`
- `datepicker.md` - `DatePicker`
- `daterangepicker.md` - `DateRangePicker`
- `timepicker.md` - `TimePicker`
- `avatar.md` - `Avatar`
- `pager.md` - `Pager`
- `fullscreen.md` - `Fullscreen`
- `modal.md` - `Modal`
- `modalarea.md` - `ModalArea`
- `sidearea.md` - `SideArea`
- `globals.md` - `Globals`, `showNotice`, `showModal`
- `themes.md` - `Willow`, `WillowDark`, theme CSS variables
- `locale.md` - `Locale`, `locale`, `en`, bundled locale imports

#### Shared Contracts

- Most controls expose bindable `value` and an `onchange` callback. Event payloads differ by widget and are documented in each file.
- Option-based widgets generally use `{ id, label }` options and emit selected ids as values.
- Dropdown-backed widgets share `DropdownOptions` for position, align, width, inline mode, scroll tracking, and virtualization.


## File: core/avatar.md

> Source: `core/avatar.md`

### SVAR Svelte Core Avatar

Package: `@svar-ui/svelte-core`

#### Package

```js
import { Avatar } from "@svar-ui/svelte-core";
```

#### Supported Functionality

- Displays one user or a stack of users.
- User object fields are `id`, `name`, `avatar`, and `color`.
- `size` controls circle size and computed font size; default is `32`.
- `limit` caps visible users before responsive fitting is applied.
- When users are hidden, the last visible avatar shows a `+N` overlay.
- If `avatar` is present, it renders an image; otherwise initials are derived from `name`.

#### Public Types

```ts
import type { Component } from "svelte";

export interface IUser {
	id: string | number;
	name?: string;
	avatar?: string;
	color?: string;
}

export declare const Avatar: Component<{
	value: IUser | IUser[];
	size?: number;
	limit?: number;
}>;
```

#### Styling

- Root: `.wx-avatar-root`
- Stack: `.wx-avatar-stack`
- Avatar item: `.wx-avatar`, `.wx-avatar-item`
- Overflow state and badge: `.wx-avatar-overflow`, `.wx-avatar-overflow-badge`
- Image selector: `.wx-avatar img`
- Initial text selector: `.wx-avatar span`

```svelte
<div class="people">
	<Avatar value={users} size={36} limit={5} />
</div>

<style>
	.people {
		width: 180px;
	}

	.people .wx-avatar {
		border: 2px solid var(--wx-background);
	}
</style>
```

#### Recipes

##### User Stack With Responsive Overflow

```svelte
<script>
	import { Avatar } from "@svar-ui/svelte-core";

	const users = [
		{ id: 1, name: "Jane Smith", avatar: "/avatars/jane.png" },
		{ id: 2, name: "Lee Park", color: "#2ecc71" },
		{ id: 3, name: "Ana Stone", color: "#e74c3c" },
		{ id: 4, name: "Kai Wong", color: "#37a9ef" },
	];
</script>

<div style="width: 160px">
	<Avatar value={users} size={32} limit={4} />
</div>
```

##### Single Initial Avatar

```svelte
<script>
	import { Avatar } from "@svar-ui/svelte-core";
</script>

<Avatar value={{ id: 1, name: "Jane Smith", color: "#2f77e3" }} size={40} />
```


## File: core/button.md

> Source: `core/button.md`

### SVAR Svelte Core Button

Package: `@svar-ui/svelte-core`

#### Package

```js
import { Button } from "@svar-ui/svelte-core";
```

#### Supported Functionality

- Renders a native `<button class="wx-button">`.
- `type` is split on spaces and each part becomes a `wx-*` class.
- Typed values are `primary`, `secondary`, `danger`, `link`, and each with `block`.
- `css` is appended to the button class list.
- `icon` renders an `<i class={icon}>` before content.
- When `icon` is set and no `children` are supplied, the button also gets `.wx-icon` icon-only styling.
- Renders `children` when provided; otherwise renders `text`.
- `onclick` receives the native `MouseEvent`.

#### Public Types

```ts
import type { Component } from "svelte";

export declare const Button: Component<{
	type?:
		| "primary"
		| "secondary"
		| "danger"
		| "link"
		| "primary block"
		| "secondary block"
		| "danger block"
		| "link block";
	css?: string;
	icon?: string;
	disabled?: boolean;
	title?: string;
	text?: string;
	children?: () => any;
	onclick?: (ev: MouseEvent) => void;
}>;
```

#### Styling

- Button class: `.wx-button`
- Type/state classes: `.wx-primary`, `.wx-secondary`, `.wx-danger`, `.wx-link`, `.wx-block`, `.wx-pressed`, `.wx-icon`
- Disabled styling uses the native `[disabled]` attribute.
- Icon child selector is `i`.

```svelte
<Button css="save-button" type="primary" icon="wxi-check">Save</Button>

<style>
	:.wx-button.save-button {
		min-width: 120px;
	}
</style>
```

#### Recipes

##### Variants And Click Handler

```svelte
<script>
	import { Button } from "@svar-ui/svelte-core";

	function save(ev) {
		console.log(ev.currentTarget);
	}
</script>

<Button type="primary" icon="wxi-check" onclick={save}>Save</Button>
<Button type="secondary block">Full Width</Button>
<Button type="danger" disabled>Delete</Button>
<Button type="link">Details</Button>
```

##### Icon-Only Button

```svelte
<script>
	import { Button } from "@svar-ui/svelte-core";
</script>

<Button
	icon="wxi-search"
	title="Search"
	onclick={() => console.log("search")}
/>
```

#### Implementation Notes

- Source has `.wx-square` styles, but `square` is not in the public `type` union.
- `Button` does not call `preventDefault` or stop propagation; handler receives the raw event.


## File: core/calendar.md

> Source: `core/calendar.md`

### SVAR Svelte Core Calendar

Package: `@svar-ui/svelte-core`

#### Package

```js
import { Calendar } from "@svar-ui/svelte-core";
```

#### Supported Functionality

- Full single-date calendar with header navigation and optional action buttons.
- `value` is bindable and is a `Date` or `null`.
- `current` is bindable and controls the visible month; source normalizes it to the first day of that month.
- `buttons` defaults to `["clear", "today"]`; pass `false` to hide buttons or `true` for the default set.
- `markers(date)` can return a CSS class string appended to the matching `.wx-day`.
- `onchange` receives `{ value: Date | null }`.
- Internally wraps the calendar panel in `Locale`, so it can work without an outer locale provider.

#### Public Types

```ts
import type { Component } from "svelte";

export declare const Calendar: Component<{
	value?: Date;
	current?: Date;
	markers?: (date: Date) => string;
	buttons?: boolean | ("clear" | "today")[];
	onchange?: (ev: { value: Date | null }) => void;
}>;
```

#### Styling

- Calendar wrapper: `.wx-calendar`
- Layout: `.wx-wrap`, `.wx-buttons`, `.wx-button-item`
- Header: `.wx-header`, `.wx-pager`, `.wx-spacer`, `.wx-label`
- Month grid comes from `Month`: `.wx-weekdays`, `.wx-weekday`, `.wx-days`, `.wx-day`, `.wx-out`, `.wx-selected`, `.wx-weekend`, `.wx-inactive`
- Year/month pickers: `.wx-months`, `.wx-month`, `.wx-years`, `.wx-year`, `.wx-current`, `.wx-prev-decade`, `.wx-next-decade`

```svelte
<div class="compact-calendar">
	<Calendar value={new Date(2025, 4, 1)} />
</div>

<style>
	.compact-calendar {
		--wx-calendar-cell-size: 28px;
		--wx-calendar-padding: 8px;
	}

	.compact-calendar .holiday {
		outline: 1px solid var(--wx-color-warning);
	}
</style>
```

#### Recipes

##### Mark Dates And Keep Visible Month Bound

```svelte
<script>
	import { Calendar } from "@svar-ui/svelte-core";

	let value = $state(new Date(2025, 4, 1));
	let current = $state(new Date(2025, 4, 1));

	function markers(date) {
		return date.getDay() === 0 ? "holiday" : "";
	}
</script>

<Calendar
	bind:value
	bind:current
	{markers}
	buttons={["today"]}
	onchange={ev => console.log(ev.value)}
/>
```

##### Hide Action Buttons

```svelte
<script>
	import { Calendar } from "@svar-ui/svelte-core";
</script>

<Calendar buttons={false} onchange={ev => console.log(ev.value)} />
```

#### Implementation Notes

- Selecting a date clones it with `new Date(...)` before assigning `value`.
- Clearing sets `value` to `null`.
- Source calls `onchange` after updating the bindable `value`.


## File: core/checkbox.md

> Source: `core/checkbox.md`

### SVAR Svelte Core Checkbox

Package: `@svar-ui/svelte-core`

Use this file standalone for `Checkbox` and `CheckboxGroup`.

#### Package

```js
import { Checkbox, CheckboxGroup } from "@svar-ui/svelte-core";
```

#### Supported Functionality

- `Checkbox.value` is a bindable boolean.
- `Checkbox.inputValue` is emitted alongside the checked state; default is an empty string.
- `Checkbox.onchange` emits `{ value, inputValue }`.
- `CheckboxGroup.options` are `{ id, label }`.
- `CheckboxGroup.value` is a bindable array of selected option ids.
- Group `onchange` emits `{ value }`.
- Group `type` supports `inline` and `grid`; default layout is one item per row.

#### Public Types

```ts
import type { Component } from "svelte";

export declare const Checkbox: Component<{
	id?: string | number;
	label?: string;
	inputValue?: string | number;
	value?: boolean;
	style?: string;
	disabled?: boolean;
	onchange?: (ev: { value: boolean; inputValue: string | number }) => void;
}>;

export declare const CheckboxGroup: Component<{
	options?: { id: string | number; label: string }[];
	value?: (string | number)[];
	type?: "inline" | "grid";
	onchange?: (ev: { value: (string | number)[] }) => void;
}>;
```

#### Styling

- Checkbox wrapper: `.wx-checkbox`
- `style` prop is applied to the checkbox wrapper.
- Group wrapper: `.wx-checkboxgroup`, `.wx-checkboxgroup.wx-inline`, `.wx-checkboxgroup.wx-grid`
- Group item wrapper: `.wx-item`

```svelte
<div class="todo-checks">
	<CheckboxGroup {options} bind:value />
</div>

<style>
	.todo-checks .wx-checkboxgroup .wx-item {
		margin-top: 8px;
	}
</style>
```

#### Recipes

##### Single Checkbox

```svelte
<script>
	import { Checkbox } from "@svar-ui/svelte-core";

	let done = $state(false);
</script>

<Checkbox
	label="Done"
	inputValue="done"
	bind:value={done}
	onchange={ev => console.log(ev.value, ev.inputValue)}
/>
```

##### Checkbox Group

```svelte
<script>
	import { CheckboxGroup } from "@svar-ui/svelte-core";

	const options = [
		{ id: "new", label: "New" },
		{ id: "open", label: "Open" },
		{ id: "done", label: "Done" },
	];

	let selected = $state(["new"]);
</script>

<CheckboxGroup {options} bind:value={selected} type="inline" />
```

#### Implementation Notes

- `CheckboxGroup` does not pass disabled state through option objects.


## File: core/colorboard.md

> Source: `core/colorboard.md`

### SVAR Svelte Core ColorBoard

Package: `@svar-ui/svelte-core`

#### Package

```js
import { ColorBoard } from "@svar-ui/svelte-core";
```

#### Supported Functionality

- HSV color board with hue line, saturation/value block, text input, preview, and optional select button.
- `value` is bindable and defaults to `"#65D3B3"`.
- Valid typed hex is normalized to uppercase `#RRGGBB`; 3-digit hex is expanded.
- Moving sliders or typing a valid color emits `{ value, input: true }`.
- With `button={true}`, clicking the select button emits a final `{ value }`.
- Keyboard arrow keys move the focused block/line slider.

#### Public Types

```ts
import type { Component } from "svelte";

export declare const ColorBoard: Component<{
	value?: string;
	button?: boolean;
	onchange?: (ev: { value: string; input?: boolean }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-colorboard`
- Saturation/value block: `.wx-color-block`
- Block slider: `.wx-color-block-slider.wx-slider`
- Hue line: `.wx-color-line`
- Hue slider: `.wx-color-line-slider.wx-slider`
- Controls row: `.wx-color-controls`
- Preview: `.wx-color`
- Text input: `.wx-text`

```svelte
<div class="picker-board">
	<ColorBoard bind:value />
</div>

<style>
	.picker-board .wx-color-block {
		height: 180px;
	}
</style>
```

#### Recipes

##### Inline Color Board

```svelte
<script>
	import { ColorBoard } from "@svar-ui/svelte-core";

	let value = $state("#48C8E2");
</script>

<div style="width: 300px">
	<ColorBoard
		bind:value
		onchange={ev => {
			if (!ev.input) console.log(ev.value);
		}}
	/>
</div>
```


## File: core/colorpicker.md

> Source: `core/colorpicker.md`

### SVAR Svelte Core ColorPicker

Package: `@svar-ui/svelte-core`

#### Package

```js
import { ColorPicker } from "@svar-ui/svelte-core";
```

#### Supported Functionality

- Input-like color picker that opens `ColorBoard` in a `Dropdown`.
- `value` is a bindable color string.
- The inner `ColorBoard` is rendered with `button="true"`.
- `ColorPicker` ignores `ColorBoard` input events and updates only on the final select event.
- Final selection closes the popup and emits `{ value }`.
- `clear` shows a close icon when value is set and not disabled.
- `dropdown` is forwarded to `Dropdown`.

#### Public Types

```ts
import type { Component } from "svelte";

export interface DropdownOptions {
	inline?: boolean;
	position?: "top" | "right" | "bottom" | "left";
	align?: "start" | "center" | "end";
	css?: string;
	width?: string | "unset" | "auto";
	trackScroll?: boolean;
	virtualized?: boolean;
}

export declare const ColorPicker: Component<{
	value?: string;
	id?: string | number;
	placeholder?: string;
	title?: string;
	disabled?: boolean;
	error?: boolean;
	clear?: boolean;
	dropdown?: DropdownOptions;
	onchange?: (ev: { value: string }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-colorpicker`
- Selected swatch: `.wx-color`
- Clear icon: `.wxi-close`
- Input state classes: `.wx-focus`, `.wx-error`
- Dropdown content uses `ColorBoard` hooks such as `.wx-colorboard`, `.wx-color-block`, `.wx-color-line`.


```svelte
<ColorPicker dropdown={{ css: "color-popup", width: "300px" }} />

<style>
	.wx-popup.color-popup {
		width: 300px;
	}
</style>
```

#### Recipes

##### Color Picker In A Field

```svelte
<script>
	import { ColorPicker, Field } from "@svar-ui/svelte-core";

	let color = $state("#65D3B3");
</script>

<Field label="Color" position="left">
	<ColorPicker
		bind:value={color}
		placeholder="Select a color"
		clear
		onchange={ev => console.log(ev.value)}
	/>
</Field>
```

#### Implementation Notes

- `ColorPicker` displays the current `value` as swatch background without validating it.


## File: core/colorselect.md

> Source: `core/colorselect.md`

### SVAR Svelte Core ColorSelect

Package: `@svar-ui/svelte-core`

#### Package

```js
import { ColorSelect } from "@svar-ui/svelte-core";
```

#### Supported Functionality

- Input-like color palette selector.
- `value` is a bindable hex color string or empty string.
- Default colors are `#00a037`, `#37a9ef`, `#f5a623`, `#ff4c3b`, `#a0a0a0`, `#000000`, `#ffffff`.
- Clicking the input opens a `Dropdown` unless disabled.
- Palette includes an empty color item that selects `""`.
- `clear` shows a close icon when value is set and not disabled.
- `onchange` emits `{ value }`.

#### Public Types

```ts
import type { Component } from "svelte";

export declare const ColorSelect: Component<{
	colors?: string[];
	value?: string;
	id?: string | number;
	clear?: boolean;
	placeholder?: string;
	title?: string;
	disabled?: boolean;
	error?: boolean;
	onchange?: (ev: { value: string }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-colorselect`
- Selected swatch: `.wx-selected`
- Dropdown palette: `.wx-colors`
- Swatch: `.wx-color`
- Empty swatch: `.wx-empty`
- Clear icon: `.wx-clear.wxi-close`


```svelte
<ColorSelect {colors} bind:value clear />

<style>
	.wx-colorselect .wx-color {
		border-radius: 50%;
	}
</style>
```

#### Recipes

##### Custom Palette

```svelte
<script>
	import { ColorSelect, Field } from "@svar-ui/svelte-core";

	let color = $state("");
</script>

<Field label="Color" position="left">
	<ColorSelect
		colors={["#65D3B3", "#FFC975", "#58C3FE"]}
		bind:value={color}
		placeholder="Select a color"
		clear
	/>
</Field>
```


## File: core/combo.md

> Source: `core/combo.md`

### SVAR Svelte Core Combo

Package: `@svar-ui/svelte-core`

#### Package

```js
import { Combo } from "@svar-ui/svelte-core";
```

#### Supported Functionality

- Searchable single-select input backed by `SuggestDropdown`.
- `options` are `{ id, label }` by default.
- `textField` controls display/filter field; default is `"label"`.
- `textOptions` can provide selected display objects when visible `options` are filtered or partial.
- Typing filters `options` case-insensitively by `textField`.
- Blur selects exact text match first, then first containing match, then previous value or first option.
- Dropdown selection updates bindable `value` and emits `{ value }`.
- `children` snippet receives `{ option }` for custom list row content.
- `dropdown` is forwarded to `SuggestDropdown`/`Dropdown`.

#### Public Types

```ts
import type { Component } from "svelte";

export interface DropdownOptions {
	inline?: boolean;
	position?: "top" | "right" | "bottom" | "left";
	align?: "start" | "center" | "end";
	css?: string;
	width?: string | "unset" | "auto";
	trackScroll?: boolean;
	virtualized?: boolean;
}

export declare const Combo: Component<{
	value?: string | number;
	id?: string | number;
	options?: { id: string | number; label: string }[];
	textOptions?: { id: string | number; label: string }[];
	textField?: string;
	placeholder?: string;
	title?: string;
	disabled?: boolean;
	error?: boolean;
	clear?: boolean;
	dropdown?: DropdownOptions & {
		virtualized?: boolean;
	};
	children?: () => any;
	onchange?: (ev: { value: string | number }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-combo`
- Icon: `.wx-icon`, close icon `.wxi-close`
- Error class is applied to the input as `.wx-error`.
- Dropdown list hooks from `SuggestDropdown`: `.wx-list`, `.wx-item`, `.wx-focus`, `.wx-no-data`.
- Non-inline dropdown `css` is appended to `.wx-popup`.


```svelte
<Combo options={users} dropdown={{ css: "users-popup", width: "320px" }} />

<style>
	.wx-popup.users-popup .wx-list {
		max-height: 360px;
	}
</style>
```

#### Recipes

##### Custom Option Template And Virtualized List

```svelte
<script>
	import { Combo } from "@svar-ui/svelte-core";

	const users = Array.from({ length: 10000 }, (_, id) => ({
		id,
		label: `User ${id}`,
		email: `user${id}@example.com`,
	}));

	let value = $state(9000);
</script>

<Combo
	options={users}
	bind:value
	dropdown={{ virtualized: true, width: "320px" }}
>
	{#snippet children({ option })}
		<div class="user-option">
			<strong>{option.label}</strong>
			<span>{option.email}</span>
		</div>
	{/snippet}
</Combo>
```

##### Hidden Selected Option

```svelte
<script>
	import { Combo } from "@svar-ui/svelte-core";

	const allUsers = [
		{ id: 87, label: "Berni Mayou" },
		{ id: 103, label: "Ned Stark" },
	];

	const visibleUsers = [{ id: 103, label: "Ned Stark" }];
</script>

<Combo textOptions={allUsers} options={visibleUsers} value={87} clear />
```

#### Implementation Notes

- Filtering assumes `option[textField]` is a string


## File: core/counter.md

> Source: `core/counter.md`

### SVAR Svelte Core Counter

Package: `@svar-ui/svelte-core`

#### Package

```js
import { Counter } from "@svar-ui/svelte-core";
```

#### Supported Functionality

- Numeric input with decrement and increment buttons.
- Bindable `value`, default `0`.
- `step` defaults to `1`, `min` defaults to `0`, `max` defaults to `Infinity`.
- Button clicks update `value` and emit `{ value }`.
- Typing emits `{ value, input: true }` without immediately mutating the bound value in the handler payload path.
- Blur normalizes the bound value to min/max and step, then emits `{ value }`.
- `readonly` blocks button changes and blur normalization.
- `disabled` disables the input and both buttons.

#### Public Types

```ts
import type { Component } from "svelte";

export declare const Counter: Component<{
	id?: string | number;
	value?: number;
	step?: number;
	min?: number;
	max?: number;
	error?: boolean;
	disabled?: boolean;
	readonly?: boolean;
	onchange?: (ev: { value: number; input?: boolean }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-counter`
- State classes: `.wx-disabled`, `.wx-readonly`, `.wx-error`
- Input: `.wx-input`
- Buttons: `.wx-btn`, `.wx-btn-dec`, `.wx-btn-inc`
- SVG icons: `.wx-dec`, `.wx-inc`

```svelte
<Counter bind:value min={0} max={30} />

<style>
	.wx-counter .wx-input {
		width: 64px;
	}
</style>
```

#### Recipes

##### Counter With Final Change Handling

```svelte
<script>
	import { Counter, Field } from "@svar-ui/svelte-core";

	let count = $state(5);
</script>

<Field label="Quantity">
	<Counter
		bind:value={count}
		min={0}
		max={30}
		step={3}
		onchange={ev => {
			if (!ev.input) console.log(ev.value);
		}}
	/>
</Field>
```


## File: core/datepicker.md

> Source: `core/datepicker.md`

### SVAR Svelte Core DatePicker

Package: `@svar-ui/svelte-core`

#### Package

```js
import { DatePicker } from "@svar-ui/svelte-core";
```

#### Supported Functionality

- Input-like single-date picker backed by `Text`, `Dropdown`, and `Calendar`.
- `value` is bindable and is a `Date` or `null`.
- `format` can be a date format string or `(value: Date) => string`; locale date format is used by default.
- `editable={true}` parses committed text with `new Date(text)`.
- `editable={fn}` uses the custom parser and expects `Date | null`.
- `clear` passes through to the inner `Text` clear icon.
- `buttons` is forwarded to `Calendar`; default is `["clear", "today"]`.
- `dropdown` is forwarded to `Dropdown`; date dropdowns default width to `"unset"` when no width is provided.
- Popup closes on window scroll.
- `onchange` receives `{ value: Date | null }` after the bindable value is updated.

#### Public Types

```ts
import type { Component } from "svelte";

export interface DropdownOptions {
	inline?: boolean;
	position?: "top" | "right" | "bottom" | "left";
	align?: "start" | "center" | "end";
	css?: string;
	width?: string | "unset" | "auto";
	trackScroll?: boolean;
	virtualized?: boolean;
}

export declare const DatePicker: Component<{
	value?: Date;
	id?: string | number;
	disabled?: boolean;
	error?: boolean;
	width?: string;
	align?: "start" | "center" | "end";
	placeholder?: string;
	format?: string | ((value: Date) => string);
	buttons?: boolean | ("clear" | "today")[];
	css?: string;
	title?: string;
	editable?: boolean | ((value: string) => Date | null);
	clear?: boolean;
	dropdown?: DropdownOptions;
	onchange?: (ev: { value: Date | null }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-datepicker`
- `css` is passed to the inner `Text`; use `css="wx-icon-left"` for the left-icon input variant.
- Inner input classes come from `Text`: `.wx-text`, `.wx-input`, `.wx-icon`, `.wx-error`, `.wx-disabled`, `.wx-focus`.
- Popup surface uses `Dropdown`/`Popup` hooks such as `.wx-popup`.
- Calendar hooks come from `Calendar` and `Month`.


```svelte
<DatePicker css="wx-icon-left date-input" dropdown={{ css: "date-popup" }} />

<style>
	.wx-text.date-input {
		--wx-input-width: 220px;
	}

	.wx-popup.date-popup {
		padding: 4px;
	}
</style>
```

#### Recipes

##### Bound Date In A Field

```svelte
<script>
	import { DatePicker, Field } from "@svar-ui/svelte-core";

	let value = $state(new Date(2025, 4, 1));
</script>

<Field label="Date" position="left">
	<DatePicker bind:value clear onchange={ev => console.log(ev.value)} />
</Field>
```

##### Editable Date With Custom Parser

```svelte
<script>
	import { DatePicker } from "@svar-ui/svelte-core";

	let value = $state(new Date(2025, 4, 1));

	function parseDate(text) {
		const p = text.match(/(..)(..)(.+)/);
		return p ? new Date(p.slice(1, 4).join("/")) : null;
	}
</script>

<DatePicker
	bind:value
	editable={parseDate}
	format="%m%d%Y"
	clear
	dropdown={{ width: "280px", align: "start" }}
/>
```

#### Implementation Notes

- Public types include `width` and `align`, but source does not use those props directly; use `dropdown={{ width, align }}`.
- Selecting the same date value does not emit `onchange`.


## File: core/daterangepicker.md

> Source: `core/daterangepicker.md`

### SVAR Svelte Core DateRangePicker

Package: `@svar-ui/svelte-core`

#### Package

```js
import { DateRangePicker } from "@svar-ui/svelte-core";
```

#### Supported Functionality

- Input-like date range picker backed by `Text`, `Dropdown`, and `RangeCalendar`.
- `value` is bindable and is `{ start: Date; end?: Date }` or `null`.
- `format` can be a date format string or `(date: Date) => string`; locale date format is used by default.
- Display text is `start - end`; missing `end` displays only the start.
- `months` is forwarded to `RangeCalendar` and is `1` or `2`.
- `buttons` is forwarded to `RangeCalendar`; arrays can include `"done"`.
- `editable={true}` parses committed text with `new Date(text)`.
- `editable={fn}` uses the custom parser and expects `Date | null`.
- Editable parsing splits text on `" -"`.
- `clear` passes through to the inner `Text` clear icon.
- `dropdown` is forwarded to `Dropdown`; date dropdowns default width to `"unset"` when no width is provided.
- Popup closes on window scroll.
- `onchange` receives `{ value: { start: Date; end: Date | null } | null }`.

#### Public Types

```ts
import type { Component } from "svelte";

export interface DropdownOptions {
	inline?: boolean;
	position?: "top" | "right" | "bottom" | "left";
	align?: "start" | "center" | "end";
	css?: string;
	width?: string | "unset" | "auto";
	trackScroll?: boolean;
	virtualized?: boolean;
}

export declare const DateRangePicker: Component<{
	value?: { start: Date; end?: Date };
	id?: string | number;
	disabled?: boolean;
	error?: boolean;
	width?: string;
	align?: "start" | "center" | "end";
	placeholder?: string;
	css?: string;
	title?: string;
	format?: string | ((date: Date) => string);
	months?: 1 | 2;
	buttons?: boolean | ("clear" | "today" | "done")[];
	editable?: boolean | ((value: string) => Date | null);
	clear?: boolean;
	dropdown?: DropdownOptions;
	onchange?: (ev: {
		value: { start: Date; end: Date | null } | null;
	}) => void;
}>;
```

#### Styling

- Wrapper: `.wx-daterangepicker`
- State classes: `.wx-disabled`, `.wx-error`
- `css` is passed to the inner `Text`.
- Inner input classes come from `Text`: `.wx-text`, `.wx-input`, `.wx-icon`.
- Popup surface uses `Dropdown`/`Popup` hooks such as `.wx-popup`.
- Calendar hooks come from `RangeCalendar`, `Calendar`, and `Month`.

```svelte
<DateRangePicker css="range-input" dropdown={{ css: "range-popup" }} />

<style>
	.wx-text.range-input {
		--wx-input-width: 280px;
	}
</style>
```

#### Recipes

##### Two-Month Range Picker

```svelte
<script>
	import { DateRangePicker, Field } from "@svar-ui/svelte-core";

	let value = $state({
		start: new Date(2025, 4, 1),
		end: new Date(2025, 4, 7),
	});
</script>

<Field label="Range" position="left">
	<DateRangePicker
		bind:value
		months={2}
		buttons={["done", "clear", "today"]}
		clear
		onchange={ev => console.log(ev.value)}
	/>
</Field>
```

##### Editable Range

```svelte
<script>
	import { DateRangePicker } from "@svar-ui/svelte-core";

	let value = $state();
</script>

<DateRangePicker
	bind:value
	editable
	placeholder="Start - end"
	dropdown={{ width: "unset", align: "start" }}
/>
```

#### Implementation Notes

- Public types include `width` and `align`, but source does not use those props directly; use `dropdown={{ width, align }}`.
- If the popup closes while only `start` is selected, source emits the pending single-start range.
- With a `"done"` button, `RangeCalendar` holds intermediate selection changes until done is pressed.


## File: core/dropdown.md

> Source: `core/dropdown.md`

### SVAR Svelte Core Dropdown

Package: `@svar-ui/svelte-core`

#### Package

```js
import { Dropdown } from "@svar-ui/svelte-core";
```

#### Supported Functionality

- Anchored dropdown surface for arbitrary child content.
- `position` is `top`, `right`, `bottom`, or `left`; default is `bottom`.
- `align` is `start`, `center`, or `end`; default is `start`.
- `width` defaults to `"100%"`.
- Non-inline mode renders a `Portal` containing `Popup` anchored to the trigger's parent node.
- `inline={true}` renders `.wx-dropdown` in place without `Portal`.
- `trackScroll` is passed to `Popup` in non-inline mode.
- `oncancel` is called by click-outside behavior and scroll tracking where enabled.

#### Public Types

```ts
import type { Component } from "svelte";

export interface DropdownOptions {
	inline?: boolean;
	position?: "top" | "right" | "bottom" | "left";
	align?: "start" | "center" | "end";
	css?: string;
	width?: string | "unset" | "auto";
	trackScroll?: boolean;
	virtualized?: boolean;
}

export declare const Dropdown: Component<
	DropdownOptions & {
		children?: () => any;
		oncancel?: (ev: MouseEvent) => void;
	}
>;
```

#### Styling

- Inline dropdown container: `.wx-dropdown`
- Inline position classes: `.wx-top-start`, `.wx-top-center`, `.wx-top-end`, `.wx-bottom-start`, `.wx-bottom-center`, `.wx-bottom-end`, `.wx-left-start`, `.wx-left-center`, `.wx-left-end`, `.wx-right-start`, `.wx-right-center`, `.wx-right-end`
- Non-inline dropdown uses `Popup`; `css` is appended to `.wx-popup`.
- Hidden anchor marker: `.wx-portal-node`


```svelte
<Dropdown css="calendar-popup" width="300px">
	<div>Content</div>
</Dropdown>

<style>
	.wx-popup.calendar-popup {
		padding: 8px;
	}
</style>
```

#### Recipes

##### Anchored Dropdown

```svelte
<script>
	import { Button, Calendar, Dropdown } from "@svar-ui/svelte-core";

	let open = $state(false);
</script>

<Button onclick={() => (open = true)}>Open</Button>
{#if open}
	<Dropdown
		width="300px"
		position="bottom"
		align="start"
		css="calendar-popup"
		oncancel={() => (open = false)}
	>
		<Calendar />
	</Dropdown>
{/if}
```

##### Inline Dropdown

```svelte
<script>
	import { Dropdown } from "@svar-ui/svelte-core";
</script>

<div style="position: relative">
	<Dropdown inline width="200px" position="bottom" align="end">
		<div style="padding: 8px">Inline content</div>
	</Dropdown>
</div>
```

#### Implementation Notes

- Source supports `autoFit = true` for inline dropdowns; `DropdownOptions` does not declare `autoFit`.
- `virtualized` is part of `DropdownOptions` for list helpers; `Dropdown` itself does not implement list virtualization.


## File: core/field.md

> Source: `core/field.md`

### SVAR Svelte Core Field

Package: `@svar-ui/svelte-core`

#### Package

```js
import { Field } from "@svar-ui/svelte-core";
```

#### Supported Functionality

- Wraps controls with label and control layout.
- Default label position is top; `position="left"` creates a side label layout.
- `width` sets inline width on the `.wx-field` wrapper.
- `error` adds `.wx-error` and colors the label.
- `required` adds `.wx-required` and appends a red `*` to the label.
- `type="checkbox" | "slider" | "switch"` adjusts vertical padding for those controls in left-label layout.
- Sets Svelte context `wx-input-id`; child controls that call `getInputId` share the generated id with the label.

#### Public Types

```ts
import type { Component } from "svelte";

export declare const Field: Component<{
	label?: string;
	position?: "left";
	width?: string;
	error?: boolean;
	type?: "checkbox" | "slider" | "switch";
	required?: boolean;
	children?: () => any;
}>;
```

#### Styling

- Wrapper: `.wx-field`
- Side label modifier: `.wx-left`
- State classes: `.wx-error`, `.wx-required`
- Label: `.wx-label`
- Control wrapper: `.wx-field-control`
- Control type modifiers: `.wx-field-control.wx-checkbox`, `.wx-field-control.wx-slider`, `.wx-field-control.wx-switch`


```svelte
<Field label="Owner" position="left" width="480px">
	<slot />
</Field>

<style>
	.wx-field.wx-left > .wx-label {
		width: 140px;
	}
</style>
```

#### Recipes

##### Labeled Control

```svelte
<script>
	import { Field, Text } from "@svar-ui/svelte-core";

	let name = $state("");
</script>

<Field label="Name" required>
	<Text bind:value={name} />
</Field>
```

##### Nested Fields

```svelte
<script>
	import { Field, Text } from "@svar-ui/svelte-core";
</script>

<Field label="Name">
	<Field label="First" position="left">
		<Text />
	</Field>
	<Field label="Last" position="left">
		<Text />
	</Field>
</Field>
```


## File: core/fullscreen.md

> Source: `core/fullscreen.md`

### SVAR Svelte Core Fullscreen

Package: `@svar-ui/svelte-core`

#### Package

```js
import { Fullscreen } from "@svar-ui/svelte-core";
```

#### Supported Functionality

- Wraps content in a fullscreen-capable container.
- Default toggle button uses `Button` with `css="wx-fullscreen-button"`.
- Default icon switches between `wxi-expand` and `wxi-collapse`.
- Custom `toggleButton` snippet receives `(toggleFullscreen, inFullscreen)`.
- `hotkey` configures a scoped hotkey on the fullscreen wrapper through `@svar-ui/lib-dom` hotkeys.
- Tracks native `fullscreenchange` to keep `inFullscreen` in sync.

#### Public Types

```ts
import type { Component } from "svelte";
import type { Snippet } from "svelte";

export declare const Fullscreen: Component<{
	toggleButton?: Snippet<[(ev: MouseEvent) => void, boolean]>;
	children?: () => any;
	hotkey?: string;
}>;
```

#### Styling

- Wrapper: `.wx-fullscreen`
- Default button: `.wx-fullscreen-button`
- Default icon: `.wx-fullscreen-icon`
- Fullscreen backdrop selector: `.wx-fullscreen::backdrop`
- Wrapper is `position: relative`, `height: 100%`, `width: 100%`, `tabindex="-1"`.
- Default button is absolutely positioned at bottom right.

```svelte
<Fullscreen>
	<div class="report">Report content</div>
</Fullscreen>

<style>
	.wx-fullscreen .wx-fullscreen-button {
		right: 12px;
		bottom: 12px;
	}
</style>
```

#### Recipes

##### Custom Toggle Button

```svelte
<script>
	import { Button, Fullscreen } from "@svar-ui/svelte-core";
</script>

<Fullscreen hotkey="ctrl+shift+f">
	<div class="panel">Report content</div>

	{#snippet toggleButton(toggle, inFullscreen)}
		<Button onclick={toggle}>
			{inFullscreen ? "Exit fullscreen" : "Enter fullscreen"}
		</Button>
	{/snippet}
</Fullscreen>
```

#### Implementation Notes

- `toggleFullscreen` calls `node.requestFullscreen()` and `document.exitFullscreen()`.


## File: core/globals.md

> Source: `core/globals.md`

### SVAR Svelte Core Globals

Package: `@svar-ui/svelte-core`

#### Package

```js
import { Globals } from "@svar-ui/svelte-core";
```

#### Supported Functionality

- Renders children and installs Svelte context `wx-helpers`.
- `wx-helpers.showNotice(msg)` appends a notice.
- `wx-helpers.showModal(msg)` renders a `Modal` and returns a Promise.
- `showNotice` payload fields used by source include `text`, `type`, `expire`, and optional `id`.
- Notice `type` can be empty or classes such as `info`, `warning`, `success`, and `danger`.
- `showNotice` default expiry is `5100ms`; `expire: -1` keeps the notice until the close icon is clicked.
- `showModal` payload fields used by source include `title`, `message`, and `buttons`.
- Confirm resolves the modal Promise; cancel rejects it.
- `Notice` and `Notices` are source components but are not top-level exports.

#### Public Types

```ts
import type { Component } from "svelte";

export declare const Globals: Component<{
	children?: () => any;
}>;
```

#### Source Helper Shapes

These helper payloads are source behavior, not exported public TypeScript declarations.

```ts
type NoticeMessage = {
	id?: string | number;
	text?: string;
	type?: "" | "info" | "warning" | "success" | "danger" | string;
	expire?: number;
};

type ModalMessage = {
	title?: string;
	message?: any;
	buttons?: boolean | string[];
};
```

#### Styling

- Notice list: `.wx-notices`
- Notice item: `.wx-notice`
- Notice content: `.wx-text`
- Notice close button: `.wx-button`
- Notice type classes: `.wx-info`, `.wx-warning`, `.wx-success`, `.wx-danger`
- Modals rendered by `showModal` use `Modal` classes: `.wx-modal`, `.wx-window`, `.wx-header`, `.wx-buttons`, `.wx-button`

```svelte
<Globals>
	<App />
</Globals>

<style>
	.wx-notices {
		top: 12px;
		right: 12px;
	}
</style>
```

#### Recipes

##### Install Globals At App Root

```svelte
<script>
	import { Globals } from "@svar-ui/svelte-core";
	import Actions from "./Actions.svelte";
</script>

<Globals>
	<Actions />
</Globals>
```

##### Use Notice And Modal Helpers In A Child

```svelte
<script>
	import { Button } from "@svar-ui/svelte-core";
	import { getContext } from "svelte";

	const { showNotice, showModal } = getContext("wx-helpers");

	async function confirmDelete() {
		try {
			await showModal({ title: "Confirm", message: "Delete item?" });
			showNotice({ type: "success", text: "Deleted" });
		} catch {
			showNotice({ type: "info", text: "Canceled" });
		}
	}
</script>

<Button type="danger" onclick={confirmDelete}>Delete</Button>
<Button onclick={() => showNotice({ type: "info", text: "Saved" })}>
	Notice
</Button>
```

#### Implementation Notes

- `showModal` stores one active modal at a time.


## File: core/icon.md

> Source: `core/icon.md`

### SVAR Svelte Core Icon

Package: `@svar-ui/svelte-core`

#### Package

```js
import { Icon } from "@svar-ui/svelte-core";
```

#### Supported Functionality

- Renders `<i class="wx-icon {css}">`.
- Use `css` for icon font classes such as `wxi-search`.
- `title` is forwarded to the `<i>`.
- `onclick` is forwarded to the `<i>`.
- If `children` is provided, it is rendered inside the `<i>` and `role="img"` is added.

#### Public Types

```ts
import type { Component } from "svelte";

export declare const Icon: Component<{
	css?: string;
	title?: string;
	children?: () => any;
	onclick?: (ev: MouseEvent) => void;
}>;
```

#### Styling

- Icon class: `.wx-icon`
- `css` is appended to `.wx-icon`.

```svelte
<Icon css="wxi-search app-icon" title="Search" />

<style>
	.wx-icon.app-icon {
		color: var(--wx-color-primary);
	}
</style>
```

#### Recipes

##### Clickable Icon

```svelte
<script>
	import { Icon } from "@svar-ui/svelte-core";
</script>

<Icon
	css="wxi-information-outline"
	title="Info"
	onclick={() => console.log("info")}
/>
```

#### Implementation Notes

- The component intentionally uses an `<i>` rather than a button


## File: core/locale.md

> Source: `core/locale.md`

### SVAR Svelte Core Locale

Package: `@svar-ui/svelte-core`

#### Package

```js
import { Locale, locale, en } from "@svar-ui/svelte-core";
```

For all bundled language packs, import from `@svar-ui/core-locales`:

```js
import { en, cn, de, es, fr, it, ja, pt, ru } from "@svar-ui/core-locales";
```

#### Supported Functionality

- `Locale` reads Svelte context `wx-i18n`.
- If no locale context exists, it creates one from English words.
- If `words` is not `null`, it extends the current locale with `words`.
- `optional` is passed to the locale `extend` call.
- Use `Locale` around the smallest subtree that needs different words or formats.
- Locale affects calendar labels, date/time formats, modal buttons, pager labels, empty-list text, notices/modal helper strings, and color board select text.
- `locale` is re-exported in JS from `@svar-ui/lib-dom`.
- `en` is re-exported in JS from `@svar-ui/core-locales`.

#### Public Types

```ts
import type { Component } from "svelte";

export declare const Locale: Component<{
	words?: any;
	optional?: boolean;
	children?: () => any;
}>;

export type { ILocale, Terms, TPosition } from "@svar-ui/lib-dom";
```

#### Styling

- `Locale` does not render a wrapper element or public classes.
- It only changes locale context for children.
- Styling changes that depend on locale direction or content length must be handled by app CSS or theme variables.

#### Recipes

##### Localize A Calendar Subtree

```svelte
<script>
	import { Calendar, Locale } from "@svar-ui/svelte-core";
	import { de } from "@svar-ui/core-locales";
</script>

<Locale words={de}>
	<Calendar value={new Date(2025, 4, 1)} />
</Locale>
```

##### Override Date Formats

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

##### Use The Locale Helper Directly

```svelte
<script>
	import { en, locale } from "@svar-ui/svelte-core";

	const i18n = locale(en).extend(
		{
			core: {
				"Rows per page": "Rows",
			},
		},
		true
	);
	const _ = i18n.getGroup("core");
</script>

<span>{_("Rows per page")}</span>
```

#### Implementation Notes

- `Locale` renders only `children`; it has no DOM wrapper.

#### Other information

extra details about locales can be obtained from `../locales.md`


## File: core/modal.md

> Source: `core/modal.md`

### SVAR Svelte Core Modal

Package: `@svar-ui/svelte-core`

#### Package

```js
import { Modal } from "@svar-ui/svelte-core";
```

#### Supported Functionality

- Fixed-position backdrop and centered window.
- `title` renders the default header unless a `header` snippet is supplied.
- `children` renders the modal body.
- `footer` snippet replaces the default button row.
- `buttons` defaults to `["cancel", "ok"]`; pass `false` to hide default buttons.
- Button id `"cancel"` calls `oncancel`; every other button id calls `onconfirm`.
- Button labels are localized through locale group `core`.
- Modal focuses itself on mount.
- Enter calls `onconfirm` unless focus is inside a `TEXTAREA` or `BUTTON`; Escape calls `oncancel`.

#### Public Types

```ts
import type { Component } from "svelte";
import type { Snippet } from "svelte";

export declare const Modal: Component<{
	title?: string;
	buttons?: boolean | string[];
	header?: Snippet<[]>;
	footer?: Snippet<[]>;
	children?: () => any;
	onconfirm?: (ev: { button?: string; event: MouseEvent }) => void;
	oncancel?: (ev: { button?: string; event: MouseEvent }) => void;
}>;
```

#### Styling

- Backdrop: `.wx-modal`
- Window: `.wx-window`
- Header: `.wx-header`
- Button row: `.wx-buttons`
- Button cell: `.wx-button`

```svelte
<Modal title="Confirm">
	<div>Continue?</div>
</Modal>

<style>
	.wx-modal .wx-window {
		--wx-modal-width: 360px;
	}
</style>
```

#### Recipes

##### Portal Modal With Default Buttons

```svelte
<script>
	import { Button, Modal, Portal } from "@svar-ui/svelte-core";

	let open = $state(false);
</script>

<Button type="primary" onclick={() => (open = true)}>Show</Button>

{#if open}
	<Portal>
		<Modal
			title="Confirm"
			onconfirm={() => (open = false)}
			oncancel={() => (open = false)}
		>
			Continue?
		</Modal>
	</Portal>
{/if}
```

##### Custom Header And Footer

```svelte
<script>
	import { Button, Modal } from "@svar-ui/svelte-core";
</script>

<Modal buttons={false}>
	{#snippet header()}
		<h2>Custom Title</h2>
	{/snippet}

	<div>Body</div>

	{#snippet footer()}
		<Button type="primary">Apply</Button>
	{/snippet}
</Modal>
```

#### Implementation Notes

- Keyboard Enter/Escape handlers pass a keyboard event, while public types declare `MouseEvent`.
- Button click handlers pass `{ button, event }`.
- Default `"ok"` button is rendered as `type="block primary"`; other default buttons use `type="block secondary"`.


## File: core/modalarea.md

> Source: `core/modalarea.md`

### SVAR Svelte Core ModalArea

Package: `@svar-ui/svelte-core`

#### Package

```js
import { ModalArea } from "@svar-ui/svelte-core";
```

#### Supported Functionality

- Local absolute-position modal backdrop and centered window.
- Intended for modal content inside the current layout rather than a viewport-level fixed modal.
- Renders only `children`; it has no built-in header, footer, buttons, or cancel handler.
- Uses a short fade transition.
- Parent layout should provide a positioned containing block when local placement matters.

#### Public Types

```ts
import type { Component } from "svelte";

export declare const ModalArea: Component<{
	children?: () => any;
}>;
```

#### Styling

- Backdrop: `.wx-modal`
- Window: `.wx-window`
- Backdrop is `position: absolute`, fills the containing block, and uses `--wx-modal-backdrop`.
- Window uses modal background, shadow, border, radius, and min width variables.

```svelte
<div class="local-area">
	<ModalArea>
		<div class="inner">Local modal content</div>
	</ModalArea>
</div>

<style>
	.local-area {
		position: relative;
		min-height: 300px;
	}
</style>
```

#### Recipes

##### Local Modal Overlay

```svelte
<script>
	import { Button, ModalArea } from "@svar-ui/svelte-core";

	let open = $state(false);
</script>

<div style="position: relative; min-height: 300px">
	<Button onclick={() => (open = true)}>Open local modal</Button>

	{#if open}
		<ModalArea>
			<Button onclick={() => (open = false)}>Close</Button>
		</ModalArea>
	{/if}
</div>
```

#### Implementation Notes

- `ModalArea` does not trap focus or handle Escape.
- Use `Modal` when you need built-in title, buttons, confirmation, or cancellation behavior.


## File: core/month.md

> Source: `core/month.md`

### SVAR Svelte Core Month

Package: `@svar-ui/svelte-core`

#### Package

```js
import { Month } from "@svar-ui/svelte-core";
```

#### Supported Functionality

- Low-level month grid used by `Calendar` and `RangeCalendar`.
- `current` is the visible month; pass a date inside the month to render.
- `part="normal"` is required for standalone single-date selection with `value={Date}`.
- Range rendering uses `value={{ start, end }}` and `part` values such as `"left"`, `"right"`, or `"both"`.
- `markers(date)` can return a CSS class string appended to `.wx-day`.
- `onchange` receives a `Date` directly, not an object.
- After selecting a date, source calls `oncancel()` if provided.
- Weekday labels and week start come from locale context, falling back to the default locale.

#### Public Types

```ts
import type { Component } from "svelte";

export declare const Month: Component<{
	value?: { start: Date; end: Date } | Date;
	current?: Date;
	part?: string;
	markers?: (date: Date) => string;
	oncancel?: () => void;
	onchange?: (ev: Date) => void;
}>;
```

#### Styling

- Weekday row: `.wx-weekdays`, `.wx-weekday`
- Day grid: `.wx-days`, `.wx-day`
- Date state classes: `.wx-out`, `.wx-selected`, `.wx-left`, `.wx-right`, `.wx-inrange`, `.wx-weekend`, `.wx-inactive`
- Marker classes from `markers(date)` are appended to `.wx-day`.

```svelte
<Month current={new Date(2025, 4, 1)} part="normal" {markers} />

<style>
	.wx-day.payday {
		font-weight: 700;
	}
</style>
```

#### Recipes

##### Standalone Single-Month Picker

```svelte
<script>
	import { Month } from "@svar-ui/svelte-core";

	let value = $state(new Date(2025, 4, 15));
	let current = $state(new Date(2025, 4, 1));
</script>

<Month
	bind:value
	bind:current
	part="normal"
	onchange={date => (value = date)}
/>
```

##### Range Markup Preview

```svelte
<script>
	import { Month } from "@svar-ui/svelte-core";

	const value = {
		start: new Date(2025, 4, 10),
		end: new Date(2025, 4, 18),
	};
</script>

<Month
	{value}
	current={value.start}
	part="both"
	onchange={date => console.log(date)}
/>
```

#### Implementation Notes

- Source default `part` is `""`; that path treats `value` as a range object. Use `part="normal"` for a plain `Date`.
- Days outside the current month get `.wx-out` and `.wx-inactive`.
- `Month` does not render calendar header or action buttons; use `Calendar` or `RangeCalendar` for those.


## File: core/multicombo.md

> Source: `core/multicombo.md`

### SVAR Svelte Core MultiCombo

Package: `@svar-ui/svelte-core`

#### Package

```js
import { MultiCombo } from "@svar-ui/svelte-core";
```

#### Supported Functionality

- Multi-select searchable input backed by `SuggestDropdown`.
- `value` is a bindable array of selected ids.
- `options` are `{ id, label }` by default.
- `textField` controls display/filter field; default is `"label"`.
- `textOptions` can provide selected tag display objects when visible `options` are partial.
- Typing filters options case-insensitively by `textField`.
- Selected options render as tags with remove icons.
- `checkboxes` shows non-interactive checkboxes in dropdown rows.
- `children` snippet receives `{ option }` for both tags and list rows.
- `onchange` emits `{ value }`.

#### Public Types

```ts
import type { Component } from "svelte";

export interface DropdownOptions {
	inline?: boolean;
	position?: "top" | "right" | "bottom" | "left";
	align?: "start" | "center" | "end";
	css?: string;
	width?: string | "unset" | "auto";
	trackScroll?: boolean;
	virtualized?: boolean;
}

export declare const MultiCombo: Component<{
	id?: string | number;
	value?: (string | number)[];
	options?: { id: string | number; label: string }[];
	textOptions?: { id: string | number; label: string }[];
	textField?: string;
	placeholder?: string;
	title?: string;
	disabled?: boolean;
	error?: boolean;
	checkboxes?: boolean;
	dropdown?: DropdownOptions & {
		virtualized?: boolean;
	};
	children?: () => any;
	onchange?: (ev: { value: (string | number)[] }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-multicombo`
- State classes: `.wx-focus`, `.wx-disabled`, `.wx-error`, `.wx-not-empty`
- Border wrapper: `.wx-wrapper`
- Tags wrapper: `.wx-tags`, tag `.wx-tag`
- Input row: `.wx-select`
- Icons: `.wx-icon`, `.wxi-close`
- Dropdown list hooks: `.wx-list`, `.wx-item`, `.wx-focus`

```svelte
<MultiCombo {options} bind:value dropdown={{ css: "roles-popup" }} />

<style>
	.wx-multicombo .wx-tag {
		max-width: 180px;
	}
</style>
```

#### Recipes

##### Multi Select With Checkboxes

```svelte
<script>
	import { MultiCombo } from "@svar-ui/svelte-core";

	const options = [
		{ id: "editor", label: "Editor" },
		{ id: "owner", label: "Owner" },
		{ id: "viewer", label: "Viewer" },
	];

	let roles = $state(["viewer"]);
</script>

<MultiCombo
	{options}
	bind:value={roles}
	checkboxes
	placeholder="Select roles"
/>
```

##### Custom Tag And Row Content

```svelte
<script>
	import { MultiCombo } from "@svar-ui/svelte-core";

	const users = [
		{ id: 104, label: "Lord Varys", email: "little.birds@mail" },
	];
</script>

<MultiCombo options={users} value={[104]}>
	{#snippet children({ option })}
		<strong>{option.label}</strong>
	{/snippet}
</MultiCombo>
```

#### Implementation Notes

- Filtering assumes `option[textField]` is a string
- The source `onselect` path ignores falsy ids; avoid empty-string ids for selected options.


## File: core/pager.md

> Source: `core/pager.md`

### SVAR Svelte Core Pager

Package: `@svar-ui/svelte-core`

#### Package

```js
import { Pager } from "@svar-ui/svelte-core";
```

#### Supported Functionality

- Pagination control with rows-per-page input, page navigation icons, current page input, and total page count.
- `value` is the bindable current page; default is `1`.
- `pageSize` is bindable; default is `20`.
- `pageCount` is `Math.ceil(total / pageSize)`.
- `from` is the zero-based row offset: `(value - 1) * pageSize`.
- `to` is capped by `total`: `Math.min(value * pageSize, total)`.
- Page navigation emits `{ value, from, to }` after updating the bound page.
- Labels come from locale group `core`.

#### Public Types

```ts
import type { Component } from "svelte";

export declare const Pager: Component<{
	total?: number;
	pageSize?: number;
	value?: number;
	onchange?: (ev: { value: number; from: number; to: number }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-pager`
- Sections: `.wx-left`, `.wx-center`, `.wx-right`
- Navigation icons: `.wx-icon`, icon font classes `wxi-angle-dbl-left`, `wxi-angle-left`, `wxi-angle-right`, `wxi-angle-dbl-right`
- Disabled icons: `.wx-disabled`
- Inputs use local `input` styles inside the component.

```svelte
<div class="grid-footer">
	<Pager total={100} />
</div>

<style>
	.grid-footer .wx-pager {
		justify-content: flex-end;
	}
</style>
```

#### Recipes

##### Bound Page And Page Size

```svelte
<script>
	import { Pager } from "@svar-ui/svelte-core";

	let page = $state(2);
	let pageSize = $state(10);
</script>

<Pager
	total={100}
	bind:value={page}
	bind:pageSize
	onchange={ev => console.log(ev.value, ev.from, ev.to)}
/>
```

#### Implementation Notes

- Page-size input calls `onchange` with `value` equal to the entered page size, not the active page.
- Page navigation calls `onchange` with `value` equal to the active page.
- Current-page input rejects values below `1`, above `pageCount`, or `NaN`.


## File: core/popup.md

> Source: `core/popup.md`

### SVAR Svelte Core Popup

Package: `@svar-ui/svelte-core`

#### Package

```js
import { Popup } from "@svar-ui/svelte-core";
```

#### Supported Functionality

- Low-level absolutely positioned popup surface.
- Position is calculated with `calculatePosition` from `@svar-ui/lib-dom`.
- Use `parent` to anchor to an element, or use `left`/`top` with an `at` position.
- `at` defaults to `"bottom"` in source.
- `oncancel` is called by click-outside behavior.
- `width` can be number, "auto" or percentage like `100%` - calculated from `parent.offsetWidth`.
- `trackScroll`; when enabled hides on scroll outside of popup.

#### Public Types

```ts
import { TPosition } from "@svar-ui/lib-dom";
import type { Component } from "svelte";

export declare const Popup: Component<{
	left?: number;
	top?: number;
	at?: TPosition;
	css: string;
	width: number | string;
	trackScroll: boolean;
	parent?: HTMLElement;
	children?: () => any;
	oncancel?: (ev: MouseEvent) => void;
}>;
```

#### Styling

- Container: `.wx-popup`
- Source appends `css` to `.wx-popup`.
- Inline style sets `position:absolute`, calculated `top`, `left`, and `width`.

```svelte
<Popup parent={buttonNode} css="help-popup">
	<div class="body">Help</div>
</Popup>

<style>
	.wx-popup.help-popup {
		padding: 12px;
	}
</style>
```

#### Recipes

##### Popup Anchored To A Button

```svelte
<script>
	import { Button, Popup } from "@svar-ui/svelte-core";

	let parent = $state(null);
</script>

<div bind:this={parent}>
	<Button>Anchor</Button>
</div>

{#if parent}
	<Popup {parent} at="bottom" oncancel={() => (parent = null)}>
		<div style="padding: 12px">Popup content</div>
	</Popup>
{/if}
```

#### Implementation Notes

- Use `Dropdown` for the common anchored dropdown case; it handles `Portal` and parent discovery.


## File: core/portal.md

> Source: `core/portal.md`

### SVAR Svelte Core Portal

Package: `@svar-ui/svelte-core`

#### Package

```js
import { Portal, popupContainer } from "@svar-ui/svelte-core";
```

#### Supported Functionality

- `Portal` moves its themed child node to `target` or the nearest `data-wx-portal-root` ancestor.
- If no local portal root exists, source appends to the top node from `@svar-ui/lib-dom` environment.
- `theme` defaults from `wx-theme` context when not supplied.
- Children receive an internal `{ mount }` callback argument in source.
- `popupContainer(node)` marks a local portal root with a generated `data-wx-portal-root` attribute.

#### Public Types

```ts
import type { Component } from "svelte";

export declare const Portal: Component<{
	theme?: "willow" | "willow-dark";
	target?: HTMLElement;
	children?: () => any;
}>;

export declare function popupContainer(node: HTMLElement): void;
```

#### Styling

- Source wrapper `.wx-portal` is `display: none`.
- Moved node receives `.wx-{theme}-theme`, such as `.wx-willow-theme`.
- `popupContainer` has no class; it sets a data attribute.

```svelte
<div use:popupContainer class="local-root">
	<slot />
</div>
```

#### Recipes

##### Render A Modal Through Portal

```svelte
<script>
	import { Button, Modal, Portal } from "@svar-ui/svelte-core";

	let open = $state(false);
</script>

<Button onclick={() => (open = true)}>Open</Button>

{#if open}
	<Portal>
		<Modal title="Portal Modal" oncancel={() => (open = false)}>
			Content
		</Modal>
	</Portal>
{/if}
```

##### Local Portal Root

```svelte
<script>
	import { DatePicker, popupContainer } from "@svar-ui/svelte-core";
</script>

<div use:popupContainer class="local-root">
	<DatePicker />
</div>
```


## File: core/radio.md

> Source: `core/radio.md`

### SVAR Svelte Core Radio

Package: `@svar-ui/svelte-core`

Use this file standalone for `RadioButton` and `RadioButtonGroup`.

#### Package

```js
import { RadioButton, RadioButtonGroup } from "@svar-ui/svelte-core";
```

#### Supported Functionality

- `RadioButton.value` is a bindable boolean checked state.
- `RadioButton.onchange` fires only when the radio becomes checked and emits `{ value: true, inputValue }`.
- Standalone radio buttons need a shared `name` to behave as one browser radio group.
- `RadioButtonGroup.options` are `{ id, label }`.
- `RadioButtonGroup.value` is the selected option id.
- Group `onchange` emits `{ value }`.
- Group `type` supports `inline` and `grid`; default layout is one item per row.

#### Public Types

```ts
import type { Component } from "svelte";

export declare const RadioButton: Component<{
	id?: string | number;
	label?: string;
	value?: boolean;
	name?: string;
	inputValue?: string | number;
	disabled?: boolean;
	onchange?: (ev: { value: boolean; inputValue: string | number }) => void;
}>;

export declare const RadioButtonGroup: Component<{
	options?: { id: string | number; label: string }[];
	value?: string | number;
	type?: "inline" | "grid";
	onchange?: (ev: { value: string | number }) => void;
}>;
```

#### Styling

- Radio wrapper: `.wx-radio`
- Group wrapper: `.wx-radiogroup`, `.wx-radiogroup.wx-inline`, `.wx-radiogroup.wx-grid`
- Group item wrapper: `.wx-item`

```svelte
<RadioButtonGroup {options} bind:value type="grid" />

<style>
	.wx-radiogroup.wx-grid .wx-item {
		flex-basis: 33.333%;
		max-width: 33.333%;
	}
</style>
```

#### Recipes

##### Standalone Radio Buttons

```svelte
<script>
	import { RadioButton } from "@svar-ui/svelte-core";
</script>

<RadioButton label="One" name="mode" inputValue="one" value={true} />
<RadioButton label="Two" name="mode" inputValue="two" />
```

##### Radio Group

```svelte
<script>
	import { RadioButtonGroup } from "@svar-ui/svelte-core";

	const options = [
		{ id: 1, label: "Option 1" },
		{ id: 2, label: "Option 2" },
		{ id: 3, label: "Option 3" },
	];

	let value = $state(1);
</script>

<RadioButtonGroup {options} bind:value type="inline" />
```

#### Implementation Notes

- `RadioButtonGroup` does not pass disabled state through option objects.


## File: core/rangecalendar.md

> Source: `core/rangecalendar.md`

### SVAR Svelte Core RangeCalendar

Package: `@svar-ui/svelte-core`

#### Package

```js
import { RangeCalendar } from "@svar-ui/svelte-core";
```

#### Supported Functionality

- Date range calendar with bindable `start` and `end`.
- `months` is `1` or `2`; default is `2`.
- Two-month mode renders left and right panels with synchronized months.
- `buttons` defaults to `["clear", "today"]`; arrays can include `"done"`.
- When `buttons` includes `"done"`, selection changes are held until the done action emits the final value.
- Selection order is normalized: selecting an end before the start swaps `start` and `end`.
- `markers(date)` can return a class string appended to `.wx-day`.
- `onchange` receives `{ start: Date | null, end: Date | null }`.

#### Public Types

```ts
import type { Component } from "svelte";

export declare const RangeCalendar: Component<{
	start?: Date;
	end?: Date;
	current?: Date;
	months?: 1 | 2;
	markers?: (date: Date) => string;
	buttons?: boolean | ("clear" | "today" | "done")[];
	onchange?: (ev: { start: Date | null; end: Date | null }) => void;
}>;
```

#### Styling

- Two-month wrapper: `.wx-rangecalendar`
- Panel wrapper: `.wx-half`
- Calendar panels use `.wx-calendar`, `.wx-wrap`, `.wx-buttons`, `.wx-button-item`
- Month range states: `.wx-selected`, `.wx-left`, `.wx-right`, `.wx-inrange`

```svelte
<div class="range-shell">
	<RangeCalendar months={2} />
</div>

<style>
	.range-shell {
		--wx-calendar-cell-size: 30px;
	}
</style>
```

#### Recipes

##### Two-Month Range With Done Button

```svelte
<script>
	import { RangeCalendar } from "@svar-ui/svelte-core";

	let start = $state(new Date(2025, 4, 1));
	let end = $state(new Date(2025, 4, 7));
</script>

<RangeCalendar
	bind:start
	bind:end
	months={2}
	buttons={["done", "clear", "today"]}
	onchange={ev => console.log(ev.start, ev.end)}
/>
```

##### Single-Month Range

```svelte
<script>
	import { RangeCalendar } from "@svar-ui/svelte-core";

	let start = $state();
	let end = $state();
</script>

<RangeCalendar
	bind:start
	bind:end
	months={1}
	buttons={false}
	onchange={ev => console.log(ev.start, ev.end)}
/>
```

#### Implementation Notes

- Source initializes the visible month from `start`, then `current`, then `new Date()`.
- Clearing emits `{ start: null, end: null }`.


## File: core/richselect.md

> Source: `core/richselect.md`

### SVAR Svelte Core RichSelect

Package: `@svar-ui/svelte-core`

#### Package

```js
import { RichSelect } from "@svar-ui/svelte-core";
```

#### Supported Functionality

- Non-input single-select control backed by `SuggestDropdown`.
- `value` is the selected id and is bindable.
- `options` are `{ id, label }` by default.
- `textField` controls display field; default is `"label"`.
- `textOptions` can provide selected display objects when visible `options` are partial.
- `clear` shows a close icon when value is set and not disabled.
- `children` snippet receives the option object directly for both selected content and list rows.
- `onchange` emits `{ value }`.

#### Public Types

```ts
import type { Component } from "svelte";

export interface DropdownOptions {
	inline?: boolean;
	position?: "top" | "right" | "bottom" | "left";
	align?: "start" | "center" | "end";
	css?: string;
	width?: string | "unset" | "auto";
	trackScroll?: boolean;
	virtualized?: boolean;
}

export declare const RichSelect: Component<{
	value?: string | number;
	options?: { id: string | number; label: string }[];
	textOptions?: { id: string | number; label: string }[];
	placeholder?: string;
	disabled?: boolean;
	error?: boolean;
	title?: string;
	textField?: string;
	clear?: boolean;
	dropdown?: DropdownOptions & {
		virtualized?: boolean;
	};
	children?: () => any;
	onchange?: (ev: { value: string | number }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-richselect`
- State classes: `.wx-disabled`, `.wx-error`, `.wx-nowrap`
- Content label: `.wx-label`
- Placeholder: `.wx-placeholder`
- Icon: `.wx-icon`, close icon `.wxi-close`
- Dropdown list hooks: `.wx-list`, `.wx-item`, `.wx-focus`

```svelte
<RichSelect
	options={users}
	value={104}
	dropdown={{ css: "user-select-menu" }}
/>

<style>
	.wx-popup.user-select-menu .wx-item {
		min-height: 40px;
	}
</style>
```

#### Recipes

##### Rich Select With Custom Template

```svelte
<script>
	import { RichSelect } from "@svar-ui/svelte-core";

	const users = [
		{ id: 104, label: "Lord Varys", email: "little.birds@mail" },
		{ id: 103, label: "Ned Stark", email: "winterhell@mail" },
	];
</script>

<RichSelect options={users} value={104}>
	{#snippet children(option)}
		<div>
			<strong>{option.label}</strong>
			<span>{option.email}</span>
		</div>
	{/snippet}
</RichSelect>
```

##### Hidden Selected Option

```svelte
<script>
	import { RichSelect } from "@svar-ui/svelte-core";

	const allUsers = [
		{ id: 87, label: "Berni Mayou" },
		{ id: 103, label: "Ned Stark" },
	];

	const visibleUsers = [{ id: 103, label: "Ned Stark" }];
</script>

<RichSelect textOptions={allUsers} options={visibleUsers} value={87} clear />
```

#### Implementation Notes

- Without a custom snippet, `.wx-nowrap` is added to ellipsize the selected label.


## File: core/segmented.md

> Source: `core/segmented.md`

### SVAR Svelte Core Segmented

Package: `@svar-ui/svelte-core`

#### Package

```js
import { Segmented } from "@svar-ui/svelte-core";
```

#### Supported Functionality

- Renders an inline segmented button group.
- `options` are `{ id, label, icon?, title? }`.
- `value` is the selected id and is bindable.
- Clicking an option sets `value = option.id` and emits `onchange({ value })`.
- `css` is appended to `.wx-segmented`.
- Default content renders `option.icon` and `option.label`.
- `children` snippet receives `{ option }` for custom option content.

#### Public Types

```ts
import type { Component } from "svelte";

export declare const Segmented: Component<{
	options?: {
		id: string | number;
		label: string;
		icon?: string;
		title?: string;
	}[];
	value?: string | number;
	css?: string;
	children?: () => any;
	onchange?: (ev: { value: string | number }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-segmented`
- Selected button: `.wx-selected`
- Default icon: `.wx-icon`, icon-only modifier `.wx-only`
- Default label: `.wx-label`

```svelte
<Segmented css="view-mode" {options} bind:value />

<style>
	.wx-segmented.view-mode {
		--wx-segmented-padding: 3px;
	}
</style>
```

#### Recipes

##### Basic Segmented Control

```svelte
<script>
	import { Segmented } from "@svar-ui/svelte-core";

	const options = [
		{ id: "list", label: "List", icon: "wxi-view-sequential" },
		{ id: "grid", label: "Grid", icon: "wxi-view-grid" },
	];

	let value = $state("list");
</script>

<Segmented {options} bind:value onchange={ev => console.log(ev.value)} />
```

##### Custom Option Content

```svelte
<script>
	import { Segmented } from "@svar-ui/svelte-core";

	const options = [
		{ id: "left", label: "Left", icon: "wxi-align-left" },
		{ id: "right", label: "Right", icon: "wxi-align-right" },
	];
</script>

<Segmented {options} value="left">
	{#snippet children({ option })}
		<i class={option.icon}></i>
		<span>{option.label}</span>
	{/snippet}
</Segmented>
```


## File: core/select.md

> Source: `core/select.md`

### SVAR Svelte Core Select

Package: `@svar-ui/svelte-core`

#### Package

```js
import { Select } from "@svar-ui/svelte-core";
```

#### Supported Functionality

- Renders a native `<select>` inside `.wx-select`.
- `options` are `{ id, label }` by default.
- `textField` changes the displayed field; default is `"label"`.
- `value` is bindable and stores the selected option id.
- `placeholder` is shown as an overlay when value is empty and not `0`.
- `clear` shows a close icon when the component has a value and is not disabled.
- `onchange` emits `{ value }`.

#### Public Types

```ts
import type { Component } from "svelte";

export declare const Select: Component<{
	value?: string | number;
	options?: { id: string | number; label: string }[];
	placeholder?: string;
	title?: string;
	disabled?: boolean;
	error?: boolean;
	textField?: string;
	clear?: boolean;
	id?: string | number;
	onchange?: (ev: { value: string | number }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-select`
- Placeholder overlay: `.wx-placeholder`
- Icon: `.wx-icon`, close icon `.wxi-close`
- Error class is applied to the native `select` as `.wx-error`.

```svelte
<div class="owner-select">
	<Select options={users} bind:value clear />
</div>

<style>
	.owner-select .wx-select {
		--wx-input-width: 280px;
	}
</style>
```

#### Recipes

##### Native Select With Clear

```svelte
<script>
	import { Field, Select } from "@svar-ui/svelte-core";

	const users = [
		{ id: 103, label: "Ned Stark" },
		{ id: 104, label: "Lord Varys" },
	];

	let owner = $state("");
</script>

<Field label="Owner" position="left">
	<Select
		options={users}
		bind:value={owner}
		placeholder="Select owner"
		clear
	/>
</Field>
```

#### Implementation Notes

- `Select` has no `css` prop; use a parent/global selector for styling.


## File: core/sidearea.md

> Source: `core/sidearea.md`

### SVAR Svelte Core SideArea

Package: `@svar-ui/svelte-core`

#### Package

```js
import { SideArea } from "@svar-ui/svelte-core";
```

#### Supported Functionality

- Absolute-position side panel for local layouts.
- `position` public type supports only `"right"`; source defaults to `"right"`.
- Clicking outside the panel calls `oncancel`.
- Uses a fly transition from the right.
- Renders arbitrary `children`.

#### Public Types

```ts
import type { Component } from "svelte";

export declare const SideArea: Component<{
	position?: "right";
	children?: () => any;
	oncancel?: () => void;
}>;
```

#### Styling

- Panel: `.wx-sidearea`
- Right position: `.wx-pos-right`

```svelte
<div class="side-host">
	<SideArea>
		<div class="side-content">Panel</div>
	</SideArea>
</div>

<style>
	.side-host {
		position: relative;
		min-height: 300px;
	}

	.side-content {
		width: 400px;
		padding: 20px;
	}
</style>
```

#### Recipes

##### Right-Side Local Panel

```svelte
<script>
	import { Button, SideArea } from "@svar-ui/svelte-core";

	let open = $state(false);
</script>

<div style="position: relative; min-height: 300px">
	<Button onclick={() => (open = true)}>Open side panel</Button>

	{#if open}
		<SideArea oncancel={() => (open = false)}>
			<div style="width: 400px; padding: 20px">Panel content</div>
		</SideArea>
	{/if}
</div>
```


## File: core/slider.md

> Source: `core/slider.md`

### SVAR Svelte Core Slider

Package: `@svar-ui/svelte-core`

#### Package

```js
import { Slider } from "@svar-ui/svelte-core";
```

#### Supported Functionality

- Renders an input range with optional label.
- Bindable `value`, default `0`.
- `min` defaults to `0`, `max` to `100`, `step` to `1`.
- `width` sets inline width on `.wx-slider`.
- During drag, `onchange` emits `{ value, previous, input: true }`.
- On final change, `onchange` emits `{ value, previous }`.
- `previous` tracks the previous input/final value separately for drag and final changes.

#### Public Types

```ts
import type { Component } from "svelte";

export declare const Slider: Component<{
	id?: string | number;
	label?: string;
	width?: string;
	min?: number;
	max?: number;
	value?: number;
	step?: number;
	title?: string;
	disabled?: boolean;
	onchange?: (ev: {
		value: number;
		previous: number;
		input?: boolean;
	}) => void;
}>;
```

#### Styling

- Wrapper: `.wx-slider`
- Inner range input is styled through input pseudo-elements.
- Label is a native `label` inside `.wx-slider`.

```svelte
<Slider width="240px" bind:value />

<style>
	.wx-slider {
		--wx-slider-thumb-size: 18px;
	}
</style>
```

#### Recipes

##### Slider With Drag And Final Events

```svelte
<script>
	import { Field, Slider } from "@svar-ui/svelte-core";

	let progress = $state(50);
</script>

<Field label="Progress" position="left" type="slider">
	<Slider
		label={`Progress: ${progress}%`}
		bind:value={progress}
		min={0}
		max={100}
		onchange={ev => {
			if (ev.input) console.log("drag", ev.previous, ev.value);
			else console.log("final", ev.previous, ev.value);
		}}
	/>
</Field>
```


## File: core/suggest-dropdown.md

> Source: `core/suggest-dropdown.md`

### SVAR Svelte Core SuggestDropdown

Package: `@svar-ui/svelte-core`

#### Package

```js
import { SuggestDropdown } from "@svar-ui/svelte-core";
```

#### Supported Functionality

- Low-level dropdown list helper used by `Combo`, `MultiCombo`, and `RichSelect`.
- Renders only when navigation index is not `null`; callers open it through `onready.navigate`.
- `items` are `{ id, label }`.
- `onready` receives navigation helpers: `navigate`, `keydown`, and `move`.
- `onselect` emits `{ id }`; in multiselect mode `id` is the next selected id array.
- `multiselect` toggles id arrays instead of a single id.
- `checkboxes` renders a non-interactive `Checkbox` in each row.
- `virtualized` renders only visible rows with fixed measured item height and overscan.
- `children` snippet receives `{ option }`.

#### Public Types

```ts
import type { Component } from "svelte";

export interface DropdownOptions {
	inline?: boolean;
	position?: "top" | "right" | "bottom" | "left";
	align?: "start" | "center" | "end";
	css?: string;
	width?: string | "unset" | "auto";
	trackScroll?: boolean;
	virtualized?: boolean;
}

export declare const SuggestDropdown: Component<
	DropdownOptions & {
		items?: { id: string | number; label: string }[];
		children?: () => any;
		onselect?: (ev: { id: string | number | (string | number)[] }) => void;
		onready?: (ev: {
			navigate?: (dir: number | null, ev?: KeyboardEvent) => void;
			keydown?: (ev: KeyboardEvent, dir: number) => void;
			move?: (ev: KeyboardEvent) => void;
		}) => void;
		multiselect?: boolean;
		checkboxes?: boolean;
		value?: string | number | (string | number)[];
		virtualized?: boolean;
	}
>;
```

#### Styling

- List container: `.wx-list`
- Virtual wrapper/content: `.wx-list-wrapper`, `.wx-list-content`
- Row: `.wx-item`
- Focus row: `.wx-item.wx-focus`
- Empty state: `.wx-no-data`
- Non-inline dropdown `css` is appended to `.wx-popup`.

```svelte
<SuggestDropdown {items} css="suggest-menu" />

<style>
	.wx-popup.suggest-menu .wx-list {
		max-height: 180px;
	}
</style>
```

#### Recipes

##### Controlled Suggest Dropdown

```svelte
<script>
	import { SuggestDropdown } from "@svar-ui/svelte-core";

	const items = [
		{ id: 1, label: "One" },
		{ id: 2, label: "Two" },
	];

	let api;
</script>

<button onclick={() => api.navigate(0)}>Open</button>

<SuggestDropdown
	{items}
	onready={ev => (api = ev)}
	onselect={ev => console.log(ev.id)}
/>
```

#### Implementation Notes

- Keyboard handlers use `ev.code` values `Enter`, `Space`, `Escape`, `Tab`, `ArrowDown`, and `ArrowUp`.
- Virtual mode measures the first rendered item and assumes all rows have that height.


## File: core/switch.md

> Source: `core/switch.md`

### SVAR Svelte Core Switch

Package: `@svar-ui/svelte-core`

#### Package

```js
import { Switch } from "@svar-ui/svelte-core";
```

#### Supported Functionality

- Renders a labeled checkbox styled as a switch.
- `value` is a bindable boolean.
- `disabled` is forwarded to the hidden checkbox input.
- `onchange` emits `{ value }` after the checked state changes.
- `id` is used through the shared input id helper, so it can connect with a surrounding `Field`.

#### Public Types

```ts
import type { Component } from "svelte";

export declare const Switch: Component<{
	id?: string | number;
	value?: boolean;
	disabled?: boolean;
	onchange?: (ev: { value: boolean }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-switch`
- Internal elements are an invisible checkbox input and a visual `span`.

```svelte
<Switch bind:value />

<style>
	.wx-switch {
		--wx-switch-width: 56px;
	}
</style>
```

#### Recipes

##### Bound Switch In A Field

```svelte
<script>
	import { Field, Switch } from "@svar-ui/svelte-core";

	let enabled = $state(true);
</script>

<Field label={`Enabled: ${enabled}`} position="left" type="switch">
	<Switch bind:value={enabled} onchange={ev => console.log(ev.value)} />
</Field>
```

#### Implementation Notes

- The component does not expose `css`; style through parent/global selectors or theme variables.


## File: core/tabs.md

> Source: `core/tabs.md`

### SVAR Svelte Core Tabs

Package: `@svar-ui/svelte-core`

#### Package

```js
import { Tabs } from "@svar-ui/svelte-core";
```

#### Supported Functionality

- Renders a tab strip only; render the tab panel yourself based on `value`.
- `options` are `{ id, label?, title?, icon? }`.
- `value` is the active tab id and is bindable.
- Clicking a tab sets `value = option.id` and emits `onchange({ value })`.
- `type` is `top` or `bottom`; default is `top`.
- Icons use the same icon class pattern as other core controls.

#### Public Types

```ts
import type { Component } from "svelte";

export declare const Tabs: Component<{
	options?: {
		id: string | number;
		label?: string;
		title?: string;
		icon?: string;
	}[];
	value?: string | number;
	type?: "top" | "bottom";
	onchange?: (ev: { value: string | number }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-tabs`, plus `.wx-top` or `.wx-bottom`
- Active button: `.wx-active`
- Default icon: `.wx-icon`, icon-only modifier `.wx-only`
- Default label: `.wx-label`

```svelte
<Tabs options={tabs} bind:value={active} />

<style>
	.wx-tabs {
		--wx-tabs-cell-min-width: 80px;
	}
</style>
```

#### Recipes

##### Tabs With Panels

```svelte
<script>
	import { Tabs } from "@svar-ui/svelte-core";

	const tabs = [
		{ id: "info", label: "Info", icon: "wxi-alert" },
		{ id: "audit", label: "Audit" },
		{ id: "done", icon: "wxi-check", title: "Done" },
	];

	let active = $state("info");
</script>

<Tabs options={tabs} bind:value={active} />

{#if active === "info"}
	<div>Info panel</div>
{:else if active === "audit"}
	<div>Audit panel</div>
{:else}
	<div>Done panel</div>
{/if}

<Tabs options={tabs} bind:value={active} type="bottom" />
```

#### Implementation Notes

- `Tabs` has no `css` prop; style with an enclosing parent/global selector or theme variables.


## File: core/text.md

> Source: `core/text.md`

### SVAR Svelte Core Text

Package: `@svar-ui/svelte-core`

#### Package

```js
import { Text } from "@svar-ui/svelte-core";
```

#### Supported Functionality

- Bindable `value`, with `string | number` public type.
- `type` supports `text`, `number`, and `password`; default is `text`.
- `onchange` fires `{ value, input: true }` on input and `{ value }` on native change.
- `focus` and `select` focus/select the input after mount.
- `clear` shows a close icon when the input has a value; clicking it sets `value = ""` and emits `{ value }`.
- `icon` renders inside the input. It is right-aligned unless `css` includes `wx-icon-left`.
- `inputStyle` is applied to the inner `<input>`.
- `readonly`, `disabled`, `error`, `placeholder`, and `title` are forwarded to the input/wrapper.

#### Public Types

```ts
import type { Component } from "svelte";

export declare const Text: Component<{
	value?: string | number;
	id?: string | number;
	readonly?: boolean;
	focus?: boolean;
	select?: boolean;
	type?: "text" | "number" | "password";
	placeholder?: string;
	disabled?: boolean;
	error?: boolean;
	inputStyle?: string;
	title?: string;
	css?: string;
	icon?: string;
	clear?: boolean;
	onchange?: (ev: { value: string | number; input?: boolean }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-text`
- State/classes: `.wx-error`, `.wx-disabled`, `.wx-clear`, `.wx-icon-left`, `.wx-icon-right`
- Icon: `.wx-icon`; clear icon: `.wx-icon.wxi-close`
- `css` is appended to `.wx-text`.

```svelte
<Text css="search-input wx-icon-left" icon="wxi-search" clear />

<style>
	.wx-text.search-input {
		--wx-input-width: 320px;
	}
</style>
```

#### Recipes

##### Text With Clear And Left Icon

```svelte
<script>
	import { Field, Text } from "@svar-ui/svelte-core";

	let query = $state("");
</script>

<Field label="Search" position="left">
	<Text
		bind:value={query}
		placeholder="Type here"
		icon="wxi-search"
		css="wx-icon-left"
		clear
		onchange={ev => {
			if (!ev.input) console.log("final", ev.value);
		}}
	/>
</Field>
```

##### Focus And Select On Mount

```svelte
<script>
	import { Text } from "@svar-ui/svelte-core";
</script>

<Text value="Some value" focus select />
```

#### Implementation Notes

- `type="number"` still binds through the input value; account for string/number conversion in your app logic.


## File: core/textarea.md

> Source: `core/textarea.md`

### SVAR Svelte Core TextArea

Package: `@svar-ui/svelte-core`

#### Package

```js
import { TextArea } from "@svar-ui/svelte-core";
```

#### Supported Functionality

- Renders a native `<textarea class="wx-textarea">`.
- `value` is bindable.
- `onchange` fires `{ value, input: true }` on input and `{ value }` on native change.
- Supports `id`, `placeholder`, `title`, `disabled`, `error`, and `readonly`.
- The textarea is vertically resizable unless disabled.

#### Public Types

```ts
import type { Component } from "svelte";

export declare const TextArea: Component<{
	value?: string;
	id?: string | number;
	placeholder?: string;
	title?: string;
	disabled?: boolean;
	error?: boolean;
	readonly?: boolean;
	onchange?: (ev: { value: string; input?: boolean }) => void;
}>;
```

#### Styling

- Textarea: `.wx-textarea`
- Error state: `.wx-textarea.wx-error`
- Disabled state uses `[disabled]`.

```svelte
<TextArea placeholder="Details" />

<style>
	.wx-textarea {
		min-height: 140px;
	}
</style>
```

#### Recipes

##### TextArea In A Field

```svelte
<script>
	import { Field, TextArea } from "@svar-ui/svelte-core";

	let details = $state("");
</script>

<Field label="Details" error>
	<TextArea
		bind:value={details}
		error
		title="Details are required"
		placeholder="Type here"
	/>
</Field>
```

#### Implementation Notes

- There is no `css` prop; style through a parent/global selector or theme variables.


## File: core/themes.md

> Source: `core/themes.md`

### SVAR Svelte Core Themes

Package: `@svar-ui/svelte-core`

#### Package

```js
import { Willow, WillowDark } from "@svar-ui/svelte-core";
```

#### Supported Functionality

- Theme components provide Svelte context `wx-theme`.
- `Willow` sets `wx-theme` to `"willow"`.
- `WillowDark` sets `wx-theme` to `"willow-dark"`.
- When `children` are supplied, each theme renders `.wx-theme.wx-*-theme` with `height:100%`.
- `fonts` defaults to `true`.
- `Willow` and `WillowDark` load Open Sans font files and the `wxi` icon CSS.
- Use `fonts={false}` when fonts/icons are already loaded or the app manages font loading.
- Theme styling is CSS-variable driven; override variables on the theme wrapper or an ancestor around specific controls.

#### Public Types

```ts
import type { Component } from "svelte";

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


```svelte
<Willow fonts={false}>
	<div class="app-theme">
		<App />
	</div>
</Willow>

<style>
	.app-theme {
		--wx-color-primary: #0f766e;
		--wx-input-width: 280px;
		--wx-button-border-radius: 4px;
		--wx-calendar-cell-size: 30px;
	}
</style>
```

#### Recipes

##### Wrap An App In A Theme

```svelte
<script>
	import { Willow } from "@svar-ui/svelte-core";
	import AppRoutes from "./AppRoutes.svelte";
</script>

<Willow>
	<AppRoutes />
</Willow>
```

##### Dark Theme Without CDN Font Injection

```svelte
<script>
	import { WillowDark } from "@svar-ui/svelte-core";
</script>

<WillowDark fonts={false}>
	<div class="screen">Dark UI</div>
</WillowDark>
```

#### Other information

extra details about themes can be obtained from `../themes.md`


## File: core/timepicker.md

> Source: `core/timepicker.md`

### SVAR Svelte Core TimePicker

Package: `@svar-ui/svelte-core`

#### Package

```js
import { TimePicker } from "@svar-ui/svelte-core";
```

#### Supported Functionality

- Input-like time picker backed by `Text`, `Dropdown`, `Slider`, and optional `TwoState`.
- `value` is bindable and is a `Date`; only hours and minutes are used.
- Default value is `new Date(0, 0, 0, 0, 0)` when `value` is nullish.
- `format` can be a time format string or `(value: Date) => string`; locale time format is used by default.
- Locale `calendar.clockFormat == 12` enables the AM/PM `TwoState`.
- Hour and minute text inputs update on blur.
- Hour and minute sliders update through `Slider.onchange`.
- `dropdown` is forwarded to `Dropdown`; date/time dropdowns default width to `"unset"` when no width is provided.
- `onchange` receives `{ value: Date }` after assigning the new bindable value.

#### Public Types

```ts
import type { Component } from "svelte";

export interface DropdownOptions {
	inline?: boolean;
	position?: "top" | "right" | "bottom" | "left";
	align?: "start" | "center" | "end";
	css?: string;
	width?: string | "unset" | "auto";
	trackScroll?: boolean;
	virtualized?: boolean;
}

export declare const TimePicker: Component<{
	value?: Date;
	id?: string | number;
	title?: string;
	css?: string;
	disabled?: boolean;
	error?: boolean;
	format?: string | ((value: Date) => string);
	dropdown?: DropdownOptions;
	onchange?: (ev: { value: Date }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-timepicker`
- State classes: `.wx-disabled`, `.wx-error`
- `css` is passed to the inner `Text`.
- Popup content: `.wx-wrapper`, `.wx-timer`, `.wx-digit`, `.wx-separator`
- Slider rows use `Field` and `Slider` classes.
- AM/PM toggle uses `TwoState`/`Button` classes.

```svelte
<TimePicker css="time-input" dropdown={{ css: "time-popup", width: "260px" }} />

<style>
	.wx-text.time-input {
		--wx-input-width: 180px;
	}
</style>
```

#### Recipes

##### Bound Time

```svelte
<script>
	import { Field, TimePicker } from "@svar-ui/svelte-core";

	let value = $state(new Date(0, 0, 0, 14, 30));
</script>

<Field label="Time" position="left">
	<TimePicker bind:value onchange={ev => console.log(ev.value)} />
</Field>
```

##### Twelve-Hour Locale

```svelte
<script>
	import { Field, Locale, TimePicker } from "@svar-ui/svelte-core";

	let value = $state(new Date(0, 0, 0, 14, 30));
</script>

<Locale
	words={{
		formats: { timeFormat: "%g:%i %a" },
		calendar: { clockFormat: 12 },
	}}
>
	<Field label="Time" position="left">
		<TimePicker bind:value dropdown={{ width: "100%" }} />
	</Field>
</Locale>
```

#### Implementation Notes

- The visible text is readonly; typed hour/minute edits happen only inside the popup.


## File: core/twostate.md

> Source: `core/twostate.md`

### SVAR Svelte Core TwoState

Package: `@svar-ui/svelte-core`

#### Package

```js
import { TwoState } from "@svar-ui/svelte-core";
```

#### Supported Functionality

- Wraps `Button` and toggles bindable boolean `value`.
- When active, adds `pressed` to the forwarded `type`.
- `textActive` and `iconActive` replace `text` and `icon` while active.
- `children` renders inactive/default content; `active` snippet renders active content when `value` is true.
- Click order: `onclick(ev)` first, then value toggle and `onchange({ value })`.
- Calling `ev.preventDefault()` inside `onclick` prevents the toggle and `onchange`.

#### Public Types

```ts
import type { Component } from "svelte";
import type { Snippet } from "svelte";

export declare const TwoState: Component<{
	value?: boolean;
	type?:
		| "primary"
		| "secondary"
		| "danger"
		| "link"
		| "primary block"
		| "secondary block"
		| "danger block"
		| "link block";
	icon?: string;
	disabled?: boolean;
	iconActive?: string;
	title?: string;
	css?: string;
	text?: string;
	textActive?: string;
	active?: Snippet<[]>;
	children?: () => any;
	onclick?: (ev: MouseEvent) => void;
	onchange?: (ev: { value: boolean }) => void;
}>;
```

#### Styling

- Uses `Button`, so styling hooks are `.wx-button` plus `.wx-pressed` when active.
- `css` is passed to the inner `Button`.
- Button type variables such as `--wx-button-pressed`, `--wx-button-primary-pressed`, and `--wx-button-box-shadow` control active state.

```svelte
<TwoState css="favorite-button" icon="wxi-star" iconActive="wxi-check" />

<style>
	.wx-button.favorite-button.wx-pressed {
		font-weight: 700;
	}
</style>
```

#### Recipes

##### Toggle With Active Content

```svelte
<script>
	import { TwoState } from "@svar-ui/svelte-core";

	let active = $state(false);
</script>

<TwoState
	bind:value={active}
	type="primary"
	icon="wxi-star"
	iconActive="wxi-check"
	onchange={ev => console.log(ev.value)}
>
	Favorite
	{#snippet active()}
		Favorited
	{/snippet}
</TwoState>
```

##### Prevent Toggle

```svelte
<script>
	import { TwoState } from "@svar-ui/svelte-core";

	function beforeToggle(ev) {
		if (!confirm("Toggle?")) ev.preventDefault();
	}
</script>

<TwoState onclick={beforeToggle}>Toggle</TwoState>
```

#### Implementation Notes

- The active snippet is rendered only when `value` is true.
- If `active` is not supplied, the component reuses `children` or `text` with active icon/text substitutions.


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


## File: toolbar/index.md

> Source: `toolbar/index.md`

Use when UI of app requires Toolbar, configuring, or modifying SVAR Svelte Toolbar / @svar-ui/svelte-toolbar components

#### Package

```js
import { Toolbar, registerToolbarItem } from "@svar-ui/svelte-toolbar";
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
- all extra properties passthrough to the Svelte components

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

Widgets from `@svar-ui/svelte-core` which can be used as components: Slider, Text, CheckboxGroup, RichSelect, DatePicker, ColorPicker, ColorSelect, Checkbox, Tabs, Pager, Segmented, Switch, TwoState, Combo, MultiCombo.

#### Public Types

```ts
import type { Component } from "svelte";

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

```svelte
<script>
	let message = $state("");
	function onClick(item) {
		message = `Button '${item.id}' clicked`;
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

<Toolbar {items} />
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

```svelte
<Toolbar
	items={[
		{ id: "edit", comp: "button", icon: "wxi-edit-outline" },
		{ id: "delete", comp: "button", icon: "wxi-delete-outline" },
	]}
	onclick={ev => console.log(ev.item.id)}
/>
```

##### Keyed Values

```svelte
<script>
	// component must support `value` handler and `onchange` callback to be bound, most svelte-core controls fit
	import { Slider } from "@svar-ui/svelte-core";
	let values = $state({ size: 15 });
</script>

<Toolbar
	items={[{ comp: Slider, min: 0, max: 100, key: "size" }]}
	bind:values
	onchange={ev => console.log(ev.item.key, ev.value)}
/>
```

##### Common core controls

```svelte
<script>
	import { Slider, Segmented, Switch } from "@svar-ui/svelte-core";

	const options = [
		{ id: 1, label: "One" },
		{ id: 2, label: "Two" },
	];
</script>

<Toolbar
	css="demo-toolbar"
	values={{ size: 14, mode: 1, enabled: true }}
	items={[
		{ text: "Controls" },
		{ comp: "spacer" },
		{ comp: Slider, min: 0, max: 100, key: "size" },
		{ comp: Segmented, options, key: "mode" },
		{ comp: Switch, key: "enabled" },
	]}
/>
```

##### Custom Component Contract

```svelte
<!-- CustomToolbarItem.svelte -->
<script>
	let {
		value,
		onchange,
		onclick,
		menu,
		text = "",
		disabled = false,
	} = $props();
</script>

<button
	class:in-menu={menu}
	{disabled}
	onclick={() => {
		onclick?.();
		onchange?.({ value: !value });
	}}
>
	{text}
</button>
```

```js
import CustomToolbarItem from "./CustomToolbarItem.svelte";

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

```svelte
<Toolbar
	values={{ name: "Item X12-A" }}
	items={[
		{ comp: "label", spacer: true, key: "name" },
		{ comp: "separator" },
		{
			icon: "wxi-dots-v",
			collapsed: true,
			layout: "column",
			items: [
				{ id: "done", comp: "item", text: "Mark as finished task" },
				{
					id: "delete",
					comp: "item",
					css: "danger",
					text: "Delete item",
				},
			],
		},
	]}
/>
```

##### Vertical Toolbar

```svelte
<Toolbar
	layout="column"
	items={[
		{ id: "new", comp: "button", icon: "wxi-plus" },
		{ id: "edit", comp: "button", icon: "wxi-edit-outline" },
		{ comp: "separator" },
		{ id: "delete", comp: "button", icon: "wxi-delete-outline" },
	]}
/>
```


## File: layout/index.md

> Source: `layout/index.md`

Use when building, configuring, styling, or modifying SVAR Svelte Layout / @svar-ui/svelte-layout components

#### Package

```js
import { Layout, Cell, Panel } from "@svar-ui/svelte-layout";
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

- Expanded `Panel` always renders `.wx-cell-header` with a toggle button; custom `header` snippet replaces label text but not the toggle.
- Collapsed row panels become a vertical bar; collapsed column panels become a horizontal bar.
- Collapsed size is controlled by `--wx-panel-collapsed-size`, default `24px`.
- Collapsed panels can't be resized

#### Public Types

```ts
import { type Snippet, type Component } from "svelte";

interface ILayoutProps {
	direction?: "column" | "row";
	preset?: "clean" | "line" | "wide" | "space";
	gap?: number;
	padding?: number;
	resizable?: boolean;
	css?: string;
	children: Snippet;
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
	children: Snippet;
	header?: Snippet;
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
	children: Snippet;
	header?: Snippet;
	oncollapse?: (collapsed: boolean) => void;
}

export declare const Layout: Component<ILayoutProps>;
export declare const Cell: Component<ICellProps>;
export declare const Panel: Component<IPanelProps>;
```

#### Styling

- `css` is appended to the component root: `.wx-layout`, `.wx-cell`, or `.wx-cell.wx-panel`.
- Layout hooks: `.wx-layout`, `.wx-layout-{preset}`, `.wx-column`, `.wx-row`.
- Cell hooks: `.wx-cell`, `.wx-cell-header`, `.wx-cell-body`.
- Panel hooks: `.wx-panel`, `.wx-panel-collapsed`, `.wx-panel-animating`, `.wx-panel-row`, `.wx-panel-column`, `.wx-panel-collapsed-bar`, `.wx-panel-toggle`, `.wx-panel-icon`, `.wx-panel-label`.
- Resizer hooks: `.wx-resizer` is inserted between direct cells; `.wx-resize-overlay` is a temporary fixed overlay during drag.
- global `.wx-scroll` sets `overflow:auto` on the component root.
- global `.wx-border` adds border
- Built-in variables: `--wx-layout-gap-color`, `--wx-layout-line-color`, `--wx-layout-resizer-hover`, `--wx-layout-resizer-active`, `--wx-panel-collapsed-size`.

```svelte
<Layout direction="row" preset="line" css="app-layout">
	<Cell label="Files" width={220} css="app-pane">Files</Cell>
	<Cell label="Editor">Editor</Cell>
</Layout>

<style>
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

```svelte
<script>
	import { Layout, Cell } from "@svar-ui/svelte-layout";
</script>

<div class="workspace">
	<Layout direction="row" preset="line">
		<Cell label="Sidebar" width={240} minWidth={160}>
			<nav>Navigation</nav>
		</Cell>
		<Cell label="Main" grow={3}>
			<main>Content</main>
		</Cell>
	</Layout>
</div>

<style>
	.workspace {
		width: 100%;
		height: 100vh;
	}
</style>
```

##### Resizable IDE Layout

```svelte
<script>
	import { Layout, Cell, Panel } from "@svar-ui/svelte-layout";

	let sidebarWidth = $state(220);
</script>

<Layout
	direction="row"
	padding={6}
	resizable
	oncellresize={sizes => (sidebarWidth = sizes[0])}
>
	<Panel label="Files" width={sidebarWidth} minWidth={120}>
		<div>File tree</div>
	</Panel>

	<Cell>
		<Layout preset="line">
			<Cell grow={3}>
				{#snippet header()}<span>Editor</span>{/snippet}
				<div>Editor area</div>
			</Cell>
			<Panel grow={1} label="Terminal">
				<div>Terminal</div>
			</Panel>
		</Layout>
	</Cell>
</Layout>
```

##### Controlled Panel Collapse

```svelte
<script>
	import { Layout, Cell, Panel } from "@svar-ui/svelte-layout";

	let collapsed = $state(false);
</script>

<Layout direction="row" preset="line">
	<Panel
		label="Sidebar"
		width={220}
		minWidth={140}
		{collapsed}
		oncollapse={value => (collapsed = value)}
	>
		<div>Sidebar content</div>
	</Panel>
	<Cell>
		<div>Main content</div>
	</Cell>
</Layout>
```

##### Custom Header Snippet

```svelte
<script>
	import { Layout, Cell } from "@svar-ui/svelte-layout";
</script>

<Layout>
	<Cell height={48}>
		{#snippet header()}
			<div class="bar">
				<span>Toolbar</span>
				<button>Save</button>
			</div>
		{/snippet}
		<div>Body</div>
	</Cell>
	<Cell scroll>
		<div>Long content</div>
	</Cell>
</Layout>
```

##### Presets And Explicit Spacing

```svelte
<script>
	import { Layout, Cell } from "@svar-ui/svelte-layout";
</script>

<Layout direction="row" preset="space" gap={12} padding={16}>
	<Cell css="wx-border">Left</Cell>
	<Cell css="wx-border">Right</Cell>
</Layout>
```

#### Implementation Notes

- `Cell` renders `.wx-cell-header` and `.wx-cell-body` only when `header` or `label` is provided.
- `Panel` detects row vs column from the parent DOM class `.wx-row`; outside a `Layout`, it behaves as column-oriented.
- Resizable layouts query only `:scope > .wx-cell`, so wrapping a `Cell` or `Panel` in another element prevents it from being resized.
- Drag resizing mutates inline styles on the adjacent cells during the pointer drag. Originally flexible cells are restored after pointer up; originally fixed cells keep their dragged pixel size.


## File: grid/index.md

> Source: `grid/index.md`

Use when building, configuring, styling, or modifying SVAR Svelte Grid / @svar-ui/svelte-grid data tables, toolbars, context menus, themes, inline editors, filters, sorting, selection, tree data, responsive layouts, export, or print behavior.

#### Package

```js
import {
	Grid,
	HeaderMenu,
	Tooltip,
	ContextMenu,
	Toolbar,
	Willow,
	WillowDark,
	registerInlineEditor,
	getEditorConfig,
	defaultMenuOptions,
	defaultToolbarButtons,
} from "@svar-ui/svelte-grid";
```

#### Supported functionality

##### Grid Data And Columns

- `data` is an array of row objects; stable `row.id` is expected.
- Missing row ids are mutated into `temp://...` ids by the store.
- In tree mode, rows use nested `row.data`; the store mutates rows with `$level`, `$parent`, and `$count`.
- `columns` configure `id`, `header`, `footer`, `width`, `flexgrow`, `hidden`, `resize`, `sort`, `template`, `cell`, `editor`, `options`, `getter`, `setter`, `treetoggle`, and `draggable`.
- Cell values are read with `column.getter(row)` or `row[column.id]`.
- Cell updates write with `column.setter(row, value)` or assign `row[column.id] = value`.
- `column.options` use `{ id, label }`; display text comes from `optionsMap` unless `template` is supplied.
- `autoConfig={true}` creates columns from first data row keys except `id` and keys starting with `$` only when `columns` is empty.
- `autoConfig={object}` merges that object into every generated column only when `columns` is empty.
- Default sizes from source: `rowHeight: 37`, `columnWidth: 160`, `headerHeight: 36`, `footerHeight: 36`.

##### Header, Footer, And Layout

- `header` defaults to `true`; `footer` defaults to `false`.
- `column.header` and `column.footer` can be a string, an object, or an array of strings/objects.
- Header/footer object fields include `text`, `cell`, `css`, `rowspan`, `colspan`, `collapsible`, `collapsed`, `vertical`, and header-only `filter`.
- `column.width` produces fixed pixel width; `column.flexgrow` produces flexible width.
- `split={{ left }}` fixes the first visible columns on the left.
- Source supports `split={{ right }}` for fixed right columns; the `Grid` prop type inherits `IConfig`, which only types `split.left`.
- The grid root is `height: 100%`; the parent must provide a height for useful vertical scrolling.
- Virtual rendering is built in for rows and columns.

##### Selection

- `select` defaults to `true`; `select={false}` disables row click selection.
- `multiselect` enables Ctrl/Cmd toggle and Shift range selection.
- `selectedRows` is an initial/sync prop passed into the store; read live selection with `api.getState().selectedRows`, `api.getReactiveState().selectedRows`, or `onselectrow`.
- Custom checkbox cells should call `api.exec("select-row", { id: row.id, toggle: true, mode: value })` and wrap the control in `data-action="ignore-click"` when row click selection should not fire.

##### Events And API

- Use `bind:this={api}` or `init={api => ...}` to access the grid API.
- API methods: `exec`, `on`, `intercept`, `detach`, `getState`, `getReactiveState`, `setNext`, `getStores`, `getRow`, `getColumn`.
- Action names are exposed as prop callbacks by removing hyphens and prefixing `on`: `select-row` -> `onselectrow`, `request-data` -> `onrequestdata`.
- Prop event callbacks receive the same payload passed to `api.exec`.
- `api.intercept(action, fn)` can return `false` to block an action before the normal handling path.
- `api.on(action, fn)` observes actions.
- Common actions: `add-row`, `delete-row`, `update-row`, `update-cell`, `select-row`, `resize-column`, `hide-column`, `sort-rows`, `filter-rows`, `search-rows`, `open-editor`, `close-editor`, `collapse-column`, `move-item`, `copy-row`, `open-row`, `close-row`, `export-data`, `scroll`, `print`, `undo`, `redo`, `request-data`.

##### Sorting And Filtering

- `column.sort: true` enables header click sorting.
- `column.sort: (a, b) => 1 | -1 | 0` supplies custom sort logic.
- Ctrl/Cmd-click on sortable headers adds multi-sort marks.
- `sortMarks` shape is `{ [columnId]: { order: "asc" | "desc", index?: number } }`.
- Header filters are configured as `header: { filter: "text" }` or `header: { filter: { type, config } }`.
- Built-in filter types: `text`, `richselect`, `datepicker`.
- `filter.config` is forwarded to the underlying Svelte Core control.
- `richselect` filter options come from `filter.config.options`, then `column.options`, then unique values in grid data.
- `api.exec("filter-rows", {})` clears all filters.
- `api.exec("filter-rows", { key, value })` updates `filterValues[key]` and applies the generated column filters.
- `api.exec("filter-rows", { filter })` applies a custom row predicate.

##### Inline Editors

- Double-clicking a cell runs `open-editor` for the row and column.
- Built-in editor names: `text`, `combo`, `datepicker`, `richselect`, `multiselect`.
- `column.editor` can be a string, `{ type, config }`, or `(row, column) => editor | null`.
- Returning `null` from an editor handler makes that cell non-editable.
- `combo`, `richselect`, and `multiselect` use `column.options` with `{ id, label }`.
- `multiselect` expects the cell value to be an array of option ids.
- Editor `config.template` renders option/value text; `config.cell` renders custom option/value components; `config.dropdown` is passed to dropdown-based editors.
- `datepicker` supports `config.buttons` with `["clear" | "today"]`.
- `registerInlineEditor(type, Component)` registers a custom editor component.

##### Custom Components

- `column.cell` receives `{ api, row, column, onaction }`.
- Header/footer `cell` receives `{ api, cell, column, row, onaction }`.
- Calling `onaction({ action, data })` inside a custom cell executes `api.exec(action, data)`.
- Custom action names are routed to prop callbacks, for example `onaction({ action: "custom-check", data })` -> `oncustomcheck={...}`.
- `overlay` can be text or a component; overlay components receive `onaction`.
- `Tooltip` can use default cell text, `column.tooltip(row)`, or `content={Component}`; tooltip content receives `{ data }`.

##### Toolbar And Menus

- `Toolbar` wraps `@svar-ui/svelte-toolbar` and defaults to `defaultToolbarButtons`.
- `Toolbar` auto-runs `handleAction(api, item.id)` before calling its own `onclick`.
- Default toolbar actions: `add-row`, `open-editor`, `delete-row`, `copy-row`, `cut-row`, `paste-row`, `move-item:up`, `move-item:down`, `undo`, `redo`.
- `Toolbar` filters move actions when `reorder` is off and undo/redo when `undo` is off.
- `ContextMenu` wraps `@svar-ui/svelte-menu` and defaults to `defaultMenuOptions`.
- `ContextMenu` defaults `at="point"` and uses row `data-context-id` through the base menu's default `dataKey`.
- The default resolver selects the right-clicked row if it is not already selected.
- `ContextMenu` auto-runs `handleAction(api, ev.action.id)` before calling its own `onclick`; base menu events also expose `ev.option`.
- Default context menu actions: `add-row:before`, `add-row:after`, `copy-row`, `cut-row`, `paste-row`, `move-item:up`, `move-item:down`, `delete-row`.
- `HeaderMenu` wraps grid content and opens on header right-click using `data-header-id`; clicking an item runs `hide-column`.
- `HeaderMenu columns={{ id: true }}` limits which columns appear in the hide/show menu.

##### Saving

- `RestDataProvider` from `@svar-ui/grid-data-provider` persists data changes to a REST backend.
- Wire it once with `api.setNext(provider)` in `init`; the provider then forwards every data action (`add-row`, `update-row`, `update-cell`, `delete-row`, `move-item`, `copy-row`, `sort-rows`, etc.) emitted on the event bus as the matching REST call. No per-action save handlers needed.
- Initial load uses `provider.getData()`; the optional second constructor arg is a per-row coercion callback (e.g. cast string fields to numbers).

```js
import { RestDataProvider } from "@svar-ui/grid-data-provider";

const provider = new RestDataProvider("/api/films");

function init(api) {
	api.setNext(provider); // forwards all row mutations to REST
}
```

##### Themes

- Theme components: `Willow`, `WillowDark`.
- Each theme accepts `fonts?: boolean` and optional children.
- Theme wrappers delegate to `@svar-ui/svelte-core` and add grid CSS variables to `.wx-material-theme`, `.wx-willow-theme`, or `.wx-willow-dark-theme`.
- If no `wx-theme` context exists, the store calls `suggestSkin()` and defaults to Willow.

#### Public Types

```ts
import type { Component, ComponentProps } from "svelte";
import { ContextMenu as BaseContextMenu } from "@svar-ui/svelte-menu";
import { Toolbar as BaseToolbar } from "@svar-ui/svelte-toolbar";

import type {
	IColumn,
	IRow,
	IApi,
	ISizeConfig,
	TMethodsConfig,
	IConfig,
	TEditorType,
	TEditorConfig,
	IColumnEditor,
	IHeaderCell,
} from "@svar-ui/grid-store";

export * from "@svar-ui/grid-store";

export interface IColumnEditorConfig extends IColumnEditor {
	config?: IColumnEditor["config"] & {
		cell?: Component<{
			data: any;
			onaction: (ev: {
				action?: any;
				data?: { [key: string]: any };
			}) => void;
		}>;
	};
}

export type TEditorHandlerConfig = (
	row?: IRow,
	column?: IColumn
) => TEditorType | IColumnEditorConfig | null;

export interface ICellProps {
	api: IApi;
	row: IRow;
	column: IColumn;
	onaction: (ev: { action?: any; data?: { [key: string]: any } }) => void;
}

export interface IHeaderCellConfig extends IHeaderCell {
	cell?: Component<
		ICellProps & {
			cell: Omit<IHeaderCell, "cell">;
		}
	>;
}

export type TColumnHeaderConfig =
	| string
	| IHeaderCellConfig
	| (string | IHeaderCellConfig)[];

export interface IColumnConfig
	extends Omit<
		IColumn,
		"left" | "right" | "fixed" | "optionsMap" | "header" | "footer"
	> {
	cell?: Component<ICellProps>;
	editor?: TEditorType | IColumnEditorConfig | TEditorHandlerConfig;
	header?: TColumnHeaderConfig;
	footer?: TColumnHeaderConfig;
}

export declare const Grid: Component<
	{
		rowStyle?: (row: any) => string;
		columnStyle?: (column: IColumn) => string;
		cellStyle?: (row: any, column: IColumn) => string;
		multiselect?: boolean;
		autoConfig?: boolean | IColumnConfig;
		header?: boolean;
		footer?: boolean;
		reorder?: boolean;
		autoRowHeight?: boolean;
		responsive?: {
			[key: string]: {
				sizes?: ISizeConfig;
				columns?: IColumnConfig[];
			};
		};
		init?: (api: IApi) => void;

		overlay?: string | Component;
		columns: IColumnConfig[];
		hotkeys?:
			| false
			| { [key: string]: ((e?: KeyboardEvent) => void) | boolean };
	} & IConfig &
		GridActions<TMethodsConfig>
>;

export declare const HeaderMenu: Component<{
	columns?: { [key: string]: boolean };
	api?: IApi;
	children?: () => any;
}>;

export declare const ContextMenu: Component<
	ComponentProps<typeof BaseContextMenu> & {
		api?: IApi;
	}
>;

export declare const Toolbar: Component<
	ComponentProps<typeof BaseToolbar> & {
		api?: IApi;
	}
>;

export declare const Tooltip: Component<{
	content?: Component;
	api?: IApi;
	children?: () => any;
}>;

export declare const Willow: Component<{
	fonts?: boolean;
	children?: () => any;
}>;

export declare const WillowDark: Component<{
	fonts?: boolean;
	children?: () => any;
}>;

export declare function registerInlineEditor(
	type: string,
	component: Component<{
		editor: TEditorConfig;
		onsave?: (ignoreFocus: boolean) => void;
		oncancel?: () => void;
		onapply?: (value: any) => void;
		onaction?: (ev: {
			action: string;
			data?: { [key: string]: any };
		}) => void;
	}>
): void;

/* get component events from store actions*/
type RemoveHyphen<S extends string> = S extends `${infer Head}-${infer Tail}`
	? `${Head}${RemoveHyphen<Tail>}`
	: S;

type EventName<K extends string> = `on${RemoveHyphen<K>}`;

export type GridActions<TMethodsConfig extends Record<string, any>> = {
	[K in keyof TMethodsConfig as EventName<K & string>]?: (
		ev: TMethodsConfig[K]
	) => void;
} & {
	[key: `on${string}`]: (ev?: any) => void;
};
```

Common public action payloads from `@svar-ui/grid-store`:

```ts
export type IDataMethodsConfig = CombineTypes<
	{
		["update-cell"]: {
			id: TID;
			column: TID;
			value: string | number | Date;
			eventSource?: string;
		};
		["add-row"]: {
			id?: TID;
			before?: TID;
			after?: TID;
			row: IRow;
			select?: boolean;
			eventSource?: string;
		};
		["delete-row"]: { id: TID; eventSource?: string };
		["update-row"]: {
			id: TID;
			row: Record<string, any>;
			eventSource?: string;
		};
		["select-row"]: {
			id: TID;
			toggle?: boolean;
			range?: boolean;
			mode?: boolean;
			show?: boolean;
			column?: TID;
		};
		["resize-column"]: {
			id: TID;
			width?: number;
			auto?: boolean | "data" | "header";
			maxRows?: number;
			inProgress?: boolean;
			eventSource?: string;
		};
		["hide-column"]: {
			id: TID;
			mode?: boolean;
			eventSource?: string;
		} & ISkipUndoAction;
		["sort-rows"]: {
			key: TID;
			order?: "asc" | "desc";
			add?: boolean | number;
			sort?: (a: IRow, b: IRow) => 1 | -1 | 0;
		};
		["search-rows"]: {
			search: string;
			columns?: Partial<Record<TID, boolean>>;
		};
		["open-editor"]: {
			id: TID;
			column?: TID;
		};
		["close-editor"]: {
			ignore?: boolean;
		};
		["editor"]: {
			value: any;
		};
		["filter-rows"]: {
			filter?: any;
			key?: TID;
			value?: any;
		};
		["collapse-column"]: {
			id: TID;
			row?: number;
			mode?: boolean;
			eventSource?: string;
		};
		["move-item"]: {
			id: TID;
			target?: TID;
			mode?: "before" | "after" | "up" | "down";
			inProgress?: boolean;
			eventSource?: string;
		};
		["copy-row"]: {
			id: TID;
			target?: TID;
			mode?: "before" | "after";
			eventSource?: string;
		};
		["open-row"]: {
			id: TID;
			nested?: boolean;
			eventSource?: string;
		};
		["close-row"]: {
			id: TID;
			nested?: boolean;
			eventSource?: string;
		};
		["export-data"]: IExportOptions;
		["scroll"]: {
			row?: TID;
			column?: TID;
		};
		["hotkey"]: {
			key: string;
			event: any;
			isInput?: boolean;
		};
		["focus-cell"]: {
			row?: TID;
			column?: TID;
			eventSource?: string;
		};
		["print"]: IPrintConfig;
		["undo"]: void;
		["redo"]: void;
		["request-data"]: {
			row: {
				start: number;
				end: number;
			};
		};
	},
	{
		[key: string]: any;
	}
>;
```

#### Styling

- `Grid` has no `css`, `class`, or `style` passthrough prop.
- Style through wrapper elements, `rowStyle`, `columnStyle`, `cellStyle`, header/footer cell `css`, and theme CSS variables.
- `rowStyle(row)` appends a class to `.wx-row`.
- `columnStyle(column)` appends a class to body, header, footer, and print cells.
- `cellStyle(row, column)` appends a class to body and print cells only.
- Header/footer cell `css` appends to the header/footer `.wx-cell`.
- `IColumn.css` exists in store types and is used in auto-width measurement helpers, but it is not appended to rendered body cells by `Cell.svelte`.

Stable class hooks visible in source:

- root and containers: `.wx-grid`, `.wx-responsive-{level}`, `.wx-table-box`, `.wx-scroll`, `.wx-header-wrapper`, `.wx-header`, `.wx-footer`, `.wx-h-row`, `.wx-f-row`, `.wx-body`, `.wx-data`, `.wx-row`
- cells: `.wx-cell`, `.wx-selected`, `.wx-inactive`, `.wx-autoheight`, `.wx-fixed`, `.wx-fixed-right`, `.wx-shadow`, `.wx-rowspan`, `.wx-colspan`, `.wx-vertical`, `.wx-collapsed`, `.wx-filter`
- header controls: `.wx-grip`, `.wx-sort`, `.wx-order`, `.wx-collapse`
- body controls: `.wx-draggable`, `.wx-draggable-stub`, `.wx-table-tree-toggle`, `.wx-search`
- wrappers: `.wx-overlay`, `.tooltip`, `.wx-table-menu`
- print: `.wx-print-container`, `.wx-print-grid`, `.wx-print-grid-wrapper`, `.wx-print-cell`, `.wx-print-cell-header`, `.wx-print-cell-footer`, `.wx-print-cell-filter`, `.wx-print-filter`, `.wx-print-draggable`, `.wx-print-grid-tree-toggle`

Layout defaults from source:

- `.wx-grid` height is `100%`.
- `.wx-table-box` is `display: flex`, `flex-direction: column`, `height: 100%`, `position: relative`, `overflow: hidden`, with `border: var(--wx-table-cell-border)`.
- `.wx-scroll` is `position: relative`, `flex: 1`, and owns scrollbars.
- `.wx-row` is `display: flex` and gets row height from `sizes.rowHeight` or `row.rowHeight`.
- `.wx-cell` default body padding is `8px`, with overflow hidden and nowrap text.
- Header/footer `.wx-cell` default padding is `8px`; filter header cells use `4px`.
- Column widths are inline styles from `width`, `min-width`, `flex-grow`, and sticky left/right offsets.

Grid CSS variables set by theme components:

```css
--wx-table-select-background
--wx-table-select-color
--wx-table-border
--wx-table-select-border
--wx-table-header-border
--wx-table-header-cell-border
--wx-table-footer-cell-border
--wx-table-cell-border
--wx-header-font-weight
--wx-table-header-background
--wx-table-fixed-column-border
--wx-table-editor-dropdown-border
--wx-table-editor-dropdown-shadow
--wx-table-drag-over-background
--wx-table-drag-zone-shadow
```

Scoped styling pattern:

```svelte
<div class="orders-grid">
	<Grid {data} {columns} rowStyle={row => (row.priority ? "is-priority" : "")} />
</div>

<style>
	.orders-grid {
		height: 420px;
	}

	.orders-grid .wx-row.is-priority:not(.wx-selected) .wx-cell {
		background: #fff7d6;
	}

	.orders-grid .wx-header .wx-cell {
		padding: 6px 8px;
	}
</style>
```

#### Recipes

##### Basic Grid

```svelte
<script>
	import { Grid } from "@svar-ui/svelte-grid";

	const data = [
		{ id: 1, name: "Alex Brown", year: 1974 },
		{ id: 2, name: "Maria Ford", year: 1988 },
	];

	const columns = [
		{ id: "name", header: "Name", flexgrow: 1, sort: true },
		{ id: "year", header: "Year", width: 100, sort: true },
	];
</script>

<div style="height: 360px;">
	<Grid {data} {columns} />
</div>
```

##### API, Events, And Selection

```svelte
<script>
	import { Grid } from "@svar-ui/svelte-grid";

	let api = $state();
	let selected = $state([]);

	const data = [
		{ id: 1, city: "London" },
		{ id: 2, city: "Paris" },
	];
	const columns = [{ id: "city", header: "City", flexgrow: 1 }];

	function init(grid) {
		grid.intercept("select-row", ev => {
			if (ev.id === 1) return false;
		});
	}

	function addRow() {
		api.exec("add-row", { row: { city: "New city" } });
	}

	function updateSelected() {
		selected = api.getState().selectedRows;
	}
</script>

<button onclick={addRow}>Add</button>
<Grid
	{data}
	{columns}
	{init}
	bind:this={api}
	multiselect
	onselectrow={updateSelected}
/>
```

##### Sort, Header Filters, And Inline Editors

```svelte
<script>
	import { Grid } from "@svar-ui/svelte-grid";

	const countries = [
		{ id: "pl", label: "Poland" },
		{ id: "us", label: "United States" },
	];

	const data = [
		{ id: 1, name: "Alex", country: "pl", joined: new Date() },
		{ id: 2, name: "Sam", country: "us", joined: new Date() },
	];

	const columns = [
		{
			id: "name",
			header: [{ text: "Name" }, { filter: "text" }],
			editor: "text",
			sort: true,
			flexgrow: 1,
		},
		{
			id: "country",
			header: {
				filter: { type: "richselect", config: { options: countries } },
			},
			editor: "richselect",
			options: countries,
			width: 180,
		},
		{
			id: "joined",
			header: { text: "Joined" },
			editor: { type: "datepicker", config: { buttons: ["today", "clear"] } },
			template: value => (value ? value.toLocaleDateString() : ""),
			width: 140,
		},
	];
</script>

<Grid {data} {columns} />
```

##### Custom Body, Header, And Footer Cells

```svelte
<!-- CheckCell.svelte -->
<script>
	import { Checkbox } from "@svar-ui/svelte-core";

	let { api, row, column, onaction } = $props();

	function change({ value }) {
		api.exec("update-cell", { id: row.id, column: column.id, value });
		onaction({
			action: "checked-change",
			data: { row: row.id, column: column.id, value },
		});
	}
</script>

<div data-action="ignore-click">
	<Checkbox value={row[column.id]} onchange={change} />
</div>
```

```svelte
<script>
	import { Grid } from "@svar-ui/svelte-grid";
	import CheckCell from "./CheckCell.svelte";
	import HeaderTitle from "./HeaderTitle.svelte";

	const data = [{ id: 1, checked: true, name: "Alex" }];
	const columns = [
		{
			id: "checked",
			width: 44,
			cell: CheckCell,
			header: { cell: HeaderTitle, text: "Active" },
			footer: { text: "Active", css: "center" },
		},
		{ id: "name", header: "Name", flexgrow: 1 },
	];
</script>

<Grid
	{data}
	{columns}
	footer
	oncheckedchange={ev => console.log(ev.row, ev.value)}
/>
```

##### Custom Inline Editor

```svelte
<!-- ColorEditor.svelte -->
<script>
	import { ColorBoard, Dropdown } from "@svar-ui/svelte-core";
	import { clickOutside } from "@svar-ui/lib-dom";

	let { editor, onsave, onapply, oncancel } = $props();
	let value = $state(editor.value);

	function change({ value, input }) {
		if (input) onapply(value);
		else onsave();
	}
</script>

<button onclick={oncancel}>{value}</button>
<Dropdown width="auto" trackScroll {oncancel}>
	<div use:clickOutside={() => onsave(true)}>
		<ColorBoard {value} onchange={change} button />
	</div>
</Dropdown>
```

```svelte
<script>
	import { Grid, registerInlineEditor } from "@svar-ui/svelte-grid";
	import ColorEditor from "./ColorEditor.svelte";

	registerInlineEditor("color", ColorEditor);

	const data = [{ id: 1, color: "#35D6A7" }];
	const columns = [
		{ id: "color", header: "Color", editor: "color", width: 180 },
	];
</script>

<Grid {data} {columns} />
```

##### Toolbar, Context Menu, And Header Menu

```svelte
<script>
	import { Grid, Toolbar, ContextMenu, HeaderMenu } from "@svar-ui/svelte-grid";

	let api = $state();
	const data = [
		{ id: 1, name: "Alex" },
		{ id: 2, name: "Sam" },
	];
	const columns = [
		{ id: "name", header: "Name", editor: "text", flexgrow: 1 },
	];
</script>

<Toolbar {api} />
<ContextMenu {api}>
	<HeaderMenu {api}>
		<Grid {data} {columns} bind:this={api} multiselect reorder undo />
	</HeaderMenu>
</ContextMenu>
```

##### Dynamic Data Loading

```svelte
<script>
	import { Grid } from "@svar-ui/svelte-grid";

	const raw = Array.from({ length: 10000 }, (_, id) => ({
		id,
		name: `Row ${id}`,
	}));

	const columns = [{ id: "name", header: "Name", flexgrow: 1 }];
	let data = $state([]);

	function provideData({ row }) {
		data = raw.slice(row.start, row.end);
	}
</script>

<div style="height: 500px;">
	<Grid
		{data}
		{columns}
		dynamic={{ rowCount: raw.length }}
		onrequestdata={provideData}
	/>
</div>
```

##### Responsive Columns And Fixed Columns

```svelte
<script>
	import { Grid } from "@svar-ui/svelte-grid";

	const data = [{ id: 1, name: "Alex", email: "alex@example.com" }];
	const columns = [
		{ id: "id", width: 50 },
		{ id: "name", header: "Name", flexgrow: 1 },
		{ id: "email", header: "Email", flexgrow: 1 },
	];

	const responsive = {
		600: {
			columns: [
				{ id: "id", width: 50 },
				{ id: "name", header: "Name", flexgrow: 1 },
				{ id: "email", header: "Email", hidden: true },
			],
			sizes: { rowHeight: 44, columnWidth: 140 },
		},
	};
</script>

<div class="grid-shell">
	<Grid {data} {columns} {responsive} split={{ left: 1 }} />
</div>

<style>
	.grid-shell {
		height: 420px;
	}

	.grid-shell .wx-grid.wx-responsive-600 .wx-cell {
		padding-top: 10px;
		padding-bottom: 10px;
	}
</style>
```

##### Tree Grid

```svelte
<script>
	import { Grid } from "@svar-ui/svelte-grid";

	let api = $state();
	const data = [
		{
			id: 1,
			name: "Project",
			open: true,
			data: [{ id: 2, name: "Task" }],
		},
	];

	const columns = [
		{ id: "name", header: "Name", treetoggle: true, flexgrow: 1 },
	];
</script>

<button onclick={() => api.exec("open-row", { id: 1, nested: true })}>
	Open
</button>
<button onclick={() => api.exec("close-row", { id: 1, nested: true })}>
	Close
</button>

<Grid {data} {columns} bind:this={api} tree />
```

##### External Editor From Grid Columns

```svelte
<script>
	import { Grid, getEditorConfig } from "@svar-ui/svelte-grid";
	import { Editor } from "@svar-ui/svelte-editor";

	let api = $state();
	let editing = $state(null);

	const data = [{ id: 1, name: "Alex" }];
	const columns = [
		{ id: "name", header: "Name", editor: "text", flexgrow: 1 },
	];

	function init(grid) {
		grid.intercept("open-editor", ({ id }) => {
			editing = grid.getRow(id);
			return false;
		});
	}
</script>

<Grid {data} {columns} {init} bind:this={api} />

{#if editing}
	<Editor
		values={editing}
		items={getEditorConfig(columns)}
		onsave={({ values }) =>
			api.exec("update-row", { id: editing.id, row: values })}
	/>
{/if}
```

#### Implementation Notes

- `Grid` reinitializes the store reactively from props; changing `data`, `columns`, `sizes`, `selectedRows`, `sortMarks`, `filterValues`, `split`, `tree`, `undo`, or `reorder` can reset or recalculate store state.
- When `data` identity changes, the store clears `_filterIds`, `filterValues`, `sortMarks`, and `search`, and resets history.
- Header/footer configs are copied and normalized internally, but source `columns` are mutated for `optionsMap`; row objects can also be mutated for generated ids and tree metadata.
- `column.tooltip` is used by `Tooltip.svelte` but is not present in `IColumn` types.
- `HeaderMenu` uses menu item `type: "table-header"`


## File: editor/index.md

> Source: `editor/index.md`

Use when building, configuring, styling, or modifying SVAR Svelte Editor / @svar-ui/svelte-editor forms, field items, validation, save flows, panels, toolbars, sections, batches, or custom editor item renderers.

#### Package

```js
import {
	Editor,
	registerEditorItem,
	Willow,
	WillowDark,
} from "@svar-ui/svelte-editor";
```

#### Supported functionality

##### Components

- `Editor` - main editor shell with inline, sidebar, or modal placement, optional top/bottom toolbars, sections, columns layout, validation, hotkeys, and save flow.
- `registerEditorItem(type, handler)` - registers a Svelte component for `item.comp`.
- `Willow`, `WillowDark` - wrappers around matching `@svar-ui/svelte-core` themes

##### Built-in item components

- `text` - registered to `Text` from `@svar-ui/svelte-core`; default when `comp` is omitted.
- `textarea` - registered to `TextArea` from `@svar-ui/svelte-core`.
- `checkbox` - registered to `Checkbox` from `@svar-ui/svelte-core`.
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

- `item.comp` can be a registered string or a Svelte component directly, use `registerEditorItem` to link component to string
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
- `topBar` and `bottomBar` accept `false`, `true`, or `{ items: IToolbarItem[] }`; toolbar items are passed to `@svar-ui/svelte-toolbar`.
- Automatic default bars are generated only when `topBar === true && bottomBar === true`.
- Automatic manual-save modal uses bottom `{ spacer, save, cancel }`; modal columns use top `{ spacer, save, cancel }`; inline/sidebar manual save uses top `{ spacer, cancel, save }`; auto-save and read-only use top `{ spacer, close }`.
- Toolbar `onchange({ item, value })` is mapped into editor field changes as `{ key: item.key, value }`, so toolbar controls can edit `values`.
- Default hotkeys are enabled unless `hotkeys={false}`: `ctrl+s` triggers save, `escape` triggers cancel/close, and `delete` triggers a `delete` toolbar item when present.
- Custom `hotkeys` are merged with defaults.
- `focus={true}` selects and focuses the first enabled input, textarea, or select after mount.
- Editor `children` render above generated fields inside the content area; demos use this for tabs, segmented controls, and external toolbars.

#### Public Types

```ts
import type { Component } from "svelte";
import type { IToolbarItem } from "@svar-ui/svelte-toolbar";

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

- `Editor` `css` is appended to the root panel: `.wx-inline-form {css}` for inline placement, `.wx-panel {css}` for modal/sidebar placement.
- Root panel classes: `.wx-inline-form`, `.wx-panel`.
- Content container: `.wx-content`; columns mode adds `.wx-layout-columns`.
- Form body: `.wx-sections` with `--wx-field-width: 600px`.
- Columns layout: `.wx-cols`, `.wx-left`, `.wx-right`; source defaults include `.wx-left { min-width: 640px }`, `.wx-right { width: 364px; background: var(--wx-background-alt) }`.
- Toolbar wrapper: `.wx-editor-toolbar`, `.wx-topbar`, `.wx-bottom`
- Section header: `.wx-section`, `.wx-section-active`, nested `.wx-icon`
- Validation and empty states: `.wx-message`, `.wx-overlay`

```svelte
<Editor {items} {values} layout="columns" css="task-editor" />

<style>
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

```svelte
<script>
	import { Editor } from "@svar-ui/svelte-editor";

	const items = [
		{ comp: "text", key: "name", label: "Name" },
		{ comp: "checkbox", key: "admin", label: "Is Admin" },
		{ comp: "textarea", key: "descr", label: "Description" },
	];

	let values = $state({
		name: "John Doe",
		admin: true,
		descr: "Notes",
	});
</script>

<Editor {items} {values} topBar={false} />
```

##### Manual Save With Validation

```svelte
<script>
	import { Editor } from "@svar-ui/svelte-editor";

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

	let values = $state({ firstName: "John", email: "john@example.org" });
	let visible = $state(true);

	function handleAction({ item, changes }) {
		if (item.id === "save" && changes.length) return;
		visible = false;
	}

	function handleSave({ values: next }) {
		values = next;
		visible = false;
	}
</script>

{#if visible}
	<Editor
		placement="sidebar"
		autoSave={false}
		{items}
		{values}
		onaction={handleAction}
		onsave={handleSave}
	/>
{/if}
```

##### Auto Save Sidebar With Custom Toolbar

```svelte
<script>
	import { Editor } from "@svar-ui/svelte-editor";

	const items = [
		{ comp: "text", key: "label", label: "Label" },
		{ comp: "textarea", key: "description", label: "Description" },
	];

	let values = $state({ id: 1, label: "Task", description: "" });
	let open = $state(true);

	function handleAction({ item }) {
		if (item.id === "close" || item.id === "delete") open = false;
	}

	function handleSave({ values: next }) {
		values = next;
	}
</script>

{#if open}
	<Editor
		placement="sidebar"
		autoSave={true}
		topBar={{
			items: [
				{ comp: "icon", icon: "wxi-close", id: "close" },
				{ comp: "spacer" },
				{ comp: "button", type: "danger", text: "Delete", id: "delete" },
				{ comp: "button", type: "primary", text: "Save", id: "save" },
			],
		}}
		{items}
		{values}
		onaction={handleAction}
		onsave={handleSave}
	/>
{/if}
```

##### Update Multiple Values From One Change

```svelte
<script>
	import { Editor, registerEditorItem } from "@svar-ui/svelte-editor";
	import { Combo } from "@svar-ui/svelte-core";

	registerEditorItem("combo", Combo);

	let items = $state([
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

	let values = $state({ country: "", city: "" });

	function handleChange(ev) {
		if (ev.key !== "country") return;

		items[1] = {
			...items[1],
			disabled: false,
			options: cities[ev.value],
		};

		ev.update = {
			country: ev.value,
			city: "",
		};
	}
</script>

<Editor {items} {values} onchange={handleChange} topBar={false} />
```

##### Register A Custom Item

```svelte
<!-- PriorityCombo.svelte -->
<script>
	import { Combo } from "@svar-ui/svelte-core";

	let { value, options, onchange, ...restProps } = $props();
</script>

<Combo {value} {options} {onchange} {...restProps}>
	{#snippet children({ option })}
		<span class="priority-dot" style:background={option.color}></span>
		{option.label}
	{/snippet}
</Combo>
```

```svelte
<script>
	import { Editor, registerEditorItem } from "@svar-ui/svelte-editor";
	import PriorityCombo from "./PriorityCombo.svelte";

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

	let values = $state({ priority: 1 });
</script>

<Editor {items} {values} topBar={false} />
```

##### Sections And Accordion Panels

```svelte
<script>
	import { Editor } from "@svar-ui/svelte-editor";

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

	let values = $state({ name: "John", admin: false });
</script>

<Editor {items} {values} topBar={false} />
```

##### Batch Switcher In Children

```svelte
<script>
	import { Editor } from "@svar-ui/svelte-editor";
	import { Segmented } from "@svar-ui/svelte-core";

	const options = [
		{ id: "main", label: "Personal" },
		{ id: "cfg", label: "Settings" },
	];

	const items = [
		{ comp: "text", key: "name", label: "Name", batch: "main" },
		{ comp: "textarea", key: "descr", label: "Description", batch: "main" },
		{ comp: "checkbox", key: "admin", label: "Is Admin", batch: "cfg" },
	];

	let values = $state({ name: "John", descr: "", admin: false });
	let activeBatch = $state("main");
</script>

<Editor topBar={false} {items} {values} {activeBatch}>
	<Segmented {options} bind:value={activeBatch} />
</Editor>
```

##### Modal Columns Layout

```svelte
<script>
	import { Editor } from "@svar-ui/svelte-editor";

	const items = [
		{ comp: "text", key: "name", label: "Name", column: "left" },
		{ comp: "textarea", key: "descr", label: "Description", column: "left" },
		{ comp: "checkbox", key: "admin", label: "Is Admin" },
	];

	let values = $state({ name: "John", descr: "", admin: false });
	let visible = $state(true);
</script>

{#if visible}
	<Editor
		placement="modal"
		layout="columns"
		autoSave={false}
		{items}
		{values}
		onaction={() => (visible = false)}
	/>
{/if}
```

#### Implementation Notes

- `onvalidation` can receive `errors: null`
- Dot-path keys assume intermediate objects already exist for default getter/setter access.
- `config` is promoted into top-level item props and also remains as `item.config`.
- `readonly={true}` converts every rendered item to the built-in `readonly` renderer.
- `Action` toolbar items with `id: "save"` are special; other IDs are forwarded through `onaction`
- `SideArea` cancel trigger `onaction` with `item.id === "close"`.


## File: filter/index.md

> Source: `filter/index.md`

Use when building, configuring, styling, or modifying SVAR Svelte Filter / @svar-ui/svelte-filter FilterBuilder, FilterEditor, FilterBar, or FilterQuery components

Package: `@svar-ui/svelte-filter`

Use this skill as an index. Load only the component reference needed for the task; each linked file is independent.

- `FilterBuilder.md` - visual query builder, nested filter groups, builder API/actions, builder styling.
- `FilterEditor.md` - standalone single-rule editor, field selector mode, option includes, editor styling.
- `FilterBar.md` - compact filter input row, `all` and `dynamic` field modes, bar styling.
- `FilterQuery.md` - query-string input, parse modes, autocomplete, natural text integrations, query styling.


## File: filter/FilterBar.md

> Source: `filter/FilterBar.md`

### FilterBar

Package: `@svar-ui/svelte-filter`

Use this file independently when building, configuring, styling, or modifying `FilterBar`.

#### Import

```js
import {
	FilterBar,
	Willow,
	WillowDark,
	createArrayFilter,
	createFilter,
	createFilterRule,
} from "@svar-ui/svelte-filter";
```

#### Supported Functionality

##### Data Contract

- `FilterBar` emits an `IFilterSet` through `onchange({ value })`.
- `IFilterSet`: `{ glue?: "and" | "or", rules?: (IFilter | IFilterSet)[] }`.
- string field shorthand becomes `{ id, type: "text", filter: "contains" }`.
- object fields produce one `IFilter` when the current value is truthy.
- `type: "all"` can emit an OR `IFilterSet` across multiple fields.
- empty fields are omitted from the emitted rules.
- when one rule is produced by `type: "all"` and it has `glue: "or"`, that OR set is returned directly.

##### Field Configurations

- simple field object: `{ id, type, filter?, options?, value?, label?, placeholder? }`.
- `type`: `"text"`, `"number"`, or `"date"` in source.
- `filter` defaults to `"equal"` when `options` exists, otherwise `"contains"`.
- non-date `options` render a `RichSelect`; string/number options become `{ id, label }`.
- `$empty` / `None` is prepended to select options and is converted back to `""`.
- `type: "all"` renders one text input and builds `contains` OR rules across every field in `by`.
- `type: "dynamic"` renders a field selector plus the selected field's input; switching fields clears the previous field value.
- `by` accepts strings or field config objects.

Common field configs:

```js
"last_name"
{ id: "age", type: "number", filter: "greater", placeholder: "Older than..." }
{ id: "country", type: "text", options: ["USA", "Germany"], value: "USA" }
{ id: "start", type: "date", filter: "between" }
{ type: "all", label: "Search", by: ["age", "first_name", "last_name"] }
{
	type: "dynamic",
	label: "Filter by",
	by: ["last_name", { id: "start", type: "date", filter: "greater" }],
}
```

##### Events And Timing

- `debounce` defaults to `300`.
- text and number input changes use `debounce`.
- select and date changes dispatch after `1ms`.
- `onchange({ value })` receives the current `IFilterSet`.
- initial `value` field configs populate controls but do not emit until a change happens.

#### Public Types

```ts
import type { Component } from "svelte";
import type {
	IFilterSet,
	IFilterBarField,
} from "@svar-ui/filter-store";

export declare const FilterBar: Component<{
	fields: (
		| string
		| IFilterBarField
		| {
				type: "all" | "dynamic";
				by: (string | IFilterBarField)[];
				label?: string;
				placeholder?: string;
		  }
	)[];
	debounce?: number;
	onchange?: (ev: { value: IFilterSet }) => void;
}>;
```

Relevant `@svar-ui/filter-store` public shapes:

```ts
export type AnyData = number | string | Date;
export type TGlue = "and" | "or";
export type TType = "number" | "text" | "date" | "tuple";
export type TFilterType =
	| "greater"
	| "less"
	| "greaterOrEqual"
	| "lessOrEqual"
	| "equal"
	| "notEqual"
	| "contains"
	| "notContains"
	| "beginsWith"
	| "notBeginsWith"
	| "endsWith"
	| "notEndsWith"
	| "between"
	| "notBetween";

export interface IFilterSet {
	rules?: (IFilter | IFilterSet)[];
	glue?: TGlue;
}

export interface IFilter {
	field: string | "*";
	type?: TType;
	predicate?: "month" | "year" | "yearMonth";
	filter?: TFilterType;
	includes?: AnyData[];
	value?: AnyData;
}

export interface IFilterBarField {
	type: string;
	id: string;
	filter?: TFilterType;
	options?: { id: string | number; label: string }[];
	value?: any;
	label?: string;
	placeholder?: string;
}
```

#### Styling

- no `css`, `class`, `className`, or `style` passthrough prop exists on `FilterBar`.
- use theme wrappers around the component: `<Willow>`, `<WillowDark>`.
- label variables consumed by source: `--wx-label-font-family`, `--wx-label-font-size`, `--wx-label-line-height`, `--wx-label-font-weight`, `--wx-label-font-color`.

Class hooks:

- root: `.wx-filter-bar`
- labels: `.wx-label`
- select wrappers: `.wx-select`
- text/number input wrappers: `.wx-text`
- date picker wrappers: `.wx-date`

Layout defaults:

- `.wx-filter-bar`: `display: flex`, `padding: 14px 2px`, `width: 610px`, `gap: 10px`.
- `.wx-label`: max width `160px`, no wrap, ellipsis overflow, centered with `align-content: center`.
- `.wx-select`: `flex: 1`.
- `.wx-text` and `.wx-date`: `flex: 2`.

```svelte
<div class="bar-scope">
	<Willow>
		<FilterBar fields={fields} onchange={handleChange} />
	</Willow>
</div>

<style>
	.bar-scope {
		--wx-label-font-size: 14px;
		--wx-label-font-weight: 600;
	}

	.bar-scope .wx-filter-bar {
		width: 100%;
		gap: 16px;
		padding: 10px 0;
	}
</style>
```

#### Recipes

##### Basic Text, Number, And Select Fields

```svelte
<script>
	import { FilterBar, createArrayFilter } from "@svar-ui/svelte-filter";

	let rows = $state(data);

	function apply({ value }) {
		rows = createArrayFilter(value)(data);
	}
</script>

<FilterBar
	fields={[
		"last_name",
		{ id: "age", type: "number", filter: "greater" },
		{
			id: "country",
			type: "text",
			options: ["USA", "Germany"],
			value: "USA",
		},
	]}
	onchange={apply}
/>
```

##### Date Fields And Ranges

```svelte
<FilterBar
	fields={[
		{
			id: "start",
			type: "date",
			filter: "greater",
			value: new Date("2025-01-01"),
		},
		{
			id: "end",
			type: "date",
			filter: "less",
			value: new Date("2025-05-01"),
		},
		{
			id: "created",
			type: "date",
			filter: "between",
		},
	]}
	onchange={({ value }) => applyFilter(value)}
/>
```

##### Search Across Many Fields

```svelte
<FilterBar
	fields={[
		{
			type: "all",
			label: "Search",
			placeholder: "Search people",
			by: ["age", "first_name", "last_name"],
		},
	]}
	onchange={({ value }) => applyFilter(value)}
/>
```

##### Dynamic Field Selector

```svelte
<FilterBar
	fields={[
		{
			type: "dynamic",
			label: "Filter by",
			placeholder: "Enter value",
			by: [
				{ id: "first_name", type: "text", filter: "contains" },
				"last_name",
				{ id: "age", type: "number", filter: "greater" },
				{
					id: "country",
					type: "text",
					options: ["USA", "Germany"],
					value: "USA",
				},
				{
					id: "start",
					type: "date",
					filter: "greater",
					value: new Date("2025-01-01"),
				},
			],
		},
	]}
	onchange={({ value }) => applyFilter(value)}
/>
```

##### Faster Text Updates

```svelte
<FilterBar
	debounce={100}
	fields={["first_name", "last_name"]}
	onchange={({ value }) => applyFilter(value)}
/>
```

#### Implementation Notes

- `FilterBar` stores one `lastField` for dynamic selectors; avoid multiple independent `type: "dynamic"` groups
- `normalizeField` only maps `options` for non-date fields.
- select options can be strings, numbers, or `{ id, label }` objects


## File: filter/FilterBuilder.md

> Source: `filter/FilterBuilder.md`

### FilterBuilder

Package: `@svar-ui/svelte-filter`

Use this file independently when building, configuring, styling, or modifying `FilterBuilder`.

#### Import

```js
import {
	FilterBuilder,
	Willow,
	WillowDark,
	createArrayFilter,
	createFilter,
	getOptionsMap,
} from "@svar-ui/svelte-filter";
```

#### Supported Functionality

##### Data Contract

- `fields`: array of `{ id, label, type, predicate?, format? }`.
- supported field `type`: `"text"`, `"number"`, `"date"`, `"tuple"`.
- `options`: `{ [fieldId]: AnyData[] }` or `(fieldId) => AnyData[] | Promise<AnyData[]>`.
- `value`: `IFilterSet`, default `{ glue: "and", rules: [] }`.
- `IFilterSet`: `{ glue?: "and" | "or", rules?: (IFilter | IFilterSet)[] }`.
- `IFilter`: `{ field, type?, predicate?, filter?, includes?, value? }`.
- `includes` matches exact option values; `filter + value` uses an operator.
- `between` and `notBetween` use `value: { start, end }`.
- date editor UI values should be `Date` objects or `{ start: Date, end: Date }`; convert date strings before passing visual editor values.

##### Built-In Filters

- text: `equal`, `notEqual`, `contains`, `notContains`, `beginsWith`, `notBeginsWith`, `endsWith`, `notEndsWith`
- number: text filters plus `greater`, `less`, `greaterOrEqual`, `lessOrEqual`, `between`, `notBetween`
- date: `equal`, `notEqual`, `greater`, `less`, `greaterOrEqual`, `lessOrEqual`, `between`, `notBetween`
- tuple: `greater`, `less`, `greaterOrEqual`, `lessOrEqual`, `equal`, `notEqual`

Common rule objects:

```js
{ field: "name", type: "text", filter: "contains", value: "Alex" }
{ field: "age", type: "number", filter: "greater", value: 30 }
{ field: "start", type: "date", filter: "between", value: { start, end } }
{ field: "country", includes: ["USA", "Germany"] }
{ glue: "or", rules: [/* filters or nested groups */] }
```

##### Props And Modes

- source props: `value = { glue: "and", rules: [] }`, `fields = []`, `options = null`, `type = "list"`, `init = null`, plus action callback props in `...restProps`.
- `type="list"`: vertical layout, nested groups, AND/OR glue, context menu, top Add filter button.
- `type="line"`: horizontal layout with scrollable rules, context menu, Add filter button at the right.
- `type="simple"`: horizontal flat layout; Add filter opens a dropdown of unused fields, no nested groups, no context menu, delete icon per rule.
- `onchange` receives `{ value: IFilterSet }` after store-changing actions.
- other action callback props use event names with hyphens removed: `onaddrule`, `onaddgroup`, `oneditrule`, `onupdaterule`, `ondeleterule`, `ontoggleglue`, `onchangerule`.
- `init(api)` runs once after initial store setup.
- `bind:this` exposes `exec`, `on`, `intercept`, `detach`, `setNext`, `getState`, `getReactiveState`, `getStores`, `getValue`.
- public actions: `add-rule`, `add-group`, `edit-rule`, `update-rule`, `delete-rule`, `toggle-glue`, `change-rule`, `change`.

#### Public Types

```ts
import type { Component } from "svelte";
import type {
	IApi,
	TMethodsConfig,
	IConfig,
} from "@svar-ui/filter-store";

export declare const FilterBuilder: Component<
	{
		type?: "list" | "line" | "simple";
		init?: (api: IApi) => void;
	} & IConfig &
		FilterBuilderActions<TMethodsConfig>
>;

/* get component events from store actions*/
type RemoveHyphen<S extends string> = S extends `${infer Head}-${infer Tail}`
	? `${Head}${RemoveHyphen<Tail>}`
	: S;

type EventName<K extends string> = `on${RemoveHyphen<K>}`;

export type FilterBuilderActions<TMethodsConfig extends Record<string, any>> = {
	[K in keyof TMethodsConfig as EventName<K & string>]?: (
		ev: TMethodsConfig[K]
	) => void;
} & {
	[key: `on${string}`]: (ev?: any) => void;
};
```

Relevant `@svar-ui/filter-store` public shapes:

```ts
export type AnyData = number | string | Date;
export type TGlue = "and" | "or";
export type TPredicate = "month" | "year" | "yearMonth";
export type TType = "number" | "text" | "date" | "tuple";
export type TFilterType =
	| "greater"
	| "less"
	| "greaterOrEqual"
	| "lessOrEqual"
	| "equal"
	| "notEqual"
	| "contains"
	| "notContains"
	| "beginsWith"
	| "notBeginsWith"
	| "endsWith"
	| "notEndsWith"
	| "between"
	| "notBetween";

export type TOptions =
	| IDataHash<AnyData[]>
	| ((field: string) => AnyData[] | Promise<AnyData[]>);

export interface IFilterSet {
	rules?: (IFilter | IFilterSet)[];
	glue?: TGlue;
}

export interface IFilter {
	field: string | "*";
	type?: TType;
	predicate?: TPredicate;
	filter?: TFilterType;
	includes?: AnyData[];
	value?: AnyData;
}

export interface IField {
	id: string;
	label: string;
	type: TType;
	predicate?: TPredicate;
	format?: string | ((value: AnyData) => string);
}

export interface IConfig {
	value?: IFilterSet;
	fields: IField[];
	options: TOptions;
}

export interface IDataHash<T> {
	[key: string]: T;
}
```

#### Styling

- no `css`, `class`, `className`, or `style` passthrough prop exists on `FilterBuilder`.
- use theme wrappers around the component: `<Willow>`, `<WillowDark>`.
- filter variables: `--wx-filter-value-color`, `--wx-filter-and-background`, `--wx-filter-or-background`, `--wx-filter-and-font-color`, `--wx-filter-or-font-color`, `--wx-filter-border`.
- shared variables used directly: `--wx-background`, `--wx-background-alt`, `--wx-border`, `--wx-border-radius`, `--wx-font-weight-md`, `--wx-line-height`.
- editor/input variables inside the rule editor come from `FilterEditor` and `@svar-ui/svelte-core`.

Class hooks:

- root and modes: `.wx-filter-builder`, `.wx-list`, `.wx-line`, `.wx-simple`
- toolbar/layout: `.wx-toolbar`, `.wx-filters`, `.wx-button`
- groups: `.wx-group`, `.wx-top`, `.wx-inner`
- rule wrappers: `.wx-rule-wrapper`, `.wx-glue-wrapper`, `.wx-editor-wrapper`, `.wx-panel`
- rule display: `.wx-rule`, `.wx-filter`, `.wx-field`, `.wx-value`, `.wx-menu-icon`
- glue display: `.wx-glue`, `.wx-and`, `.wx-or`

Layout defaults:

- `.wx-filter-builder.wx-list`: `padding: 0`, `max-width: 470px`.
- `.wx-toolbar.wx-line` and `.wx-toolbar.wx-simple`: flex rows with `gap: 20px`, `height: 67px`.
- `.wx-toolbar.wx-line`: `justify-content: space-between`.
- `.wx-filters`: horizontal scroll container in `line` and `simple`.
- `.wx-group.wx-inner.wx-list`: `margin-left: 20px`, `padding: 4px 0 0 8px`, `border-left: var(--wx-border)`.
- `.wx-group.wx-line`: `display: flex`, `gap: 10px`, `padding: 4px`.
- `.wx-rule.wx-list`: `padding: 12px 8px`, `margin: 10px 0`.
- `.wx-rule.wx-line`: `height: 36px`, `padding: 8px`.
- `.wx-editor-wrapper`: `padding: 0 10px`, `min-width: 280px`, `max-width: 320px`.

```svelte
<div class="builder-scope">
	<Willow>
		<FilterBuilder {fields} {options} onchange={handleChange} />
	</Willow>
</div>

<style>
	.builder-scope {
		--wx-filter-value-color: #7048e8;
		--wx-filter-and-background: #ffe066;
		--wx-filter-or-background: #b2f2bb;
	}

	.builder-scope .wx-rule {
		border-radius: 6px;
	}

	.builder-scope .wx-group.wx-line {
		gap: 14px;
	}
</style>
```

#### Recipes

##### Local Array Filtering

```svelte
<script>
	import { FilterBuilder, Willow, createArrayFilter } from "@svar-ui/svelte-filter";

	const fields = [
		{ id: "first_name", label: "First Name", type: "text" },
		{ id: "age", label: "Age", type: "number" },
		{ id: "start", label: "Start Date", type: "date" },
	];
	const options = {
		first_name: ["Alex", "Daisy", "John"],
		age: [24, 35, 45],
	};
	const data = [
		{ first_name: "Alex", age: 45, start: new Date("2025-03-13") },
		{ first_name: "Daisy", age: 33, start: new Date("2024-12-04") },
	];
	let rows = $state(data);
	let value = $state({ glue: "and", rules: [] });

	function applyFilter({ value }) {
		rows = createArrayFilter(value)(data);
	}
</script>

<Willow>
	<FilterBuilder {value} {fields} {options} onchange={applyFilter} />
</Willow>
```

##### Line Or Simple Layout

```svelte
<FilterBuilder
	{value}
	{fields}
	{options}
	type="line"
	onchange={({ value }) => applyFilter(value)}
/>

<FilterBuilder
	{value}
	{fields}
	{options}
	type="simple"
	onchange={({ value }) => applyFilter(value)}
/>
```

##### Async Options

```svelte
<script>
	import { FilterBuilder } from "@svar-ui/svelte-filter";

	async function loadOptions(fieldId) {
		await new Promise(resolve => setTimeout(resolve, 300));
		return optionMap[fieldId] || [];
	}
</script>

<FilterBuilder {value} {fields} options={loadOptions} />
```

##### API And Event Interception

```svelte
<script>
	import { FilterBuilder } from "@svar-ui/svelte-filter";

	let api = $state();
	let valueText = $state("");

	function init(api) {
		api.intercept("add-rule", ev => {
			ev.edit = false;
		});
		api.on("change", ({ value }) => {
			valueText = JSON.stringify(value, null, 2);
		});
	}

	function addAgeRule() {
		api.exec("add-rule", {
			rule: { field: "age", type: "number", filter: "greater", value: 30 },
			edit: false,
		});
	}
</script>

<button onclick={addAgeRule}>Add age rule</button>
<FilterBuilder bind:this={api} {fields} {options} {init} />
<pre>{valueText}</pre>
```

##### Convert Date Strings Around Builder UI

```svelte
<script>
	import { FilterBuilder } from "@svar-ui/svelte-filter";

	const incoming = {
		rules: [{ field: "start", filter: "greater", value: "2025-01-01" }],
	};

	let value = $state({
		...incoming,
		rules: incoming.rules.map(rule =>
			rule.field === "start"
				? { ...rule, type: "date", value: new Date(rule.value) }
				: rule
		),
	});

	function init(api) {
		api.on("change", ({ value }) => {
			console.log(JSON.stringify(value));
		});
	}
</script>

<FilterBuilder {value} {fields} {options} {init} />
```


## File: filter/FilterEditor.md

> Source: `filter/FilterEditor.md`

### FilterEditor

Package: `@svar-ui/svelte-filter`

Use this file independently when building, configuring, styling, or modifying `FilterEditor`.

#### Import

```js
import {
	FilterEditor,
	Willow,
	WillowDark,
	createArrayFilter,
	createFilter,
	getOptions,
} from "@svar-ui/svelte-filter";
```

#### Supported Functionality

##### Data Contract

- emits one `IFilter` rule through `onapply` and `onchange`.
- `IFilter`: `{ field?, type, predicate?, filter, includes, value }`.
- `field` is present when the `field` prop is set or when `fields` mode is active.
- `includes` is a selected subset only when non-empty and smaller than visible options; otherwise it emits `[]`.
- `value` is a scalar for most filters and `{ start, end }` for `between` / `notBetween`.
- date editor UI values should be `Date` objects or `{ start: Date, end: Date }`.
- `options` can be a fixed array or `(fieldId) => AnyData[] | Promise<AnyData[]>` in field-aware mode.

##### Built-In Filters

- text: `equal`, `notEqual`, `contains`, `notContains`, `beginsWith`, `notBeginsWith`, `endsWith`, `notEndsWith`
- number: text filters plus `greater`, `less`, `greaterOrEqual`, `lessOrEqual`, `between`, `notBetween`
- date: `equal`, `notEqual`, `greater`, `less`, `greaterOrEqual`, `lessOrEqual`, `between`, `notBetween`
- tuple: `greater`, `less`, `greaterOrEqual`, `lessOrEqual`, `equal`, `notEqual`
- date predicates: `month`, `year`, `yearMonth`

##### Props And Behavior

- source props: `fields = null`, `fieldsSelector = true`, `field = null`, `buttons = true`, `options = null`, `includes = null`, `type = "text"`, `filter = ""`, `value = ""`, `format = null`, `predicate = null`, `onapply`, `oncancel`, `onchange`.
- single-field mode: pass `type`, `field`, `filter`, `value`, `options`, `includes`, `format`, and `predicate` directly.
- multi-field mode: pass `fields`; selected field controls type, format, predicate, and loaded options.
- `fieldsSelector={false}` hides the field dropdown while keeping the selected field.
- `type="date"` uses `DatePicker`, except `filter="between"`/`"notBetween"` use `DateRangePicker`.
- `type="number"` uses numeric `Text`; `type="text"` uses text `Text`.
- `type="tuple"` uses `Combo` with options plus an automatic empty `$empty` / `None` option.
- option checkboxes are filtered by the current operator/value.
- `onchange({ value })` fires for UI changes when operator, value, field, or includes change.
- `onapply({ value })` fires from the Apply button.
- `oncancel()` fires from Cancel with no payload in source.
- `buttons={false}` hides Apply/Cancel and is normally paired with `onchange`.

#### Public Types

```ts
import type { Component } from "svelte";
import type {
	TSingleOptions,
	TFilterType,
	TType,
	TPredicate,
	AnyData,
	IFilter,
	IConfig,
	IField,
} from "@svar-ui/filter-store";

export declare const FilterEditor: Component<{
	fields?: IConfig["fields"];
	fieldsSelector?: boolean;
	field?: string;
	buttons?: boolean;
	options?: TSingleOptions;
	includes?: AnyData[];
	type?: TType;
	filter?: TFilterType;
	value?: AnyData | { start?: Date; end: Date };
	format?: string | ((value: AnyData) => string);
	predicate: TPredicate;
	onapply: (ev: { value: IFilter }) => void;
	oncancel: (ev: { value: IFilter }) => void;
	onchange: (ev: { value: IFilter }) => void;
}>;
```

Relevant `@svar-ui/filter-store` public shapes:

```ts
export type AnyData = number | string | Date;
export type TGlue = "and" | "or";
export type TPredicate = "month" | "year" | "yearMonth";
export type TType = "number" | "text" | "date" | "tuple";
export type TFilterType =
	| "greater"
	| "less"
	| "greaterOrEqual"
	| "lessOrEqual"
	| "equal"
	| "notEqual"
	| "contains"
	| "notContains"
	| "beginsWith"
	| "notBeginsWith"
	| "endsWith"
	| "notEndsWith"
	| "between"
	| "notBetween";

export type TSingleOptions =
	| AnyData[]
	| ((field: string) => AnyData[] | Promise<AnyData[]>);

export type TOptions =
	| IDataHash<AnyData[]>
	| ((field: string) => AnyData[] | Promise<AnyData[]>);

export interface IFilterSet {
	rules?: (IFilter | IFilterSet)[];
	glue?: TGlue;
}

export interface IFilter {
	field: string | "*";
	type?: TType;
	predicate?: TPredicate;
	filter?: TFilterType;
	includes?: AnyData[];
	value?: AnyData;
}

export interface IField {
	id: string;
	label: string;
	type: TType;
	predicate?: TPredicate;
	format?: string | ((value: AnyData) => string);
}

export interface IConfig {
	value?: IFilterSet;
	fields: IField[];
	options: TOptions;
}

export interface IDataHash<T> {
	[key: string]: T;
}
```

#### Styling

- no `css`, `class`, `className`, or `style` passthrough prop exists on `FilterEditor`.
- use theme wrappers around the component: `<Willow>`, `<WillowDark>`.
- editor sets `--wx-input-border: var(--wx-filter-border)` on `.wx-filter-editor`.
- filter variables from themes: `--wx-filter-border`, `--wx-filter-value-color`, `--wx-filter-and-background`, `--wx-filter-or-background`, `--wx-filter-and-font-color`, `--wx-filter-or-font-color`.
- shared/core input variables come from `@svar-ui/svelte-core`, including `--wx-input-*`.

Class hooks:

- root: `.wx-filter-editor`
- rows and cells: `.wx-wrapper`, `.wx-cell`
- option list: `.wx-list`, `.wx-item`

Layout defaults:

- `.wx-wrapper`: `display: flex`, `justify-content: right`, `gap: 10px`, `align-items: center`, `margin: 8px 0`.
- `.wx-cell`: `flex: 1`.
- `.wx-list`: `height: 150px`, `overflow-y: auto`, `margin: 8px 0`, `border: var(--wx-filter-border)`.
- `.wx-item`: `user-select: none`, `padding: 8px 12px`, `border-bottom: var(--wx-filter-border)`.

```svelte
<div class="editor-scope">
	<Willow>
		<FilterEditor type="text" options={values} onapply={handleApply} />
	</Willow>
</div>

<style>
	.editor-scope {
		--wx-filter-border: 1px solid #d0d5dd;
	}

	.editor-scope .wx-item {
		padding: 12px 16px;
	}
</style>
```

#### Recipes

##### Single Text Rule With Apply

```svelte
<script>
	import { FilterEditor, createArrayFilter } from "@svar-ui/svelte-filter";

	const options = ["Alex", "Daisy", "John"];
	let rows = $state(data);

	function apply({ value }) {
		rows = createArrayFilter({ rules: [value] })(data);
	}
</script>

<FilterEditor
	type="text"
	field="first_name"
	{options}
	onapply={apply}
/>
```

##### Live Rule Without Buttons

```svelte
<script>
	import { FilterEditor, createArrayFilter } from "@svar-ui/svelte-filter";

	let rule = $state({});
	let rows = $state(data);

	function update({ value }) {
		rule = value;
		rows = createArrayFilter({ rules: [value] })(data);
	}
</script>

<FilterEditor
	type="text"
	field="first_name"
	options={["Alex", "Daisy", "John"]}
	buttons={false}
	includes={rule.includes}
	filter={rule.filter}
	value={rule.value}
	onchange={update}
/>
```

##### Field Selector With Async Options

```svelte
<script>
	import { FilterEditor } from "@svar-ui/svelte-filter";

	const fields = [
		{ id: "first_name", label: "First Name", type: "text" },
		{ id: "age", label: "Age", type: "number" },
		{ id: "start", label: "Start Date", type: "date" },
	];

	async function loadOptions(field) {
		return optionMap[field] || [];
	}
</script>

<FilterEditor
	{fields}
	field="age"
	options={loadOptions}
	onapply={({ value }) => console.log(value)}
/>
```

##### Date Range Rule

```svelte
<script>
	import { FilterEditor, getOptions } from "@svar-ui/svelte-filter";

	const options = getOptions(data, "start");
</script>

<FilterEditor
	field="start"
	{options}
	type="date"
	filter="between"
	value={{
		start: new Date("2024-11-01"),
		end: new Date("2025-05-01"),
	}}
	onapply={({ value }) => console.log(value)}
/>
```

##### Tuple With Formatted Options

```svelte
<script>
	import { FilterEditor, getOptions } from "@svar-ui/svelte-filter";

	const options = getOptions(data, "start", {
		predicate: "month",
		sort: (a, b) => a - b,
	});
	const monthName = value => monthLabels[value] || String(value);
</script>

<FilterEditor
	field="start"
	{options}
	format={monthName}
	filter="greater"
	type="tuple"
	onapply={({ value }) => console.log(value)}
/>
```

#### Implementation Notes

- `FilterEditor` source treats `predicate`, `onapply`, `oncancel`, and `onchange` as optional
- source calls `oncancel()` with no payload, although the declaration types it as `(ev: { value: IFilter }) => void`.


## File: filter/FilterQuery.md

> Source: `filter/FilterQuery.md`

### FilterQuery

Package: `@svar-ui/svelte-filter`

Use this file independently when building, configuring, styling, or modifying `FilterQuery`.

#### Import

```js
import {
	FilterQuery,
	Willow,
	WillowDark,
	createArrayFilter,
	createFilter,
	getQueryHtml,
	getQueryString,
} from "@svar-ui/svelte-filter";
```

#### Supported Functionality

##### Data Contract

- `value` is bindable and stores the query string with field IDs.
- displayed `text` uses sanitized field labels when `fields` include labels.
- field labels are sanitized by removing parser-special characters; `{ id: "first_name", label: "First Name" }` displays as `FirstName:`.
- `fields`: array of `{ id, label, type, predicate?, format? }`.
- `options`: `{ [fieldId]: AnyData[] }`; tag suggestions use `options["#"]`.
- parse-enabled callbacks receive `value: IFilterSet | IFilter | null`.
- `parse="none"` callbacks receive raw `value` and `text` strings.
- `startProgress()` and `endProgress()` control the top progress bar for async filtering.

##### Parse Modes

- `parse` defaults to `"allowFreeText"`.
- `parse="allowFreeText"` parses query syntax and converts plain words into `field: "*"` `contains` filters.
- `parse="strict"` parses query syntax but disables free-text fallback.
- `parse="none"` disables parser, syntax highlight, autocomplete, and validation; use it for natural-language endpoints.
- Enter and the Search button call `onchange`.
- clear button resets local text and bound `value`, but does not call `onchange` until the user submits again.

##### Query Syntax Highlights

- field-value: `Status: Open`
- implicit AND: `Status: Open Age: >30`
- explicit logic: `Status: Open or Status: Review`
- multiple values: `Status: Open, Review`
- negation: `Status: -Closed`, `Name: -contains test`
- text operators: `contains`, `starts`, `ends`
- wildcards: `Name: Alex*`, `Email: *@company.com`, `Title: *urgent*`
- comparisons: `Age: >30`, `Age: <=60`
- ranges: `Age: 25 .. 50`, `StartDate: 2024-01-01 .. 2025-01-01`
- date predicates: `StartDate.year: 2024`, `StartDate.month: 6`; `YYYY` and `YYYY-MM` infer predicates.
- tags / any-field exact search: `#urgent`, `-#done`

##### Autocomplete

- field suggestions match field `id` and sanitized `label`, and insert the label into text.
- value suggestions come from `options[fieldId]`.
- tag suggestions come from `options["#"]`.
- date predicate suggestions are `year` and `month`.
- value suggestion labels use the field `format` function when present.
- suggestions rank starts-with matches before contains matches.
- keyboard support: ArrowDown/ArrowUp navigates, Enter selects when focused, Escape/Tab closes.

##### Events

- `onchange` runs on Enter, Search button, and external `value` updates after the first non-empty set.
- parse-enabled event shape: `{ parsed, value, text, error, startProgress, endProgress }`.
- `parsed` is a `ParseResult`.
- `error` is `null` or a localized `ValidationError` with `message`.
- with parse enabled, `text` is `parseResult.naturalText || ""` when there is no blocking error, otherwise the current query text.
- with `parse="none"`, event shape is `{ value, text, startProgress, endProgress }`.

#### Public Types

```ts
import type { Component } from "svelte";
import type {
	IFilterSet,
	IFilter,
	IField,
	IDataHash,
	AnyData,
	ParseResult,
	ValidationError,
} from "@svar-ui/filter-store";

export interface FilterQueryEvent {
	value: string | IFilterSet | IFilter | null;
	text: string;
	parsed?: ParseResult;
	error?: ValidationError | null;
	startProgress: () => void;
	endProgress: () => void;
}

export declare const FilterQuery: Component<{
	value?: string;
	placeholder?: string;
	parse?: "none" | "strict" | "allowFreeText";
	fields?: IField[];
	options?: IDataHash<AnyData[]>;
	onchange?: (ev: FilterQueryEvent) => void;
}>;
```

Relevant `@svar-ui/filter-store` public shapes:

```ts
export type AnyData = number | string | Date;
export type TGlue = "and" | "or";
export type TPredicate = "month" | "year" | "yearMonth";
export type TType = "number" | "text" | "date" | "tuple";
export type TFilterType =
	| "greater"
	| "less"
	| "greaterOrEqual"
	| "lessOrEqual"
	| "equal"
	| "notEqual"
	| "contains"
	| "notContains"
	| "beginsWith"
	| "notBeginsWith"
	| "endsWith"
	| "notEndsWith"
	| "between"
	| "notBetween";

export interface IFilterSet {
	rules?: (IFilter | IFilterSet)[];
	glue?: TGlue;
}

export interface IFilter {
	field: string | "*";
	type?: TType;
	predicate?: TPredicate;
	filter?: TFilterType;
	includes?: AnyData[];
	value?: AnyData;
}

export interface IField {
	id: string;
	label: string;
	type: TType;
	predicate?: TPredicate;
	format?: string | ((value: AnyData) => string);
}

export interface IDataHash<T> {
	[key: string]: T;
}

export type ValidationErrorCode =
	| "UNKNOWN_FIELD"
	| "EXPECTED_NUMBER"
	| "EXPECTED_DATE"
	| "PARSE_ERROR"
	| "NO_DATA";

export type HighlightTokenType =
	| "field"
	| "value"
	| "operator"
	| "textop"
	| "comparison"
	| "symbol"
	| "wildcard"
	| "negation"
	| "hash"
	| "error";

export interface HighlightToken {
	type: HighlightTokenType;
	start: number;
	end: number;
	invalid?: boolean;
}

export interface ValidationError {
	code: ValidationErrorCode;
	field?: string;
	value?: string;
	message?: string;
}

export interface ParseResult {
	config: IFilterSet | IFilter | null;
	isInvalid: boolean | ValidationError;
	startOperation: string | null;
	tokens: HighlightToken[];
	naturalText: string | null;
}
```

#### Styling

- no `css`, `class`, `className`, or `style` passthrough prop exists on `FilterQuery`.
- use theme wrappers around the component: `<Willow>`, `<WillowDark>`.
- token variables with fallbacks in `getQueryHtml`: `--wx-filter-query-field-color`, `--wx-filter-query-value-color`, `--wx-filter-query-operator-color`, `--wx-filter-query-comparison-color`, `--wx-filter-query-symbol-color`, `--wx-filter-query-negation-color`, `--wx-filter-query-error-color`.
- layout/input variables: `--wx-border`, `--wx-border-radius`, `--wx-background`, `--wx-background-alt`, `--wx-padding`, `--wx-color-font`, `--wx-color-font-alt`, `--wx-color-primary`, `--wx-color-primary-font`, `--wx-color-success`, `--wx-font-size`, `--wx-font-family`.
- autocomplete variables: `--wx-input-font-family`, `--wx-input-font-size`, `--wx-input-line-height`, `--wx-input-font-weight`, `--wx-input-font-color`, `--wx-input-padding`, `--wx-background-hover`.

Class hooks:

- root: `.wx-filter-query`
- progress: `.wx-progress-bar`, `.active`, `.wx-progress-fill`
- row/layout: `.wx-filter-query-row`, `.wx-filter-query-input-wrapper`
- overlay/input: `.wx-filter-query-highlight`, `.wx-placeholder`, `.wx-filter-query-input`, `.wx-parse-mode`
- buttons: `.wx-filter-query-clear`, `.wx-filter-query-search`
- autocomplete dropdown from `Suggest`: `.wx-list`, `.wx-item`, `.wx-focus`
- standalone highlight helper component: `.wx-query-highlight`

Layout defaults:

- `.wx-filter-query`: `display: flex`, `flex-direction: column`, `position: relative`.
- `.wx-progress-bar`: absolute top edge, `height: 3px`.
- `.wx-filter-query-row`: flex row with `border: var(--wx-border)`, `border-radius: var(--wx-border-radius)`, `background: var(--wx-background)`.
- `.wx-filter-query-highlight`: absolute overlay, `padding: 6px 12px`, `white-space: pre`, hidden scrollbars.
- `.wx-filter-query-input`: `width: 100%`, no border, `padding: var(--wx-padding) 12px`, transparent background.
- `.wx-filter-query-input.wx-parse-mode`: transparent text with visible caret so the highlight layer provides token colors.
- autocomplete `.wx-list`: `max-height: 250px`, vertical scroll.

```svelte
<div class="query-scope">
	<Willow>
		<FilterQuery {fields} {options} onchange={handleFilter} />
	</Willow>
</div>

<style>
	.query-scope {
		--wx-filter-query-field-color: #7c3aed;
		--wx-filter-query-value-color: #059669;
		--wx-color-primary: #7c3aed;
	}

	.query-scope .wx-filter-query-search {
		background: #0f172a;
		color: #f8fafc;
	}
</style>
```

#### Recipes

##### Structured Query With Local Filtering

```svelte
<script>
	import { FilterQuery, createArrayFilter } from "@svar-ui/svelte-filter";

	let value = $state("");
	let rows = $state(data);

	function handleFilter({ value, error }) {
		if (error && error.code !== "NO_DATA") return;
		rows = createArrayFilter(value, {}, fields)(data);
	}
</script>

<FilterQuery
	bind:value
	placeholder="e.g. FirstName: Alex or #urgent"
	{fields}
	options={{ ...options, "#": ["urgent", "review", "done"] }}
	onchange={handleFilter}
/>
```

##### Strict Query Syntax

```svelte
<FilterQuery
	bind:value={query}
	parse="strict"
	placeholder="Status: Open and Age: >30"
	{fields}
	{options}
	onchange={({ value, error }) => {
		if (!error) applyFilter(value);
	}}
/>
```

##### Natural Text Endpoint

```svelte
<script>
	import { FilterQuery, createArrayFilter, getQueryString } from "@svar-ui/svelte-filter";

	let normalizedQuery = $state("");
	let rows = $state(data);

	async function handleNatural({ text, startProgress, endProgress }) {
		try {
			startProgress();
			const filter = await textToFilter(text, fields);
			normalizedQuery = filter ? getQueryString(filter).query : "";
			rows = createArrayFilter(filter || { rules: [] })(data);
		} finally {
			endProgress();
		}
	}
</script>

<FilterQuery
	parse="none"
	placeholder="first name contains Alex and age greater than 30"
	onchange={handleNatural}
/>

<pre>{normalizedQuery}</pre>
```

##### Mixed Query And Natural Text

```svelte
<script>
	import { FilterQuery, createArrayFilter, getQueryString } from "@svar-ui/svelte-filter";

	let query = $state("start: 2024");
	let rows = $state(data);

	async function handleMixed({ value, error, text, startProgress, endProgress }) {
		if (text) {
			try {
				startProgress();
				value = await textToFilter(text, fields);
				query = value ? getQueryString(value).query : "";
				error = null;
			} finally {
				endProgress();
			}
		}

		if (error && error.code !== "NO_DATA") return;
		rows = createArrayFilter(value, {}, fields)(data);
	}
</script>

<FilterQuery
	bind:value={query}
	placeholder="FirstName: contains Alex and Age: >30"
	{fields}
	{options}
	onchange={handleMixed}
/>
```

##### Render Query HTML

```svelte
<script>
	import { getQueryHtml, getQueryString } from "@svar-ui/svelte-filter";

	let html = $derived(
		filterValue
			? getQueryHtml(getQueryString(filterValue).query, { fields })
			: ""
	);
</script>

<!-- eslint-disable-next-line svelte/no-at-html-tags -->
{@html html}
```

#### Implementation Notes

- `parse="none"` bypasses highlight, autocomplete, parsing, and validation entirely.
- `NO_DATA` errors still pass parsed config and can be treated as non-blocking
- `getQueryHtml` returns inline styled HTML; only use it in trusted/internal query display contexts.


## File: gantt/index.md

> Source: `gantt/index.md`

Use when building, configuring, styling, or modifying SVAR Svelte Gantt / @svar-ui/svelte-gantt timelines, grids, task editors, toolbars, context menus, tooltips, scales, links, and Gantt data actions.

#### Package

```js
import {
	Gantt,
	ContextMenu,
	HeaderMenu,
	Toolbar,
	Tooltip,
	Editor,
	Willow,
	WillowDark,
	version,
	defaultEditorItems,
	defaultToolbarButtons,
	defaultMenuOptions,
	defaultColumns,
	defaultTaskTypes,
	getEditorItems,
	getToolbarButtons,
	getMenuOptions,
	registerScaleUnit,
	registerEditorItem,
} from "@svar-ui/svelte-gantt";
```

#### Components

- `Gantt` - main grid plus timeline chart; `bind:this` exposes the Gantt API object from source.
- `Toolbar` - Gantt-aware wrapper around `@svar-ui/svelte-toolbar`; accepts `api` and optional `items`.
- `ContextMenu` - Gantt-aware wrapper around `@svar-ui/svelte-menu` context menu; resolves tasks from Gantt `data-id`.
- `Editor` - Gantt-aware wrapper around `@svar-ui/svelte-editor`; opens for `activeTask` / `show-editor`.
- `Tooltip` - wraps a Gantt and displays task text or a custom content component from `data-tooltip-id`.
- `HeaderMenu` - wraps `@svar-ui/svelte-grid` header menu and passes `api.getTable()` to it.
- `Willow`, `WillowDark` - theme wrappers; each accepts `fonts?: boolean` and optional children.

#### Supported functionality

##### Gantt Data

- `tasks` is an array of task objects; common fields are `id`, `text`, `start`, `end`, `duration`, `progress`, `parent`, `type`, `open`, `details`, `data`, `unscheduled`, `segments`, `base_start`, `base_end`, `base_duration`, `rollup`.
- `links` is an array of dependency links with `id`, `source`, `target`, `type`, optional `lag`.
- link `type` values are `s2s`, `s2e`, `e2s`, `e2e`.
- task `type` defaults are `task`, `summary`, `milestone`; custom types are supported through `taskTypes`.
- milestone tasks are normalized with `duration = 0` and no `end`.
- summary task dates are calculated from children when `start` / `end` are missing.
- `parseTaskDates(tasks, { durationUnit, splitTasks, calendar })` runs inside `Gantt` and mutates task date fields unless `_export` is set.

Common data objects:

```js
const tasks = [
	{
		id: 1,
		text: "Project",
		type: "summary",
		parent: 0,
		open: true,
	},
	{
		id: 10,
		text: "Task",
		type: "task",
		parent: 1,
		start: new Date(2026, 3, 2),
		duration: 3,
		progress: 40,
	},
	{
		id: 11,
		text: "Milestone",
		type: "milestone",
		parent: 1,
		start: new Date(2026, 3, 8),
	},
];

const links = [{ id: 1, source: 10, target: 11, type: "e2s" }];
```

##### Gantt Config

- default scales: `[{ unit: "month", step: 1, format: "%F %Y" }, { unit: "day", step: 1, format: "%j" }]`.
- `scales` rows accept `unit`, `step`, `format?: string | (date, next) => string`, `css?: (date) => string`.
- `start`, `end`, and `autoScale` control timeline bounds; `autoScale` includes tasks, markers, baselines, `projectStart`, and `projectEnd`.
- `zoom` accepts `true` or `IZoomConfig`; chart zoom is handled by Ctrl/Command + wheel and emits `zoom-scale`.
- `columns` defaults to `defaultColumns`; `columns={false}` hides the grid and resizer.
- the `text` column is rendered with the built-in `TextCell`; `add-task` uses `ActionCell`, is removed in `readonly`, and moves to the first column in compact chart mode.
- `cellWidth`, `cellHeight`, `scaleHeight` control timeline width, row height, and scale row height.
- `lengthUnit` controls chart math; `durationUnit` controls task duration calculation and is `"day"` or `"hour"`.
- `cellBorders` is `"column"` or `"full"`.
- `readonly` disables task drag, progress editing, link editing, grid add column behavior, and editor opening from double click.
- `selected` and `activeTask` are config inputs, not `$bindable()` props; read or change live selection through `api.getReactiveState()` and `api.exec("select-task", ...)`.
- `highlightTime(date, unit)` can return a CSS class for timescale cells and chart background cells when min unit is `day` or `hour`.
- compact mode is driven by a `ResizeObserver` on `document.body`; width `<= 650` switches the layout to grid/chart modes.

Common config objects:

```js
const columns = [
	{ id: "text", header: "Task name", flexgrow: 1, editor: "text" },
	{ id: "start", header: "Start date", align: "center", editor: "datepicker" },
	{ id: "duration", header: "Duration", width: 100, align: "center" },
	{ id: "add-task", header: "Add task", width: 50, align: "center" },
];

const scales = [
	{ unit: "month", step: 1, format: "%F %Y" },
	{ unit: "week", step: 1, format: "Week %w" },
	{ unit: "day", step: 1, format: "%j", css: date => date.getDay() === 0 ? "wx-weekend" : "" },
];

const zoom = {
	level: 2,
	minCellWidth: 40,
	maxCellWidth: 180,
};
```

##### Pro And Advanced Config

- `baselines` shows `base_start` / `base_end` / `base_duration`.
- `rollups` accepts `true` or `{ type: "all" | "closest" }`; tasks with `rollup: true` are drawn on summary rows.
- `markers` is an array of `{ start: Date, text?: string, css?: string }`.
- `criticalPath={{ type: "strict" | "flexible" }}` marks critical tasks and links.
- `schedule={{ type?: "forward", auto?: boolean }}` enables scheduling behavior; `projectStart` and `projectEnd` provide bounds.
- `calendar` accepts a `Calendar` from `@svar-ui/gantt-store`; Gantt then creates default weekend highlighting when `calendar` is set.
- `undo` enables history state plus `undo` / `redo` actions and toolbar buttons.
- `splitTasks` enables task `segments` editing, split toolbar/menu actions, and segment-aware editor/context-menu targets.
- `summary={{ autoProgress?: boolean, autoConvert?: boolean }}` controls summary progress and summary type conversion behavior.
- `slack` shows task slack visuals.
- `unscheduledTasks` enables task `unscheduled` support and editor scheduling controls.
- `api.exec("export-data", config)` supports `format: "pdf" | "png" | "xlsx" | "mspx"` through `IExportConfig`.
- `api.exec("import-data", { data, format: "mspx" })` imports MS Project XML.

##### API And Events

`Gantt` exposes this API from source through `bind:this` or `init(api)`:

- state: `getState()`, `getReactiveState()`, `getStores()`
- events/actions: `exec(action, data)`, `on(action, callback, config?)`, `intercept(action, callback, config?)`, `detach(tag)`, `setNext(eventBusOrProvider)`
- task/table helpers: `getTask(id)`, `getTable(waitRender?)`, `serialize()`, `getHistory()`

Component callback props are generated from action names by removing hyphens and prefixing `on`:

- `add-task` -> `onaddtask`
- `update-task` -> `onupdatetask`
- `select-task` -> `onselecttask`
- custom `taskTemplate` action `"custom-click"` -> `oncustomclick`

Source routes actions through `DataStore` first, then calls the matching component callback prop if present.

Common actions:

```js
api.exec("add-task", {
	task: { text: "New task", type: "task" },
	target: 10,
	mode: "after",
	show: true,
});

api.exec("update-task", {
	id: 10,
	task: { text: "Updated", progress: 75 },
});

api.exec("select-task", {
	id: 10,
	toggle: false,
	range: false,
	show: "xy",
	focus: "grid",
});

api.exec("move-task", { id: 10, target: 1, mode: "child" });
api.exec("filter-tasks", { filter: task => task.text?.includes("API"), open: true });
api.exec("scroll-chart", { date: new Date(2026, 4, 1) });
```

Use `api.intercept(action, cb)` to block or replace built-in behavior; returning `false` blocks the action. Use `api.setNext(provider)` to forward data changes to a provider such as `RestDataProvider`.

##### Saving

- `RestDataProvider` from `@svar-ui/gantt-data-provider` persists data changes to a REST backend.
- Wire it once with `api.setNext(provider)` in `init`; the provider then forwards every data action (`add-task`, `update-task`, `delete-task`, `move-task`, `add-link`, `update-link`, `delete-link`, etc.) emitted on the event bus as the matching REST call. No per-action save handlers needed.
- Initial load uses `provider.getData()`; lazy branches use `provider.getData(id)` inside `request-data` and dispatch back through `provide-data`.
- Optional `{ batchURL }` constructor option batches concurrent writes into a single endpoint.

```js
import { RestDataProvider } from "@svar-ui/gantt-data-provider";

const provider = new RestDataProvider("/api/gantt");

function init(api) {
	api.setNext(provider); // forwards all task/link mutations to REST
}
```

##### Toolbar

- `Toolbar` source props are `api = null` and `items = []`.
- default items come from `getToolbarButtons({ undo: $undo, splitTasks: $splitTasks })`.
- default handled ids are wired through `handleAction(api, item.id, null, _)`.
- custom item `handler` functions are preserved only when the id is not one of the handled default action ids.
- if no task is selected, default toolbar keeps only targetless items such as `add-task` and history controls.
- `undo` adds `undo` and `redo`; `splitTasks` adds `split-task`.

Default toolbar ids:

```js
[
	"add-task",
	"edit-task",
	"delete-task",
	"move-task:up",
	"move-task:down",
	"copy-task",
	"cut-task",
	"paste-task",
	"indent-task:add",
	"indent-task:remove",
];
```

##### Context Menu

- `ContextMenu` source props are `options`, `api`, `resolver`, `filter`, `at = "point"`, `children`, `onclick`, `css`.
- the wrapper passes `dataKey="id"` to `@svar-ui/svelte-menu`; Gantt grid rows and bars expose `data-id`.
- built-in menu options are from `getMenuOptions({ splitTasks, taskTypes, summary })`.
- right-clicking a task selects it when it is not already selected.
- `resolver(id, event)` can return `true` to use the default task, return a replacement context object, or return a falsy value to prevent task resolution.
- `filter(option, task)` is applied across selected tasks; built-in `isHidden` and `isDisabled` are also applied.
- wrapper `onclick` receives the menu event used in demos as `{ context, action }`.
- built-in handled `action.id` values are executed through `handleAction(api, action.id, activeId, _)` before user `onclick`.
- with `splitTasks`, segment targets use `{ id, segmentIndex }` internally for edit/delete/split actions.

Default menu ids:

```js
[
	"add-task:child",
	"add-task:before",
	"add-task:after",
	"convert-task:<taskType>",
	"edit-task",
	"cut-task",
	"copy-task",
	"paste-task",
	"move-task:up",
	"move-task:down",
	"indent-task:add",
	"indent-task:remove",
	"delete-task",
];
```

##### Editor

- `Editor` source props are `api`, `items = []`, `css = ""`, `layout = "default"`, `readonly = false`, `placement = "sidebar"`, `bottomBar = true`, `topBar = true`, `autoSave = true`, `focus = false`, `hotkeys = {}`.
- editor renders only when `api.getReactiveState()._activeTask` exists.
- default items come from `getEditorItems({ unscheduledTasks, rollups, summary, taskTypes })`.
- built-in editor comps registered by the wrapper: `select`, `date`, `twostate`, `slider`, `counter`, `links`, `checkbox`.
- `registerEditorItem(name, Component)` registers custom comps for `items`.
- item `key` is the task field; editor values are task objects keyed by those `key` values.
- `autoSave={true}` saves valid changes on field change; `autoSave={false}` stores local values and saves from a `save` top/bottom bar action.
- saved task payload removes `links` and `data`; `duration` may be removed when no duration editor is present.
- `links` editor changes are batched in the wrapper and saved through link actions.
- default `topBar={true}` in editable mode creates close/spacer/delete buttons, plus save when `autoSave={false}`.

Default editor keys:

```js
["text", "details", "type", "start", "end", "duration", "progress", "links"]
```

##### Tooltip

- `Tooltip` source props are `api`, `content`, `children`.
- default tooltip text is the task `text`, or segment `text` when `data-segment` is present.
- custom `content` component receives `{ data }`; source also passes `segmentIndex` for split-task segments.
- direct tooltip override can use a DOM `data-tooltip` attribute; placement hint uses `data-tooltip-at="left"`.
- tooltip lookup is debounced by 300ms.

##### Header Menu

- `HeaderMenu` source props are `api`, `columns`, `children`.
- wrapper calls `api?.getTable()` and passes that table API to `@svar-ui/svelte-grid` `HeaderMenu`.
- use it when the grid table API is needed for column visibility/menu behavior.

#### Public Types

```ts
import type { Component, ComponentProps } from "svelte";
import { ContextMenu as BaseContextMenu } from "@svar-ui/svelte-menu";
import { Toolbar as BaseToolbar } from "@svar-ui/svelte-toolbar";
import { Editor as BaseEditor } from "@svar-ui/svelte-editor";
import {
	HeaderMenu as BaseHeaderMenu,
	IColumnConfig as ITableColumn,
} from "@svar-ui/svelte-grid";

import type {
	TMethodsConfig,
	IApi,
	IConfig,
	ITask,
	IGanttColumn,
} from "@svar-ui/gantt-store";

export * from "@svar-ui/gantt-store";
export { registerEditorItem } from "@svar-ui/svelte-editor";

export interface IColumnConfig extends Omit<IGanttColumn, "header"> {
	cell?: ITableColumn["cell"];
	header?: ITableColumn["header"];
	editor?: ITableColumn["editor"];
}

export declare const Gantt: Component<
	{
		columns?: false | IColumnConfig[];
		taskTemplate?: Component<{
			data: ITask;
			api: IApi;
			onaction: (ev: {
				action: string;
				data: { [key: string]: any };
			}) => void;
		}>;
		readonly?: boolean;
		cellBorders?: "column" | "full";
		highlightTime?: (date: Date, unit: "day" | "hour") => string;
		init?: (api: IApi) => void;
	} & IConfig &
		GanttActions<TMethodsConfig>
>;

export declare const HeaderMenu: Component<
	ComponentProps<typeof BaseHeaderMenu> & {
		api?: IApi;
	}
>;

export declare const ContextMenu: Component<
	ComponentProps<typeof BaseContextMenu> & {
		api?: IApi;
	}
>;

export declare const Toolbar: Component<
	ComponentProps<typeof BaseToolbar> & {
		api?: IApi;
	}
>;

export declare const Editor: Component<
	ComponentProps<typeof BaseEditor> & {
		api?: IApi;
	}
>;

export declare const Tooltip: Component<{
	content?: Component<{
		data: ITask;
	}>;
	api?: IApi;
	children?: () => any;
}>;

export declare const Willow: Component<{
	fonts?: boolean;
	children?: () => any;
}>;

export declare const WillowDark: Component<{
	fonts?: boolean;
	children?: () => any;
}>;

/* get component events from store actions*/
type RemoveHyphen<S extends string> = S extends `${infer Head}-${infer Tail}`
	? `${Head}${RemoveHyphen<Tail>}`
	: S;

type EventName<K extends string> = `on${RemoveHyphen<K>}`;

export type GanttActions<TMethodsConfig extends Record<string, any>> = {
	[K in keyof TMethodsConfig as EventName<K & string>]?: (
		ev: TMethodsConfig[K]
	) => void;
} & {
	[key: `on${string}`]: (ev?: any) => void;
};
```

#### Styling

Main hooks:

- root/layout: `.wx-gantt`, `.wx-pseudo-rows`, `.wx-stuck`, `.wx-layout`, `.wx-content`
- grid: `.wx-table-container`, `.wx-table`, `.wx-grid`, `.wx-header`, `.wx-body`, `.wx-row`, `.wx-cell`, `.wx-action`, `.wx-toggle-icon`, `.wx-action-icon`
- chart: `.wx-chart`, `.wx-scale`, `.wx-area`, `.wx-bars`, `.wx-bar`, `.wx-task`, `.wx-summary`, `.wx-milestone`, `.wx-content`, `.wx-text-out`
- custom task types: built-ins render as `.wx-task`, `.wx-summary`, `.wx-milestone`; custom task types render as `.wx-task.<customType>`
- task state: `.wx-selected`, `.wx-critical`, `.wx-reorder-task`, `.wx-split`, `.wx-touch`
- progress/links: `.wx-progress-wrapper`, `.wx-progress-percent`, `.wx-progress-marker`, `.wx-link`, `.wx-line`, `.wx-line-selected`, `.wx-delete-link`
- split/rollup/baseline/slack: `.wx-segments`, `.wx-segment`, `.wx-rollup`, `.wx-task-rollup`, `.wx-summary-rollup`, `.wx-milestone-rollup`, `.wx-baseline`, `.wx-slack`, `.wx-slack-task`
- scales/markers/holidays: `.wx-scale`, `.wx-row`, `.wx-cell`, `.wx-weekend`, `.wx-markers`, `.wx-marker`
- companion components: `.wx-gantt-editor`, `.wx-gantt-tooltip`, `.wx-gantt-tooltip-text`, `.wx-tooltip-area`, `.wx-menu`, `.wx-option`
- resizer/display controls: `.wx-resizer`, `.wx-resizer-display-all`, `.wx-resizer-display-grid`, `.wx-resizer-display-chart`, `.wx-button-expand-left`, `.wx-button-expand-right`

Layout defaults:

- the host container must provide height; `.wx-gantt` uses `height: 100%; width: 100%; overflow-y: auto`.
- `.wx-layout` is a flex row with hidden overflow.
- `.wx-table-container` uses `flex: 0 0 <grid width>` and `height: 100%`.
- `.wx-chart` uses `flex: 1 1 auto` with horizontal scrolling.
- `.wx-scale` is sticky at the top of the chart.
- `columns={false}` removes grid and resizer; otherwise grid and chart are split by the resizer.

Important CSS variables:

- bars: `--wx-gantt-bar-font`, `--wx-gantt-bar-border-radius`, `--wx-gantt-bar-shadow`
- tasks: `--wx-gantt-task-color`, `--wx-gantt-task-fill-color`, `--wx-gantt-task-font-color`, `--wx-gantt-task-border`, `--wx-gantt-task-border-color`
- summaries/milestones: `--wx-gantt-summary-color`, `--wx-gantt-summary-fill-color`, `--wx-gantt-summary-font-color`, `--wx-gantt-milestone-color`, `--wx-gantt-milestone-border-radius`
- critical/slack: `--wx-gantt-critical-color`, `--wx-gantt-task-critical-color`, `--wx-gantt-task-critical-fill-color`, `--wx-gantt-task-slack-color`, `--wx-gantt-task-slack-border-color`
- links: `--wx-gantt-link-color`, `--wx-gantt-link-color-hovered`, `--wx-gantt-link-critical-color`, `--wx-gantt-link-critical-color-hovered`, `--wx-gantt-link-marker-background`, `--wx-gantt-link-marker-color`
- grid/scale: `--wx-gantt-border`, `--wx-gantt-select-color`, `--wx-grid-body-font`, `--wx-grid-header-font`, `--wx-timescale-font`, `--wx-timescale-border`, `--wx-timescale-shadow`
- markers/tooltips: `--wx-gantt-marker-color`, `--wx-gantt-marker-font`, `--wx-gantt-marker-font-color`, `--wx-tooltip-background`, `--wx-tooltip-font`, `--wx-tooltip-font-color`

```svelte
<script>
	import { Gantt, Willow } from "@svar-ui/svelte-gantt";
</script>

<div class="gantt-shell">
	<Willow>
		<Gantt {tasks} {links} />
	</Willow>
</div>

<style>
	.gantt-shell {
		height: 100%;
	}

	.gantt-shell .wx-gantt .wx-bar.wx-task.urgent {
		background-color: #f49a82;
		border: 1px solid #f45e36;
	}

	.gantt-shell .wx-gantt .wx-bar.wx-task.urgent .wx-progress-percent {
		background-color: #f45e36;
	}

	.gantt-shell .wx-gantt .my-marker {
		background-color: rgba(255, 84, 84, 0.77);
	}
</style>
```

#### Recipes

##### Basic Gantt With Theme

```svelte
<script>
	import { Gantt, Willow } from "@svar-ui/svelte-gantt";

	const tasks = [
		{ id: 1, text: "Planning", type: "summary", parent: 0, open: true },
		{
			id: 10,
			text: "Research",
			type: "task",
			parent: 1,
			start: new Date(2026, 3, 2),
			duration: 3,
			progress: 50,
		},
	];
	const links = [];
</script>

<div class="gtcell">
	<Willow>
		<Gantt {tasks} {links} />
	</Willow>
</div>

<style>
	.gtcell {
		height: 100%;
	}
</style>
```

##### Toolbar, Context Menu, And Editor

```svelte
<script>
	import { Gantt, Toolbar, ContextMenu, Editor } from "@svar-ui/svelte-gantt";

	let api = $state();
</script>

<Toolbar {api} />

<div class="gtcell">
	<ContextMenu {api}>
		<Gantt bind:this={api} {tasks} {links} {scales} undo />
	</ContextMenu>
	<Editor {api} />
</div>

<style>
	.gtcell {
		height: calc(100% - 50px);
		border-top: var(--wx-gantt-border);
	}
</style>
```

##### Initialize API And Handle Actions

```svelte
<script>
	import { Gantt, Editor } from "@svar-ui/svelte-gantt";

	let api = $state();

	function init(ganttApi) {
		api = ganttApi;

		api.on("add-task", ({ id }) => {
			api.exec("show-editor", { id });
		});

		api.intercept("sort-tasks", ev => {
			return ev.key === "text";
		});
	}
</script>

<Gantt
	{init}
	{tasks}
	{links}
	onupdatetask={ev => console.log(ev.id, ev.task)}
/>
<Editor {api} />
```

##### Custom Columns And Inline Editors

```svelte
<script>
	import { Gantt } from "@svar-ui/svelte-gantt";
	import AvatarCell from "./AvatarCell.svelte";

	const columns = [
		{ id: "text", header: "Task name", width: 220, editor: "text" },
		{ id: "assigned", header: "Assigned", width: 160, cell: AvatarCell },
		{
			id: "start",
			header: ["Start date", { filter: { type: "datepicker" } }],
			align: "center",
			width: 130,
			editor: "datepicker",
		},
		{ id: "add-task", header: "Add task", width: 50, align: "center" },
	];
</script>

<Gantt {tasks} {links} {columns} cellHeight={40} />
```

##### Custom Task Content And Custom Event

```svelte
<!-- TaskContent.svelte -->
<script>
	let { data, onaction } = $props();

	function toggle(ev) {
		ev.stopPropagation();
		onaction({
			action: "custom-click",
			data: { id: data.id, clicked: !data.clicked },
		});
	}
</script>

<button onclick={toggle}>{data.clicked ? "Clicked" : "Click"}</button>
```

```svelte
<script>
	import { Gantt } from "@svar-ui/svelte-gantt";
	import TaskContent from "./TaskContent.svelte";

	let api = $state();
</script>

<Gantt
	bind:this={api}
	{tasks}
	{links}
	taskTemplate={TaskContent}
	oncustomclick={ev =>
		api.exec("update-task", {
			id: ev.id,
			task: { clicked: ev.clicked },
		})}
/>
```

##### Custom Editor Items

```svelte
<script>
	import {
		Gantt,
		Editor,
		getEditorItems,
		registerEditorItem,
		defaultTaskTypes,
	} from "@svar-ui/svelte-gantt";
	import { RadioButtonGroup } from "@svar-ui/svelte-core";

	registerEditorItem("radio", RadioButtonGroup);

	const base = getEditorItems();
	const items = base.map(item =>
		item.key === "type"
			? {
					key: "type",
					comp: "radio",
					label: "Type",
					options: defaultTaskTypes.map(type => ({
						...type,
						value: type.id,
					})),
					config: { type: "inline" },
				}
			: item
	);

	let api = $state();
</script>

<Gantt bind:this={api} {tasks} {links} />
<Editor {api} {items} placement="modal" autoSave={false} />
```

##### Custom Menu Options

```svelte
<script>
	import { Gantt, ContextMenu, Editor, getMenuOptions } from "@svar-ui/svelte-gantt";

	let api = $state();
	const ids = ["cut-task", "copy-task", "paste-task", "delete-task"];
	const options = [
		{ id: "add-task:after", text: "Add below", icon: "wxi-plus" },
		...getMenuOptions().filter(op => ids.includes(op.id)),
		{
			id: "custom-action",
			text: "Custom action",
			icon: "wxi-empty",
			handler: () => console.log("custom action"),
		},
	];
</script>

<ContextMenu
	{api}
	{options}
	onclick={({ context, action }) => console.log(context?.id, action?.id)}
>
	<Gantt bind:this={api} {tasks} {links} />
</ContextMenu>
<Editor {api} />
```

##### Scales, Zoom, Markers, And Holidays

```svelte
<script>
	import { Gantt } from "@svar-ui/svelte-gantt";

	const scales = [
		{ unit: "year", step: 1, format: "%Y" },
		{ unit: "month", step: 1, format: "%F" },
		{ unit: "day", step: 1, format: "%j" },
	];

	const markers = [
		{ start: new Date(2026, 3, 2), text: "Start" },
		{ start: new Date(2026, 3, 8), text: "Review", css: "my-marker" },
	];

	function highlightTime(date, unit) {
		const weekend = date.getDay() === 0 || date.getDay() === 6;
		return unit === "day" && weekend ? "wx-weekend" : "";
	}
</script>

<Gantt
	{tasks}
	{links}
	{scales}
	{markers}
	{highlightTime}
	start={new Date(2026, 3, 1)}
	end={new Date(2026, 4, 1)}
	cellWidth={60}
	zoom
/>
```

##### Pro Feature Bundle

```svelte
<script>
	import {
		Gantt,
		ContextMenu,
		Editor,
		Toolbar,
		Tooltip,
	} from "@svar-ui/svelte-gantt";
	import { Calendar } from "@svar-ui/gantt-store";
	import TooltipContent from "./TooltipContent.svelte";

	const calendar = new Calendar({
		weekHours: {
			monday: 8,
			tuesday: 8,
			wednesday: 8,
			thursday: 8,
			friday: 8,
			saturday: 0,
			sunday: 0,
		},
	});

	let api = $state();
</script>

<Toolbar {api} />
<div class="gtcell">
	<ContextMenu {api}>
		<Tooltip {api} content={TooltipContent}>
			<Gantt
				bind:this={api}
				{tasks}
				{links}
				{calendar}
				baselines
				splitTasks
				rollups={{ type: "closest" }}
				criticalPath={{ type: "flexible" }}
				summary={{ autoProgress: true }}
				undo
			/>
		</Tooltip>
	</ContextMenu>
	<Editor {api} />
</div>
```

##### Server Provider And Lazy Data

```svelte
<script>
	import { Gantt, ContextMenu, Editor } from "@svar-ui/svelte-gantt";
	import { RestDataProvider } from "@svar-ui/gantt-data-provider";

	const provider = new RestDataProvider("/api/gantt");
	let api = $state();
	let tasks = $state([]);
	let links = $state([]);

	provider.getData().then(data => {
		tasks = data.tasks;
		links = data.links;
	});

	function init(ganttApi) {
		api = ganttApi;
		api.setNext(provider);
		api.on("request-data", ev => {
			provider.getData(ev.id).then(data => {
				api.exec("provide-data", { id: ev.id, data });
			});
		});
	}
</script>

<ContextMenu {api}>
	<Gantt {init} bind:this={api} {tasks} {links} />
</ContextMenu>
<Editor {api} />
```

#### Implementation Notes

- `Tooltip.content` is typed as receiving only `{ data }`, but source also passes `segmentIndex` for split-task segment tooltips.
- `show-editor` public action type is `{ id: TID }`, but split-task source also passes `segmentIndex`.
- `Gantt` mutates task objects during date normalization; clone `tasks` before passing them if caller-owned data must remain unchanged.
- `columns` can be `false` for no grid; it is normalized to an empty column set by the store.
- date column templates are added automatically for `start`, `end`, and `duration` unless a column has a custom `template`.
- default `add-task` actions create `{ type: "task", text: _("New Task") }` and usually select or show the new task depending on caller.


## File: tasklist/index.md

> Source: `tasklist/index.md`

Use when building, configuring, styling, localizing, or modifying SVAR Svelte Tasklist / @svar-ui/svelte-tasklist components

#### Package

```js
import { Tasklist } from "@svar-ui/svelte-tasklist";
```

#### Supported functionality

`Tasklist` renders a vertical task list with built-in add, edit, delete, and status controls.

##### Data

- `value` accepts either an `ITask[]` array or a `string | number` key used with `ondata`.
- Without `ondata`, `value` is used as the task array.
- With `ondata`, `ondata(value)` is called only when `value` is truthy; it may return `ITask[]` or a promise.
- While async data is pending, the component renders an empty list in readonly mode.
- `ITask.content` is required; `status` is numeric and `1` marks a completed task in the UI.
- Existing tasks should have stable unique `id` values because rows are keyed by `task.id`.

##### Events and persistence

- `onchange` receives an `IChange` object for `add`, `update`, and `delete`.
- `Tasklist` adds `originalValue` to the event before calling the user handler.
- Add event shape: `{ action: "add", task, value, originalValue }`.
- Update event shape: `{ action: "update", id, task, value, originalValue }`.
- Delete event shape: `{ action: "delete", id, value, originalValue }`.
- `value` is not bindable; use `onchange` to persist `ev.value` in app state or a backend.
- For add only, if `onchange` returns an object or a promise resolving to an object, that object is merged into the newly added task (can't be used to change `id`)

##### Other

- `readonly={true}` hides the add, edit, and delete controls and prevents double-click edit.


#### Public Types

```ts
import type { Component } from "svelte";

export interface IChange {
	action: "add" | "update" | "delete";
	id?: string | number;
	task?: ITask;
	value: ITask[];
	originalValue: string | number | ITask[];
}

export interface ITask {
	id?: string | number;
	content: string;
	status?: number;
}

export declare const Tasklist: Component<{
	ondata?: (value: string | number) => Promise<ITask[]> | ITask[];
	onchange?: (ev: IChange) => void;
	value?: string | number | ITask[];
	readonly?: boolean;
}>;
```

#### Styling
- Parent layout matters: `.wx-tasks-list` is `height: 100%`, so give the containing element an explicit height when scroll behavior matters.
- List container: `.wx-list`
- Task row: `.wx-task`
- Editor textarea class is `.wx-texarea`

```svelte
<div class="tasklist-panel">
	<Tasklist value={tasks} />
</div>

<style>
	.tasklist-panel {
		height: 420px;
		max-width: 768px;
		margin: 20px;
	}

	.tasklist-panel .wx-task {
		padding: 10px 0 6px;
	}

	.tasklist-panel .wx-list {
		gap: 2px;
	}
</style>
```

#### Recipes

##### Basic Tasklist

```svelte
<script>
	import { Tasklist } from "@svar-ui/svelte-tasklist";

	const tasks = [
		{ id: 1, content: "Write project notes", status: 0 },
		{ id: 2, content: "Send status update", status: 1 },
	];
</script>

<div class="tasks">
	<Tasklist value={tasks} />
</div>

<style>
	.tasks {
		height: 360px;
		max-width: 768px;
	}
</style>
```

##### Persist Changes

```svelte
<script>
	import { Tasklist } from "@svar-ui/svelte-tasklist";

	let tasks = $state([]);

	async function onchange(ev) {
		tasks = ev.value;

		if (ev.action === "add") {
			return api.createTask(ev.task);
		}

		if (ev.action === "update") {
			await api.updateTask(ev.id, ev.task);
		}

		if (ev.action === "delete") {
			await api.deleteTask(ev.id);
		}
	}
</script>

<Tasklist value={tasks} {onchange} />
```

##### Resolve Data From A Key

```svelte
<script>
	import { Tasklist } from "@svar-ui/svelte-tasklist";

	let listId = $state(1);
</script>

<Tasklist
	value={listId}
	ondata={id => api.getTasks(id)}
	onchange={({ action, task, id: taskId, originalValue }) =>
		api.saveTaskChange(originalValue, action, task, taskId)}
/>
```

##### Readonly List

```svelte
<script>
	import { Tasklist } from "@svar-ui/svelte-tasklist";

	const tasks = [{ id: 1, content: "Review release notes", status: 0 }];
</script>

<Tasklist value={tasks} readonly={true} />
```


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


## File: filemanager/index.md

> Source: `filemanager/index.md`

Use when building, configuring, styling, or modifying SVAR Svelte Filemanager / @svar-ui/svelte-filemanager components, menus, themes, store actions, or backend data provider integration.

#### Package

```js
import {
	Filemanager,
	Willow,
	WillowDark,
	getMenuOptions,
} from "@svar-ui/svelte-filemanager";
```

#### Supported functionality

##### Components and themes

- `Filemanager` renders the full file explorer: toolbar, search, sidebar tree, cards/table/panels views, preview/info panel, context/action menus, upload drop area, and modals.
- `Willow`, and `WillowDark` wrap matching `@svar-ui/svelte-core` themes and add filemanager CSS variables.
- Theme components accept `fonts?: boolean` and optional Svelte children.
- `Filemanager` has no `children` snippet, slot, `class`, `style`, or `css` passthrough prop.

##### Data model

- `data` is a flat `IEntity[]`; each item must have path-like `id`, such as `"/Code/Button.js"`.
- Root `"/"` is generated internally as a folder named `"My files"`.
- `FileTree.parseId` derives `parent`, `name`, and `ext` from `id`; missing `type` defaults to `"file"`.
- Folder items are the only records rendered in the sidebar tree.
- `date` is expected as a `Date` object for built-in formatting.
- `lazy: true` on a folder triggers `request-data` when the folder path is opened.
- Duplicate create/copy names are made unique by appending `.new` before the extension, for example `"/file.new.txt"`.
- `drive` is optional and only renders storage info when both `used` and `total` are present.

##### Modes and layout

- `mode` supports `"cards"`, `"table"`, `"panels"`, and `"search"`.
- Toolbar mode buttons only expose `"table"`, `"cards"`, and `"panels"`.
- Search runs `filter-files`; non-empty text switches to `"search"` mode and clearing text restores previous `mode` and `panels`.
- `preview` toggles the info pane; on containers narrower than `768px`, preview uses a narrow full-content layout.
- `panels` accepts partial panel state; common fields are `path` and `selected`.
- `activePanel` is `0` or `1` and is used in panels mode and upload drop handling.

##### API and events

- Use `init(api)` for first-time API setup; it is called once after initial store setup.
- `bind:this={api}` exposes the same public methods: `exec`, `on`, `intercept`, `detach`, `setNext`, `getState`, `getReactiveState`, `getStores`, `getFile`, and `serialize`.
- Component event props are generated from store action names by removing hyphens and prefixing `on`, for example `onrequestdata`, `ondownloadfile`, `onopenfile`, `oncreatefile`.
- Event callback payloads are the same objects passed to `api.exec(action, payload)`.
- Action flow is store first, then component event props, then any next bus set by `api.setNext(...)`.
- `api.intercept(action, callback)` can cancel or replace built-in behavior by returning `false`, as shown by backend filtering demos.
- The store mutates some action payloads before downstream handlers/providers: `rename-file.newId`, `create-file.newId`, `copy-files.newIds`, `move-files.newIds`, and `skipProvider` when copy/move into self is rejected.

##### Built-in actions

- Selection/navigation: `select-file`, `set-path`, `set-active-panel`, `open-tree-folder`.
- View/search/sort: `show-preview`, `filter-files`, `set-mode`, `sort-files`.
- File operations: `create-file`, `rename-file`, `delete-files`, `copy-files`, `move-files`.
- Backend/user hooks: `request-data`, `provide-data`, `download-file`, `open-file`.
- Hotkeys use the current `menuOptions` result, so removed menu items also remove their default hotkey behavior.
- Built-in hotkeys include `Ctrl/Cmd+C`, `Ctrl/Cmd+X`, `Ctrl/Cmd+V`, `Ctrl/Cmd+R`, `Ctrl/Cmd+D`, `Delete`, `Enter`, and arrow navigation with Ctrl/Cmd or Shift selection modifiers.

##### Menus

- `menuOptions(mode, item)` receives one of `"folder"`, `"file"`, `"body"`, `"add"`, or `"multiselect"` plus the current item when applicable.
- Return `false`, `null`, `undefined`, or an empty array to suppress a menu for that context.
- Default `"add"` menu: `add-file`, `add-folder`, and `upload` with `comp: "upload"`.
- Default `"body"` menu: `paste`.
- Default `"multiselect"` menu: `copy`, `move`, separator, `delete`.
- Default file menu: `download`, `copy`, `move`, `paste`, separator, `rename`, `delete`.
- Default folder menu omits `download`.
- Root folder context menu is filtered to `paste` only.
- Search mode filters out `paste`.
- Readonly mode hides add controls and edit menus; desktop readonly file menus include only `download`, while narrow mode prepends `preview`.
- Before menu display, item text is localized and `hotkey` is copied to `subtext`; tree-context menu options have `hotkey` cleared.
- Custom menu option `handler` receives a menu pack with `context`; use `context.id` for file operations.
- Filemanager registers the custom menu item type `"upload"` internally through `registerMenuItem("upload", UploadButton)`.

##### Icons, previews, and info

- `icons(file, size)` is used for image URLs in cards/table/info; `size` is `"big"` or `"small"`.
- `icons="simple"` is supported by source and demos and disables image icon URLs, falling back to icon font classes.
- Default icons use `https://cdn.svar.dev/icons/filemanager/vivid/${size}/${icon}.svg`.
- `previews(file, width, height)` is used for card thumbnails and info preview; return a URL string or a falsy value.
- `extraInfo(file)` runs for a single selected item in the info pane; it may return an object, a promise, or null.
- Extra info object entries are appended to the info grid as name/value rows.

##### Saving

- `RestDataProvider` from `@svar-ui/filemanager-data-provider` persists data changes to a REST backend.
- Wire it once with `api.setNext(provider)` in `init`; the provider then forwards every data action (`create-file`, `rename-file`, `move-files`, `copy-files`, `delete-files`) emitted on the event bus as the matching REST call. No per-action save handlers needed.
- Uploads are sent from `create-file` when `ev.file.file` exists; otherwise create sends JSON.
- Initial load and lazy folders use `provider.loadFiles(id)` / `loadInfo(id)`; dispatch results back through `provide-data` for `request-data`.
- Provider emits `"file-renamed"` when backend-generated ids differ from local ids - re-emit `rename-file` with `skipProvider: true` to sync the store.

```js
import { RestDataProvider } from "@svar-ui/filemanager-data-provider";

const provider = new RestDataProvider("/api/files");

function init(api) {
	api.setNext(provider); // forwards all file mutations to REST
}
```

#### Public Types

```ts
import type { Component } from "svelte";
import type { IMenuOption } from "@svar-ui/svelte-menu";

import type {
	TMethodsConfig,
	IApi,
	IConfig,
	TContextMenuType,
	IExtraInfo,
	IParsedEntity,
} from "@svar-ui/filemanager-store";

export * from "@svar-ui/filemanager-store";

export interface IFileMenuOption extends IMenuOption {
	hotkey: string;
}

export type FilePreview = IParsedEntity & {
	type: "file" | "folder" | "search" | "multiple" | "none";
};

export declare const Filemanager: Component<
	{
		readonly?: boolean;
		menuOptions?: (
			mode: TContextMenuType,
			item?: IParsedEntity
		) => IFileMenuOption[];
		extraInfo?: (
			file: IParsedEntity
		) => Promise<IExtraInfo> | IExtraInfo | null;
		icons?: (file: IParsedEntity, size: "big" | "small") => string;
		previews?: (
			file: FilePreview,
			width: number,
			height: number
		) => string | null;
		init?: (api: IApi) => void;
	} & IConfig &
		FilemanagerActions<TMethodsConfig>
>;

export declare const Willow: Component<{
	fonts?: boolean;
	children?: () => any;
}>;

export declare const WillowDark: Component<{
	fonts?: boolean;
	children?: () => any;
}>;

/* get component events from store actions*/
type RemoveHyphen<S extends string> = S extends `${infer Head}-${infer Tail}`
	? `${Head}${RemoveHyphen<Tail>}`
	: S;

type EventName<K extends string> = `on${RemoveHyphen<K>}`;

export type FilemanagerActions<TMethodsConfig extends Record<string, any>> = {
	[K in keyof TMethodsConfig as EventName<K & string>]?: (
		ev: TMethodsConfig[K]
	) => void;
} & {
	[key: `on${string}`]: (ev?: any) => void;
};
```

Important store shapes for wiring handlers, condensed from `store/dist/types`:

```ts
export type TID = string;
export type TContextMenuType =
	| "folder"
	| "file"
	| "body"
	| "add"
	| "multiselect";

export interface IEntity {
	id: TID;
	type?: "file" | "folder";
	size?: number;
	lazy?: boolean;
	date?: Date;
	[key: string]: any;
}

export interface IParsedEntity extends IEntity {
	parent: TID;
	name: string;
	ext: string;
	$level: number;
	open?: boolean;
	data?: IParsedEntity[];
}

export interface IFile {
	name: string;
	date?: Date;
	type?: "file" | "folder";
	size?: number;
	file?: File;
}

export type TMode = "cards" | "table" | "panels" | "search";
export type TActivePanel = 0 | 1;

export interface IPanel {
	path: TID;
	selected: TID[];
	_selected: IParsedEntity[];
	_files: IParsedEntity[];
	_crumbs: IParsedEntity[];
	_sorts: { [key: TID]: { key: string; order: "asc" | "desc" } };
	_lastSelected: TID;
	_selectNavigation: boolean;
}

export interface IConfig {
	data?: IEntity[];
	mode?: TMode;
	drive?: IDrive;
	preview?: boolean;
	panels?: Partial<IPanel>[];
	activePanel?: TActivePanel;
}

export interface IDrive {
	used?: number;
	total?: number;
}

export interface IExtraInfo {
	Size: string;
	Count: string;
	[key: string]: any;
}

type WithActionMeta<T> = T & {
	skipProvider?: boolean;
	[key: string]: any;
};

export type TMethodsConfig = {
	["select-file"]: WithActionMeta<{
		id?: TID;
		toggle?: boolean;
		range?: boolean;
		panel?: TActivePanel;
		type?: "navigation";
	}>;
	["set-path"]: WithActionMeta<{
		id: TID;
		selected?: TID[];
		panel?: TActivePanel;
	}>;
	["set-active-panel"]: WithActionMeta<{ panel: TActivePanel }>;
	["open-tree-folder"]: WithActionMeta<{ id: TID; mode: boolean }>;
	["show-preview"]: WithActionMeta<{ mode: boolean }>;
	["filter-files"]: WithActionMeta<{ text: string }>;
	["set-mode"]: WithActionMeta<{ mode: TMode }>;
	["rename-file"]: WithActionMeta<{ id: TID; name: string; newId?: string }>;
	["create-file"]: WithActionMeta<{
		file: IFile;
		parent: TID;
		newId?: string;
	}>;
	["delete-files"]: WithActionMeta<{ ids: TID[] }>;
	["move-files"]: WithActionMeta<{
		ids: TID[];
		target: TID;
		newIds?: TID[];
	}>;
	["copy-files"]: WithActionMeta<{
		ids: TID[];
		target: TID;
		newIds?: TID[];
	}>;
	["request-data"]: WithActionMeta<{ id: TID }>;
	["provide-data"]: WithActionMeta<{ id: TID; data: IEntity[] }>;
	["download-file"]: WithActionMeta<{ id: TID }>;
	["open-file"]: WithActionMeta<{ id: TID }>;
	["sort-files"]: WithActionMeta<{
		key: string;
		order: "asc" | "desc";
		panel?: TActivePanel;
		path?: string;
	}>;
};
```

#### Styling

- `Filemanager` does not accept `css`, `class`, `className`, or `style`; wrap it in a parent element and target global classes from that parent.
- The root component class is `.wx-filemanager`; it is `display: flex`, `flex-direction: column`, `height: 100%`, `max-width: 100vw`, `max-height: 100vh`, and `overflow: hidden`.
- The parent container must provide a usable height, usually `height: 100%` or a fixed height.
- Theme variables defined by package themes: `--wx-fm-background`, `--wx-fm-box-shadow`, `--wx-fm-select-background`, `--wx-fm-grid-border`, `--wx-fm-grid-header-color`, `--wx-fm-button-font-color`, `--wx-fm-toolbar-height`.
- Other consumed variables include core/theme variables such as `--wx-background`, `--wx-border`, `--wx-color-primary`, `--wx-color-primary-selected`, `--wx-color-font-alt`, `--wx-icon-color`, `--wx-button-background`, `--wx-table-select-background`, and `--wx-table-select-focus-background`.
- Toolbar: `.wx-toolbar`, `.wx-left`, `.wx-right`, `.wx-preview-icon`, `.wx-modes`; height comes from `--wx-fm-toolbar-height`, default theme value `56px`, with `gap: 8px` and `padding: 0 12px`.
- Layout: `.wx-content-wrapper` has `margin-top: 10px`; `.wx-sidebar` is `width: 238px` with `padding: 0 10px 10px`; `.wx-content-item` uses `width: 67%`; `.wx-info` uses `width: 38%`.
- Cards: `.wx-cards` uses flex wrapping and `padding: 30px 20px 10px`; card `.wx-item` is `210px x 200px` with `margin: 0 20px 20px 0`.
- Cards item hooks: `.wx-preview`, `.wx-file-preview`, `.wx-file-icon`, `.wx-card-preview`, `.wx-info`, `.wx-folder-name`, `.wx-file-name`, `.wx-more`, `.wx-back`, `.wx-selected`.
- Table hooks: `.wx-list`, `.wx-grid`, `.wx-row`, `.wx-header`, `.wx-cell`, `.wx-each-cell`; row/header height is configured as `42px`.
- Tree hooks: `.wx-tree`, `.wx-folder`, `.wx-toggle`, `.wx-toggle-placeholder`, `.wx-selected`; folder indentation is inline `padding-left` based on tree level.
- Breadcrumb hooks: `.wx-breadcrumbs`, `.wx-refresh-icon`, `.wx-item`.
- Search hooks: `.wx-search`, `.wx-search-input`, `.wx-icon`, `.wx-text`.
- Preview/info hooks: `.wx-info`, `.wx-info-narrow`, `.wx-wrapper`, `.wx-preview`, `.wx-info-panel`, `.wx-no-info-panel`, `.wx-img-wrapper`, `.wx-icon-wrapper`, `.wx-title`, `.wx-list`, `.wx-name`, `.wx-value`.
- Panels mode hooks: `.wx-panels`; child `.wx-item` uses `width: calc(50% - 10px)` and the first panel has `margin-right: 10px`.
- Upload hooks: `.wx-upload-area`, `.wx-upload-area.wx-active`; active drop background uses `--wx-color-primary-selected`.
- Menu popups come from `@svar-ui/svelte-menu` and use `.wx-menu`, `.wx-option`, `.wx-separator`, `.wx-subtext`, and related menu hooks; the popup is portaled outside the filemanager layout.
- Several classes are generic (`.wx-list`, `.wx-item`, `.wx-wrapper`, `.wx-name`); always scope selectors from a wrapper or a more specific filemanager section.

```svelte
<div class="filemanager">
	<Filemanager {data} {drive} />
</div>

<style>
	.filemanager {
		height: 100%;
		width: 100%;
		--wx-color-primary: rgb(11, 162, 208);
		--wx-fm-background: rgb(207, 209, 221);
		--wx-fm-select-background: rgb(235, 235, 255);
		--wx-table-select-background: rgba(33, 195, 255, 0.1);
		--wx-table-select-focus-background: rgba(33, 195, 255, 0.1);
	}

	.filemanager > .wx-filemanager .wx-cards .wx-back {
		color: rgb(74, 93, 237);
	}
</style>
```

#### Recipes

##### Basic Filemanager

```svelte
<script>
	import { Filemanager, Willow } from "@svar-ui/svelte-filemanager";

	const data = [
		{ id: "/Code", type: "folder", date: new Date(2023, 11, 2, 17, 25) },
		{ id: "/Code/Button.js", type: "file", size: 1177, date: new Date() },
	];

	const drive = {
		used: 15200000000,
		total: 50000000000,
	};
</script>

<Willow>
	<Filemanager {data} {drive} />
</Willow>
```

##### Initial Mode, Path, Selection, And Preview

```svelte
<script>
	import { Filemanager } from "@svar-ui/svelte-filemanager";

	const panels = [
		{ path: "/Code", selected: ["/Code/Button.js"] },
		{ path: "/", selected: ["/Music"] },
	];
</script>

<Filemanager
	{data}
	{drive}
	mode="panels"
	{panels}
	activePanel={0}
	preview
/>
```

##### Handle API And Component Events

```svelte
<script>
	import { Filemanager } from "@svar-ui/svelte-filemanager";

	let api;
	let saved = [];

	function init(fm) {
		api = fm;

		api.on("download-file", ({ id }) => {
			window.open(`/download?id=${encodeURIComponent(id)}`, "_self");
		});

		api.on("open-file", ({ id }) => {
			window.open(`/direct?id=${encodeURIComponent(id)}`, "_blank");
		});
	}

	function serializeCode() {
		saved = api.serialize("/Code");
		api.exec("provide-data", { id: "/Code", data: [] });
	}

	function loadLazy({ id }) {
		fetch(`/files/${encodeURIComponent(id)}`)
			.then(res => res.json())
			.then(data => api.exec("provide-data", { id, data }));
	}
</script>

<button onclick={serializeCode}>Serialize /Code</button>

<Filemanager
	bind:this={api}
	{init}
	{data}
	{drive}
	onrequestdata={loadLazy}
/>
```

##### Customize Context Menus

```svelte
<script>
	import { Filemanager, getMenuOptions } from "@svar-ui/svelte-filemanager";

	let api;

	function init(fm) {
		api = fm;
	}

	function menuOptions(mode, item) {
		if ((mode === "file" || mode === "folder") && item.id === "/Code") {
			return false;
		}

		if (mode === "file" || mode === "folder") {
			return [
				...getMenuOptions(mode),
				{ comp: "separator" },
				{
					id: "clone",
					text: "Clone",
					icon: "wxi-content-copy",
					hotkey: "Ctrl+Shift+V",
					handler: ({ context }) => {
						const { panels, activePanel } = api.getState();
						api.exec("copy-files", {
							ids: [context.id],
							target: panels[activePanel].path,
						});
					},
				},
			];
		}

		return getMenuOptions(mode);
	}
</script>

<Filemanager {data} {drive} {init} {menuOptions} />
```

##### Use Server Data And RestDataProvider

```svelte
<script>
	import { Filemanager } from "@svar-ui/svelte-filemanager";
	import { RestDataProvider } from "@svar-ui/filemanager-data-provider";

	const server = "https://example.com/api";
	const provider = new RestDataProvider(server);

	let api;
	let data = $state([]);
	let drive = $state({});

	function init(fm) {
		api = fm;
		api.setNext(provider);

		api.on("download-file", ({ id }) => {
			window.open(`${server}/direct?id=${encodeURIComponent(id)}&download=true`, "_self");
		});

		api.on("open-file", ({ id }) => {
			window.open(`${server}/direct?id=${encodeURIComponent(id)}`, "_blank");
		});
	}

	function loadData({ id }) {
		provider.loadFiles(id).then(files => {
			api.exec("provide-data", { id, data: files });
		});
	}

	provider.on("file-renamed", ({ id, newId }) => {
		const name = newId.slice(newId.lastIndexOf("/") + 1);
		api.exec("rename-file", { id, name, skipProvider: true });
	});

	Promise.all([provider.loadFiles(), provider.loadInfo()]).then(([files, info]) => {
		data = files;
		drive = info;
	});
</script>

<Filemanager {init} {data} {drive} onrequestdata={loadData} />
```

##### Custom Icons, Previews, And Extra Info

```svelte
<script>
	import { Filemanager } from "@svar-ui/svelte-filemanager";
	import { formatSize } from "@svar-ui/filemanager-store";

	const server = "https://example.com/api";

	function icons(file, size) {
		const name = file.type === "file" ? file.ext : file.type;
		return `${server}/icons/${size}/${name}.svg`;
	}

	function previews(file, width, height) {
		if (file.ext === "png" || file.ext === "jpg" || file.ext === "jpeg") {
			return `${server}/preview?width=${width}&height=${height}&id=${encodeURIComponent(file.id)}`;
		}
		return null;
	}

	function extraInfo(file) {
		if (file.type === "folder") {
			return { Size: formatSize(file.size || 0), Count: "folder" };
		}
		return null;
	}
</script>

<Filemanager {data} {drive} {icons} {previews} {extraInfo} preview />
```

##### Backend Search Intercept

```svelte
<script>
	import { Filemanager } from "@svar-ui/svelte-filemanager";

	let api;

	function init(fm) {
		api = fm;

		api.intercept("filter-files", ({ text }) => {
			const { panels, activePanel } = api.getState();
			const id = panels[activePanel].path;

			fetch(`/files/${encodeURIComponent(id)}?text=${text || ""}`)
				.then(res => res.json())
				.then(data => {
					api.exec("set-mode", { mode: text ? "search" : "cards" });
					api.exec("provide-data", { id, data });
				});

			return false;
		});
	}
</script>

<Filemanager {init} {data} {drive} />
```

##### Localize Filemanager

```svelte
<script>
	import { Locale } from "@svar-ui/svelte-core";
	import { cn } from "@svar-ui/filemanager-locales";
	import { cn as cnCore } from "@svar-ui/core-locales";
	import { Filemanager } from "@svar-ui/svelte-filemanager";
</script>

<Locale words={{ ...cn, ...cnCore }}>
	<Filemanager {data} {drive} />
</Locale>
```

#### Implementation Notes

- `Filemanager.svelte` stores all unknown props in `restProps` for generated action callbacks; unknown props are not spread onto DOM.
- Source supports `icons="simple"`, but the declaration types `icons` only as a function.
- Source default `icons` can return `false` for folders, but the declaration says `string`.
- Source accepts falsy `previews` return values, but the declaration says `string | null`.
- `menuOptions` can suppress menus with falsy returns, but the declaration says it returns `IFileMenuOption[]`.
- Store source `IMenuOption.id` is `string | number`, while generated `store/dist/types/types.d.ts` has `id?: string`.
- `RestDataProvider.loadFiles()` and `loadInfo()` are called without arguments in demos, but generated provider declarations require `id: TID`.
- `DataStore` mutates the input file objects during parse by adding `parent`, `name`, `ext`, default `type`, and tree state fields.
- Context/action menus and tests rely on ids encoded by `setID`; use raw file ids in app code and let the library set data attributes.
- `registerMenuItem("upload", UploadButton)` runs inside `Sidebar.svelte`; a custom `"upload"` add item only works through the built-in sidebar add menu.
- `extraInfo` errors are caught and logged, then ignored.
- In readonly mode, hotkeys use readonly menu options, so edit hotkeys do not open modals.
