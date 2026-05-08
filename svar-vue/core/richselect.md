# SVAR Vue Core RichSelect

Package: `@svar-ui/vue-core`

## Package

```js
import { RichSelect } from "@svar-ui/vue-core";
```

## Supported Functionality

- Non-input single-select control backed by `SuggestDropdown`.
- `value` is the selected id and is bindable.
- `options` are `{ id, label }` by default.
- `textField` controls display field; default is `"label"`.
- `textOptions` can provide selected display objects when visible `options` are partial.
- `clear` shows a close icon when value is set and not disabled.
- `children` slot receives the option object directly for both selected content and list rows.
- `onchange` emits `{ value }`.

## Public Types

```ts
import type { Component } from "vue";

export interface DropdownOptions {
	inline?: boolean;
	position?: "top" | "right" | "bottom" | "left";
	align?: "start" | "center" | "end";
	css?: string;
	width?: string | "unset" | "auto";
	trackScroll?: boolean;
	virtualized?: boolean;
}

export declare const RichSelect: Component<{
	value?: string | number;
	options?: { id: string | number; label: string }[];
	textOptions?: { id: string | number; label: string }[];
	placeholder?: string;
	disabled?: boolean;
	error?: boolean;
	title?: string;
	textField?: string;
	clear?: boolean;
	dropdown?: DropdownOptions & {
		virtualized?: boolean;
	};
	children?: () => any;
	onchange?: (ev: { value: string | number }) => void;
}>;
```

## Styling

- Wrapper: `.wx-richselect`
- State classes: `.wx-disabled`, `.wx-error`, `.wx-nowrap`
- Content label: `.wx-label`
- Placeholder: `.wx-placeholder`
- Icon: `.wx-icon`, close icon `.wxi-close`
- Dropdown list hooks: `.wx-list`, `.wx-item`, `.wx-focus`

```vue
<template>
  <RichSelect
    :options="users"
    :value="104"
    :dropdown="{ css: 'user-select-menu' }"
  />
</template>

<style scoped>
.wx-popup.user-select-menu .wx-item {
	min-height: 40px;
}
</style>
```

## Recipes

### Rich Select With Custom Template

```vue
<script setup>
import { RichSelect } from "@svar-ui/vue-core";

const users = [
	{ id: 104, label: "Lord Varys", email: "little.birds@mail" },
	{ id: 103, label: "Ned Stark", email: "winterhell@mail" },
];
</script>

<template>
  <RichSelect :options="users" :value="104">
    <template #children="option">
      <div>
        <strong>{{ option.label }}</strong>
        <span>{{ option.email }}</span>
      </div>
    </template>
  </RichSelect>
</template>
```

### Hidden Selected Option

```vue
<script setup>
import { RichSelect } from "@svar-ui/vue-core";

const allUsers = [
	{ id: 87, label: "Berni Mayou" },
	{ id: 103, label: "Ned Stark" },
];

const visibleUsers = [{ id: 103, label: "Ned Stark" }];
</script>

<template>
  <RichSelect :textOptions="allUsers" :options="visibleUsers" :value="87" clear />
</template>
```

## Implementation Notes

- Without a custom slot, `.wx-nowrap` is added to ellipsize the selected label.
