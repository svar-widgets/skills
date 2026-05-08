Use when building, configuring, styling, or modifying SVAR Svelte Editor / @svar-ui/svelte-editor forms, field items, validation, save flows, panels, toolbars, sections, batches, or custom editor item renderers.

## Package

```js
import {
	Editor,
	registerEditorItem,
	Willow,
	WillowDark,
} from "@svar-ui/svelte-editor";
```

## Supported functionality

### Components

- `Editor` - main editor shell with inline, sidebar, or modal placement, optional top/bottom toolbars, sections, columns layout, validation, hotkeys, and save flow.
- `registerEditorItem(type, handler)` - registers a Svelte component for `item.comp`.
- `Willow`, `WillowDark` - wrappers around matching `@svar-ui/svelte-core` themes

### Built-in item components

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

### External and custom item components

- `item.comp` can be a registered string or a Svelte component directly, use `registerEditorItem` to link component to string
- Normal field components receive `value`, `onchange`, `error`, all item fields, and promoted `config` fields; `label` is set to `undefined`
- `section` and `readonly` receives all item fields, and `onclick` for section toggling.
- A custom item must call `onchange({ value })`; it may include `input` to mark input-origin (in-progress) updates.

### Values and binding

- `values` is an object; each rendered editor reads and writes `values[item.key]`
- String keys containing dots use nested getter/setter functions, for example `key: "user.name"` reads/writes `values.user.name`.
- `config` is shallow-merged into the item before rendering, so `config: { placeholder: "Name" }` becomes a direct prop.
- Custom `getter` and `setter` functions on an item replace the default key access.
- `labelTemplate(value)` replaces the displayed label for normal fields.
- `options` are passed through to item components and are also used by `readonly` to map `value` to `option.label` by matching `option.id`.

### Events and save flow

- Field change order: child item `onchange({ value, input? })` -> editor `onchange({ key, value, update, input? })` -> diff/validation -> save handling.
- `onchange` can replace `ev.update` to update multiple fields from one field change.
- With `autoSave={true}`, valid changes are written back to the original `values` object and `onsave({ changes, values })` fires immediately.
- With `autoSave={false}`, changed keys stay in `notSaved` until "save" button click ( toolbar item `id: "save"` ) runs validation and save.
- Toolbar action order: internal save or section toggle is handled first, then `onaction({ item, values, changes })` fires.
- Parent code must hide modal/sidebar editors in `onaction`; `cancel`, `close`, and custom actions do not remove the component themselves.
- `onvalidation({ errors, values })` fires when validation result changes; `errors` can be `null`.
- Runtime `changes` is an array of changed keys

### Validation

- `required: true` fails when `!values[key]`
- `validation(value)` must return truthy for valid values.
- `validationMessage` overrides the displayed error text.
- Required errors use `{ errorType: "required" }`; custom validation errors use `{ errorType: "validation" }`.

### Sections and batches

- A `section` item toggles all items whose `section` equals the section item `key`.
- `activeSection: true` opens a section initially.
- Normal sections can be toggled independently.
- `sectionMode: "accordion"` opens one section and closes other sections; an open accordion section does not close itself on click.
- `sectionMode: "exclusive"` shows only the active section header and its children.
- `activeBatch` hides every item whose `batch` does not equal `activeBatch`; when `activeBatch` is set, items without a matching `batch` are hidden.

### Layout, placement, toolbar, and hotkeys

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

## Public Types

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

## Styling

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

## Recipes

### Basic Inline Editor

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

### Manual Save With Validation

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

### Auto Save Sidebar With Custom Toolbar

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

### Update Multiple Values From One Change

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

### Register A Custom Item

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

### Sections And Accordion Panels

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

### Batch Switcher In Children

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

### Modal Columns Layout

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

## Implementation Notes

- `onvalidation` can receive `errors: null`
- Dot-path keys assume intermediate objects already exist for default getter/setter access.
- `config` is promoted into top-level item props and also remains as `item.config`.
- `readonly={true}` converts every rendered item to the built-in `readonly` renderer.
- `Action` toolbar items with `id: "save"` are special; other IDs are forwarded through `onaction`
- `SideArea` cancel trigger `onaction` with `item.id === "close"`.
