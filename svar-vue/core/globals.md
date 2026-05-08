# SVAR Vue Core Globals

Package: `@svar-ui/vue-core`

## Package

```js
import { Globals } from "@svar-ui/vue-core";
```

## Supported Functionality

- Renders children and installs Vue inject key `wx-helpers`.
- `wx-helpers.showNotice(msg)` appends a notice.
- `wx-helpers.showModal(msg)` renders a `Modal` and returns a Promise.
- `showNotice` payload fields used by source include `text`, `type`, `expire`, and optional `id`.
- Notice `type` can be empty or classes such as `info`, `warning`, `success`, and `danger`.
- `showNotice` default expiry is `5100ms`; `expire: -1` keeps the notice until the close icon is clicked.
- `showModal` payload fields used by source include `title`, `message`, and `buttons`.
- Confirm resolves the modal Promise; cancel rejects it.
- `Notice` and `Notices` are source components but are not top-level exports.

## Public Types

```ts
import type { Component } from "vue";

export declare const Globals: Component<{
	children?: () => any;
}>;
```

## Source Helper Shapes

These helper payloads are source behavior, not exported public TypeScript declarations.

```ts
type NoticeMessage = {
	id?: string | number;
	text?: string;
	type?: "" | "info" | "warning" | "success" | "danger" | string;
	expire?: number;
};

type ModalMessage = {
	title?: string;
	message?: any;
	buttons?: boolean | string[];
};
```

## Styling

- Notice list: `.wx-notices`
- Notice item: `.wx-notice`
- Notice content: `.wx-text`
- Notice close button: `.wx-button`
- Notice type classes: `.wx-info`, `.wx-warning`, `.wx-success`, `.wx-danger`
- Modals rendered by `showModal` use `Modal` classes: `.wx-modal`, `.wx-window`, `.wx-header`, `.wx-buttons`, `.wx-button`

```vue
<template>
  <Globals>
    <App />
  </Globals>
</template>

<style scoped>
.wx-notices {
	top: 12px;
	right: 12px;
}
</style>
```

## Recipes

### Install Globals At App Root

```vue
<script setup>
import { Globals } from "@svar-ui/vue-core";
import Actions from "./Actions.vue";
</script>

<template>
  <Globals>
    <Actions />
  </Globals>
</template>
```

### Use Notice And Modal Helpers In A Child

```vue
<script setup>
import { Button } from "@svar-ui/vue-core";
import { inject } from "vue";

const { showNotice, showModal } = inject("wx-helpers");

async function confirmDelete() {
	try {
		await showModal({ title: "Confirm", message: "Delete item?" });
		showNotice({ type: "success", text: "Deleted" });
	} catch {
		showNotice({ type: "info", text: "Canceled" });
	}
}
</script>

<template>
  <Button type="danger" :onclick="confirmDelete">Delete</Button>
  <Button :onclick="() => showNotice({ type: 'info', text: 'Saved' })">
    Notice
  </Button>
</template>
```

## Implementation Notes

- `showModal` stores one active modal at a time.
