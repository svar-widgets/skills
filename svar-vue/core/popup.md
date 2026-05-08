# SVAR Vue Core Popup

Package: `@svar-ui/vue-core`

## Package

```js
import { Popup } from "@svar-ui/vue-core";
```

## Supported Functionality

- Low-level absolutely positioned popup surface.
- Position is calculated with `calculatePosition` from `@svar-ui/lib-dom`.
- Use `parent` to anchor to an element, or use `left`/`top` with an `at` position.
- `at` defaults to `"bottom"` in source.
- `oncancel` is called by click-outside behavior.
- `width` can be number, "auto" or percentage like `100%` - calculated from `parent.offsetWidth`.
- `trackScroll`; when enabled hides on scroll outside of popup.

## Public Types

```ts
import { TPosition } from "@svar-ui/lib-dom";
import type { Component } from "vue";

export declare const Popup: Component<{
	left?: number;
	top?: number;
	at?: TPosition;
	css: string;
	width: number | string;
	trackScroll: boolean;
	parent?: HTMLElement;
	children?: () => any;
	oncancel?: (ev: MouseEvent) => void;
}>;
```

## Styling

- Container: `.wx-popup`
- Source appends `css` to `.wx-popup`.
- Inline style sets `position:absolute`, calculated `top`, `left`, and `width`.

```vue
<template>
  <Popup :parent="buttonNode" css="help-popup">
    <div class="body">Help</div>
  </Popup>
</template>

<style scoped>
.wx-popup.help-popup {
	padding: 12px;
}
</style>
```

## Recipes

### Popup Anchored To A Button

```vue
<script setup>
import { ref } from "vue";
import { Button, Popup } from "@svar-ui/vue-core";

const parent = ref(null);
</script>

<template>
  <div ref="parent">
    <Button>Anchor</Button>
  </div>

  <Popup v-if="parent" :parent="parent" at="bottom" :oncancel="() => (parent = null)">
    <div style="padding: 12px">Popup content</div>
  </Popup>
</template>
```

## Implementation Notes

- Use `Dropdown` for the common anchored dropdown case; it handles `Portal` and parent discovery.
