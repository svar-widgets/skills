# SVAR Vue Core ColorSelect

Package: `@svar-ui/vue-core`

## Package

```js
import { ColorSelect } from "@svar-ui/vue-core";
```

## Supported Functionality

- Input-like color palette selector.
- `value` is a bindable hex color string or empty string.
- Default colors are `#00a037`, `#37a9ef`, `#f5a623`, `#ff4c3b`, `#a0a0a0`, `#000000`, `#ffffff`.
- Clicking the input opens a `Dropdown` unless disabled.
- Palette includes an empty color item that selects `""`.
- `clear` shows a close icon when value is set and not disabled.
- `onchange` emits `{ value }`.

## Public Types

```ts
import type { Component } from "vue";

export declare const ColorSelect: Component<{
	colors?: string[];
	value?: string;
	id?: string | number;
	clear?: boolean;
	placeholder?: string;
	title?: string;
	disabled?: boolean;
	error?: boolean;
	onchange?: (ev: { value: string }) => void;
}>;
```

## Styling

- Wrapper: `.wx-colorselect`
- Selected swatch: `.wx-selected`
- Dropdown palette: `.wx-colors`
- Swatch: `.wx-color`
- Empty swatch: `.wx-empty`
- Clear icon: `.wx-clear.wxi-close`


```vue
<template>
  <ColorSelect :colors="colors" v-model:value="value" clear />
</template>

<style scoped>
.wx-colorselect .wx-color {
	border-radius: 50%;
}
</style>
```

## Recipes

### Custom Palette

```vue
<script setup>
import { ref } from "vue";
import { ColorSelect, Field } from "@svar-ui/vue-core";

const color = ref("");
</script>

<template>
  <Field label="Color" position="left">
    <ColorSelect
      :colors="['#65D3B3', '#FFC975', '#58C3FE']"
      v-model:value="color"
      placeholder="Select a color"
      clear
    />
  </Field>
</template>
```
