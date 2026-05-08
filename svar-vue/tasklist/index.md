Use when building, configuring, styling, localizing, or modifying SVAR Vue Tasklist / @svar-ui/vue-tasklist components

## Package

```js
import { Tasklist } from "@svar-ui/vue-tasklist";

import "@svar-ui/vue-tasklist/all.css";
```

## Supported functionality

`Tasklist` renders a vertical task list with built-in add, edit, delete, and status controls.

### Data

- `value` accepts either an `ITask[]` array or a `string | number` key used with `ondata`.
- Without `ondata`, `value` is used as the task array.
- With `ondata`, `ondata(value)` is called only when `value` is truthy; it may return `ITask[]` or a promise.
- While async data is pending, the component renders an empty list in readonly mode.
- `ITask.content` is required; `status` is numeric and `1` marks a completed task in the UI.
- Existing tasks should have stable unique `id` values because rows are keyed by `task.id`.

### Events and persistence

- `onchange` receives an `IChange` object for `add`, `update`, and `delete`.
- `Tasklist` adds `originalValue` to the event before calling the user handler.
- Add event shape: `{ action: "add", task, value, originalValue }`.
- Update event shape: `{ action: "update", id, task, value, originalValue }`.
- Delete event shape: `{ action: "delete", id, value, originalValue }`.
- `value` is not bindable; use `onchange` to persist `ev.value` in app state or a backend.
- For add only, if `onchange` returns an object or a promise resolving to an object, that object is merged into the newly added task (can't be used to change `id`)

### Other

- `readonly={true}` hides the add, edit, and delete controls and prevents double-click edit.


## Public Types

```ts
import type { Component } from "vue";

export interface IChange {
	action: "add" | "update" | "delete";
	id?: string | number;
	task?: ITask;
	value: ITask[];
	originalValue: string | number | ITask[];
}

export interface ITask {
	id?: string | number;
	content: string;
	status?: number;
}

export declare const Tasklist: Component<{
	ondata?: (value: string | number) => Promise<ITask[]> | ITask[];
	onchange?: (ev: IChange) => void;
	value?: string | number | ITask[];
	readonly?: boolean;
}>;
```

## Styling

Import the package CSS before using the component (`all.css` includes dependency styles, `style.css` is this component only)

- Parent layout matters: `.wx-tasks-list` is `height: 100%`, so give the containing element an explicit height when scroll behavior matters.
- List container: `.wx-list`
- Task row: `.wx-task`
- Editor textarea class is `.wx-texarea`

```vue
<template>
  <div class="tasklist-panel">
    <Tasklist :value="tasks" />
  </div>
</template>

<style scoped>
.tasklist-panel {
	height: 420px;
	max-width: 768px;
	margin: 20px;
}

.tasklist-panel .wx-task {
	padding: 10px 0 6px;
}

.tasklist-panel .wx-list {
	gap: 2px;
}
</style>
```

## Recipes

### Basic Tasklist

```vue
<script setup>
import { Tasklist } from "@svar-ui/vue-tasklist";

const tasks = [
	{ id: 1, content: "Write project notes", status: 0 },
	{ id: 2, content: "Send status update", status: 1 },
];
</script>

<template>
  <div class="tasks">
    <Tasklist :value="tasks" />
  </div>
</template>

<style scoped>
.tasks {
	height: 360px;
	max-width: 768px;
}
</style>
```

### Persist Changes

```vue
<script setup>
import { ref } from "vue";
import { Tasklist } from "@svar-ui/vue-tasklist";

const tasks = ref([]);

async function onchange(ev) {
	tasks.value = ev.value;

	if (ev.action === "add") {
		return api.createTask(ev.task);
	}

	if (ev.action === "update") {
		await api.updateTask(ev.id, ev.task);
	}

	if (ev.action === "delete") {
		await api.deleteTask(ev.id);
	}
}
</script>

<template>
  <Tasklist :value="tasks" :onchange="onchange" />
</template>
```

### Resolve Data From A Key

```vue
<script setup>
import { ref } from "vue";
import { Tasklist } from "@svar-ui/vue-tasklist";

const listId = ref(1);
</script>

<template>
  <Tasklist
    :value="listId"
    :ondata="id => api.getTasks(id)"
    :onchange="({ action, task, id: taskId, originalValue }) =>
      api.saveTaskChange(originalValue, action, task, taskId)"
  />
</template>
```

### Readonly List

```vue
<script setup>
import { Tasklist } from "@svar-ui/vue-tasklist";

const tasks = [{ id: 1, content: "Review release notes", status: 0 }];
</script>

<template>
  <Tasklist :value="tasks" :readonly="true" />
</template>
```
