# SVAR Vue Core Field

Package: `@svar-ui/vue-core`

## Package

```js
import { Field } from "@svar-ui/vue-core";
```

## Supported Functionality

- Wraps controls with label and control layout.
- Default label position is top; `position="left"` creates a side label layout.
- `width` sets inline width on the `.wx-field` wrapper.
- `error` adds `.wx-error` and colors the label.
- `required` adds `.wx-required` and appends a red `*` to the label.
- `type="checkbox" | "slider" | "switch"` adjusts vertical padding for those controls in left-label layout.
- Sets Vue inject key `wx-input-id`; child controls that call `getInputId` share the generated id with the label.

## Public Types

```ts
import type { Component } from "vue";

export declare const Field: Component<{
	label?: string;
	position?: "left";
	width?: string;
	error?: boolean;
	type?: "checkbox" | "slider" | "switch";
	required?: boolean;
	children?: () => any;
}>;
```

## Styling

- Wrapper: `.wx-field`
- Side label modifier: `.wx-left`
- State classes: `.wx-error`, `.wx-required`
- Label: `.wx-label`
- Control wrapper: `.wx-field-control`
- Control type modifiers: `.wx-field-control.wx-checkbox`, `.wx-field-control.wx-slider`, `.wx-field-control.wx-switch`


```vue
<template>
  <Field label="Owner" position="left" width="480px">
    <slot />
  </Field>
</template>

<style scoped>
.wx-field.wx-left > .wx-label {
	width: 140px;
}
</style>
```

## Recipes

### Labeled Control

```vue
<script setup>
import { ref } from "vue";
import { Field, Text } from "@svar-ui/vue-core";

const name = ref("");
</script>

<template>
  <Field label="Name" required>
    <Text v-model:value="name" />
  </Field>
</template>
```

### Nested Fields

```vue
<script setup>
import { Field, Text } from "@svar-ui/vue-core";
</script>

<template>
  <Field label="Name">
    <Field label="First" position="left">
      <Text />
    </Field>
    <Field label="Last" position="left">
      <Text />
    </Field>
  </Field>
</template>
```
