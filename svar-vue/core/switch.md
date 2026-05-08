# SVAR Vue Core Switch

Package: `@svar-ui/vue-core`

## Package

```js
import { Switch } from "@svar-ui/vue-core";
```

## Supported Functionality

- Renders a labeled checkbox styled as a switch.
- `value` is a bindable boolean.
- `disabled` is forwarded to the hidden checkbox input.
- `onchange` emits `{ value }` after the checked state changes.
- `id` is used through the shared input id helper, so it can connect with a surrounding `Field`.

## Public Types

```ts
import type { Component } from "vue";

export declare const Switch: Component<{
	id?: string | number;
	value?: boolean;
	disabled?: boolean;
	onchange?: (ev: { value: boolean }) => void;
}>;
```

## Styling

- Wrapper: `.wx-switch`
- Internal elements are an invisible checkbox input and a visual `span`.

```vue
<template>
  <Switch v-model:value="value" />
</template>

<style scoped>
.wx-switch {
	--wx-switch-width: 56px;
}
</style>
```

## Recipes

### Bound Switch In A Field

```vue
<script setup>
import { ref } from "vue";
import { Field, Switch } from "@svar-ui/vue-core";

const enabled = ref(true);
</script>

<template>
  <Field :label="`Enabled: ${enabled}`" position="left" type="switch">
    <Switch v-model:value="enabled" :onchange="ev => console.log(ev.value)" />
  </Field>
</template>
```

## Implementation Notes

- The component does not expose `css`; style through parent/global selectors or theme variables.
