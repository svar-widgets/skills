# SVAR Vue Core Checkbox

Package: `@svar-ui/vue-core`

Use this file standalone for `Checkbox` and `CheckboxGroup`.

## Package

```js
import { Checkbox, CheckboxGroup } from "@svar-ui/vue-core";
```

## Supported Functionality

- `Checkbox.value` is a bindable boolean.
- `Checkbox.inputValue` is emitted alongside the checked state; default is an empty string.
- `Checkbox.onchange` emits `{ value, inputValue }`.
- `CheckboxGroup.options` are `{ id, label }`.
- `CheckboxGroup.value` is a bindable array of selected option ids.
- Group `onchange` emits `{ value }`.
- Group `type` supports `inline` and `grid`; default layout is one item per row.

## Public Types

```ts
import type { Component } from "vue";

export declare const Checkbox: Component<{
	id?: string | number;
	label?: string;
	inputValue?: string | number;
	value?: boolean;
	style?: string;
	disabled?: boolean;
	onchange?: (ev: { value: boolean; inputValue: string | number }) => void;
}>;

export declare const CheckboxGroup: Component<{
	options?: { id: string | number; label: string }[];
	value?: (string | number)[];
	type?: "inline" | "grid";
	onchange?: (ev: { value: (string | number)[] }) => void;
}>;
```

## Styling

- Checkbox wrapper: `.wx-checkbox`
- `style` prop is applied to the checkbox wrapper.
- Group wrapper: `.wx-checkboxgroup`, `.wx-checkboxgroup.wx-inline`, `.wx-checkboxgroup.wx-grid`
- Group item wrapper: `.wx-item`

```vue
<template>
  <div class="todo-checks">
    <CheckboxGroup :options="options" v-model:value="value" />
  </div>
</template>

<style scoped>
.todo-checks .wx-checkboxgroup .wx-item {
	margin-top: 8px;
}
</style>
```

## Recipes

### Single Checkbox

```vue
<script setup>
import { ref } from "vue";
import { Checkbox } from "@svar-ui/vue-core";

const done = ref(false);
</script>

<template>
  <Checkbox
    label="Done"
    inputValue="done"
    v-model:value="done"
    :onchange="ev => console.log(ev.value, ev.inputValue)"
  />
</template>
```

### Checkbox Group

```vue
<script setup>
import { ref } from "vue";
import { CheckboxGroup } from "@svar-ui/vue-core";

const options = [
	{ id: "new", label: "New" },
	{ id: "open", label: "Open" },
	{ id: "done", label: "Done" },
];

const selected = ref(["new"]);
</script>

<template>
  <CheckboxGroup :options="options" v-model:value="selected" type="inline" />
</template>
```

## Implementation Notes

- `CheckboxGroup` does not pass disabled state through option objects.
