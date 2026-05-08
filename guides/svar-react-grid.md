# svar-react — grid

_Generated 2026-05-08T13:35:37.052Z_

## Contents

- [`grid/index.md`](#file-grid-index-md)
- [`locales.md`](#file-locales-md)
- [`themes.md`](#file-themes-md)


## File: grid/index.md

> Source: `grid/index.md`

Use when building, configuring, styling, or modifying SVAR React Grid / @svar-ui/react-grid data tables, toolbars, context menus, themes, inline editors, filters, sorting, selection, tree data, responsive layouts, export, or print behavior.

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
} from "@svar-ui/react-grid";
import "@svar-ui/react-grid/all.css";
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
- `selectedRows` is an initial/sync prop passed into the store; read live selection with `api.getState().selectedRows`, `api.getReactiveState().selectedRows`, or `onSelectRow`.
- Custom checkbox cells should call `api.exec("select-row", { id: row.id, toggle: true, mode: value })` and wrap the control in `data-action="ignore-click"` when row click selection should not fire.

##### Events And API

- Use `ref={apiRef}` or `init={api => ...}` to access the grid API.
- API methods: `exec`, `on`, `intercept`, `detach`, `getState`, `getReactiveState`, `setNext`, `getStores`, `getRow`, `getColumn`.
- Action names are exposed as prop callbacks by removing hyphens and prefixing `on` (camelCase in React): `select-row` -> `onSelectRow`, `request-data` -> `onRequestData`.
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
- `filter.config` is forwarded to the underlying React Core control.
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

- `column.cell` receives `{ api, row, column, onAction }`.
- Header/footer `cell` receives `{ api, cell, column, row, onAction }`.
- Calling `onAction({ action, data })` inside a custom cell executes `api.exec(action, data)`.
- Custom action names are routed to prop callbacks, for example `onAction({ action: "custom-check", data })` -> `onCustomCheck={...}`.
- `overlay` can be text or a component; overlay components receive `onAction`.
- `Tooltip` can use default cell text, `column.tooltip(row)`, or `content={Component}`; tooltip content receives `{ data }`.

##### Toolbar And Menus

- `Toolbar` wraps `@svar-ui/react-toolbar` and defaults to `defaultToolbarButtons`.
- `Toolbar` auto-runs `handleAction(api, item.id)` before calling its own `onClick`.
- Default toolbar actions: `add-row`, `open-editor`, `delete-row`, `copy-row`, `cut-row`, `paste-row`, `move-item:up`, `move-item:down`, `undo`, `redo`.
- `Toolbar` filters move actions when `reorder` is off and undo/redo when `undo` is off.
- `ContextMenu` wraps `@svar-ui/react-menu` and defaults to `defaultMenuOptions`.
- `ContextMenu` defaults `at="point"` and uses row `data-context-id` through the base menu's default `dataKey`.
- The default resolver selects the right-clicked row if it is not already selected.
- `ContextMenu` auto-runs `handleAction(api, ev.action.id)` before calling its own `onClick`; base menu events also expose `ev.option`.
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
- Theme wrappers delegate to `@svar-ui/react-core` and add grid CSS variables to `.wx-material-theme`, `.wx-willow-theme`, or `.wx-willow-dark-theme`.
- If no `wx-theme` context exists, the store calls `suggestSkin()` and defaults to Willow.

#### Public Types

```ts
import type { ComponentType, ComponentProps, ReactNode } from "react";
import { ContextMenu as BaseContextMenu } from "@svar-ui/react-menu";
import { Toolbar as BaseToolbar } from "@svar-ui/react-toolbar";

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
		cell?: ComponentType<{
			data: any;
			onAction: (ev: {
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
	onAction: (ev: { action?: any; data?: { [key: string]: any } }) => void;
}

export interface IHeaderCellConfig extends IHeaderCell {
	cell?: ComponentType<
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
	cell?: ComponentType<ICellProps>;
	editor?: TEditorType | IColumnEditorConfig | TEditorHandlerConfig;
	header?: TColumnHeaderConfig;
	footer?: TColumnHeaderConfig;
}

export declare const Grid: ComponentType<
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

		overlay?: string | ComponentType;
		columns: IColumnConfig[];
		hotkeys?:
			| false
			| { [key: string]: ((e?: KeyboardEvent) => void) | boolean };
	} & IConfig &
		GridActions<TMethodsConfig>
>;

export declare const HeaderMenu: ComponentType<{
	columns?: { [key: string]: boolean };
	api?: IApi;
	children?: ReactNode;
}>;

export declare const ContextMenu: ComponentType<
	ComponentProps<typeof BaseContextMenu> & {
		api?: IApi;
	}
>;

export declare const Toolbar: ComponentType<
	ComponentProps<typeof BaseToolbar> & {
		api?: IApi;
	}
>;

export declare const Tooltip: ComponentType<{
	content?: ComponentType;
	api?: IApi;
	children?: ReactNode;
}>;

export declare const Willow: ComponentType<{
	fonts?: boolean;
	children?: ReactNode;
}>;

export declare const WillowDark: ComponentType<{
	fonts?: boolean;
	children?: ReactNode;
}>;

export declare function registerInlineEditor(
	type: string,
	component: ComponentType<{
		editor: TEditorConfig;
		onSave?: (ignoreFocus: boolean) => void;
		onCancel?: () => void;
		onApply?: (value: any) => void;
		onAction?: (ev: {
			action: string;
			data?: { [key: string]: any };
		}) => void;
	}>
): void;

/* get component events from store actions*/
type RemoveHyphen<S extends string> = S extends `${infer Head}-${infer Tail}`
	? `${Head}${Capitalize<RemoveHyphen<Tail>>}`
	: S;

type EventName<K extends string> = `on${Capitalize<RemoveHyphen<K>>}`;

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

Import the package CSS before using the component (`all.css` includes dependency styles, `style.css` is this component only)

- `Grid` has no `css`, `class`, or `style` passthrough prop.
- Style through wrapper elements, `rowStyle`, `columnStyle`, `cellStyle`, header/footer cell `css`, and theme CSS variables.
- `rowStyle(row)` appends a class to `.wx-row`.
- `columnStyle(column)` appends a class to body, header, footer, and print cells.
- `cellStyle(row, column)` appends a class to body and print cells only.
- Header/footer cell `css` appends to the header/footer `.wx-cell`.
- `IColumn.css` exists in store types and is used in auto-width measurement helpers, but it is not appended to rendered body cells by `Cell`.

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

```jsx
import "./OrdersGrid.css";

<div className="orders-grid">
	<Grid data={data} columns={columns} rowStyle={row => (row.priority ? "is-priority" : "")} />
</div>

/* OrdersGrid.css
.orders-grid {
	height: 420px;
}

.orders-grid .wx-row.is-priority:not(.wx-selected) .wx-cell {
	background: #fff7d6;
}

.orders-grid .wx-header .wx-cell {
	padding: 6px 8px;
}
*/
```

#### Recipes

##### Basic Grid

```jsx
import { Grid } from "@svar-ui/react-grid";

function BasicGrid() {
	const data = [
		{ id: 1, name: "Alex Brown", year: 1974 },
		{ id: 2, name: "Maria Ford", year: 1988 },
	];

	const columns = [
		{ id: "name", header: "Name", flexgrow: 1, sort: true },
		{ id: "year", header: "Year", width: 100, sort: true },
	];

	return (
		<div style={{ height: 360 }}>
			<Grid data={data} columns={columns} />
		</div>
	);
}
```

##### API, Events, And Selection

```jsx
import { useRef, useState } from "react";
import { Grid } from "@svar-ui/react-grid";

function ApiGrid() {
	const apiRef = useRef(null);
	const [selected, setSelected] = useState([]);

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
		apiRef.current.exec("add-row", { row: { city: "New city" } });
	}

	function updateSelected() {
		setSelected(apiRef.current.getState().selectedRows);
	}

	return (
		<>
			<button onClick={addRow}>Add</button>
			<Grid
				data={data}
				columns={columns}
				init={init}
				ref={apiRef}
				multiselect
				onSelectRow={updateSelected}
			/>
		</>
	);
}
```

##### Sort, Header Filters, And Inline Editors

```jsx
import { Grid } from "@svar-ui/react-grid";

function SortFilterGrid() {
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

	return <Grid data={data} columns={columns} />;
}
```

##### Custom Body, Header, And Footer Cells

```jsx
// CheckCell.jsx
import { Checkbox } from "@svar-ui/react-core";

function CheckCell({ api, row, column, onAction }) {
	function change({ value }) {
		api.exec("update-cell", { id: row.id, column: column.id, value });
		onAction({
			action: "checked-change",
			data: { row: row.id, column: column.id, value },
		});
	}

	return (
		<div data-action="ignore-click">
			<Checkbox value={row[column.id]} onChange={change} />
		</div>
	);
}

export default CheckCell;
```

```jsx
import { Grid } from "@svar-ui/react-grid";
import CheckCell from "./CheckCell.jsx";
import HeaderTitle from "./HeaderTitle.jsx";

function CustomCellGrid() {
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

	return (
		<Grid
			data={data}
			columns={columns}
			footer
			onCheckedChange={ev => console.log(ev.row, ev.value)}
		/>
	);
}
```

##### Custom Inline Editor

```jsx
// ColorEditor.jsx
import { useEffect, useRef, useState } from "react";
import { ColorBoard, Dropdown } from "@svar-ui/react-core";
import { clickOutside } from "@svar-ui/lib-dom";

function ColorEditor({ editor, onSave, onApply, onCancel }) {
	const [value, setValue] = useState(editor.value);
	const containerRef = useRef(null);

	function change({ value, input }) {
		setValue(value);
		if (input) onApply(value);
		else onSave();
	}

	useEffect(() => {
		if (!containerRef.current) return;
		const cleanup = clickOutside(containerRef.current, () => onSave(true));
		return () => cleanup?.destroy?.() ?? cleanup?.();
	}, [onSave]);

	return (
		<>
			<button onClick={onCancel}>{value}</button>
			<Dropdown width="auto" trackScroll onCancel={onCancel}>
				<div ref={containerRef}>
					<ColorBoard value={value} onChange={change} button />
				</div>
			</Dropdown>
		</>
	);
}

export default ColorEditor;
```

```jsx
import { Grid, registerInlineEditor } from "@svar-ui/react-grid";
import ColorEditor from "./ColorEditor.jsx";

registerInlineEditor("color", ColorEditor);

function ColorGrid() {
	const data = [{ id: 1, color: "#35D6A7" }];
	const columns = [
		{ id: "color", header: "Color", editor: "color", width: 180 },
	];

	return <Grid data={data} columns={columns} />;
}
```

##### Toolbar, Context Menu, And Header Menu

```jsx
import { useRef } from "react";
import { Grid, Toolbar, ContextMenu, HeaderMenu } from "@svar-ui/react-grid";

function ToolbarGrid() {
	const apiRef = useRef(null);
	const data = [
		{ id: 1, name: "Alex" },
		{ id: 2, name: "Sam" },
	];
	const columns = [
		{ id: "name", header: "Name", editor: "text", flexgrow: 1 },
	];

	return (
		<>
			<Toolbar api={apiRef.current} />
			<ContextMenu api={apiRef.current}>
				<HeaderMenu api={apiRef.current}>
					<Grid data={data} columns={columns} ref={apiRef} multiselect reorder undo />
				</HeaderMenu>
			</ContextMenu>
		</>
	);
}
```

##### Dynamic Data Loading

```jsx
import { useState } from "react";
import { Grid } from "@svar-ui/react-grid";

function DynamicGrid() {
	const raw = Array.from({ length: 10000 }, (_, id) => ({
		id,
		name: `Row ${id}`,
	}));

	const columns = [{ id: "name", header: "Name", flexgrow: 1 }];
	const [data, setData] = useState([]);

	function provideData({ row }) {
		setData(raw.slice(row.start, row.end));
	}

	return (
		<div style={{ height: 500 }}>
			<Grid
				data={data}
				columns={columns}
				dynamic={{ rowCount: raw.length }}
				onRequestData={provideData}
			/>
		</div>
	);
}
```

##### Responsive Columns And Fixed Columns

```jsx
import "./GridShell.css";
import { Grid } from "@svar-ui/react-grid";

function ResponsiveGrid() {
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

	return (
		<div className="grid-shell">
			<Grid data={data} columns={columns} responsive={responsive} split={{ left: 1 }} />
		</div>
	);
}

/* GridShell.css
.grid-shell {
	height: 420px;
}

.grid-shell .wx-grid.wx-responsive-600 .wx-cell {
	padding-top: 10px;
	padding-bottom: 10px;
}
*/
```

##### Tree Grid

```jsx
import { useRef } from "react";
import { Grid } from "@svar-ui/react-grid";

function TreeGrid() {
	const apiRef = useRef(null);
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

	return (
		<>
			<button onClick={() => apiRef.current.exec("open-row", { id: 1, nested: true })}>
				Open
			</button>
			<button onClick={() => apiRef.current.exec("close-row", { id: 1, nested: true })}>
				Close
			</button>

			<Grid data={data} columns={columns} ref={apiRef} tree />
		</>
	);
}
```

##### External Editor From Grid Columns

```jsx
import { useRef, useState } from "react";
import { Grid, getEditorConfig } from "@svar-ui/react-grid";
import { Editor } from "@svar-ui/react-editor";

function ExternalEditorGrid() {
	const apiRef = useRef(null);
	const [editing, setEditing] = useState(null);

	const data = [{ id: 1, name: "Alex" }];
	const columns = [
		{ id: "name", header: "Name", editor: "text", flexgrow: 1 },
	];

	function init(grid) {
		grid.intercept("open-editor", ({ id }) => {
			setEditing(grid.getRow(id));
			return false;
		});
	}

	return (
		<>
			<Grid data={data} columns={columns} init={init} ref={apiRef} />

			{editing && (
				<Editor
					values={editing}
					items={getEditorConfig(columns)}
					onSave={({ values }) =>
						apiRef.current.exec("update-row", { id: editing.id, row: values })}
				/>
			)}
		</>
	);
}
```

#### Implementation Notes

- `Grid` reinitializes the store reactively from props; changing `data`, `columns`, `sizes`, `selectedRows`, `sortMarks`, `filterValues`, `split`, `tree`, `undo`, or `reorder` can reset or recalculate store state.
- When `data` identity changes, the store clears `_filterIds`, `filterValues`, `sortMarks`, and `search`, and resets history.
- Header/footer configs are copied and normalized internally, but source `columns` are mutated for `optionsMap`; row objects can also be mutated for generated ids and tree metadata.
- `column.tooltip` is used by `Tooltip` but is not present in `IColumn` types.
- `HeaderMenu` uses menu item `type: "table-header"`


## File: locales.md

> Source: `locales.md`

i18n patterns common to all SVAR React components - Locale wrapper, bundled language packs, extending words and formats

### Localizing SVAR React Components

All `@svar-ui/react-*` widgets read locale data from a single React context (`wx-i18n`). The mechanics live in `@svar-ui/react-core`; every other package consumes them.

#### Locale Wrapper

Wrap the subtree you want to localize. With no wrapper, widgets fall back to English.

```jsx
import { Calendar, Locale } from "@svar-ui/react-core";
import { de } from "@svar-ui/core-locales";

function App() {
    return (
        <Locale words={de}>
            <Calendar value={new Date(2025, 4, 1)} />
        </Locale>
    );
}
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

```jsx
import { Gantt } from "@svar-ui/react-gantt";
import { Locale } from "@svar-ui/react-core";
import { cn } from "@svar-ui/gantt-locales";
import { cn as cnCore } from "@svar-ui/core-locales";

function App() {
    return (
        <Locale words={{ ...cn, ...cnCore }}>
            <Gantt {...settings} />
        </Locale>
    );
}
```

#### Extending Or Overriding Words

`Locale words` accepts a partial pack and extends the current context. Spread an existing pack to keep its formats and override only what you need:

```jsx
import { Calendar, Locale } from "@svar-ui/react-core";
import { cn } from "@svar-ui/core-locales";

function App() {
    const words = {
        ...cn,
        formats: {
            ...cn.formats,
            monthYearFormat: "%Y年%F",
            yearFormat: "%Y年",
        },
    };

    return (
        <Locale words={words}>
            <Calendar value={new Date(2025, 4, 1)} />
        </Locale>
    );
}
```

Pass `optional={true}` to make merged terms additive fallbacks rather than overrides - useful for layering app-specific strings on top of a full pack.

#### Affected Surfaces

Locale changes calendar labels, date/time formats, modal buttons, pager strings, empty-list text, notice/modal helpers, color-board select text - any widget that displays static strings or formats values reads them through this context.

#### Direct Helper

For non-component code, use the `locale` helper to build a translator:

```js
import { en, locale } from "@svar-ui/react-core";

const i18n = locale(en).extend(
    { core: { "Rows per page": "Rows" } },
    true
);
const _ = i18n.getGroup("core");
_("Rows per page"); // "Rows"
```


## File: themes.md

> Source: `themes.md`

### Styling SVAR React Components

All `@svar-ui/react-*` widgets share the same theming pipeline. The mechanics live in `@svar-ui/react-core`; every other package consumes them.

#### Per widget css files

Each package ships `style.css` (this component only) and `all.css` (this component plus all dependencies).

```css
@import "@svar-ui/react-gantt/style.css";
```

#### Theme Wrapper

Wrap the part of the app that uses SVAR widgets in a theme component from `@svar-ui/react-core`:

```jsx
import { Willow } from "@svar-ui/react-core";

function Root() {
    return (
        <Willow>
            <App />
        </Willow>
    );
}
```

Available themes: `Willow`, `WillowDark`. The wrapper:

- sets the React context `wx-theme`
- renders `.wx-theme.wx-{name}-theme` with `height:100%`
- loads Open Sans + the `wxi` icon CSS by default; pass `fonts={false}` to skip when the host app manages fonts itself

Without a theme wrapper widgets still render but lose theme variables and font/icon CSS.

#### Per-widget Willow / WillowDark themes

Several widgets ship their **own** `Willow` / `WillowDark` components on top of the core base. The widget version wraps the core theme and layers in widget-specific CSS variables (bar colors, grid borders, timescale fonts, etc.). When using such a widget, import the theme from the widget package - not from core - so both layers apply.

Widgets that expose custom `Willow` / `WillowDark` themes:

- `@svar-ui/react-core` - base
- `@svar-ui/react-gantt`
- `@svar-ui/react-grid`
- `@svar-ui/react-editor`
- `@svar-ui/react-filter`
- `@svar-ui/react-filemanager`
- `@svar-ui/react-comments`
- `@svar-ui/react-kanban`

The widget theme delegates to core and adds extra rules scoped to `.wx-willow-theme` (or `.wx-willow-dark-theme`):

```jsx
import "./WidgetTheme.css";
import { Willow } from "@svar-ui/react-core";

function WidgetTheme({ fonts = true, children }) {
    return children
        ? <Willow fonts={fonts}>{children}</Willow>
        : <Willow fonts={fonts} />;
}

/* WidgetTheme.css
.wx-willow-theme {
    --wx-gantt-border-color: #e6e6e6;
    --wx-gantt-task-color: #3983eb;
    /* ...widget-specific overrides... *\/
}
*/
```

Mount the widget's own theme once at the app root. The wrapper internally renders the core `Willow`, so a separate core import is not needed:

```jsx
import { Willow, Gantt } from "@svar-ui/react-gantt";

function App() {
    return (
        <>
            <Willow />
            <Gantt {...settings} />
        </>
    );
}
```

#### CSS Variables

Theme styling is variable-driven. Override variables on the theme wrapper or on any ancestor of the widgets you want to restyle - overrides cascade to every SVAR widget in the subtree.

```jsx
import "./Brand.css";

<Willow>
    <div className="brand">
        <App />
    </div>
</Willow>

/* Brand.css
.brand {
    --wx-color-primary: #0f766e;
    --wx-input-width: 280px;
    --wx-button-border-radius: 4px;
    --wx-calendar-cell-size: 30px;
}
*/
```

Nest different wrapper blocks for per-section restyling without forking the theme.

#### `css` Prop Convention

Most widgets accept a `css` prop. The string is appended to the widget's root class, so it works as a parent styling hook:

```jsx
<Toolbar css="my-toolbar" items={items} />

/* CSS
.my-toolbar {
    padding: 8px 12px;
}
*/
```

Composite widgets often expose secondary css props for nested popups (`menuCss` on `Toolbar`/`MenuBar`, etc.). Check the per-component file for the exact set.

#### Class Hooks

The per-component file lists the exact selectors that widget exposes.

#### Custom CSS class overrides

When writing custom rules to override widget styles, always use **at least two selectors** (e.g. `.a .b {}`). Component styles in the bundled SVAR widgets carry higher specificity than a plain `.b`. A two-selector rule (`.a .b`) matches or beats that specificity and wins.

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
