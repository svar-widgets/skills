# FilterBuilder

Package: `@svar-ui/react-filter`

Use this file independently when building, configuring, styling, or modifying `FilterBuilder`.

## Import

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

## Supported Functionality

### Data Contract

- `fields`: array of `{ id, label, type, predicate?, format? }`.
- supported field `type`: `"text"`, `"number"`, `"date"`, `"tuple"`.
- `options`: `{ [fieldId]: AnyData[] }` or `(fieldId) => AnyData[] | Promise<AnyData[]>`.
- `value`: `IFilterSet`, default `{ glue: "and", rules: [] }`.
- `IFilterSet`: `{ glue?: "and" | "or", rules?: (IFilter | IFilterSet)[] }`.
- `IFilter`: `{ field, type?, predicate?, filter?, includes?, value? }`.
- `includes` matches exact option values; `filter + value` uses an operator.
- `between` and `notBetween` use `value: { start, end }`.
- date editor UI values should be `Date` objects or `{ start: Date, end: Date }`; convert date strings before passing visual editor values.

### Built-In Filters

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

### Props And Modes

- source props: `value = { glue: "and", rules: [] }`, `fields = []`, `options = null`, `type = "list"`, `init = null`, plus action callback props in `...restProps`.
- `type="list"`: vertical layout, nested groups, AND/OR glue, context menu, top Add filter button.
- `type="line"`: horizontal layout with scrollable rules, context menu, Add filter button at the right.
- `type="simple"`: horizontal flat layout; Add filter opens a dropdown of unused fields, no nested groups, no context menu, delete icon per rule.
- `onChange` receives `{ value: IFilterSet }` after store-changing actions.
- other action callback props use event names with hyphens removed and camelCased: `onAddRule`, `onAddGroup`, `onEditRule`, `onUpdateRule`, `onDeleteRule`, `onToggleGlue`, `onChangeRule`.
- `init(api)` runs once after initial store setup.
- `ref` exposes `exec`, `on`, `intercept`, `detach`, `setNext`, `getState`, `getReactiveState`, `getStores`, `getValue`.
- public actions: `add-rule`, `add-group`, `edit-rule`, `update-rule`, `delete-rule`, `toggle-glue`, `change-rule`, `change`.

## Public Types

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

## Styling

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

## Recipes

### Local Array Filtering

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

### Line Or Simple Layout

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

### Async Options

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

### API And Event Interception

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

### Convert Date Strings Around Builder UI

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
