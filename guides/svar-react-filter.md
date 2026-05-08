# svar-react — filter

_Generated 2026-05-08T13:35:37.052Z_

## Contents

- [`filter/index.md`](#file-filter-index-md)
- [`filter/FilterBar.md`](#file-filter-filterbar-md)
- [`filter/FilterBuilder.md`](#file-filter-filterbuilder-md)
- [`filter/FilterEditor.md`](#file-filter-filtereditor-md)
- [`filter/FilterQuery.md`](#file-filter-filterquery-md)
- [`locales.md`](#file-locales-md)
- [`themes.md`](#file-themes-md)


## File: filter/index.md

> Source: `filter/index.md`

Use when building, configuring, styling, or modifying SVAR React Filter / @svar-ui/react-filter FilterBuilder, FilterEditor, FilterBar, or FilterQuery components

Package: `@svar-ui/react-filter`
Styles: `@svar-ui/react-filter/all.css`

The package ships `style.css` (this component only) and `all.css` (this component plus all dependencies).

Use this skill as an index. Load only the component reference needed for the task; each linked file is independent.

- `FilterBuilder.md` - visual query builder, nested filter groups, builder API/actions, builder styling.
- `FilterEditor.md` - standalone single-rule editor, field selector mode, option includes, editor styling.
- `FilterBar.md` - compact filter input row, `all` and `dynamic` field modes, bar styling.
- `FilterQuery.md` - query-string input, parse modes, autocomplete, natural text integrations, query styling.


## File: filter/FilterBar.md

> Source: `filter/FilterBar.md`

### FilterBar

Package: `@svar-ui/react-filter`

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
} from "@svar-ui/react-filter";
```

#### Supported Functionality

##### Data Contract

- `FilterBar` emits an `IFilterSet` through `onChange({ value })`.
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
- `onChange({ value })` receives the current `IFilterSet`.
- initial `value` field configs populate controls but do not emit until a change happens.

#### Public Types

```ts
import type { ComponentType } from "react";
import type {
	IFilterSet,
	IFilterBarField,
} from "@svar-ui/filter-store";

export declare const FilterBar: ComponentType<{
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
	onChange?: (ev: { value: IFilterSet }) => void;
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

```jsx
import "./BarScope.css";

<div className="bar-scope">
	<Willow>
		<FilterBar fields={fields} onChange={handleChange} />
	</Willow>
</div>

/* BarScope.css
.bar-scope {
	--wx-label-font-size: 14px;
	--wx-label-font-weight: 600;
}

.bar-scope .wx-filter-bar {
	width: 100%;
	gap: 16px;
	padding: 10px 0;
}
*/
```

#### Recipes

##### Basic Text, Number, And Select Fields

```jsx
import { useState } from "react";
import { FilterBar, createArrayFilter } from "@svar-ui/react-filter";

function BasicFilterBar() {
	const [rows, setRows] = useState(data);

	function apply({ value }) {
		setRows(createArrayFilter(value)(data));
	}

	return (
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
			onChange={apply}
		/>
	);
}
```

##### Date Fields And Ranges

```jsx
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
	onChange={({ value }) => applyFilter(value)}
/>
```

##### Search Across Many Fields

```jsx
<FilterBar
	fields={[
		{
			type: "all",
			label: "Search",
			placeholder: "Search people",
			by: ["age", "first_name", "last_name"],
		},
	]}
	onChange={({ value }) => applyFilter(value)}
/>
```

##### Dynamic Field Selector

```jsx
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
	onChange={({ value }) => applyFilter(value)}
/>
```

##### Faster Text Updates

```jsx
<FilterBar
	debounce={100}
	fields={["first_name", "last_name"]}
	onChange={({ value }) => applyFilter(value)}
/>
```

#### Implementation Notes

- `FilterBar` stores one `lastField` for dynamic selectors; avoid multiple independent `type: "dynamic"` groups
- `normalizeField` only maps `options` for non-date fields.
- select options can be strings, numbers, or `{ id, label }` objects


## File: filter/FilterBuilder.md

> Source: `filter/FilterBuilder.md`

### FilterBuilder

Package: `@svar-ui/react-filter`

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
} from "@svar-ui/react-filter";
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
- `onChange` receives `{ value: IFilterSet }` after store-changing actions.
- other action callback props use event names with hyphens removed and camelCased: `onAddRule`, `onAddGroup`, `onEditRule`, `onUpdateRule`, `onDeleteRule`, `onToggleGlue`, `onChangeRule`.
- `init(api)` runs once after initial store setup.
- `ref` exposes `exec`, `on`, `intercept`, `detach`, `setNext`, `getState`, `getReactiveState`, `getStores`, `getValue`.
- public actions: `add-rule`, `add-group`, `edit-rule`, `update-rule`, `delete-rule`, `toggle-glue`, `change-rule`, `change`.

#### Public Types

```ts
import type { ComponentType } from "react";
import type {
	IApi,
	TMethodsConfig,
	IConfig,
} from "@svar-ui/filter-store";

export declare const FilterBuilder: ComponentType<
	{
		type?: "list" | "line" | "simple";
		init?: (api: IApi) => void;
	} & IConfig &
		FilterBuilderActions<TMethodsConfig>
>;

/* get component events from store actions*/
type RemoveHyphen<S extends string> = S extends `${infer Head}-${infer Tail}`
	? `${Head}${Capitalize<RemoveHyphen<Tail>>}`
	: S;

type EventName<K extends string> = `on${Capitalize<RemoveHyphen<K>>}`;

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
- editor/input variables inside the rule editor come from `FilterEditor` and `@svar-ui/react-core`.

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

```jsx
import "./BuilderScope.css";

<div className="builder-scope">
	<Willow>
		<FilterBuilder fields={fields} options={options} onChange={handleChange} />
	</Willow>
</div>

/* BuilderScope.css
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
*/
```

#### Recipes

##### Local Array Filtering

```jsx
import { useState } from "react";
import { FilterBuilder, Willow, createArrayFilter } from "@svar-ui/react-filter";

function LocalFilterBuilder() {
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
	const [rows, setRows] = useState(data);
	const [value, setValue] = useState({ glue: "and", rules: [] });

	function applyFilter({ value }) {
		setValue(value);
		setRows(createArrayFilter(value)(data));
	}

	return (
		<Willow>
			<FilterBuilder value={value} fields={fields} options={options} onChange={applyFilter} />
		</Willow>
	);
}
```

##### Line Or Simple Layout

```jsx
<FilterBuilder
	value={value}
	fields={fields}
	options={options}
	type="line"
	onChange={({ value }) => applyFilter(value)}
/>

<FilterBuilder
	value={value}
	fields={fields}
	options={options}
	type="simple"
	onChange={({ value }) => applyFilter(value)}
/>
```

##### Async Options

```jsx
import { FilterBuilder } from "@svar-ui/react-filter";

async function loadOptions(fieldId) {
	await new Promise(resolve => setTimeout(resolve, 300));
	return optionMap[fieldId] || [];
}

function AsyncOptions() {
	return <FilterBuilder value={value} fields={fields} options={loadOptions} />;
}
```

##### API And Event Interception

```jsx
import { useRef, useState } from "react";
import { FilterBuilder } from "@svar-ui/react-filter";

function ApiBuilder() {
	const apiRef = useRef(null);
	const [valueText, setValueText] = useState("");

	function init(api) {
		apiRef.current = api;
		api.intercept("add-rule", ev => {
			ev.edit = false;
		});
		api.on("change", ({ value }) => {
			setValueText(JSON.stringify(value, null, 2));
		});
	}

	function addAgeRule() {
		apiRef.current.exec("add-rule", {
			rule: { field: "age", type: "number", filter: "greater", value: 30 },
			edit: false,
		});
	}

	return (
		<>
			<button onClick={addAgeRule}>Add age rule</button>
			<FilterBuilder ref={apiRef} fields={fields} options={options} init={init} />
			<pre>{valueText}</pre>
		</>
	);
}
```

##### Convert Date Strings Around Builder UI

```jsx
import { useState } from "react";
import { FilterBuilder } from "@svar-ui/react-filter";

function ConvertDateBuilder() {
	const incoming = {
		rules: [{ field: "start", filter: "greater", value: "2025-01-01" }],
	};

	const [value, setValue] = useState({
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

	return <FilterBuilder value={value} fields={fields} options={options} init={init} />;
}
```


## File: filter/FilterEditor.md

> Source: `filter/FilterEditor.md`

### FilterEditor

Package: `@svar-ui/react-filter`

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
} from "@svar-ui/react-filter";
```

#### Supported Functionality

##### Data Contract

- emits one `IFilter` rule through `onApply` and `onChange`.
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

- source props: `fields = null`, `fieldsSelector = true`, `field = null`, `buttons = true`, `options = null`, `includes = null`, `type = "text"`, `filter = ""`, `value = ""`, `format = null`, `predicate = null`, `onApply`, `onCancel`, `onChange`.
- single-field mode: pass `type`, `field`, `filter`, `value`, `options`, `includes`, `format`, and `predicate` directly.
- multi-field mode: pass `fields`; selected field controls type, format, predicate, and loaded options.
- `fieldsSelector={false}` hides the field dropdown while keeping the selected field.
- `type="date"` uses `DatePicker`, except `filter="between"`/`"notBetween"` use `DateRangePicker`.
- `type="number"` uses numeric `Text`; `type="text"` uses text `Text`.
- `type="tuple"` uses `Combo` with options plus an automatic empty `$empty` / `None` option.
- option checkboxes are filtered by the current operator/value.
- `onChange({ value })` fires for UI changes when operator, value, field, or includes change.
- `onApply({ value })` fires from the Apply button.
- `onCancel()` fires from Cancel with no payload in source.
- `buttons={false}` hides Apply/Cancel and is normally paired with `onChange`.

#### Public Types

```ts
import type { ComponentType } from "react";
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

export declare const FilterEditor: ComponentType<{
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
	onApply: (ev: { value: IFilter }) => void;
	onCancel: (ev: { value: IFilter }) => void;
	onChange: (ev: { value: IFilter }) => void;
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
- shared/core input variables come from `@svar-ui/react-core`, including `--wx-input-*`.

Class hooks:

- root: `.wx-filter-editor`
- rows and cells: `.wx-wrapper`, `.wx-cell`
- option list: `.wx-list`, `.wx-item`

Layout defaults:

- `.wx-wrapper`: `display: flex`, `justify-content: right`, `gap: 10px`, `align-items: center`, `margin: 8px 0`.
- `.wx-cell`: `flex: 1`.
- `.wx-list`: `height: 150px`, `overflow-y: auto`, `margin: 8px 0`, `border: var(--wx-filter-border)`.
- `.wx-item`: `user-select: none`, `padding: 8px 12px`, `border-bottom: var(--wx-filter-border)`.

```jsx
<div className="editor-scope">
	<Willow>
		<FilterEditor type="text" options={values} onApply={handleApply} />
	</Willow>
</div>
```

```css
.editor-scope {
	--wx-filter-border: 1px solid #d0d5dd;
}

.editor-scope .wx-item {
	padding: 12px 16px;
}
```

#### Recipes

##### Single Text Rule With Apply

```jsx
import { useState } from "react";
import { FilterEditor, createArrayFilter } from "@svar-ui/react-filter";

function Example() {
	const options = ["Alex", "Daisy", "John"];
	const [rows, setRows] = useState(data);

	function apply({ value }) {
		setRows(createArrayFilter({ rules: [value] })(data));
	}

	return (
		<FilterEditor
			type="text"
			field="first_name"
			options={options}
			onApply={apply}
		/>
	);
}
```

##### Live Rule Without Buttons

```jsx
import { useState } from "react";
import { FilterEditor, createArrayFilter } from "@svar-ui/react-filter";

function Example() {
	const [rule, setRule] = useState({});
	const [rows, setRows] = useState(data);

	function update({ value }) {
		setRule(value);
		setRows(createArrayFilter({ rules: [value] })(data));
	}

	return (
		<FilterEditor
			type="text"
			field="first_name"
			options={["Alex", "Daisy", "John"]}
			buttons={false}
			includes={rule.includes}
			filter={rule.filter}
			value={rule.value}
			onChange={update}
		/>
	);
}
```

##### Field Selector With Async Options

```jsx
import { FilterEditor } from "@svar-ui/react-filter";

function Example() {
	const fields = [
		{ id: "first_name", label: "First Name", type: "text" },
		{ id: "age", label: "Age", type: "number" },
		{ id: "start", label: "Start Date", type: "date" },
	];

	async function loadOptions(field) {
		return optionMap[field] || [];
	}

	return (
		<FilterEditor
			fields={fields}
			field="age"
			options={loadOptions}
			onApply={({ value }) => console.log(value)}
		/>
	);
}
```

##### Date Range Rule

```jsx
import { FilterEditor, getOptions } from "@svar-ui/react-filter";

function Example() {
	const options = getOptions(data, "start");

	return (
		<FilterEditor
			field="start"
			options={options}
			type="date"
			filter="between"
			value={{
				start: new Date("2024-11-01"),
				end: new Date("2025-05-01"),
			}}
			onApply={({ value }) => console.log(value)}
		/>
	);
}
```

##### Tuple With Formatted Options

```jsx
import { FilterEditor, getOptions } from "@svar-ui/react-filter";

function Example() {
	const options = getOptions(data, "start", {
		predicate: "month",
		sort: (a, b) => a - b,
	});
	const monthName = value => monthLabels[value] || String(value);

	return (
		<FilterEditor
			field="start"
			options={options}
			format={monthName}
			filter="greater"
			type="tuple"
			onApply={({ value }) => console.log(value)}
		/>
	);
}
```

#### Implementation Notes

- `FilterEditor` source treats `predicate`, `onApply`, `onCancel`, and `onChange` as optional
- source calls `onCancel()` with no payload, although the declaration types it as `(ev: { value: IFilter }) => void`.


## File: filter/FilterQuery.md

> Source: `filter/FilterQuery.md`

### FilterQuery

Package: `@svar-ui/react-filter`

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
} from "@svar-ui/react-filter";
```

#### Supported Functionality

##### Data Contract

- `value` is a controlled prop and stores the query string with field IDs.
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
- Enter and the Search button call `onChange`.
- clear button resets local text and controlled `value`, but does not call `onChange` until the user submits again.

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

- `onChange` runs on Enter, Search button, and external `value` updates after the first non-empty set.
- parse-enabled event shape: `{ parsed, value, text, error, startProgress, endProgress }`.
- `parsed` is a `ParseResult`.
- `error` is `null` or a localized `ValidationError` with `message`.
- with parse enabled, `text` is `parseResult.naturalText || ""` when there is no blocking error, otherwise the current query text.
- with `parse="none"`, event shape is `{ value, text, startProgress, endProgress }`.

#### Public Types

```ts
import type { ComponentType } from "react";
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

export declare const FilterQuery: ComponentType<{
	value?: string;
	placeholder?: string;
	parse?: "none" | "strict" | "allowFreeText";
	fields?: IField[];
	options?: IDataHash<AnyData[]>;
	onChange?: (ev: FilterQueryEvent) => void;
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

```jsx
<div className="query-scope">
	<Willow>
		<FilterQuery fields={fields} options={options} onChange={handleFilter} />
	</Willow>
</div>
```

```css
.query-scope {
	--wx-filter-query-field-color: #7c3aed;
	--wx-filter-query-value-color: #059669;
	--wx-color-primary: #7c3aed;
}

.query-scope .wx-filter-query-search {
	background: #0f172a;
	color: #f8fafc;
}
```

#### Recipes

##### Structured Query With Local Filtering

```jsx
import { useState } from "react";
import { FilterQuery, createArrayFilter } from "@svar-ui/react-filter";

function Example() {
	const [value, setValue] = useState("");
	const [rows, setRows] = useState(data);

	function handleFilter({ value, error }) {
		setValue(value);
		if (error && error.code !== "NO_DATA") return;
		setRows(createArrayFilter(value, {}, fields)(data));
	}

	return (
		<FilterQuery
			value={value}
			placeholder="e.g. FirstName: Alex or #urgent"
			fields={fields}
			options={{ ...options, "#": ["urgent", "review", "done"] }}
			onChange={handleFilter}
		/>
	);
}
```

##### Strict Query Syntax

```jsx
<FilterQuery
	value={query}
	onChange={({ value, error }) => {
		setQuery(value);
		if (!error) applyFilter(value);
	}}
	parse="strict"
	placeholder="Status: Open and Age: >30"
	fields={fields}
	options={options}
/>
```

##### Natural Text Endpoint

```jsx
import { useState } from "react";
import { FilterQuery, createArrayFilter, getQueryString } from "@svar-ui/react-filter";

function Example() {
	const [normalizedQuery, setNormalizedQuery] = useState("");
	const [rows, setRows] = useState(data);

	async function handleNatural({ text, startProgress, endProgress }) {
		try {
			startProgress();
			const filter = await textToFilter(text, fields);
			setNormalizedQuery(filter ? getQueryString(filter).query : "");
			setRows(createArrayFilter(filter || { rules: [] })(data));
		} finally {
			endProgress();
		}
	}

	return (
		<>
			<FilterQuery
				parse="none"
				placeholder="first name contains Alex and age greater than 30"
				onChange={handleNatural}
			/>

			<pre>{normalizedQuery}</pre>
		</>
	);
}
```

##### Mixed Query And Natural Text

```jsx
import { useState } from "react";
import { FilterQuery, createArrayFilter, getQueryString } from "@svar-ui/react-filter";

function Example() {
	const [query, setQuery] = useState("start: 2024");
	const [rows, setRows] = useState(data);

	async function handleMixed({ value, error, text, startProgress, endProgress }) {
		if (text) {
			try {
				startProgress();
				value = await textToFilter(text, fields);
				setQuery(value ? getQueryString(value).query : "");
				error = null;
			} finally {
				endProgress();
			}
		} else {
			setQuery(value);
		}

		if (error && error.code !== "NO_DATA") return;
		setRows(createArrayFilter(value, {}, fields)(data));
	}

	return (
		<FilterQuery
			value={query}
			placeholder="FirstName: contains Alex and Age: >30"
			fields={fields}
			options={options}
			onChange={handleMixed}
		/>
	);
}
```

##### Render Query HTML

```jsx
import { useMemo } from "react";
import { getQueryHtml, getQueryString } from "@svar-ui/react-filter";

function Example({ filterValue, fields }) {
	const html = useMemo(
		() =>
			filterValue
				? getQueryHtml(getQueryString(filterValue).query, { fields })
				: "",
		[filterValue, fields]
	);

	return <div dangerouslySetInnerHTML={{ __html: html }} />;
}
```

#### Implementation Notes

- `parse="none"` bypasses highlight, autocomplete, parsing, and validation entirely.
- `NO_DATA` errors still pass parsed config and can be treated as non-blocking
- `getQueryHtml` returns inline styled HTML; only use it in trusted/internal query display contexts.


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
