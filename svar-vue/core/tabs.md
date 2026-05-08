# SVAR Vue Core Tabs

Package: `@svar-ui/vue-core`

## Package

```js
import { Tabs } from "@svar-ui/vue-core";
```

## Supported Functionality

- Renders a tab strip only; render the tab panel yourself based on `value`.
- `options` are `{ id, label?, title?, icon? }`.
- `value` is the active tab id and is bindable.
- Clicking a tab sets `value = option.id` and emits `onchange({ value })`.
- `type` is `top` or `bottom`; default is `top`.
- Icons use the same icon class pattern as other core controls.

## Public Types

```ts
import type { Component } from "vue";

export declare const Tabs: Component<{
	options?: {
		id: string | number;
		label?: string;
		title?: string;
		icon?: string;
	}[];
	value?: string | number;
	type?: "top" | "bottom";
	onchange?: (ev: { value: string | number }) => void;
}>;
```

## Styling

- Wrapper: `.wx-tabs`, plus `.wx-top` or `.wx-bottom`
- Active button: `.wx-active`
- Default icon: `.wx-icon`, icon-only modifier `.wx-only`
- Default label: `.wx-label`

```vue
<template>
  <Tabs :options="tabs" v-model:value="active" />
</template>

<style scoped>
.wx-tabs {
	--wx-tabs-cell-min-width: 80px;
}
</style>
```

## Recipes

### Tabs With Panels

```vue
<script setup>
import { ref } from "vue";
import { Tabs } from "@svar-ui/vue-core";

const tabs = [
	{ id: "info", label: "Info", icon: "wxi-alert" },
	{ id: "audit", label: "Audit" },
	{ id: "done", icon: "wxi-check", title: "Done" },
];

const active = ref("info");
</script>

<template>
  <Tabs :options="tabs" v-model:value="active" />

  <div v-if="active === 'info'">Info panel</div>
  <div v-else-if="active === 'audit'">Audit panel</div>
  <div v-else>Done panel</div>

  <Tabs :options="tabs" v-model:value="active" type="bottom" />
</template>
```

## Implementation Notes

- `Tabs` has no `css` prop; style with an enclosing parent/global selector or theme variables.
