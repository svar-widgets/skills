# SVAR Vue Core Select

Package: `@svar-ui/vue-core`

## Package

```js
import { Select } from "@svar-ui/vue-core";
```

## Supported Functionality

- Renders a native `<select>` inside `.wx-select`.
- `options` are `{ id, label }` by default.
- `textField` changes the displayed field; default is `"label"`.
- `value` is bindable and stores the selected option id.
- `placeholder` is shown as an overlay when value is empty and not `0`.
- `clear` shows a close icon when the component has a value and is not disabled.
- `onchange` emits `{ value }`.

## Public Types

```ts
import type { Component } from "vue";

export declare const Select: Component<{
	value?: string | number;
	options?: { id: string | number; label: string }[];
	placeholder?: string;
	title?: string;
	disabled?: boolean;
	error?: boolean;
	textField?: string;
	clear?: boolean;
	id?: string | number;
	onchange?: (ev: { value: string | number }) => void;
}>;
```

## Styling

- Wrapper: `.wx-select`
- Placeholder overlay: `.wx-placeholder`
- Icon: `.wx-icon`, close icon `.wxi-close`
- Error class is applied to the native `select` as `.wx-error`.

```vue
<template>
  <div class="owner-select">
    <Select :options="users" v-model:value="value" clear />
  </div>
</template>

<style scoped>
.owner-select .wx-select {
	--wx-input-width: 280px;
}
</style>
```

## Recipes

### Native Select With Clear

```vue
<script setup>
import { ref } from "vue";
import { Field, Select } from "@svar-ui/vue-core";

const users = [
	{ id: 103, label: "Ned Stark" },
	{ id: 104, label: "Lord Varys" },
];

const owner = ref("");
</script>

<template>
  <Field label="Owner" position="left">
    <Select
      :options="users"
      v-model:value="owner"
      placeholder="Select owner"
      clear
    />
  </Field>
</template>
```

## Implementation Notes

- `Select` has no `css` prop; use a parent/global selector for styling.
