# SVAR Vue Core SideArea

Package: `@svar-ui/vue-core`

## Package

```js
import { SideArea } from "@svar-ui/vue-core";
```

## Supported Functionality

- Absolute-position side panel for local layouts.
- `position` public type supports only `"right"`; source defaults to `"right"`.
- Clicking outside the panel calls `oncancel`.
- Uses a fly transition from the right.
- Renders arbitrary `children`.

## Public Types

```ts
import type { Component } from "vue";

export declare const SideArea: Component<{
	position?: "right";
	children?: () => any;
	oncancel?: () => void;
}>;
```

## Styling

- Panel: `.wx-sidearea`
- Right position: `.wx-pos-right`

```vue
<template>
  <div class="side-host">
    <SideArea>
      <div class="side-content">Panel</div>
    </SideArea>
  </div>
</template>

<style scoped>
.side-host {
	position: relative;
	min-height: 300px;
}

.side-content {
	width: 400px;
	padding: 20px;
}
</style>
```

## Recipes

### Right-Side Local Panel

```vue
<script setup>
import { ref } from "vue";
import { Button, SideArea } from "@svar-ui/vue-core";

const open = ref(false);
</script>

<template>
  <div style="position: relative; min-height: 300px">
    <Button :onclick="() => (open = true)">Open side panel</Button>

    <SideArea v-if="open" :oncancel="() => (open = false)">
      <div style="width: 400px; padding: 20px">Panel content</div>
    </SideArea>
  </div>
</template>
```
