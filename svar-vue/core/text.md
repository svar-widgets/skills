# SVAR Vue Core Text

Package: `@svar-ui/vue-core`

## Package

```js
import { Text } from "@svar-ui/vue-core";
```

## Supported Functionality

- Bindable `value`, with `string | number` public type.
- `type` supports `text`, `number`, and `password`; default is `text`.
- `onchange` fires `{ value, input: true }` on input and `{ value }` on native change.
- `focus` and `select` focus/select the input after mount.
- `clear` shows a close icon when the input has a value; clicking it sets `value = ""` and emits `{ value }`.
- `icon` renders inside the input. It is right-aligned unless `css` includes `wx-icon-left`.
- `inputStyle` is applied to the inner `<input>`.
- `readonly`, `disabled`, `error`, `placeholder`, and `title` are forwarded to the input/wrapper.

## Public Types

```ts
import type { Component } from "vue";

export declare const Text: Component<{
	value?: string | number;
	id?: string | number;
	readonly?: boolean;
	focus?: boolean;
	select?: boolean;
	type?: "text" | "number" | "password";
	placeholder?: string;
	disabled?: boolean;
	error?: boolean;
	inputStyle?: string;
	title?: string;
	css?: string;
	icon?: string;
	clear?: boolean;
	onchange?: (ev: { value: string | number; input?: boolean }) => void;
}>;
```

## Styling

- Wrapper: `.wx-text`
- State/classes: `.wx-error`, `.wx-disabled`, `.wx-clear`, `.wx-icon-left`, `.wx-icon-right`
- Icon: `.wx-icon`; clear icon: `.wx-icon.wxi-close`
- `css` is appended to `.wx-text`.

```vue
<template>
  <Text css="search-input wx-icon-left" icon="wxi-search" clear />
</template>

<style scoped>
.wx-text.search-input {
	--wx-input-width: 320px;
}
</style>
```

## Recipes

### Text With Clear And Left Icon

```vue
<script setup>
import { ref } from "vue";
import { Field, Text } from "@svar-ui/vue-core";

const query = ref("");
</script>

<template>
  <Field label="Search" position="left">
    <Text
      v-model:value="query"
      placeholder="Type here"
      icon="wxi-search"
      css="wx-icon-left"
      clear
      :onchange="ev => {
        if (!ev.input) console.log('final', ev.value);
      }"
    />
  </Field>
</template>
```

### Focus And Select On Mount

```vue
<script setup>
import { Text } from "@svar-ui/vue-core";
</script>

<template>
  <Text value="Some value" focus select />
</template>
```

## Implementation Notes

- `type="number"` still binds through the input value; account for string/number conversion in your app logic.
