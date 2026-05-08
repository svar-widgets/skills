# SVAR Vue Core Button

Package: `@svar-ui/vue-core`

## Package

```js
import { Button } from "@svar-ui/vue-core";
```

## Supported Functionality

- Renders a native `<button class="wx-button">`.
- `type` is split on spaces and each part becomes a `wx-*` class.
- Typed values are `primary`, `secondary`, `danger`, `link`, and each with `block`.
- `css` is appended to the button class list.
- `icon` renders an `<i class={icon}>` before content.
- When `icon` is set and no `children` are supplied, the button also gets `.wx-icon` icon-only styling.
- Renders `children` slot when provided; otherwise renders `text`.
- `onclick` receives the native `MouseEvent`.

## Public Types

```ts
import type { Component } from "vue";

export declare const Button: Component<{
	type?:
		| "primary"
		| "secondary"
		| "danger"
		| "link"
		| "primary block"
		| "secondary block"
		| "danger block"
		| "link block";
	css?: string;
	icon?: string;
	disabled?: boolean;
	title?: string;
	text?: string;
	children?: () => any;
	onclick?: (ev: MouseEvent) => void;
}>;
```

## Styling

- Button class: `.wx-button`
- Type/state classes: `.wx-primary`, `.wx-secondary`, `.wx-danger`, `.wx-link`, `.wx-block`, `.wx-pressed`, `.wx-icon`
- Disabled styling uses the native `[disabled]` attribute.
- Icon child selector is `i`.

```vue
<template>
  <Button css="save-button" type="primary" icon="wxi-check">Save</Button>
</template>

<style scoped>
:.wx-button.save-button {
	min-width: 120px;
}
</style>
```

## Recipes

### Variants And Click Handler

```vue
<script setup>
import { Button } from "@svar-ui/vue-core";

function save(ev) {
	console.log(ev.currentTarget);
}
</script>

<template>
  <Button type="primary" icon="wxi-check" :onclick="save">Save</Button>
  <Button type="secondary block">Full Width</Button>
  <Button type="danger" disabled>Delete</Button>
  <Button type="link">Details</Button>
</template>
```

### Icon-Only Button

```vue
<script setup>
import { Button } from "@svar-ui/vue-core";
</script>

<template>
  <Button
    icon="wxi-search"
    title="Search"
    :onclick="() => console.log('search')"
  />
</template>
```

## Implementation Notes

- Source has `.wx-square` styles, but `square` is not in the public `type` union.
- `Button` does not call `preventDefault` or stop propagation; handler receives the raw event.
