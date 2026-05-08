# SVAR Vue Core DatePicker

Package: `@svar-ui/vue-core`

## Package

```js
import { DatePicker } from "@svar-ui/vue-core";
```

## Supported Functionality

- Input-like single-date picker backed by `Text`, `Dropdown`, and `Calendar`.
- `value` is bindable and is a `Date` or `null`.
- `format` can be a date format string or `(value: Date) => string`; locale date format is used by default.
- `editable={true}` parses committed text with `new Date(text)`.
- `editable={fn}` uses the custom parser and expects `Date | null`.
- `clear` passes through to the inner `Text` clear icon.
- `buttons` is forwarded to `Calendar`; default is `["clear", "today"]`.
- `dropdown` is forwarded to `Dropdown`; date dropdowns default width to `"unset"` when no width is provided.
- Popup closes on window scroll.
- `onchange` receives `{ value: Date | null }` after the bindable value is updated.

## Public Types

```ts
import type { Component } from "vue";

export interface DropdownOptions {
	inline?: boolean;
	position?: "top" | "right" | "bottom" | "left";
	align?: "start" | "center" | "end";
	css?: string;
	width?: string | "unset" | "auto";
	trackScroll?: boolean;
	virtualized?: boolean;
}

export declare const DatePicker: Component<{
	value?: Date;
	id?: string | number;
	disabled?: boolean;
	error?: boolean;
	width?: string;
	align?: "start" | "center" | "end";
	placeholder?: string;
	format?: string | ((value: Date) => string);
	buttons?: boolean | ("clear" | "today")[];
	css?: string;
	title?: string;
	editable?: boolean | ((value: string) => Date | null);
	clear?: boolean;
	dropdown?: DropdownOptions;
	onchange?: (ev: { value: Date | null }) => void;
}>;
```

## Styling

- Wrapper: `.wx-datepicker`
- `css` is passed to the inner `Text`; use `css="wx-icon-left"` for the left-icon input variant.
- Inner input classes come from `Text`: `.wx-text`, `.wx-input`, `.wx-icon`, `.wx-error`, `.wx-disabled`, `.wx-focus`.
- Popup surface uses `Dropdown`/`Popup` hooks such as `.wx-popup`.
- Calendar hooks come from `Calendar` and `Month`.


```vue
<template>
  <DatePicker css="wx-icon-left date-input" :dropdown="{ css: 'date-popup' }" />
</template>

<style scoped>
.wx-text.date-input {
	--wx-input-width: 220px;
}

.wx-popup.date-popup {
	padding: 4px;
}
</style>
```

## Recipes

### Bound Date In A Field

```vue
<script setup>
import { ref } from "vue";
import { DatePicker, Field } from "@svar-ui/vue-core";

const value = ref(new Date(2025, 4, 1));
</script>

<template>
  <Field label="Date" position="left">
    <DatePicker v-model:value="value" clear :onchange="ev => console.log(ev.value)" />
  </Field>
</template>
```

### Editable Date With Custom Parser

```vue
<script setup>
import { ref } from "vue";
import { DatePicker } from "@svar-ui/vue-core";

const value = ref(new Date(2025, 4, 1));

function parseDate(text) {
	const p = text.match(/(..)(..)(.+)/);
	return p ? new Date(p.slice(1, 4).join("/")) : null;
}
</script>

<template>
  <DatePicker
    v-model:value="value"
    :editable="parseDate"
    format="%m%d%Y"
    clear
    :dropdown="{ width: '280px', align: 'start' }"
  />
</template>
```

## Implementation Notes

- Public types include `width` and `align`, but source does not use those props directly; use `dropdown={{ width, align }}`.
- Selecting the same date value does not emit `onchange`.
