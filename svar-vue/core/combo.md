# SVAR Vue Core Combo

Package: `@svar-ui/vue-core`

## Package

```js
import { Combo } from "@svar-ui/vue-core";
```

## Supported Functionality

- Searchable single-select input backed by `SuggestDropdown`.
- `options` are `{ id, label }` by default.
- `textField` controls display/filter field; default is `"label"`.
- `textOptions` can provide selected display objects when visible `options` are filtered or partial.
- Typing filters `options` case-insensitively by `textField`.
- Blur selects exact text match first, then first containing match, then previous value or first option.
- Dropdown selection updates bindable `value` and emits `{ value }`.
- `children` slot receives `{ option }` for custom list row content.
- `dropdown` is forwarded to `SuggestDropdown`/`Dropdown`.

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

export declare const Combo: Component<{
	value?: string | number;
	id?: string | number;
	options?: { id: string | number; label: string }[];
	textOptions?: { id: string | number; label: string }[];
	textField?: string;
	placeholder?: string;
	title?: string;
	disabled?: boolean;
	error?: boolean;
	clear?: boolean;
	dropdown?: DropdownOptions & {
		virtualized?: boolean;
	};
	children?: () => any;
	onchange?: (ev: { value: string | number }) => void;
}>;
```

## Styling

- Wrapper: `.wx-combo`
- Icon: `.wx-icon`, close icon `.wxi-close`
- Error class is applied to the input as `.wx-error`.
- Dropdown list hooks from `SuggestDropdown`: `.wx-list`, `.wx-item`, `.wx-focus`, `.wx-no-data`.
- Non-inline dropdown `css` is appended to `.wx-popup`.


```vue
<template>
  <Combo :options="users" :dropdown="{ css: 'users-popup', width: '320px' }" />
</template>

<style scoped>
.wx-popup.users-popup .wx-list {
	max-height: 360px;
}
</style>
```

## Recipes

### Custom Option Template And Virtualized List

```vue
<script setup>
import { ref } from "vue";
import { Combo } from "@svar-ui/vue-core";

const users = Array.from({ length: 10000 }, (_, id) => ({
	id,
	label: `User ${id}`,
	email: `user${id}@example.com`,
}));

const value = ref(9000);
</script>

<template>
  <Combo
    :options="users"
    v-model:value="value"
    :dropdown="{ virtualized: true, width: '320px' }"
  >
    <template #children="{ option }">
      <div class="user-option">
        <strong>{{ option.label }}</strong>
        <span>{{ option.email }}</span>
      </div>
    </template>
  </Combo>
</template>
```

### Hidden Selected Option

```vue
<script setup>
import { Combo } from "@svar-ui/vue-core";

const allUsers = [
	{ id: 87, label: "Berni Mayou" },
	{ id: 103, label: "Ned Stark" },
];

const visibleUsers = [{ id: 103, label: "Ned Stark" }];
</script>

<template>
  <Combo :textOptions="allUsers" :options="visibleUsers" :value="87" clear />
</template>
```

## Implementation Notes

- Filtering assumes `option[textField]` is a string
