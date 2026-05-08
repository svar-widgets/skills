# FilterEditor

Package: `@svar-ui/react-filter`

Use this file independently when building, configuring, styling, or modifying `FilterEditor`.

## Import

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

## Supported Functionality

### Data Contract

- emits one `IFilter` rule through `onApply` and `onChange`.
- `IFilter`: `{ field?, type, predicate?, filter, includes, value }`.
- `field` is present when the `field` prop is set or when `fields` mode is active.
- `includes` is a selected subset only when non-empty and smaller than visible options; otherwise it emits `[]`.
- `value` is a scalar for most filters and `{ start, end }` for `between` / `notBetween`.
- date editor UI values should be `Date` objects or `{ start: Date, end: Date }`.
- `options` can be a fixed array or `(fieldId) => AnyData[] | Promise<AnyData[]>` in field-aware mode.

### Built-In Filters

- text: `equal`, `notEqual`, `contains`, `notContains`, `beginsWith`, `notBeginsWith`, `endsWith`, `notEndsWith`
- number: text filters plus `greater`, `less`, `greaterOrEqual`, `lessOrEqual`, `between`, `notBetween`
- date: `equal`, `notEqual`, `greater`, `less`, `greaterOrEqual`, `lessOrEqual`, `between`, `notBetween`
- tuple: `greater`, `less`, `greaterOrEqual`, `lessOrEqual`, `equal`, `notEqual`
- date predicates: `month`, `year`, `yearMonth`

### Props And Behavior

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

## Public Types

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

## Styling

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

## Recipes

### Single Text Rule With Apply

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

### Live Rule Without Buttons

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

### Field Selector With Async Options

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

### Date Range Rule

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

### Tuple With Formatted Options

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

## Implementation Notes

- `FilterEditor` source treats `predicate`, `onApply`, `onCancel`, and `onChange` as optional
- source calls `onCancel()` with no payload, although the declaration types it as `(ev: { value: IFilter }) => void`.
