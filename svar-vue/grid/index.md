Use when building, configuring, styling, or modifying SVAR Vue Grid / @svar-ui/vue-grid data tables, toolbars, context menus, themes, inline editors, filters, sorting, selection, tree data, responsive layouts, export, or print behavior.

## Package

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
} from "@svar-ui/vue-grid";

import "@svar-ui/vue-grid/all.css";
```

## Supported functionality

### Grid Data And Columns

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

### Header, Footer, And Layout

- `header` defaults to `true`; `footer` defaults to `false`.
- `column.header` and `column.footer` can be a string, an object, or an array of strings/objects.
- Header/footer object fields include `text`, `cell`, `css`, `rowspan`, `colspan`, `collapsible`, `collapsed`, `vertical`, and header-only `filter`.
- `column.width` produces fixed pixel width; `column.flexgrow` produces flexible width.
- `split={{ left }}` fixes the first visible columns on the left.
- Source supports `split={{ right }}` for fixed right columns; the `Grid` prop type inherits `IConfig`, which only types `split.left`.
- The grid root is `height: 100%`; the parent must provide a height for useful vertical scrolling.
- Virtual rendering is built in for rows and columns.

### Selection

- `select` defaults to `true`; `select={false}` disables row click selection.
- `multiselect` enables Ctrl/Cmd toggle and Shift range selection.
- `selectedRows` is an initial/sync prop passed into the store; read live selection with `api.getState().selectedRows`, `api.getReactiveState().selectedRows`, or `onselectrow`.
- Custom checkbox cells should call `api.exec("select-row", { id: row.id, toggle: true, mode: value })` and wrap the control in `data-action="ignore-click"` when row click selection should not fire.

### Events And API

- Use `ref="api"` or `init={api => ...}` to access the grid API.
- API methods: `exec`, `on`, `intercept`, `detach`, `getState`, `getReactiveState`, `setNext`, `getStores`, `getRow`, `getColumn`.
- Action names are exposed as prop callbacks by removing hyphens and prefixing `on`: `select-row` -> `onselectrow`, `request-data` -> `onrequestdata`.
- Prop event callbacks receive the same payload passed to `api.exec`.
- `api.intercept(action, fn)` can return `false` to block an action before the normal handling path.
- `api.on(action, fn)` observes actions.
- Common actions: `add-row`, `delete-row`, `update-row`, `update-cell`, `select-row`, `resize-column`, `hide-column`, `sort-rows`, `filter-rows`, `search-rows`, `open-editor`, `close-editor`, `collapse-column`, `move-item`, `copy-row`, `open-row`, `close-row`, `export-data`, `scroll`, `print`, `undo`, `redo`, `request-data`.

### Sorting And Filtering

- `column.sort: true` enables header click sorting.
- `column.sort: (a, b) => 1 | -1 | 0` supplies custom sort logic.
- Ctrl/Cmd-click on sortable headers adds multi-sort marks.
- `sortMarks` shape is `{ [columnId]: { order: "asc" | "desc", index?: number } }`.
- Header filters are configured as `header: { filter: "text" }` or `header: { filter: { type, config } }`.
- Built-in filter types: `text`, `richselect`, `datepicker`.
- `filter.config` is forwarded to the underlying Vue Core control.
- `richselect` filter options come from `filter.config.options`, then `column.options`, then unique values in grid data.
- `api.exec("filter-rows", {})` clears all filters.
- `api.exec("filter-rows", { key, value })` updates `filterValues[key]` and applies the generated column filters.
- `api.exec("filter-rows", { filter })` applies a custom row predicate.

### Inline Editors

- Double-clicking a cell runs `open-editor` for the row and column.
- Built-in editor names: `text`, `combo`, `datepicker`, `richselect`, `multiselect`.
- `column.editor` can be a string, `{ type, config }`, or `(row, column) => editor | null`.
- Returning `null` from an editor handler makes that cell non-editable.
- `combo`, `richselect`, and `multiselect` use `column.options` with `{ id, label }`.
- `multiselect` expects the cell value to be an array of option ids.
- Editor `config.template` renders option/value text; `config.cell` renders custom option/value components; `config.dropdown` is passed to dropdown-based editors.
- `datepicker` supports `config.buttons` with `["clear" | "today"]`.
- `registerInlineEditor(type, Component)` registers a custom editor component.

### Custom Components

- `column.cell` receives `{ api, row, column, onaction }`.
- Header/footer `cell` receives `{ api, cell, column, row, onaction }`.
- Calling `onaction({ action, data })` inside a custom cell executes `api.exec(action, data)`.
- Custom action names are routed to prop callbacks, for example `onaction({ action: "custom-check", data })` -> `oncustomcheck={...}`.
- `overlay` can be text or a component; overlay components receive `onaction`.
- `Tooltip` can use default cell text, `column.tooltip(row)`, or `content={Component}`; tooltip content receives `{ data }`.

### Toolbar And Menus

- `Toolbar` wraps `@svar-ui/vue-toolbar` and defaults to `defaultToolbarButtons`.
- `Toolbar` auto-runs `handleAction(api, item.id)` before calling its own `onclick`.
- Default toolbar actions: `add-row`, `open-editor`, `delete-row`, `copy-row`, `cut-row`, `paste-row`, `move-item:up`, `move-item:down`, `undo`, `redo`.
- `Toolbar` filters move actions when `reorder` is off and undo/redo when `undo` is off.
- `ContextMenu` wraps `@svar-ui/vue-menu` and defaults to `defaultMenuOptions`.
- `ContextMenu` defaults `at="point"` and uses row `data-context-id` through the base menu's default `dataKey`.
- The default resolver selects the right-clicked row if it is not already selected.
- `ContextMenu` auto-runs `handleAction(api, ev.action.id)` before calling its own `onclick`; base menu events also expose `ev.option`.
- Default context menu actions: `add-row:before`, `add-row:after`, `copy-row`, `cut-row`, `paste-row`, `move-item:up`, `move-item:down`, `delete-row`.
- `HeaderMenu` wraps grid content and opens on header right-click using `data-header-id`; clicking an item runs `hide-column`.
- `HeaderMenu columns={{ id: true }}` limits which columns appear in the hide/show menu.

### Saving

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

### Themes

- Theme components: `Willow`, `WillowDark`.
- Each theme accepts `fonts?: boolean` and optional children.
- Theme wrappers delegate to `@svar-ui/vue-core` and add grid CSS variables to `.wx-material-theme`, `.wx-willow-theme`, or `.wx-willow-dark-theme`.
- If no `wx-theme` context exists, the store calls `suggestSkin()` and defaults to Willow.

## Public Types

```ts
import type { Component, ComponentProps } from "vue";
import { ContextMenu as BaseContextMenu } from "@svar-ui/vue-menu";
import { Toolbar as BaseToolbar } from "@svar-ui/vue-toolbar";

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

## Styling

Import the package CSS before using the component (`all.css` includes dependency styles, `style.css` is this component only)

- `Grid` has no `css`, `class`, or `style` passthrough prop.
- Style through wrapper elements, `rowStyle`, `columnStyle`, `cellStyle`, header/footer cell `css`, and theme CSS variables.
- `rowStyle(row)` appends a class to `.wx-row`.
- `columnStyle(column)` appends a class to body, header, footer, and print cells.
- `cellStyle(row, column)` appends a class to body and print cells only.
- Header/footer cell `css` appends to the header/footer `.wx-cell`.
- `IColumn.css` exists in store types and is used in auto-width measurement helpers, but it is not appended to rendered body cells by `Cell.vue`.

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

```vue
<template>
  <div class="orders-grid">
    <Grid :data="data" :columns="columns" :rowStyle="row => (row.priority ? 'is-priority' : '')" />
  </div>
</template>

<style scoped>
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

## Recipes

### Basic Grid

```vue
<script setup>
import { Grid } from "@svar-ui/vue-grid";

const data = [
	{ id: 1, name: "Alex Brown", year: 1974 },
	{ id: 2, name: "Maria Ford", year: 1988 },
];

const columns = [
	{ id: "name", header: "Name", flexgrow: 1, sort: true },
	{ id: "year", header: "Year", width: 100, sort: true },
];
</script>

<template>
  <div style="height: 360px;">
    <Grid :data="data" :columns="columns" />
  </div>
</template>
```

### API, Events, And Selection

```vue
<script setup>
import { ref } from "vue";
import { Grid } from "@svar-ui/vue-grid";

const api = ref();
const selected = ref([]);

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
	api.value.exec("add-row", { row: { city: "New city" } });
}

function updateSelected() {
	selected.value = api.value.getState().selectedRows;
}
</script>

<template>
  <button :onclick="addRow">Add</button>
  <Grid
    :data="data"
    :columns="columns"
    :init="init"
    ref="api"
    multiselect
    :onselectrow="updateSelected"
  />
</template>
```

### Sort, Header Filters, And Inline Editors

```vue
<script setup>
import { Grid } from "@svar-ui/vue-grid";

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

<template>
  <Grid :data="data" :columns="columns" />
</template>
```

### Custom Body, Header, And Footer Cells

```vue
<!-- CheckCell.vue -->
<script setup>
import { Checkbox } from "@svar-ui/vue-core";

const props = defineProps({
  api: {},
  row: {},
  column: {},
  onaction: { type: Function },
});

function change({ value }) {
	props.api.exec("update-cell", { id: props.row.id, column: props.column.id, value });
	props.onaction?.({
		action: "checked-change",
		data: { row: props.row.id, column: props.column.id, value },
	});
}
</script>

<template>
  <div data-action="ignore-click">
    <Checkbox :value="props.row[props.column.id]" :onchange="change" />
  </div>
</template>
```

```vue
<script setup>
import { Grid } from "@svar-ui/vue-grid";
import CheckCell from "./CheckCell.vue";
import HeaderTitle from "./HeaderTitle.vue";

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

<template>
  <Grid
    :data="data"
    :columns="columns"
    footer
    :oncheckedchange="ev => console.log(ev.row, ev.value)"
  />
</template>
```

### Custom Inline Editor

```vue
<!-- ColorEditor.vue -->
<script setup>
import { ref } from "vue";
import { ColorBoard, Dropdown } from "@svar-ui/vue-core";
import { clickOutside } from "@svar-ui/lib-dom";
import { asDirective } from "@svar-ui/lib-vue";

const vClickOutside = asDirective(clickOutside);

const props = defineProps({
  editor: {},
  onsave: { type: Function },
  onapply: { type: Function },
  oncancel: { type: Function },
});
const value = ref(props.editor.value);

function change({ value, input }) {
	if (input) props.onapply(value);
	else props.onsave();
}
</script>

<template>
  <button :onclick="props.oncancel">{{ value }}</button>
  <Dropdown width="auto" trackScroll :oncancel="props.oncancel">
    <div v-click-outside="() => props.onsave(true)">
      <ColorBoard :value="value" :onchange="change" button />
    </div>
  </Dropdown>
</template>
```

```vue
<script setup>
import { Grid, registerInlineEditor } from "@svar-ui/vue-grid";
import ColorEditor from "./ColorEditor.vue";

registerInlineEditor("color", ColorEditor);

const data = [{ id: 1, color: "#35D6A7" }];
const columns = [
	{ id: "color", header: "Color", editor: "color", width: 180 },
];
</script>

<template>
  <Grid :data="data" :columns="columns" />
</template>
```

### Toolbar, Context Menu, And Header Menu

```vue
<script setup>
import { ref } from "vue";
import { Grid, Toolbar, ContextMenu, HeaderMenu } from "@svar-ui/vue-grid";

const api = ref();
const data = [
	{ id: 1, name: "Alex" },
	{ id: 2, name: "Sam" },
];
const columns = [
	{ id: "name", header: "Name", editor: "text", flexgrow: 1 },
];
</script>

<template>
  <Toolbar :api="api" />
  <ContextMenu :api="api">
    <HeaderMenu :api="api">
      <Grid :data="data" :columns="columns" ref="api" multiselect reorder undo />
    </HeaderMenu>
  </ContextMenu>
</template>
```

### Dynamic Data Loading

```vue
<script setup>
import { ref } from "vue";
import { Grid } from "@svar-ui/vue-grid";

const raw = Array.from({ length: 10000 }, (_, id) => ({
	id,
	name: `Row ${id}`,
}));

const columns = [{ id: "name", header: "Name", flexgrow: 1 }];
const data = ref([]);

function provideData({ row }) {
	data.value = raw.slice(row.start, row.end);
}
</script>

<template>
  <div style="height: 500px;">
    <Grid
      :data="data"
      :columns="columns"
      :dynamic="{ rowCount: raw.length }"
      :onrequestdata="provideData"
    />
  </div>
</template>
```

### Responsive Columns And Fixed Columns

```vue
<script setup>
import { Grid } from "@svar-ui/vue-grid";

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

<template>
  <div class="grid-shell">
    <Grid :data="data" :columns="columns" :responsive="responsive" :split="{ left: 1 }" />
  </div>
</template>

<style scoped>
.grid-shell {
	height: 420px;
}

.grid-shell .wx-grid.wx-responsive-600 .wx-cell {
	padding-top: 10px;
	padding-bottom: 10px;
}
</style>
```

### Tree Grid

```vue
<script setup>
import { ref } from "vue";
import { Grid } from "@svar-ui/vue-grid";

const api = ref();
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

<template>
  <button :onclick="() => api.exec('open-row', { id: 1, nested: true })">
    Open
  </button>
  <button :onclick="() => api.exec('close-row', { id: 1, nested: true })">
    Close
  </button>

  <Grid :data="data" :columns="columns" ref="api" tree />
</template>
```

### External Editor From Grid Columns

```vue
<script setup>
import { ref } from "vue";
import { Grid, getEditorConfig } from "@svar-ui/vue-grid";
import { Editor } from "@svar-ui/vue-editor";

const api = ref();
const editing = ref(null);

const data = [{ id: 1, name: "Alex" }];
const columns = [
	{ id: "name", header: "Name", editor: "text", flexgrow: 1 },
];

function init(grid) {
	grid.intercept("open-editor", ({ id }) => {
		editing.value = grid.getRow(id);
		return false;
	});
}
</script>

<template>
  <Grid :data="data" :columns="columns" :init="init" ref="api" />

  <Editor
    v-if="editing"
    :values="editing"
    :items="getEditorConfig(columns)"
    :onsave="({ values }) =>
      api.exec('update-row', { id: editing.id, row: values })"
  />
</template>
```

## Implementation Notes

- `Grid` reinitializes the store reactively from props; changing `data`, `columns`, `sizes`, `selectedRows`, `sortMarks`, `filterValues`, `split`, `tree`, `undo`, or `reorder` can reset or recalculate store state.
- When `data` identity changes, the store clears `_filterIds`, `filterValues`, `sortMarks`, and `search`, and resets history.
- Header/footer configs are copied and normalized internally, but source `columns` are mutated for `optionsMap`; row objects can also be mutated for generated ids and tree metadata.
- `column.tooltip` is used by `Tooltip.vue` but is not present in `IColumn` types.
- `HeaderMenu` uses menu item `type: "table-header"`
