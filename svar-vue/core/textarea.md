# SVAR Vue Core TextArea

Package: `@svar-ui/vue-core`

## Package

```js
import { TextArea } from "@svar-ui/vue-core";
```

## Supported Functionality

- Renders a native `<textarea class="wx-textarea">`.
- `value` is bindable.
- `onchange` fires `{ value, input: true }` on input and `{ value }` on native change.
- Supports `id`, `placeholder`, `title`, `disabled`, `error`, and `readonly`.
- The textarea is vertically resizable unless disabled.

## Public Types

```ts
import type { Component } from "vue";

export declare const TextArea: Component<{
	value?: string;
	id?: string | number;
	placeholder?: string;
	title?: string;
	disabled?: boolean;
	error?: boolean;
	readonly?: boolean;
	onchange?: (ev: { value: string; input?: boolean }) => void;
}>;
```

## Styling

- Textarea: `.wx-textarea`
- Error state: `.wx-textarea.wx-error`
- Disabled state uses `[disabled]`.

```vue
<template>
  <TextArea placeholder="Details" />
</template>

<style scoped>
.wx-textarea {
	min-height: 140px;
}
</style>
```

## Recipes

### TextArea In A Field

```vue
<script setup>
import { ref } from "vue";
import { Field, TextArea } from "@svar-ui/vue-core";

const details = ref("");
</script>

<template>
  <Field label="Details" error>
    <TextArea
      v-model:value="details"
      error
      title="Details are required"
      placeholder="Type here"
    />
  </Field>
</template>
```

## Implementation Notes

- There is no `css` prop; style through a parent/global selector or theme variables.
