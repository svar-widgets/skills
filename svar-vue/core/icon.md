# SVAR Vue Core Icon

Package: `@svar-ui/vue-core`

## Package

```js
import { Icon } from "@svar-ui/vue-core";
```

## Supported Functionality

- Renders `<i class="wx-icon {css}">`.
- Use `css` for icon font classes such as `wxi-search`.
- `title` is forwarded to the `<i>`.
- `onclick` is forwarded to the `<i>`.
- If `children` slot is provided, it is rendered inside the `<i>` and `role="img"` is added.

## Public Types

```ts
import type { Component } from "vue";

export declare const Icon: Component<{
	css?: string;
	title?: string;
	children?: () => any;
	onclick?: (ev: MouseEvent) => void;
}>;
```

## Styling

- Icon class: `.wx-icon`
- `css` is appended to `.wx-icon`.

```vue
<template>
  <Icon css="wxi-search app-icon" title="Search" />
</template>

<style scoped>
.wx-icon.app-icon {
	color: var(--wx-color-primary);
}
</style>
```

## Recipes

### Clickable Icon

```vue
<script setup>
import { Icon } from "@svar-ui/vue-core";
</script>

<template>
  <Icon
    css="wxi-information-outline"
    title="Info"
    :onclick="() => console.log('info')"
  />
</template>
```

## Implementation Notes

- The component intentionally uses an `<i>` rather than a button
