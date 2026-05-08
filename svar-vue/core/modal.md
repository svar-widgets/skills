# SVAR Vue Core Modal

Package: `@svar-ui/vue-core`

## Package

```js
import { Modal } from "@svar-ui/vue-core";
```

## Supported Functionality

- Fixed-position backdrop and centered window.
- `title` renders the default header unless a `header` slot is supplied.
- `children` renders the modal body.
- `footer` slot replaces the default button row.
- `buttons` defaults to `["cancel", "ok"]`; pass `false` to hide default buttons.
- Button id `"cancel"` calls `oncancel`; every other button id calls `onconfirm`.
- Button labels are localized through locale group `core`.
- Modal focuses itself on mount.
- Enter calls `onconfirm` unless focus is inside a `TEXTAREA` or `BUTTON`; Escape calls `oncancel`.

## Public Types

```ts
import type { Component, Slot } from "vue";

export declare const Modal: Component<{
	title?: string;
	buttons?: boolean | string[];
	header?: Slot<[]>;
	footer?: Slot<[]>;
	children?: () => any;
	onconfirm?: (ev: { button?: string; event: MouseEvent }) => void;
	oncancel?: (ev: { button?: string; event: MouseEvent }) => void;
}>;
```

## Styling

- Backdrop: `.wx-modal`
- Window: `.wx-window`
- Header: `.wx-header`
- Button row: `.wx-buttons`
- Button cell: `.wx-button`

```vue
<template>
  <Modal title="Confirm">
    <div>Continue?</div>
  </Modal>
</template>

<style scoped>
.wx-modal .wx-window {
	--wx-modal-width: 360px;
}
</style>
```

## Recipes

### Portal Modal With Default Buttons

```vue
<script setup>
import { ref } from "vue";
import { Button, Modal, Portal } from "@svar-ui/vue-core";

const open = ref(false);
</script>

<template>
  <Button type="primary" :onclick="() => (open = true)">Show</Button>

  <Portal v-if="open">
    <Modal
      title="Confirm"
      :onconfirm="() => (open = false)"
      :oncancel="() => (open = false)"
    >
      Continue?
    </Modal>
  </Portal>
</template>
```

### Custom Header And Footer

```vue
<script setup>
import { Button, Modal } from "@svar-ui/vue-core";
</script>

<template>
  <Modal :buttons="false">
    <template #header>
      <h2>Custom Title</h2>
    </template>

    <div>Body</div>

    <template #footer>
      <Button type="primary">Apply</Button>
    </template>
  </Modal>
</template>
```

## Implementation Notes

- Keyboard Enter/Escape handlers pass a keyboard event, while public types declare `MouseEvent`.
- Button click handlers pass `{ button, event }`.
- Default `"ok"` button is rendered as `type="block primary"`; other default buttons use `type="block secondary"`.
