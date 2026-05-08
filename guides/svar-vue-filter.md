# svar-vue — filter

_Generated 2026-05-08T13:35:37.091Z_

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

Use when building, configuring, styling, or modifying SVAR Vue Filter / @svar-ui/vue-filter FilterBuilder, FilterEditor, FilterBar, or FilterQuery components

Package: `@svar-ui/vue-filter`
Syles: `@svar-ui/vue-filter/all.css`

The package ships `style.css` (this component only) and `all.css` (this component plus all dependencies).

Use this skill as an index. Load only the component reference needed for the task; each linked file is independent.

- `FilterBuilder.md` - visual query builder, nested filter groups, builder API/actions, builder styling.
- `FilterEditor.md` - standalone single-rule editor, field selector mode, option includes, editor styling.
- `FilterBar.md` - compact filter input row, `all` and `dynamic` field modes, bar styling.
- `FilterQuery.md` - query-string input, parse modes, autocomplete, natural text integrations, query styling.


## File: filter/FilterBar.md

> Source: `filter/FilterBar.md`

### FilterBar

Package: `@svar-ui/vue-filter`

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
} from "@svar-ui/vue-filter";
```

#### Supported Functionality

##### Data Contract

- `FilterBar` emits an `IFilterSet` through `onchange({ value })`.
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
- `onchange({ value })` receives the current `IFilterSet`.
- initial `value` field configs populate controls but do not emit until a change happens.

#### Public Types

```ts
import type { Component } from "vue";
import type {
	IFilterSet,
	IFilterBarField,
} from "@svar-ui/filter-store";

export declare const FilterBar: Component<{
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
	onchange?: (ev: { value: IFilterSet }) => void;
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

Import the package CSS before using the component (`all.css` includes dependency styles, `style.css` is this component only)

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

```vue
<template>
	<div class="bar-scope">
		<Willow>
			<FilterBar :fields="fields" :onchange="handleChange" />
		</Willow>
	</div>
</template>

<style scoped>
.bar-scope {
	--wx-label-font-size: 14px;
	--wx-label-font-weight: 600;
}

.bar-scope .wx-filter-bar {
	width: 100%;
	gap: 16px;
	padding: 10px 0;
}
</style>
```

#### Recipes

##### Basic Text, Number, And Select Fields

```vue
<script setup>
import { ref } from "vue";
import { FilterBar, createArrayFilter } from "@svar-ui/vue-filter";

const rows = ref(data);

function apply({ value }) {
	rows.value = createArrayFilter(value)(data);
}
</script>

<template>
	<FilterBar
		:fields="[
			'last_name',
			{ id: 'age', type: 'number', filter: 'greater' },
			{
				id: 'country',
				type: 'text',
				options: ['USA', 'Germany'],
				value: 'USA',
			},
		]"
		:onchange="apply"
	/>
</template>
```

##### Date Fields And Ranges

```vue
<template>
	<FilterBar
		:fields="[
			{
				id: 'start',
				type: 'date',
				filter: 'greater',
				value: new Date('2025-01-01'),
			},
			{
				id: 'end',
				type: 'date',
				filter: 'less',
				value: new Date('2025-05-01'),
			},
			{
				id: 'created',
				type: 'date',
				filter: 'between',
			},
		]"
		:onchange="({ value }) => applyFilter(value)"
	/>
</template>
```

##### Search Across Many Fields

```vue
<template>
	<FilterBar
		:fields="[
			{
				type: 'all',
				label: 'Search',
				placeholder: 'Search people',
				by: ['age', 'first_name', 'last_name'],
			},
		]"
		:onchange="({ value }) => applyFilter(value)"
	/>
</template>
```

##### Dynamic Field Selector

```vue
<template>
	<FilterBar
		:fields="[
			{
				type: 'dynamic',
				label: 'Filter by',
				placeholder: 'Enter value',
				by: [
					{ id: 'first_name', type: 'text', filter: 'contains' },
					'last_name',
					{ id: 'age', type: 'number', filter: 'greater' },
					{
						id: 'country',
						type: 'text',
						options: ['USA', 'Germany'],
						value: 'USA',
					},
					{
						id: 'start',
						type: 'date',
						filter: 'greater',
						value: new Date('2025-01-01'),
					},
				],
			},
		]"
		:onchange="({ value }) => applyFilter(value)"
	/>
</template>
```

##### Faster Text Updates

```vue
<template>
	<FilterBar
		:debounce="100"
		:fields="['first_name', 'last_name']"
		:onchange="({ value }) => applyFilter(value)"
	/>
</template>
```

#### Implementation Notes

- `FilterBar` stores one `lastField` for dynamic selectors; avoid multiple independent `type: "dynamic"` groups
- `normalizeField` only maps `options` for non-date fields.
- select options can be strings, numbers, or `{ id, label }` objects


## File: filter/FilterBuilder.md

> Source: `filter/FilterBuilder.md`

### FilterBuilder

Package: `@svar-ui/vue-filter`

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
} from "@svar-ui/vue-filter";
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
- `onchange` receives `{ value: IFilterSet }` after store-changing actions.
- other action callback props use event names with hyphens removed: `onaddrule`, `onaddgroup`, `oneditrule`, `onupdaterule`, `ondeleterule`, `ontoggleglue`, `onchangerule`.
- `init(api)` runs once after initial store setup.
- `ref="api"` exposes `exec`, `on`, `intercept`, `detach`, `setNext`, `getState`, `getReactiveState`, `getStores`, `getValue`.
- public actions: `add-rule`, `add-group`, `edit-rule`, `update-rule`, `delete-rule`, `toggle-glue`, `change-rule`, `change`.

#### Public Types

```ts
import type { Component } from "vue";
import type {
	IApi,
	TMethodsConfig,
	IConfig,
} from "@svar-ui/filter-store";

export declare const FilterBuilder: Component<
	{
		type?: "list" | "line" | "simple";
		init?: (api: IApi) => void;
	} & IConfig &
		FilterBuilderActions<TMethodsConfig>
>;

/* get component events from store actions*/
type RemoveHyphen<S extends string> = S extends `${infer Head}-${infer Tail}`
	? `${Head}${RemoveHyphen<Tail>}`
	: S;

type EventName<K extends string> = `on${RemoveHyphen<K>}`;

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

Import the package CSS before using the component (`all.css` includes dependency styles, `style.css` is this component only)

- no `css`, `class`, `className`, or `style` passthrough prop exists on `FilterBuilder`.
- use theme wrappers around the component: `<Willow>`, `<WillowDark>`.
- filter variables: `--wx-filter-value-color`, `--wx-filter-and-background`, `--wx-filter-or-background`, `--wx-filter-and-font-color`, `--wx-filter-or-font-color`, `--wx-filter-border`.
- shared variables used directly: `--wx-background`, `--wx-background-alt`, `--wx-border`, `--wx-border-radius`, `--wx-font-weight-md`, `--wx-line-height`.
- editor/input variables inside the rule editor come from `FilterEditor` and `@svar-ui/vue-core`.

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

```vue
<template>
	<div class="builder-scope">
		<Willow>
			<FilterBuilder :fields="fields" :options="options" :onchange="handleChange" />
		</Willow>
	</div>
</template>

<style scoped>
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
</style>
```

#### Recipes

##### Local Array Filtering

```vue
<script setup>
import { ref } from "vue";
import { FilterBuilder, Willow, createArrayFilter } from "@svar-ui/vue-filter";

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
const rows = ref(data);
const value = ref({ glue: "and", rules: [] });

function applyFilter({ value }) {
	rows.value = createArrayFilter(value)(data);
}
</script>

<template>
	<Willow>
		<FilterBuilder :value="value" :fields="fields" :options="options" :onchange="applyFilter" />
	</Willow>
</template>
```

##### Line Or Simple Layout

```vue
<template>
	<FilterBuilder
		:value="value"
		:fields="fields"
		:options="options"
		type="line"
		:onchange="({ value }) => applyFilter(value)"
	/>

	<FilterBuilder
		:value="value"
		:fields="fields"
		:options="options"
		type="simple"
		:onchange="({ value }) => applyFilter(value)"
	/>
</template>
```

##### Async Options

```vue
<script setup>
import { FilterBuilder } from "@svar-ui/vue-filter";

async function loadOptions(fieldId) {
	await new Promise(resolve => setTimeout(resolve, 300));
	return optionMap[fieldId] || [];
}
</script>

<template>
	<FilterBuilder :value="value" :fields="fields" :options="loadOptions" />
</template>
```

##### API And Event Interception

```vue
<script setup>
import { ref } from "vue";
import { FilterBuilder } from "@svar-ui/vue-filter";

const api = ref(null);
const valueText = ref("");

function init(api) {
	api.intercept("add-rule", ev => {
		ev.edit = false;
	});
	api.on("change", ({ value }) => {
		valueText.value = JSON.stringify(value, null, 2);
	});
}

function addAgeRule() {
	api.value.exec("add-rule", {
		rule: { field: "age", type: "number", filter: "greater", value: 30 },
		edit: false,
	});
}
</script>

<template>
	<button :onclick="addAgeRule">Add age rule</button>
	<FilterBuilder ref="api" :fields="fields" :options="options" :init="init" />
	<pre>{{ valueText }}</pre>
</template>
```

##### Convert Date Strings Around Builder UI

```vue
<script setup>
import { ref } from "vue";
import { FilterBuilder } from "@svar-ui/vue-filter";

const incoming = {
	rules: [{ field: "start", filter: "greater", value: "2025-01-01" }],
};

const value = ref({
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
</script>

<template>
	<FilterBuilder :value="value" :fields="fields" :options="options" :init="init" />
</template>
```


## File: filter/FilterEditor.md

> Source: `filter/FilterEditor.md`

### FilterEditor

Package: `@svar-ui/vue-filter`

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
} from "@svar-ui/vue-filter";
```

#### Supported Functionality

##### Data Contract

- emits one `IFilter` rule through `onapply` and `onchange`.
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

- source props: `fields = null`, `fieldsSelector = true`, `field = null`, `buttons = true`, `options = null`, `includes = null`, `type = "text"`, `filter = ""`, `value = ""`, `format = null`, `predicate = null`, `onapply`, `oncancel`, `onchange`.
- single-field mode: pass `type`, `field`, `filter`, `value`, `options`, `includes`, `format`, and `predicate` directly.
- multi-field mode: pass `fields`; selected field controls type, format, predicate, and loaded options.
- `fieldsSelector={false}` hides the field dropdown while keeping the selected field.
- `type="date"` uses `DatePicker`, except `filter="between"`/`"notBetween"` use `DateRangePicker`.
- `type="number"` uses numeric `Text`; `type="text"` uses text `Text`.
- `type="tuple"` uses `Combo` with options plus an automatic empty `$empty` / `None` option.
- option checkboxes are filtered by the current operator/value.
- `onchange({ value })` fires for UI changes when operator, value, field, or includes change.
- `onapply({ value })` fires from the Apply button.
- `oncancel()` fires from Cancel with no payload in source.
- `buttons={false}` hides Apply/Cancel and is normally paired with `onchange`.

#### Public Types

```ts
import type { Component } from "vue";
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

export declare const FilterEditor: Component<{
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
	onapply: (ev: { value: IFilter }) => void;
	oncancel: (ev: { value: IFilter }) => void;
	onchange: (ev: { value: IFilter }) => void;
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

Import the package CSS before using the component (`all.css` includes dependency styles, `style.css` is this component only)

- no `css`, `class`, `className`, or `style` passthrough prop exists on `FilterEditor`.
- use theme wrappers around the component: `<Willow>`, `<WillowDark>`.
- editor sets `--wx-input-border: var(--wx-filter-border)` on `.wx-filter-editor`.
- filter variables from themes: `--wx-filter-border`, `--wx-filter-value-color`, `--wx-filter-and-background`, `--wx-filter-or-background`, `--wx-filter-and-font-color`, `--wx-filter-or-font-color`.
- shared/core input variables come from `@svar-ui/vue-core`, including `--wx-input-*`.

Class hooks:

- root: `.wx-filter-editor`
- rows and cells: `.wx-wrapper`, `.wx-cell`
- option list: `.wx-list`, `.wx-item`

Layout defaults:

- `.wx-wrapper`: `display: flex`, `justify-content: right`, `gap: 10px`, `align-items: center`, `margin: 8px 0`.
- `.wx-cell`: `flex: 1`.
- `.wx-list`: `height: 150px`, `overflow-y: auto`, `margin: 8px 0`, `border: var(--wx-filter-border)`.
- `.wx-item`: `user-select: none`, `padding: 8px 12px`, `border-bottom: var(--wx-filter-border)`.

```vue
<template>
	<div class="editor-scope">
		<Willow>
			<FilterEditor type="text" :options="values" :onapply="handleApply" />
		</Willow>
	</div>
</template>

<style scoped>
.editor-scope {
	--wx-filter-border: 1px solid #d0d5dd;
}

.editor-scope .wx-item {
	padding: 12px 16px;
}
</style>
```

#### Recipes

##### Single Text Rule With Apply

```vue
<script setup>
import { ref } from "vue";
import { FilterEditor, createArrayFilter } from "@svar-ui/vue-filter";

const options = ["Alex", "Daisy", "John"];
const rows = ref(data);

function apply({ value }) {
	rows.value = createArrayFilter({ rules: [value] })(data);
}
</script>

<template>
	<FilterEditor
		type="text"
		field="first_name"
		:options="options"
		:onapply="apply"
	/>
</template>
```

##### Live Rule Without Buttons

```vue
<script setup>
import { ref } from "vue";
import { FilterEditor, createArrayFilter } from "@svar-ui/vue-filter";

const rule = ref({});
const rows = ref(data);

function update({ value }) {
	rule.value = value;
	rows.value = createArrayFilter({ rules: [value] })(data);
}
</script>

<template>
	<FilterEditor
		type="text"
		field="first_name"
		:options="['Alex', 'Daisy', 'John']"
		:buttons="false"
		:includes="rule.includes"
		:filter="rule.filter"
		:value="rule.value"
		:onchange="update"
	/>
</template>
```

##### Field Selector With Async Options

```vue
<script setup>
import { FilterEditor } from "@svar-ui/vue-filter";

const fields = [
	{ id: "first_name", label: "First Name", type: "text" },
	{ id: "age", label: "Age", type: "number" },
	{ id: "start", label: "Start Date", type: "date" },
];

async function loadOptions(field) {
	return optionMap[field] || [];
}
</script>

<template>
	<FilterEditor
		:fields="fields"
		field="age"
		:options="loadOptions"
		:onapply="({ value }) => console.log(value)"
	/>
</template>
```

##### Date Range Rule

```vue
<script setup>
import { FilterEditor, getOptions } from "@svar-ui/vue-filter";

const options = getOptions(data, "start");
</script>

<template>
	<FilterEditor
		field="start"
		:options="options"
		type="date"
		filter="between"
		:value="{
			start: new Date('2024-11-01'),
			end: new Date('2025-05-01'),
		}"
		:onapply="({ value }) => console.log(value)"
	/>
</template>
```

##### Tuple With Formatted Options

```vue
<script setup>
import { FilterEditor, getOptions } from "@svar-ui/vue-filter";

const options = getOptions(data, "start", {
	predicate: "month",
	sort: (a, b) => a - b,
});
const monthName = value => monthLabels[value] || String(value);
</script>

<template>
	<FilterEditor
		field="start"
		:options="options"
		:format="monthName"
		filter="greater"
		type="tuple"
		:onapply="({ value }) => console.log(value)"
	/>
</template>
```

#### Implementation Notes

- `FilterEditor` source treats `predicate`, `onapply`, `oncancel`, and `onchange` as optional
- source calls `oncancel()` with no payload, although the declaration types it as `(ev: { value: IFilter }) => void`.


## File: filter/FilterQuery.md

> Source: `filter/FilterQuery.md`

### FilterQuery

Package: `@svar-ui/vue-filter`

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
} from "@svar-ui/vue-filter";
```

#### Supported Functionality

##### Data Contract

- `value` is bindable and stores the query string with field IDs.
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
- Enter and the Search button call `onchange`.
- clear button resets local text and bound `value`, but does not call `onchange` until the user submits again.

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

- `onchange` runs on Enter, Search button, and external `value` updates after the first non-empty set.
- parse-enabled event shape: `{ parsed, value, text, error, startProgress, endProgress }`.
- `parsed` is a `ParseResult`.
- `error` is `null` or a localized `ValidationError` with `message`.
- with parse enabled, `text` is `parseResult.naturalText || ""` when there is no blocking error, otherwise the current query text.
- with `parse="none"`, event shape is `{ value, text, startProgress, endProgress }`.

#### Public Types

```ts
import type { Component } from "vue";
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

#### Styling

Import the package CSS before using the component (`all.css` includes dependency styles, `style.css` is this component only)

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

```vue
<template>
	<div class="query-scope">
		<Willow>
			<FilterQuery :fields="fields" :options="options" :onchange="handleFilter" />
		</Willow>
	</div>
</template>

<style scoped>
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

#### Recipes

##### Structured Query With Local Filtering

```vue
<script setup>
import { ref } from "vue";
import { FilterQuery, createArrayFilter } from "@svar-ui/vue-filter";

const value = ref("");
const rows = ref(data);

function handleFilter({ value, error }) {
	if (error && error.code !== "NO_DATA") return;
	rows.value = createArrayFilter(value, {}, fields)(data);
}
</script>

<template>
	<FilterQuery
		v-model:value="value"
		placeholder="e.g. FirstName: Alex or #urgent"
		:fields="fields"
		:options="{ ...options, '#': ['urgent', 'review', 'done'] }"
		:onchange="handleFilter"
	/>
</template>
```

##### Strict Query Syntax

```vue
<template>
	<FilterQuery
		v-model:value="query"
		parse="strict"
		placeholder="Status: Open and Age: >30"
		:fields="fields"
		:options="options"
		:onchange="({ value, error }) => {
			if (!error) applyFilter(value);
		}"
	/>
</template>
```

##### Natural Text Endpoint

```vue
<script setup>
import { ref } from "vue";
import { FilterQuery, createArrayFilter, getQueryString } from "@svar-ui/vue-filter";

const normalizedQuery = ref("");
const rows = ref(data);

async function handleNatural({ text, startProgress, endProgress }) {
	try {
		startProgress();
		const filter = await textToFilter(text, fields);
		normalizedQuery.value = filter ? getQueryString(filter).query : "";
		rows.value = createArrayFilter(filter || { rules: [] })(data);
	} finally {
		endProgress();
	}
}
</script>

<template>
	<FilterQuery
		parse="none"
		placeholder="first name contains Alex and age greater than 30"
		:onchange="handleNatural"
	/>

	<pre>{{ normalizedQuery }}</pre>
</template>
```

##### Mixed Query And Natural Text

```vue
<script setup>
import { ref } from "vue";
import { FilterQuery, createArrayFilter, getQueryString } from "@svar-ui/vue-filter";

const query = ref("start: 2024");
const rows = ref(data);

async function handleMixed({ value, error, text, startProgress, endProgress }) {
	if (text) {
		try {
			startProgress();
			value = await textToFilter(text, fields);
			query.value = value ? getQueryString(value).query : "";
			error = null;
		} finally {
			endProgress();
		}
	}

	if (error && error.code !== "NO_DATA") return;
	rows.value = createArrayFilter(value, {}, fields)(data);
}
</script>

<template>
	<FilterQuery
		v-model:value="query"
		placeholder="FirstName: contains Alex and Age: >30"
		:fields="fields"
		:options="options"
		:onchange="handleMixed"
	/>
</template>
```

##### Render Query HTML

```vue
<script setup>
import { computed } from "vue";
import { getQueryHtml, getQueryString } from "@svar-ui/vue-filter";

const html = computed(() =>
	filterValue
		? getQueryHtml(getQueryString(filterValue).query, { fields })
		: ""
);
</script>

<template>
	<div v-html="html"></div>
</template>
```

#### Implementation Notes

- `parse="none"` bypasses highlight, autocomplete, parsing, and validation entirely.
- `NO_DATA` errors still pass parsed config and can be treated as non-blocking
- `getQueryHtml` returns inline styled HTML; only use it in trusted/internal query display contexts.


## File: locales.md

> Source: `locales.md`

i18n patterns common to all SVAR Vue components - Locale wrapper, bundled language packs, extending words and formats

### Localizing SVAR Vue Components

All `@svar-ui/vue-*` widgets read locale data from a single Vue inject key (`wx-i18n`). The mechanics live in `@svar-ui/vue-core`; every other package consumes them.

#### Locale Wrapper

Wrap the subtree you want to localize. With no wrapper, widgets fall back to English.

```vue
<script setup>
import { Calendar, Locale } from "@svar-ui/vue-core";
import { de } from "@svar-ui/core-locales";
</script>

<template>
  <Locale :words="de">
    <Calendar :value="new Date(2025, 4, 1)" />
  </Locale>
</template>
```

Wrap the smallest subtree that needs the alternative locale - nested `Locale` blocks let different parts of the app render in different languages.

`Locale` does not render any DOM wrapper; it only mutates the injected context, so it never affects layout.

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

If you see English fallbacks in a localized UI, the missing terms come from the package's own locale module - merge them in via `<Locale :words="..." />`.

To localize a standalone widget, merge the matching package locale with the core locale:

```vue
<script setup>
import { Gantt } from "@svar-ui/vue-gantt";
import { Locale } from "@svar-ui/vue-core";
import { cn } from "@svar-ui/gantt-locales";
import { cn as cnCore } from "@svar-ui/core-locales";
</script>

<template>
  <Locale :words="{ ...cn, ...cnCore }">
    <Gantt v-bind="settings" />
  </Locale>
</template>
```

#### Extending Or Overriding Words

`Locale words` accepts a partial pack and extends the current context. Spread an existing pack to keep its formats and override only what you need:

```vue
<script setup>
import { Calendar, Locale } from "@svar-ui/vue-core";
import { cn } from "@svar-ui/core-locales";

const words = {
    ...cn,
    formats: {
        ...cn.formats,
        monthYearFormat: "%Y年%F",
        yearFormat: "%Y年",
    },
};
</script>

<template>
  <Locale :words="words">
    <Calendar :value="new Date(2025, 4, 1)" />
  </Locale>
</template>
```

Pass `:optional="true"` to make merged terms additive fallbacks rather than overrides - useful for layering app-specific strings on top of a full pack.

#### Affected Surfaces

Locale changes calendar labels, date/time formats, modal buttons, pager strings, empty-list text, notice/modal helpers, color-board select text - any widget that displays static strings or formats values reads them through this context.

#### Direct Helper

For non-component code, use the `locale` helper to build a translator:

```js
import { en, locale } from "@svar-ui/vue-core";

const i18n = locale(en).extend(
    { core: { "Rows per page": "Rows" } },
    true
);
const _ = i18n.getGroup("core");
_("Rows per page"); // "Rows"
```


## File: themes.md

> Source: `themes.md`

### Styling SVAR Vue Components

All `@svar-ui/vue-*` widgets share the same theming pipeline. The mechanics live in `@svar-ui/vue-core`; every other package consumes them.

#### Per widget css files

Each package ships `style.css` (this component only) and `all.css` (this component plus all dependencies).

```css
@import "@svar-ui/vue-gantt/style.css";
```

#### Theme Wrapper

Wrap the part of the app that uses SVAR widgets in a theme component from `@svar-ui/vue-core`:

```vue
<script setup>
import { Willow } from "@svar-ui/vue-core";
</script>

<template>
  <Willow>
    <App />
  </Willow>
</template>
```

Available themes: `Willow`, `WillowDark`. The wrapper:

- provides the Vue inject key `wx-theme`
- renders `.wx-theme.wx-{name}-theme` with `height:100%`
- loads Open Sans + the `wxi` icon CSS by default; pass `:fonts="false"` to skip when the host app manages fonts itself

Without a theme wrapper widgets still render but lose theme variables and font/icon CSS.

#### Per-widget Willow / WillowDark themes

Several widgets ship their **own** `Willow` / `WillowDark` components on top of the core base. The widget version wraps the core theme and layers in widget-specific CSS variables (bar colors, grid borders, timescale fonts, etc.). When using such a widget, import the theme from the widget package - not from core - so both layers apply.

Widgets that expose custom `Willow` / `WillowDark` themes:

- `@svar-ui/vue-core` - base
- `@svar-ui/vue-gantt`
- `@svar-ui/vue-grid`
- `@svar-ui/vue-editor`
- `@svar-ui/vue-filter`
- `@svar-ui/vue-filemanager`
- `@svar-ui/vue-comments`
- `@svar-ui/vue-kanban`

The widget theme delegates to core and adds extra rules scoped to `.wx-willow-theme` (or `.wx-willow-dark-theme`):

```vue
<script setup>
import { Willow } from "@svar-ui/vue-core";
defineProps({ fonts: { type: Boolean, default: true } });
</script>

<template>
  <Willow :fonts="fonts">
    <slot v-if="$slots.default" />
  </Willow>
</template>

<style scoped>
:global(.wx-willow-theme) {
    --wx-gantt-border-color: #e6e6e6;
    --wx-gantt-task-color: #3983eb;
    /* ...widget-specific overrides... */
}
</style>
```

Mount the widget's own theme once at the app root. The wrapper internally renders the core `Willow`, so a separate core import is not needed:

```vue
<script setup>
import { Willow, Gantt } from "@svar-ui/vue-gantt";
</script>

<template>
  <Willow />
  <Gantt v-bind="settings" />
</template>
```

#### CSS Variables

Theme styling is variable-driven. Override variables on the theme wrapper or on any ancestor of the widgets you want to restyle - overrides cascade to every SVAR widget in the subtree.

```vue
<template>
  <Willow>
    <div class="brand">
      <App />
    </div>
  </Willow>
</template>

<style scoped>
.brand {
    --wx-color-primary: #0f766e;
    --wx-input-width: 280px;
    --wx-button-border-radius: 4px;
    --wx-calendar-cell-size: 30px;
}
</style>
```

Nest different wrapper blocks for per-section restyling without forking the theme.

#### `css` Prop Convention

Most widgets accept a `css` prop. The string is appended to the widget's root class, so it works as a parent styling hook:

```vue
<template>
  <Toolbar css="my-toolbar" :items="items" />
</template>

<style scoped>
.my-toolbar {
    padding: 8px 12px;
}
</style>
```

Composite widgets often expose secondary css props for nested popups (`menuCss` on `Toolbar`/`MenuBar`, etc.). Check the per-component file for the exact set.

#### Class Hooks

The per-component file lists the exact selectors that widget exposes.

#### Custom CSS class overrides

When writing custom rules to override widget styles, always use **at least two selectors** (e.g. `.a .b {}`). Vue scopes its component styles by appending a hash attribute which has higher specificity than a plain `.b`. A two-selector rule (`.a .b`) matches or beats that specificity and wins.

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
