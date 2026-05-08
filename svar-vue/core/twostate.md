# SVAR Vue Core TwoState

Package: `@svar-ui/vue-core`

## Package

```js
import { TwoState } from "@svar-ui/vue-core";
```

## Supported Functionality

- Wraps `Button` and toggles bindable boolean `value`.
- When active, adds `pressed` to the forwarded `type`.
- `textActive` and `iconActive` replace `text` and `icon` while active.
- `children` renders inactive/default content; `active` slot renders active content when `value` is true.
- Click order: `onclick(ev)` first, then value toggle and `onchange({ value })`.
- Calling `ev.preventDefault()` inside `onclick` prevents the toggle and `onchange`.

## Public Types

```ts
import type { Component, Slot } from "vue";

export declare const TwoState: Component<{
	value?: boolean;
	type?:
		| "primary"
		| "secondary"
		| "danger"
		| "link"
		| "primary block"
		| "secondary block"
		| "danger block"
		| "link block";
	icon?: string;
	disabled?: boolean;
	iconActive?: string;
	title?: string;
	css?: string;
	text?: string;
	textActive?: string;
	active?: Slot<[]>;
	children?: () => any;
	onclick?: (ev: MouseEvent) => void;
	onchange?: (ev: { value: boolean }) => void;
}>;
```

## Styling

- Uses `Button`, so styling hooks are `.wx-button` plus `.wx-pressed` when active.
- `css` is passed to the inner `Button`.
- Button type variables such as `--wx-button-pressed`, `--wx-button-primary-pressed`, and `--wx-button-box-shadow` control active state.

```vue
<template>
  <TwoState css="favorite-button" icon="wxi-star" iconActive="wxi-check" />
</template>

<style scoped>
.wx-button.favorite-button.wx-pressed {
	font-weight: 700;
}
</style>
```

## Recipes

### Toggle With Active Content

```vue
<script setup>
import { ref } from "vue";
import { TwoState } from "@svar-ui/vue-core";

const active = ref(false);
</script>

<template>
  <TwoState
    v-model:value="active"
    type="primary"
    icon="wxi-star"
    iconActive="wxi-check"
    :onchange="ev => console.log(ev.value)"
  >
    Favorite
    <template #active>
      Favorited
    </template>
  </TwoState>
</template>
```

### Prevent Toggle

```vue
<script setup>
import { TwoState } from "@svar-ui/vue-core";

function beforeToggle(ev) {
	if (!confirm("Toggle?")) ev.preventDefault();
}
</script>

<template>
  <TwoState :onclick="beforeToggle">Toggle</TwoState>
</template>
```

## Implementation Notes

- The active slot is rendered only when `value` is true.
- If `active` is not supplied, the component reuses `children` or `text` with active icon/text substitutions.
