# SVAR Vue Core Segmented

Package: `@svar-ui/vue-core`

## Package

```js
import { Segmented } from "@svar-ui/vue-core";
```

## Supported Functionality

- Renders an inline segmented button group.
- `options` are `{ id, label, icon?, title? }`.
- `value` is the selected id and is bindable.
- Clicking an option sets `value = option.id` and emits `onchange({ value })`.
- `css` is appended to `.wx-segmented`.
- Default content renders `option.icon` and `option.label`.
- `children` slot receives `{ option }` for custom option content.

## Public Types

```ts
import type { Component } from "vue";

export declare const Segmented: Component<{
	options?: {
		id: string | number;
		label: string;
		icon?: string;
		title?: string;
	}[];
	value?: string | number;
	css?: string;
	children?: () => any;
	onchange?: (ev: { value: string | number }) => void;
}>;
```

## Styling

- Wrapper: `.wx-segmented`
- Selected button: `.wx-selected`
- Default icon: `.wx-icon`, icon-only modifier `.wx-only`
- Default label: `.wx-label`

```vue
<template>
  <Segmented css="view-mode" :options="options" v-model:value="value" />
</template>

<style scoped>
.wx-segmented.view-mode {
	--wx-segmented-padding: 3px;
}
</style>
```

## Recipes

### Basic Segmented Control

```vue
<script setup>
import { ref } from "vue";
import { Segmented } from "@svar-ui/vue-core";

const options = [
	{ id: "list", label: "List", icon: "wxi-view-sequential" },
	{ id: "grid", label: "Grid", icon: "wxi-view-grid" },
];

const value = ref("list");
</script>

<template>
  <Segmented :options="options" v-model:value="value" :onchange="ev => console.log(ev.value)" />
</template>
```

### Custom Option Content

```vue
<script setup>
import { Segmented } from "@svar-ui/vue-core";

const options = [
	{ id: "left", label: "Left", icon: "wxi-align-left" },
	{ id: "right", label: "Right", icon: "wxi-align-right" },
];
</script>

<template>
  <Segmented :options="options" value="left">
    <template #children="{ option }">
      <i :class="option.icon"></i>
      <span>{{ option.label }}</span>
    </template>
  </Segmented>
</template>
```
