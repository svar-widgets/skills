Use when building, configuring, styling, or modifying SVAR React Editor / @svar-ui/react-editor forms, field items, validation, save flows, panels, toolbars, sections, batches, or custom editor item renderers.

## Package

```js
import {
	Editor,
	registerEditorItem,
	Willow,
	WillowDark,
} from "@svar-ui/react-editor";
import "@svar-ui/react-menu/all.css";
```

## Supported functionality

### Components

- `Editor` - main editor shell with inline, sidebar, or modal placement, optional top/bottom toolbars, sections, columns layout, validation, hotkeys, and save flow.
- `registerEditorItem(type, handler)` - registers a React component for `item.comp`.
- `Willow`, `WillowDark` - wrappers around matching `@svar-ui/react-core` themes

### Built-in item components

- `text` - registered to `Text` from `@svar-ui/react-core`; default when `comp` is omitted.
- `textarea` - registered to `TextArea` from `@svar-ui/react-core`.
- `checkbox` - registered to `Checkbox` from `@svar-ui/react-core`.
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

- `item.comp` can be a registered string or a React component directly, use `registerEditorItem` to link component to string
- Normal field components receive `value`, `onChange`, `error`, all item fields, and promoted `config` fields; `label` is set to `undefined`
- `section` and `readonly` receives all item fields, and `onClick` for section toggling.
- A custom item must call `onChange({ value })`; it may include `input` to mark input-origin (in-progress) updates.

### Values and binding

- `values` is an object; each rendered editor reads and writes `values[item.key]`
- String keys containing dots use nested getter/setter functions, for example `key: "user.name"` reads/writes `values.user.name`.
- `config` is shallow-merged into the item before rendering, so `config: { placeholder: "Name" }` becomes a direct prop.
- Custom `getter` and `setter` functions on an item replace the default key access.
- `labelTemplate(value)` replaces the displayed label for normal fields.
- `options` are passed through to item components and are also used by `readonly` to map `value` to `option.label` by matching `option.id`.

### Events and save flow

- Field change order: child item `onChange({ value, input? })` -> editor `onChange({ key, value, update, input? })` -> diff/validation -> save handling.
- `onChange` can replace `ev.update` to update multiple fields from one field change.
- With `autoSave={true}`, valid changes are written back to the original `values` object and `onSave({ changes, values })` fires immediately.
- With `autoSave={false}`, changed keys stay in `notSaved` until "save" button click ( toolbar item `id: "save"` ) runs validation and save.
- Toolbar action order: internal save or section toggle is handled first, then `onAction({ item, values, changes })` fires.
- Parent code must hide modal/sidebar editors in `onAction`; `cancel`, `close`, and custom actions do not remove the component themselves.
- `onValidation({ errors, values })` fires when validation result changes; `errors` can be `null`.
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
- `topBar` and `bottomBar` accept `false`, `true`, or `{ items: IToolbarItem[] }`; toolbar items are passed to `@svar-ui/react-toolbar`.
- Automatic default bars are generated only when `topBar === true && bottomBar === true`.
- Automatic manual-save modal uses bottom `{ spacer, save, cancel }`; modal columns use top `{ spacer, save, cancel }`; inline/sidebar manual save uses top `{ spacer, cancel, save }`; auto-save and read-only use top `{ spacer, close }`.
- Toolbar `onChange({ item, value })` is mapped into editor field changes as `{ key: item.key, value }`, so toolbar controls can edit `values`.
- Default hotkeys are enabled unless `hotkeys={false}`: `ctrl+s` triggers save, `escape` triggers cancel/close, and `delete` triggers a `delete` toolbar item when present.
- Custom `hotkeys` are merged with defaults.
- `focus={true}` selects and focuses the first enabled input, textarea, or select after mount.
- Editor `children` render above generated fields inside the content area; demos use this for tabs, segmented controls, and external toolbars.

## Public Types

```ts
import type { ComponentType, ReactNode } from "react";
import type { IToolbarItem } from "@svar-ui/react-toolbar";

export declare const Editor: ComponentType<{
	values?: Record<string, any>;
	items?: {
		comp?: string | ComponentType<any>;
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
	onChange?: (ev: {
		key: string;
		value: any;
		update: Record<string, any>;
		input?: boolean;
	}) => void;
	onSave?: (ev: {
		changes: string[];
		values: Record<string, any>;
	}) => void;
	onAction?: (ev: {
		item: IToolbarItem;
		values: Record<string, any>;
		changes: string[];
	}) => void;
	onValidation?: (ev: {
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
	children?: ReactNode;
}>;

export declare function registerEditorItem(
	type: string,
	handler: ComponentType<any>
): void;

export declare const Willow: ComponentType<{
	fonts?: boolean;
	children?: ReactNode;
}>;

export declare const WillowDark: ComponentType<{
	fonts?: boolean;
	children?: ReactNode;
}>;
```

## Styling

Import the package CSS before using the component (`all.css` includes dependency styles, `style.css` is this component only)

- `Editor` `css` is appended to the root panel: `.wx-inline-form {css}` for inline placement, `.wx-panel {css}` for modal/sidebar placement.
- Root panel classes: `.wx-inline-form`, `.wx-panel`.
- Content container: `.wx-content`; columns mode adds `.wx-layout-columns`.
- Form body: `.wx-sections` with `--wx-field-width: 600px`.
- Columns layout: `.wx-cols`, `.wx-left`, `.wx-right`; source defaults include `.wx-left { min-width: 640px }`, `.wx-right { width: 364px; background: var(--wx-background-alt) }`.
- Toolbar wrapper: `.wx-editor-toolbar`, `.wx-topbar`, `.wx-bottom`
- Section header: `.wx-section`, `.wx-section-active`, nested `.wx-icon`
- Validation and empty states: `.wx-message`, `.wx-overlay`

```jsx
import "./TaskEditor.css";

<Editor items={items} values={values} layout="columns" css="task-editor" />

/* TaskEditor.css
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
*/
```

## Recipes

### Basic Inline Editor

```jsx
import { useState } from "react";
import { Editor } from "@svar-ui/react-editor";

function BasicEditor() {
	const items = [
		{ comp: "text", key: "name", label: "Name" },
		{ comp: "checkbox", key: "admin", label: "Is Admin" },
		{ comp: "textarea", key: "descr", label: "Description" },
	];

	const [values, setValues] = useState({
		name: "John Doe",
		admin: true,
		descr: "Notes",
	});

	return <Editor items={items} values={values} topBar={false} />;
}
```

### Manual Save With Validation

```jsx
import { useState } from "react";
import { Editor } from "@svar-ui/react-editor";

function ManualSaveEditor() {
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

	const [values, setValues] = useState({ firstName: "John", email: "john@example.org" });
	const [visible, setVisible] = useState(true);

	function handleAction({ item, changes }) {
		if (item.id === "save" && changes.length) return;
		setVisible(false);
	}

	function handleSave({ values: next }) {
		setValues(next);
		setVisible(false);
	}

	return visible && (
		<Editor
			placement="sidebar"
			autoSave={false}
			items={items}
			values={values}
			onAction={handleAction}
			onSave={handleSave}
		/>
	);
}
```

### Auto Save Sidebar With Custom Toolbar

```jsx
import { useState } from "react";
import { Editor } from "@svar-ui/react-editor";

function AutoSaveEditor() {
	const items = [
		{ comp: "text", key: "label", label: "Label" },
		{ comp: "textarea", key: "description", label: "Description" },
	];

	const [values, setValues] = useState({ id: 1, label: "Task", description: "" });
	const [open, setOpen] = useState(true);

	function handleAction({ item }) {
		if (item.id === "close" || item.id === "delete") setOpen(false);
	}

	function handleSave({ values: next }) {
		setValues(next);
	}

	return open && (
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
			items={items}
			values={values}
			onAction={handleAction}
			onSave={handleSave}
		/>
	);
}
```

### Update Multiple Values From One Change

```jsx
import { useState } from "react";
import { Editor, registerEditorItem } from "@svar-ui/react-editor";
import { Combo } from "@svar-ui/react-core";

registerEditorItem("combo", Combo);

function MultiUpdateEditor() {
	const [items, setItems] = useState([
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

	const [values, setValues] = useState({ country: "", city: "" });

	function handleChange(ev) {
		if (ev.key !== "country") return;

		setItems(prev => {
			const next = [...prev];
			next[1] = {
				...next[1],
				disabled: false,
				options: cities[ev.value],
			};
			return next;
		});

		ev.update = {
			country: ev.value,
			city: "",
		};
	}

	return <Editor items={items} values={values} onChange={handleChange} topBar={false} />;
}
```

### Register A Custom Item

```jsx
// PriorityCombo.jsx
import { Combo } from "@svar-ui/react-core";

function PriorityCombo({ value, options, onChange, ...restProps }) {
	return (
		<Combo value={value} options={options} onChange={onChange} {...restProps}>
			{({ option }) => (
				<>
					<span className="priority-dot" style={{ background: option.color }}></span>
					{option.label}
				</>
			)}
		</Combo>
	);
}

export default PriorityCombo;
```

```jsx
import { useState } from "react";
import { Editor, registerEditorItem } from "@svar-ui/react-editor";
import PriorityCombo from "./PriorityCombo.jsx";

registerEditorItem("priority-combo", PriorityCombo);

function CustomItemEditor() {
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

	const [values, setValues] = useState({ priority: 1 });

	return <Editor items={items} values={values} topBar={false} />;
}
```

### Sections And Accordion Panels

```jsx
import { useState } from "react";
import { Editor } from "@svar-ui/react-editor";

function AccordionEditor() {
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

	const [values, setValues] = useState({ name: "John", admin: false });

	return <Editor items={items} values={values} topBar={false} />;
}
```

### Batch Switcher In Children

```jsx
import { useState } from "react";
import { Editor } from "@svar-ui/react-editor";
import { Segmented } from "@svar-ui/react-core";

function BatchEditor() {
	const options = [
		{ id: "main", label: "Personal" },
		{ id: "cfg", label: "Settings" },
	];

	const items = [
		{ comp: "text", key: "name", label: "Name", batch: "main" },
		{ comp: "textarea", key: "descr", label: "Description", batch: "main" },
		{ comp: "checkbox", key: "admin", label: "Is Admin", batch: "cfg" },
	];

	const [values, setValues] = useState({ name: "John", descr: "", admin: false });
	const [activeBatch, setActiveBatch] = useState("main");

	return (
		<Editor topBar={false} items={items} values={values} activeBatch={activeBatch}>
			<Segmented options={options} value={activeBatch} onChange={({ value }) => setActiveBatch(value)} />
		</Editor>
	);
}
```

### Modal Columns Layout

```jsx
import { useState } from "react";
import { Editor } from "@svar-ui/react-editor";

function ModalColumnsEditor() {
	const items = [
		{ comp: "text", key: "name", label: "Name", column: "left" },
		{ comp: "textarea", key: "descr", label: "Description", column: "left" },
		{ comp: "checkbox", key: "admin", label: "Is Admin" },
	];

	const [values, setValues] = useState({ name: "John", descr: "", admin: false });
	const [visible, setVisible] = useState(true);

	return visible && (
		<Editor
			placement="modal"
			layout="columns"
			autoSave={false}
			items={items}
			values={values}
			onAction={() => setVisible(false)}
		/>
	);
}
```

## Implementation Notes

- `onValidation` can receive `errors: null`
- Dot-path keys assume intermediate objects already exist for default getter/setter access.
- `config` is promoted into top-level item props and also remains as `item.config`.
- `readonly={true}` converts every rendered item to the built-in `readonly` renderer.
- `Action` toolbar items with `id: "save"` are special; other IDs are forwarded through `onAction`
- `SideArea` cancel trigger `onAction` with `item.id === "close"`.
