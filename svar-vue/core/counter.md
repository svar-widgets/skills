# SVAR Vue Core Counter

Package: `@svar-ui/vue-core`

## Package

```js
import { Counter } from "@svar-ui/vue-core";
```

## Supported Functionality

- Numeric input with decrement and increment buttons.
- Bindable `value`, default `0`.
- `step` defaults to `1`, `min` defaults to `0`, `max` defaults to `Infinity`.
- Button clicks update `value` and emit `{ value }`.
- Typing emits `{ value, input: true }` without immediately mutating the bound value in the handler payload path.
- Blur normalizes the bound value to min/max and step, then emits `{ value }`.
- `readonly` blocks button changes and blur normalization.
- `disabled` disables the input and both buttons.

## Public Types

```ts
import type { Component } from "vue";

export declare const Counter: Component<{
	id?: string | number;
	value?: number;
	step?: number;
	min?: number;
	max?: number;
	error?: boolean;
	disabled?: boolean;
	readonly?: boolean;
	onchange?: (ev: { value: number; input?: boolean }) => void;
}>;
```

## Styling

- Wrapper: `.wx-counter`
- State classes: `.wx-disabled`, `.wx-readonly`, `.wx-error`
- Input: `.wx-input`
- Buttons: `.wx-btn`, `.wx-btn-dec`, `.wx-btn-inc`
- SVG icons: `.wx-dec`, `.wx-inc`

```vue
<template>
  <Counter v-model:value="value" :min="0" :max="30" />
</template>

<style scoped>
.wx-counter .wx-input {
	width: 64px;
}
</style>
```

## Recipes

### Counter With Final Change Handling

```vue
<script setup>
import { ref } from "vue";
import { Counter, Field } from "@svar-ui/vue-core";

const count = ref(5);
</script>

<template>
  <Field label="Quantity">
    <Counter
      v-model:value="count"
      :min="0"
      :max="30"
      :step="3"
      :onchange="ev => {
        if (!ev.input) console.log(ev.value);
      }"
    />
  </Field>
</template>
```
