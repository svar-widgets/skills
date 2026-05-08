# SVAR Vue Core Avatar

Package: `@svar-ui/vue-core`

## Package

```js
import { Avatar } from "@svar-ui/vue-core";
```

## Supported Functionality

- Displays one user or a stack of users.
- User object fields are `id`, `name`, `avatar`, and `color`.
- `size` controls circle size and computed font size; default is `32`.
- `limit` caps visible users before responsive fitting is applied.
- When users are hidden, the last visible avatar shows a `+N` overlay.
- If `avatar` is present, it renders an image; otherwise initials are derived from `name`.

## Public Types

```ts
import type { Component } from "vue";

export interface IUser {
	id: string | number;
	name?: string;
	avatar?: string;
	color?: string;
}

export declare const Avatar: Component<{
	value: IUser | IUser[];
	size?: number;
	limit?: number;
}>;
```

## Styling

- Root: `.wx-avatar-root`
- Stack: `.wx-avatar-stack`
- Avatar item: `.wx-avatar`, `.wx-avatar-item`
- Overflow state and badge: `.wx-avatar-overflow`, `.wx-avatar-overflow-badge`
- Image selector: `.wx-avatar img`
- Initial text selector: `.wx-avatar span`

```vue
<template>
  <div class="people">
    <Avatar :value="users" :size="36" :limit="5" />
  </div>
</template>

<style scoped>
.people {
	width: 180px;
}

.people .wx-avatar {
	border: 2px solid var(--wx-background);
}
</style>
```

## Recipes

### User Stack With Responsive Overflow

```vue
<script setup>
import { Avatar } from "@svar-ui/vue-core";

const users = [
	{ id: 1, name: "Jane Smith", avatar: "/avatars/jane.png" },
	{ id: 2, name: "Lee Park", color: "#2ecc71" },
	{ id: 3, name: "Ana Stone", color: "#e74c3c" },
	{ id: 4, name: "Kai Wong", color: "#37a9ef" },
];
</script>

<template>
  <div style="width: 160px">
    <Avatar :value="users" :size="32" :limit="4" />
  </div>
</template>
```

### Single Initial Avatar

```vue
<script setup>
import { Avatar } from "@svar-ui/vue-core";
</script>

<template>
  <Avatar :value="{ id: 1, name: 'Jane Smith', color: '#2f77e3' }" :size="40" />
</template>
```
