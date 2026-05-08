Use when building, configuring, styling, localizing, or modifying SVAR React Tasklist / @svar-ui/react-tasklist components

## Package

```js
import { Tasklist } from "@svar-ui/react-tasklist";
import "@svar-ui/react-tasklist/all.css";
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

- `onChange` receives an `IChange` object for `add`, `update`, and `delete`.
- `Tasklist` adds `originalValue` to the event before calling the user handler.
- Add event shape: `{ action: "add", task, value, originalValue }`.
- Update event shape: `{ action: "update", id, task, value, originalValue }`.
- Delete event shape: `{ action: "delete", id, value, originalValue }`.
- `value` is not two-way bound; use `onChange` to persist `ev.value` in app state or a backend.
- For add only, if `onChange` returns an object or a promise resolving to an object, that object is merged into the newly added task (can't be used to change `id`)

### Other

- `readonly={true}` hides the add, edit, and delete controls and prevents double-click edit.


## Public Types

```ts
import type { ComponentType } from "react";

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

export declare const Tasklist: ComponentType<{
	ondata?: (value: string | number) => Promise<ITask[]> | ITask[];
	onChange?: (ev: IChange) => void;
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

```jsx
import "./TasklistPanel.css";

<div className="tasklist-panel">
	<Tasklist value={tasks} />
</div>

/* TasklistPanel.css
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
*/
```

## Recipes

### Basic Tasklist

```jsx
import "./TasksScope.css";
import { Tasklist } from "@svar-ui/react-tasklist";

function BasicTasklist() {
	const tasks = [
		{ id: 1, content: "Write project notes", status: 0 },
		{ id: 2, content: "Send status update", status: 1 },
	];

	return (
		<div className="tasks">
			<Tasklist value={tasks} />
		</div>
	);
}

/* TasksScope.css
.tasks {
	height: 360px;
	max-width: 768px;
}
*/
```

### Persist Changes

```jsx
import { useState } from "react";
import { Tasklist } from "@svar-ui/react-tasklist";

function PersistedTasklist() {
	const [tasks, setTasks] = useState([]);

	async function onChange(ev) {
		setTasks(ev.value);

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

	return <Tasklist value={tasks} onChange={onChange} />;
}
```

### Resolve Data From A Key

```jsx
import { useState } from "react";
import { Tasklist } from "@svar-ui/react-tasklist";

function KeyedTasklist() {
	const [listId, setListId] = useState(1);

	return (
		<Tasklist
			value={listId}
			ondata={id => api.getTasks(id)}
			onChange={({ action, task, id: taskId, originalValue }) =>
				api.saveTaskChange(originalValue, action, task, taskId)}
		/>
	);
}
```

### Readonly List

```jsx
import { Tasklist } from "@svar-ui/react-tasklist";

function ReadonlyTasklist() {
	const tasks = [{ id: 1, content: "Review release notes", status: 0 }];

	return <Tasklist value={tasks} readonly={true} />;
}
```
