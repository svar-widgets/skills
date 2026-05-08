# FilterQuery

Package: `@svar-ui/svelte-filter`

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
} from "@svar-ui/svelte-filter";
```

## Supported Functionality

### Data Contract

- `value` is bindable and stores the query string with field IDs.
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
- Enter and the Search button call `onchange`.
- clear button resets local text and bound `value`, but does not call `onchange` until the user submits again.

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

- `onchange` runs on Enter, Search button, and external `value` updates after the first non-empty set.
- parse-enabled event shape: `{ parsed, value, text, error, startProgress, endProgress }`.
- `parsed` is a `ParseResult`.
- `error` is `null` or a localized `ValidationError` with `message`.
- with parse enabled, `text` is `parseResult.naturalText || ""` when there is no blocking error, otherwise the current query text.
- with `parse="none"`, event shape is `{ value, text, startProgress, endProgress }`.

## Public Types

```ts
import type { Component } from "svelte";
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

export declare const FilterQuery: Component<{
	value?: string;
	placeholder?: string;
	parse?: "none" | "strict" | "allowFreeText";
	fields?: IField[];
	options?: IDataHash<AnyData[]>;
	onchange?: (ev: FilterQueryEvent) => void;
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

```svelte
<div class="query-scope">
	<Willow>
		<FilterQuery {fields} {options} onchange={handleFilter} />
	</Willow>
</div>

<style>
	.query-scope {
		--wx-filter-query-field-color: #7c3aed;
		--wx-filter-query-value-color: #059669;
		--wx-color-primary: #7c3aed;
	}

	.query-scope .wx-filter-query-search {
		background: #0f172a;
		color: #f8fafc;
	}
</style>
```

## Recipes

### Structured Query With Local Filtering

```svelte
<script>
	import { FilterQuery, createArrayFilter } from "@svar-ui/svelte-filter";

	let value = $state("");
	let rows = $state(data);

	function handleFilter({ value, error }) {
		if (error && error.code !== "NO_DATA") return;
		rows = createArrayFilter(value, {}, fields)(data);
	}
</script>

<FilterQuery
	bind:value
	placeholder="e.g. FirstName: Alex or #urgent"
	{fields}
	options={{ ...options, "#": ["urgent", "review", "done"] }}
	onchange={handleFilter}
/>
```

### Strict Query Syntax

```svelte
<FilterQuery
	bind:value={query}
	parse="strict"
	placeholder="Status: Open and Age: >30"
	{fields}
	{options}
	onchange={({ value, error }) => {
		if (!error) applyFilter(value);
	}}
/>
```

### Natural Text Endpoint

```svelte
<script>
	import { FilterQuery, createArrayFilter, getQueryString } from "@svar-ui/svelte-filter";

	let normalizedQuery = $state("");
	let rows = $state(data);

	async function handleNatural({ text, startProgress, endProgress }) {
		try {
			startProgress();
			const filter = await textToFilter(text, fields);
			normalizedQuery = filter ? getQueryString(filter).query : "";
			rows = createArrayFilter(filter || { rules: [] })(data);
		} finally {
			endProgress();
		}
	}
</script>

<FilterQuery
	parse="none"
	placeholder="first name contains Alex and age greater than 30"
	onchange={handleNatural}
/>

<pre>{normalizedQuery}</pre>
```

### Mixed Query And Natural Text

```svelte
<script>
	import { FilterQuery, createArrayFilter, getQueryString } from "@svar-ui/svelte-filter";

	let query = $state("start: 2024");
	let rows = $state(data);

	async function handleMixed({ value, error, text, startProgress, endProgress }) {
		if (text) {
			try {
				startProgress();
				value = await textToFilter(text, fields);
				query = value ? getQueryString(value).query : "";
				error = null;
			} finally {
				endProgress();
			}
		}

		if (error && error.code !== "NO_DATA") return;
		rows = createArrayFilter(value, {}, fields)(data);
	}
</script>

<FilterQuery
	bind:value={query}
	placeholder="FirstName: contains Alex and Age: >30"
	{fields}
	{options}
	onchange={handleMixed}
/>
```

### Render Query HTML

```svelte
<script>
	import { getQueryHtml, getQueryString } from "@svar-ui/svelte-filter";

	let html = $derived(
		filterValue
			? getQueryHtml(getQueryString(filterValue).query, { fields })
			: ""
	);
</script>

<!-- eslint-disable-next-line svelte/no-at-html-tags -->
{@html html}
```

## Implementation Notes

- `parse="none"` bypasses highlight, autocomplete, parsing, and validation entirely.
- `NO_DATA` errors still pass parsed config and can be treated as non-blocking
- `getQueryHtml` returns inline styled HTML; only use it in trusted/internal query display contexts.
