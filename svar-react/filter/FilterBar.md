# FilterBar

Package: `@svar-ui/react-filter`

Use this file independently when building, configuring, styling, or modifying `FilterBar`.

## Import

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

## Supported Functionality

### Data Contract

- `FilterBar` emits an `IFilterSet` through `onChange({ value })`.
- `IFilterSet`: `{ glue?: "and" | "or", rules?: (IFilter | IFilterSet)[] }`.
- string field shorthand becomes `{ id, type: "text", filter: "contains" }`.
- object fields produce one `IFilter` when the current value is truthy.
- `type: "all"` can emit an OR `IFilterSet` across multiple fields.
- empty fields are omitted from the emitted rules.
- when one rule is produced by `type: "all"` and it has `glue: "or"`, that OR set is returned directly.

### Field Configurations

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

### Events And Timing

- `debounce` defaults to `300`.
- text and number input changes use `debounce`.
- select and date changes dispatch after `1ms`.
- `onChange({ value })` receives the current `IFilterSet`.
- initial `value` field configs populate controls but do not emit until a change happens.

## Public Types

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

## Styling

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

## Recipes

### Basic Text, Number, And Select Fields

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

### Date Fields And Ranges

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

### Search Across Many Fields

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

### Dynamic Field Selector

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

### Faster Text Updates

```jsx
<FilterBar
	debounce={100}
	fields={["first_name", "last_name"]}
	onChange={({ value }) => applyFilter(value)}
/>
```

## Implementation Notes

- `FilterBar` stores one `lastField` for dynamic selectors; avoid multiple independent `type: "dynamic"` groups
- `normalizeField` only maps `options` for non-date fields.
- select options can be strings, numbers, or `{ id, label }` objects
