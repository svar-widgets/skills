# SVAR Vue Core ModalArea

Package: `@svar-ui/vue-core`

## Package

```js
import { ModalArea } from "@svar-ui/vue-core";
```

## Supported Functionality

- Local absolute-position modal backdrop and centered window.
- Intended for modal content inside the current layout rather than a viewport-level fixed modal.
- Renders only `children`; it has no built-in header, footer, buttons, or cancel handler.
- Uses a short fade transition.
- Parent layout should provide a positioned containing block when local placement matters.

## Public Types

```ts
import type { Component } from "vue";

export declare const ModalArea: Component<{
	children?: () => any;
}>;
```

## Styling

- Backdrop: `.wx-modal`
- Window: `.wx-window`
- Backdrop is `position: absolute`, fills the containing block, and uses `--wx-modal-backdrop`.
- Window uses modal background, shadow, border, radius, and min width variables.

```vue
<template>
  <div class="local-area">
    <ModalArea>
      <div class="inner">Local modal content</div>
    </ModalArea>
  </div>
</template>

<style scoped>
.local-area {
	position: relative;
	min-height: 300px;
}
</style>
```

## Recipes

### Local Modal Overlay

```vue
<script setup>
import { ref } from "vue";
import { Button, ModalArea } from "@svar-ui/vue-core";

const open = ref(false);
</script>

<template>
  <div style="position: relative; min-height: 300px">
    <Button :onclick="() => (open = true)">Open local modal</Button>

    <ModalArea v-if="open">
      <Button :onclick="() => (open = false)">Close</Button>
    </ModalArea>
  </div>
</template>
```

## Implementation Notes

- `ModalArea` does not trap focus or handle Escape.
- Use `Modal` when you need built-in title, buttons, confirmation, or cancellation behavior.
