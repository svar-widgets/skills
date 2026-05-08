Use when UI of app requires Menu, MenuBar, DropDownMenu, ContextMenu, or ActionMenu / @svar-ui/react-menu components

Styles must be imported separately:

## Package

```js
import {
	Menu,
	MenuBar,
	DropDownMenu,
	ContextMenu,
	ActionMenu,
	registerMenuItem,
} from "@svar-ui/react-menu";
import "@svar-ui/react-menu/all.css";
```

## Components

- `Menu` - low-level popup menu positioned from `parent` or `left`/`top`
- `DropDownMenu` - wraps trigger content, opens a menu on click
- `ContextMenu` - wraps content, opens an action menu on `contextmenu`
- `ActionMenu` - reusable menu controller; wraps clickable content or opened with `ref` and `show(ev, obj)`
- `MenuBar` - horizontal menu bar; top-level items with `data` open submenus through an internal `ActionMenu`

## Supported functionality

### Events

- option `handler`, component `onClick`
- leaf click order: `option.handler(pack)` first, then component `onClick(pack)`, where `pack` is `{ context, option, event }`
- submenu parent options do not fire `onClick`; hover/click opens the child menu
- clicking outside an open menu calls `onClick({ action: null, option: null })`

### Positioning

`at` defaults to `"bottom"` and is passed to `calculatePosition` from `@svar-ui/lib-dom`

- options: `bottom`, `right`, `left`, `top`, `bottom-right`, `bottom-left`, `bottom-fit`, `point`
- submenus internally use `at="right-overlap"`

### Context resolution (ContextMenu, ActionMenu)

- `ActionMenu.show(ev, obj)` opens from event target, sets cursor coordinates from `ev.clientX/Y`, uses `obj` as `context`
- without `obj`, locates context from a data attribute derived from `dataKey`; default `dataKey="contextId"` means `data-context-id`
- `resolver(item, event)` can replace or reject context; falsy return prevents menu opening
- `filter(option, item)` hides leaf options for a context; groups remain only when filtered children remain

### Option's properties

- `comp` - component name; built-in is `separator`; can also be a registered string renderer or a React component
- `id` - stable key returned in callbacks and used by keyed rendering; missing ids generated during normalization
- `text`, `subtext` - default label and right-side helper text
- `icon` - appended to `wx-icon`, e.g. `"wxi wxi-content-copy"`
- `data` - creates nested submenu options
- `disabled` - adds `wx-disabled`, blocks pointer interaction
- `css` - appended to option wrapper `.wx-option`
- `handler` - per-option click handler
- deprecated `type` is copied to `comp`
- custom item components receive `option` object with all configured props

### Common option configurations

```js
{ id: "edit", text: "Edit", icon: "wxi wxi-edit" }
{ id: "delete", text: "Delete", disabled: true }
{ id: "copy", text: "Copy", subtext: "Ctrl+C" }
{ id: "add", text: "Add", data: [/* submenu options */] }
{ comp: "separator" }
```

Custom renderers can be registered with `registerMenuItem("user", UserMenuItem)` and referenced as `comp: "user"`, or `comp` can be set to a React component directly.

## Public Types

```ts
import type { ComponentType, ReactNode } from "react";

export interface IMenuOption {
	id?: string | number;
	text?: string;
	subtext?: string;
	handler?: (ev: IMenuOptionClick) => void;
	data?: IMenuOption[];
	css?: string;
	icon?: string;
	disabled?: boolean;
	comp?: string | ComponentType<any>;
}

export interface IMenuOptionClick {
	context?: any;
	option: IMenuOption;
	event?: MouseEvent;
}

export declare const Menu: ComponentType<{
	options?: IMenuOption[];
	left?: number;
	top?: number;
	at?: string;
	parent?: HTMLElement;
	mount?: (callback: () => void) => void;
	context?: any;
	css?: string;
	onClick?: (ev: IMenuOptionClick) => void;
}>;

export declare const MenuBar: ComponentType<{
	css?: string;
	menuCss?: string;
	options?: IMenuOption[];
	onClick?: (ev: IMenuOptionClick) => void;
}>;

export declare const DropDownMenu: ComponentType<{
	options?: IMenuOption[];
	at?: string;
	css?: string;
	children?: ReactNode;
	onClick?: (ev: IMenuOptionClick) => void;
}>;

export declare const ContextMenu: ComponentType<{
	options?: IMenuOption[];
	at?: string;
	resolver?: (item: any, event: MouseEvent) => any;
	dataKey?: string;
	filter?: (option: IMenuOption, item: any) => boolean;
	css?: string;
	children?: ReactNode;
	onClick?: (ev: IMenuOptionClick) => void;
}>;

export declare const ActionMenu: ComponentType<{
	options?: IMenuOption[];
	at?: string;
	resolver?: (item: any, event: MouseEvent) => any;
	dataKey?: string;
	filter?: (option: IMenuOption, item: any) => boolean;
	css?: string;
	children?: ReactNode;
	onClick?: (ev: IMenuOptionClick) => void;
}>;

export declare function registerMenuItem(
	type: string,
	handler: ComponentType<{ option?: any }>
): void;
```

## Styling

Import the package CSS before using the component (`all.css` includes dependency styles, `style.css` is this component only)

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

## Recipes

### Dropdown With Click Handler

```jsx
import { DropDownMenu } from "@svar-ui/react-menu";

function DropdownExample() {
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

	return (
		<DropDownMenu options={options} onClick={clicked} at="bottom-fit">
			<button>Open</button>
		</DropDownMenu>
	);
}
```

### Low-Level Menu Anchored To An Element

```jsx
import { useState } from "react";
import { Menu } from "@svar-ui/react-menu";

function AnchoredMenu() {
	const options = [{ id: "copy", text: "Copy" }];
	const [parent, setParent] = useState(null);

	function clicked() {
		setParent(null);
	}

	return (
		<>
			<button onClick={ev => setParent(ev.currentTarget)}>Open</button>

			{parent && <Menu options={options} parent={parent} at="right" onClick={clicked} />}
		</>
	);
}
```

### Menu Bar With Submenus

```jsx
import { MenuBar } from "@svar-ui/react-menu";

function AppMenuBar() {
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

	return (
		<MenuBar
			options={options}
			css="app-menubar"
			menuCss="app-menu"
			onClick={ev => console.log(ev.option?.id)}
		/>
	);
}
```

### Context Menu With Resolver And Filter

```jsx
import { ContextMenu } from "@svar-ui/react-menu";

function ContextMenuExample() {
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

	return (
		<ContextMenu
			options={options}
			at="point"
			resolver={resolver}
			filter={filter}
			onClick={ev => console.log(ev.context, ev.option?.id)}
		>
			{rows.map(row => (
				<div key={row.id} data-context-id={row.id}>{row.name}</div>
			))}
		</ContextMenu>
	);
}
```

### Programmatic Action Menu

```jsx
import { useRef, useState } from "react";
import { ActionMenu } from "@svar-ui/react-menu";

function ProgrammaticMenu() {
	const options = [
		{ id: "a", text: "Project A" },
		{ id: "b", text: "Project B" },
	];

	const [selected, setSelected] = useState(["a", "b"]);
	const menuRef = useRef(null);

	function markSelected(option, index) {
		option.icon = option.id === selected[index] ? "wxi-check" : "wxi-empty";
		return true;
	}

	function clicked(ev) {
		if (ev.option) {
			setSelected(prev => {
				const next = [...prev];
				next[ev.context] = ev.option.id;
				return next;
			});
		}
	}

	return (
		<>
			<ActionMenu options={options} filter={markSelected} onClick={clicked} ref={menuRef} />

			{selected.map((value, index) => (
				<button key={index} onClick={ev => menuRef.current.show(ev, index)}>{value}</button>
			))}
		</>
	);
}
```

### Custom Menu Item Renderer

```jsx
// UserMenuItem.jsx
function UserMenuItem({ option }) {
	return <div className="user-option">{option.name}</div>;
}

export default UserMenuItem;
```

```jsx
import { DropDownMenu, registerMenuItem } from "@svar-ui/react-menu";
import AddUserItem from "./AddUserItem.jsx";
import UserMenuItem from "./UserMenuItem.jsx";

registerMenuItem("user", UserMenuItem);

function UserMenu() {
	const options = [
		{ id: "u1", comp: "user", name: "Alex Wolensy" },
		{ id: "add", comp: AddUserItem, name: "Add New" },
	];

	return (
		<DropDownMenu options={options}>
			<button>Select user</button>
		</DropDownMenu>
	);
}
```

## Implementation Notes

- `ActionMenu` and `ContextMenu` ignore events whose target has `data-menu-ignore`
- `dataKey` is converted from camelCase to kebab-case for DOM attribute lookup
- `ActionMenu.show(null)` closes the active menu
- `onClick` can receive `{ option: null }`
- runtime options can carry extra fields for custom renderers
