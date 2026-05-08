# FilterQuery

Package: `@svar-ui/react-filter`

Use this file independently when building, configuring, styling, or modifying `FilterQuery`.

## Import

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

## Supported Functionality

### Data Contract

- `value` is a controlled prop and stores the query string with field IDs.
- displayed `text` uses sanitized field labels when `fields` include labels.
- field labels are sanitized by removing parser-special characters; `{ id: "first_name", label: "First Name" }` displays as `FirstName:`.
- `fields`: array of `{ id, label, type, predicate?, format? }`.
- `options`: `{ [fieldId]: AnyData[] }`; tag suggestions use `options["#"]`.
- parse-enabled callbacks receive `value: IFilterSet | IFilter | null`.
- `parse="none"` callbacks receive raw `value` and `text` strings.
- `startProgress()` and `endProgress()` control the top progress bar for async filtering.

### Parse Modes

- `parse` defaults to `"allowFreeText"`.
- `parse="allowFreeText"` parses query syntax and converts plain words into `field: "*"` `contains` filters.
- `parse="strict"` parses query syntax but disables free-text fallback.
- `parse="none"` disables parser, syntax highlight, autocomplete, and validation; use it for natural-language endpoints.
- Enter and the Search button call `onChange`.
- clear button resets local text and controlled `value`, but does not call `onChange` until the user submits again.

### Query Syntax Highlights

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

### Autocomplete

- field suggestions match field `id` and sanitized `label`, and insert the label into text.
- value suggestions come from `options[fieldId]`.
- tag suggestions come from `options["#"]`.
- date predicate suggestions are `year` and `month`.
- value suggestion labels use the field `format` function when present.
- suggestions rank starts-with matches before contains matches.
- keyboard support: ArrowDown/ArrowUp navigates, Enter selects when focused, Escape/Tab closes.

### Events

- `onChange` runs on Enter, Search button, and external `value` updates after the first non-empty set.
- parse-enabled event shape: `{ parsed, value, text, error, startProgress, endProgress }`.
- `parsed` is a `ParseResult`.
- `error` is `null` or a localized `ValidationError` with `message`.
- with parse enabled, `text` is `parseResult.naturalText || ""` when there is no blocking error, otherwise the current query text.
- with `parse="none"`, event shape is `{ value, text, startProgress, endProgress }`.

## Public Types

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

## Styling

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

## Recipes

### Structured Query With Local Filtering

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

### Strict Query Syntax

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

### Natural Text Endpoint

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

### Mixed Query And Natural Text

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

### Render Query HTML

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

## Implementation Notes

- `parse="none"` bypasses highlight, autocomplete, parsing, and validation entirely.
- `NO_DATA` errors still pass parsed config and can be treated as non-blocking
- `getQueryHtml` returns inline styled HTML; only use it in trusted/internal query display contexts.
