# SVAR Vue Core Fullscreen

Package: `@svar-ui/vue-core`

## Package

```js
import { Fullscreen } from "@svar-ui/vue-core";
```

## Supported Functionality

- Wraps content in a fullscreen-capable container.
- Default toggle button uses `Button` with `css="wx-fullscreen-button"`.
- Default icon switches between `wxi-expand` and `wxi-collapse`.
- Custom `toggleButton` slot receives `(toggleFullscreen, inFullscreen)`.
- `hotkey` configures a scoped hotkey on the fullscreen wrapper through `@svar-ui/lib-dom` hotkeys.
- Tracks native `fullscreenchange` to keep `inFullscreen` in sync.

## Public Types

```ts
import type { Component, Slot } from "vue";

export declare const Fullscreen: Component<{
	toggleButton?: Slot<[(ev: MouseEvent) => void, boolean]>;
	children?: () => any;
	hotkey?: string;
}>;
```

## Styling

- Wrapper: `.wx-fullscreen`
- Default button: `.wx-fullscreen-button`
- Default icon: `.wx-fullscreen-icon`
- Fullscreen backdrop selector: `.wx-fullscreen::backdrop`
- Wrapper is `position: relative`, `height: 100%`, `width: 100%`, `tabindex="-1"`.
- Default button is absolutely positioned at bottom right.

```vue
<template>
  <Fullscreen>
    <div class="report">Report content</div>
  </Fullscreen>
</template>

<style scoped>
.wx-fullscreen .wx-fullscreen-button {
	right: 12px;
	bottom: 12px;
}
</style>
```

## Recipes

### Custom Toggle Button

```vue
<script setup>
import { Button, Fullscreen } from "@svar-ui/vue-core";
</script>

<template>
  <Fullscreen hotkey="ctrl+shift+f">
    <div class="panel">Report content</div>

    <template #toggleButton="{ toggle, inFullscreen }">
      <Button :onclick="toggle">
        {{ inFullscreen ? "Exit fullscreen" : "Enter fullscreen" }}
      </Button>
    </template>
  </Fullscreen>
</template>
```

## Implementation Notes

- `toggleFullscreen` calls `node.requestFullscreen()` and `document.exitFullscreen()`.
