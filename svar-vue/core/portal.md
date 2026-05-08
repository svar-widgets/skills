# SVAR Vue Core Portal

Package: `@svar-ui/vue-core`

## Package

```js
import { Portal, popupContainer } from "@svar-ui/vue-core";
```

## Supported Functionality

- `Portal` moves its themed child node to `target` or the nearest `data-wx-portal-root` ancestor.
- If no local portal root exists, source appends to the top node from `@svar-ui/lib-dom` environment.
- `theme` defaults from `wx-theme` context when not supplied.
- Children receive an internal `{ mount }` callback argument in source.
- `popupContainer(node)` marks a local portal root with a generated `data-wx-portal-root` attribute.

## Public Types

```ts
import type { Component } from "vue";

export declare const Portal: Component<{
	theme?: "willow" | "willow-dark";
	target?: HTMLElement;
	children?: () => any;
}>;

export declare function popupContainer(node: HTMLElement): void;
```

## Styling

- Source wrapper `.wx-portal` is `display: none`.
- Moved node receives `.wx-{theme}-theme`, such as `.wx-willow-theme`.
- `popupContainer` has no class; it sets a data attribute.

```vue
<script setup>
import { asDirective } from "@svar-ui/lib-vue";
import { popupContainer } from "@svar-ui/vue-core";
const vPopupContainer = asDirective(popupContainer);
</script>

<template>
  <div v-popup-container class="local-root">
    <slot />
  </div>
</template>
```

## Recipes

### Render A Modal Through Portal

```vue
<script setup>
import { ref } from "vue";
import { Button, Modal, Portal } from "@svar-ui/vue-core";

const open = ref(false);
</script>

<template>
  <Button :onclick="() => (open = true)">Open</Button>

  <Portal v-if="open">
    <Modal title="Portal Modal" :oncancel="() => (open = false)">
      Content
    </Modal>
  </Portal>
</template>
```

### Local Portal Root

```vue
<script setup>
import { asDirective } from "@svar-ui/lib-vue";
import { DatePicker, popupContainer } from "@svar-ui/vue-core";
const vPopupContainer = asDirective(popupContainer);
</script>

<template>
  <div v-popup-container class="local-root">
    <DatePicker />
  </div>
</template>
```
