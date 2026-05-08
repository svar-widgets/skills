# svar-vue — gantt

_Generated 2026-05-08T13:35:37.091Z_

## Contents

- [`gantt/index.md`](#file-gantt-index-md)
- [`locales.md`](#file-locales-md)
- [`themes.md`](#file-themes-md)


## File: gantt/index.md

> Source: `gantt/index.md`

Use when building, configuring, styling, or modifying SVAR Vue Gantt / @svar-ui/vue-gantt timelines, grids, task editors, toolbars, context menus, tooltips, scales, links, and Gantt data actions.

#### Package

```js
import {
	Gantt,
	ContextMenu,
	HeaderMenu,
	Toolbar,
	Tooltip,
	Editor,
	Willow,
	WillowDark,
	version,
	defaultEditorItems,
	defaultToolbarButtons,
	defaultMenuOptions,
	defaultColumns,
	defaultTaskTypes,
	getEditorItems,
	getToolbarButtons,
	getMenuOptions,
	registerScaleUnit,
	registerEditorItem,
} from "@svar-ui/vue-gantt";

import "@svar-ui/vue-gantt/all.css";
```

#### Components

- `Gantt` - main grid plus timeline chart; `ref="..."` exposes the Gantt API object from source.
- `Toolbar` - Gantt-aware wrapper around `@svar-ui/vue-toolbar`; accepts `api` and optional `items`.
- `ContextMenu` - Gantt-aware wrapper around `@svar-ui/vue-menu` context menu; resolves tasks from Gantt `data-id`.
- `Editor` - Gantt-aware wrapper around `@svar-ui/vue-editor`; opens for `activeTask` / `show-editor`.
- `Tooltip` - wraps a Gantt and displays task text or a custom content component from `data-tooltip-id`.
- `HeaderMenu` - wraps `@svar-ui/vue-grid` header menu and passes `api.getTable()` to it.
- `Willow`, `WillowDark` - theme wrappers; each accepts `fonts?: boolean` and optional children.

#### Supported functionality

##### Gantt Data

- `tasks` is an array of task objects; common fields are `id`, `text`, `start`, `end`, `duration`, `progress`, `parent`, `type`, `open`, `details`, `data`, `unscheduled`, `segments`, `base_start`, `base_end`, `base_duration`, `rollup`.
- `links` is an array of dependency links with `id`, `source`, `target`, `type`, optional `lag`.
- link `type` values are `s2s`, `s2e`, `e2s`, `e2e`.
- task `type` defaults are `task`, `summary`, `milestone`; custom types are supported through `taskTypes`.
- milestone tasks are normalized with `duration = 0` and no `end`.
- summary task dates are calculated from children when `start` / `end` are missing.
- `parseTaskDates(tasks, { durationUnit, splitTasks, calendar })` runs inside `Gantt` and mutates task date fields unless `_export` is set.

Common data objects:

```js
const tasks = [
	{
		id: 1,
		text: "Project",
		type: "summary",
		parent: 0,
		open: true,
	},
	{
		id: 10,
		text: "Task",
		type: "task",
		parent: 1,
		start: new Date(2026, 3, 2),
		duration: 3,
		progress: 40,
	},
	{
		id: 11,
		text: "Milestone",
		type: "milestone",
		parent: 1,
		start: new Date(2026, 3, 8),
	},
];

const links = [{ id: 1, source: 10, target: 11, type: "e2s" }];
```

##### Gantt Config

- default scales: `[{ unit: "month", step: 1, format: "%F %Y" }, { unit: "day", step: 1, format: "%j" }]`.
- `scales` rows accept `unit`, `step`, `format?: string | (date, next) => string`, `css?: (date) => string`.
- `start`, `end`, and `autoScale` control timeline bounds; `autoScale` includes tasks, markers, baselines, `projectStart`, and `projectEnd`.
- `zoom` accepts `true` or `IZoomConfig`; chart zoom is handled by Ctrl/Command + wheel and emits `zoom-scale`.
- `columns` defaults to `defaultColumns`; `columns={false}` hides the grid and resizer.
- the `text` column is rendered with the built-in `TextCell`; `add-task` uses `ActionCell`, is removed in `readonly`, and moves to the first column in compact chart mode.
- `cellWidth`, `cellHeight`, `scaleHeight` control timeline width, row height, and scale row height.
- `lengthUnit` controls chart math; `durationUnit` controls task duration calculation and is `"day"` or `"hour"`.
- `cellBorders` is `"column"` or `"full"`.
- `readonly` disables task drag, progress editing, link editing, grid add column behavior, and editor opening from double click.
- `selected` and `activeTask` are config inputs, not two-way bindable props; read or change live selection through `api.getReactiveState()` and `api.exec("select-task", ...)`.
- `highlightTime(date, unit)` can return a CSS class for timescale cells and chart background cells when min unit is `day` or `hour`.
- compact mode is driven by a `ResizeObserver` on `document.body`; width `<= 650` switches the layout to grid/chart modes.

Common config objects:

```js
const columns = [
	{ id: "text", header: "Task name", flexgrow: 1, editor: "text" },
	{ id: "start", header: "Start date", align: "center", editor: "datepicker" },
	{ id: "duration", header: "Duration", width: 100, align: "center" },
	{ id: "add-task", header: "Add task", width: 50, align: "center" },
];

const scales = [
	{ unit: "month", step: 1, format: "%F %Y" },
	{ unit: "week", step: 1, format: "Week %w" },
	{ unit: "day", step: 1, format: "%j", css: date => date.getDay() === 0 ? "wx-weekend" : "" },
];

const zoom = {
	level: 2,
	minCellWidth: 40,
	maxCellWidth: 180,
};
```

##### Pro And Advanced Config

- `baselines` shows `base_start` / `base_end` / `base_duration`.
- `rollups` accepts `true` or `{ type: "all" | "closest" }`; tasks with `rollup: true` are drawn on summary rows.
- `markers` is an array of `{ start: Date, text?: string, css?: string }`.
- `criticalPath={{ type: "strict" | "flexible" }}` marks critical tasks and links.
- `schedule={{ type?: "forward", auto?: boolean }}` enables scheduling behavior; `projectStart` and `projectEnd` provide bounds.
- `calendar` accepts a `Calendar` from `@svar-ui/gantt-store`; Gantt then creates default weekend highlighting when `calendar` is set.
- `undo` enables history state plus `undo` / `redo` actions and toolbar buttons.
- `splitTasks` enables task `segments` editing, split toolbar/menu actions, and segment-aware editor/context-menu targets.
- `summary={{ autoProgress?: boolean, autoConvert?: boolean }}` controls summary progress and summary type conversion behavior.
- `slack` shows task slack visuals.
- `unscheduledTasks` enables task `unscheduled` support and editor scheduling controls.
- `api.exec("export-data", config)` supports `format: "pdf" | "png" | "xlsx" | "mspx"` through `IExportConfig`.
- `api.exec("import-data", { data, format: "mspx" })` imports MS Project XML.

##### API And Events

`Gantt` exposes this API from source through `ref="..."` or `init(api)`:

- state: `getState()`, `getReactiveState()`, `getStores()`
- events/actions: `exec(action, data)`, `on(action, callback, config?)`, `intercept(action, callback, config?)`, `detach(tag)`, `setNext(eventBusOrProvider)`
- task/table helpers: `getTask(id)`, `getTable(waitRender?)`, `serialize()`, `getHistory()`

Component callback props are generated from action names by removing hyphens and prefixing `on`:

- `add-task` -> `onaddtask`
- `update-task` -> `onupdatetask`
- `select-task` -> `onselecttask`
- custom `taskTemplate` action `"custom-click"` -> `oncustomclick`

Source routes actions through `DataStore` first, then calls the matching component callback prop if present.

Common actions:

```js
api.exec("add-task", {
	task: { text: "New task", type: "task" },
	target: 10,
	mode: "after",
	show: true,
});

api.exec("update-task", {
	id: 10,
	task: { text: "Updated", progress: 75 },
});

api.exec("select-task", {
	id: 10,
	toggle: false,
	range: false,
	show: "xy",
	focus: "grid",
});

api.exec("move-task", { id: 10, target: 1, mode: "child" });
api.exec("filter-tasks", { filter: task => task.text?.includes("API"), open: true });
api.exec("scroll-chart", { date: new Date(2026, 4, 1) });
```

Use `api.intercept(action, cb)` to block or replace built-in behavior; returning `false` blocks the action. Use `api.setNext(provider)` to forward data changes to a provider such as `RestDataProvider`.

##### Saving

- `RestDataProvider` from `@svar-ui/gantt-data-provider` persists data changes to a REST backend.
- Wire it once with `api.setNext(provider)` in `init`; the provider then forwards every data action (`add-task`, `update-task`, `delete-task`, `move-task`, `add-link`, `update-link`, `delete-link`, etc.) emitted on the event bus as the matching REST call. No per-action save handlers needed.
- Initial load uses `provider.getData()`; lazy branches use `provider.getData(id)` inside `request-data` and dispatch back through `provide-data`.
- Optional `{ batchURL }` constructor option batches concurrent writes into a single endpoint.

```js
import { RestDataProvider } from "@svar-ui/gantt-data-provider";

const provider = new RestDataProvider("/api/gantt");

function init(api) {
	api.setNext(provider); // forwards all task/link mutations to REST
}
```

##### Toolbar

- `Toolbar` source props are `api = null` and `items = []`.
- default items come from `getToolbarButtons({ undo: $undo, splitTasks: $splitTasks })`.
- default handled ids are wired through `handleAction(api, item.id, null, _)`.
- custom item `handler` functions are preserved only when the id is not one of the handled default action ids.
- if no task is selected, default toolbar keeps only targetless items such as `add-task` and history controls.
- `undo` adds `undo` and `redo`; `splitTasks` adds `split-task`.

Default toolbar ids:

```js
[
	"add-task",
	"edit-task",
	"delete-task",
	"move-task:up",
	"move-task:down",
	"copy-task",
	"cut-task",
	"paste-task",
	"indent-task:add",
	"indent-task:remove",
];
```

##### Context Menu

- `ContextMenu` source props are `options`, `api`, `resolver`, `filter`, `at = "point"`, `children`, `onclick`, `css`.
- the wrapper passes `dataKey="id"` to `@svar-ui/vue-menu`; Gantt grid rows and bars expose `data-id`.
- built-in menu options are from `getMenuOptions({ splitTasks, taskTypes, summary })`.
- right-clicking a task selects it when it is not already selected.
- `resolver(id, event)` can return `true` to use the default task, return a replacement context object, or return a falsy value to prevent task resolution.
- `filter(option, task)` is applied across selected tasks; built-in `isHidden` and `isDisabled` are also applied.
- wrapper `onclick` receives the menu event used in demos as `{ context, action }`.
- built-in handled `action.id` values are executed through `handleAction(api, action.id, activeId, _)` before user `onclick`.
- with `splitTasks`, segment targets use `{ id, segmentIndex }` internally for edit/delete/split actions.

Default menu ids:

```js
[
	"add-task:child",
	"add-task:before",
	"add-task:after",
	"convert-task:<taskType>",
	"edit-task",
	"cut-task",
	"copy-task",
	"paste-task",
	"move-task:up",
	"move-task:down",
	"indent-task:add",
	"indent-task:remove",
	"delete-task",
];
```

##### Editor

- `Editor` source props are `api`, `items = []`, `css = ""`, `layout = "default"`, `readonly = false`, `placement = "sidebar"`, `bottomBar = true`, `topBar = true`, `autoSave = true`, `focus = false`, `hotkeys = {}`.
- editor renders only when `api.getReactiveState()._activeTask` exists.
- default items come from `getEditorItems({ unscheduledTasks, rollups, summary, taskTypes })`.
- built-in editor comps registered by the wrapper: `select`, `date`, `twostate`, `slider`, `counter`, `links`, `checkbox`.
- `registerEditorItem(name, Component)` registers custom comps for `items`.
- item `key` is the task field; editor values are task objects keyed by those `key` values.
- `autoSave={true}` saves valid changes on field change; `autoSave={false}` stores local values and saves from a `save` top/bottom bar action.
- saved task payload removes `links` and `data`; `duration` may be removed when no duration editor is present.
- `links` editor changes are batched in the wrapper and saved through link actions.
- default `topBar={true}` in editable mode creates close/spacer/delete buttons, plus save when `autoSave={false}`.

Default editor keys:

```js
["text", "details", "type", "start", "end", "duration", "progress", "links"]
```

##### Tooltip

- `Tooltip` source props are `api`, `content`, `children`.
- default tooltip text is the task `text`, or segment `text` when `data-segment` is present.
- custom `content` component receives `{ data }`; source also passes `segmentIndex` for split-task segments.
- direct tooltip override can use a DOM `data-tooltip` attribute; placement hint uses `data-tooltip-at="left"`.
- tooltip lookup is debounced by 300ms.

##### Header Menu

- `HeaderMenu` source props are `api`, `columns`, `children`.
- wrapper calls `api?.getTable()` and passes that table API to `@svar-ui/vue-grid` `HeaderMenu`.
- use it when the grid table API is needed for column visibility/menu behavior.

#### Public Types

```ts
import type { Component, ComponentProps } from "vue";
import { ContextMenu as BaseContextMenu } from "@svar-ui/vue-menu";
import { Toolbar as BaseToolbar } from "@svar-ui/vue-toolbar";
import { Editor as BaseEditor } from "@svar-ui/vue-editor";
import {
	HeaderMenu as BaseHeaderMenu,
	IColumnConfig as ITableColumn,
} from "@svar-ui/vue-grid";

import type {
	TMethodsConfig,
	IApi,
	IConfig,
	ITask,
	IGanttColumn,
} from "@svar-ui/gantt-store";

export * from "@svar-ui/gantt-store";
export { registerEditorItem } from "@svar-ui/vue-editor";

export interface IColumnConfig extends Omit<IGanttColumn, "header"> {
	cell?: ITableColumn["cell"];
	header?: ITableColumn["header"];
	editor?: ITableColumn["editor"];
}

export declare const Gantt: Component<
	{
		columns?: false | IColumnConfig[];
		taskTemplate?: Component<{
			data: ITask;
			api: IApi;
			onaction: (ev: {
				action: string;
				data: { [key: string]: any };
			}) => void;
		}>;
		readonly?: boolean;
		cellBorders?: "column" | "full";
		highlightTime?: (date: Date, unit: "day" | "hour") => string;
		init?: (api: IApi) => void;
	} & IConfig &
		GanttActions<TMethodsConfig>
>;

export declare const HeaderMenu: Component<
	ComponentProps<typeof BaseHeaderMenu> & {
		api?: IApi;
	}
>;

export declare const ContextMenu: Component<
	ComponentProps<typeof BaseContextMenu> & {
		api?: IApi;
	}
>;

export declare const Toolbar: Component<
	ComponentProps<typeof BaseToolbar> & {
		api?: IApi;
	}
>;

export declare const Editor: Component<
	ComponentProps<typeof BaseEditor> & {
		api?: IApi;
	}
>;

export declare const Tooltip: Component<{
	content?: Component<{
		data: ITask;
	}>;
	api?: IApi;
	children?: () => any;
}>;

export declare const Willow: Component<{
	fonts?: boolean;
	children?: () => any;
}>;

export declare const WillowDark: Component<{
	fonts?: boolean;
	children?: () => any;
}>;

/* get component events from store actions*/
type RemoveHyphen<S extends string> = S extends `${infer Head}-${infer Tail}`
	? `${Head}${RemoveHyphen<Tail>}`
	: S;

type EventName<K extends string> = `on${RemoveHyphen<K>}`;

export type GanttActions<TMethodsConfig extends Record<string, any>> = {
	[K in keyof TMethodsConfig as EventName<K & string>]?: (
		ev: TMethodsConfig[K]
	) => void;
} & {
	[key: `on${string}`]: (ev?: any) => void;
};
```

#### Styling

Import the package CSS before using the component (`all.css` includes dependency styles, `style.css` is this component only)

Main hooks:

- root/layout: `.wx-gantt`, `.wx-pseudo-rows`, `.wx-stuck`, `.wx-layout`, `.wx-content`
- grid: `.wx-table-container`, `.wx-table`, `.wx-grid`, `.wx-header`, `.wx-body`, `.wx-row`, `.wx-cell`, `.wx-action`, `.wx-toggle-icon`, `.wx-action-icon`
- chart: `.wx-chart`, `.wx-scale`, `.wx-area`, `.wx-bars`, `.wx-bar`, `.wx-task`, `.wx-summary`, `.wx-milestone`, `.wx-content`, `.wx-text-out`
- custom task types: built-ins render as `.wx-task`, `.wx-summary`, `.wx-milestone`; custom task types render as `.wx-task.<customType>`
- task state: `.wx-selected`, `.wx-critical`, `.wx-reorder-task`, `.wx-split`, `.wx-touch`
- progress/links: `.wx-progress-wrapper`, `.wx-progress-percent`, `.wx-progress-marker`, `.wx-link`, `.wx-line`, `.wx-line-selected`, `.wx-delete-link`
- split/rollup/baseline/slack: `.wx-segments`, `.wx-segment`, `.wx-rollup`, `.wx-task-rollup`, `.wx-summary-rollup`, `.wx-milestone-rollup`, `.wx-baseline`, `.wx-slack`, `.wx-slack-task`
- scales/markers/holidays: `.wx-scale`, `.wx-row`, `.wx-cell`, `.wx-weekend`, `.wx-markers`, `.wx-marker`
- companion components: `.wx-gantt-editor`, `.wx-gantt-tooltip`, `.wx-gantt-tooltip-text`, `.wx-tooltip-area`, `.wx-menu`, `.wx-option`
- resizer/display controls: `.wx-resizer`, `.wx-resizer-display-all`, `.wx-resizer-display-grid`, `.wx-resizer-display-chart`, `.wx-button-expand-left`, `.wx-button-expand-right`

Layout defaults:

- the host container must provide height; `.wx-gantt` uses `height: 100%; width: 100%; overflow-y: auto`.
- `.wx-layout` is a flex row with hidden overflow.
- `.wx-table-container` uses `flex: 0 0 <grid width>` and `height: 100%`.
- `.wx-chart` uses `flex: 1 1 auto` with horizontal scrolling.
- `.wx-scale` is sticky at the top of the chart.
- `columns={false}` removes grid and resizer; otherwise grid and chart are split by the resizer.

Important CSS variables:

- bars: `--wx-gantt-bar-font`, `--wx-gantt-bar-border-radius`, `--wx-gantt-bar-shadow`
- tasks: `--wx-gantt-task-color`, `--wx-gantt-task-fill-color`, `--wx-gantt-task-font-color`, `--wx-gantt-task-border`, `--wx-gantt-task-border-color`
- summaries/milestones: `--wx-gantt-summary-color`, `--wx-gantt-summary-fill-color`, `--wx-gantt-summary-font-color`, `--wx-gantt-milestone-color`, `--wx-gantt-milestone-border-radius`
- critical/slack: `--wx-gantt-critical-color`, `--wx-gantt-task-critical-color`, `--wx-gantt-task-critical-fill-color`, `--wx-gantt-task-slack-color`, `--wx-gantt-task-slack-border-color`
- links: `--wx-gantt-link-color`, `--wx-gantt-link-color-hovered`, `--wx-gantt-link-critical-color`, `--wx-gantt-link-critical-color-hovered`, `--wx-gantt-link-marker-background`, `--wx-gantt-link-marker-color`
- grid/scale: `--wx-gantt-border`, `--wx-gantt-select-color`, `--wx-grid-body-font`, `--wx-grid-header-font`, `--wx-timescale-font`, `--wx-timescale-border`, `--wx-timescale-shadow`
- markers/tooltips: `--wx-gantt-marker-color`, `--wx-gantt-marker-font`, `--wx-gantt-marker-font-color`, `--wx-tooltip-background`, `--wx-tooltip-font`, `--wx-tooltip-font-color`

```vue
<script setup>
import { Gantt, Willow } from "@svar-ui/vue-gantt";
</script>

<template>
  <div class="gantt-shell">
    <Willow>
      <Gantt :tasks="tasks" :links="links" />
    </Willow>
  </div>
</template>

<style scoped>
.gantt-shell {
	height: 100%;
}

.gantt-shell .wx-gantt .wx-bar.wx-task.urgent {
	background-color: #f49a82;
	border: 1px solid #f45e36;
}

.gantt-shell .wx-gantt .wx-bar.wx-task.urgent .wx-progress-percent {
	background-color: #f45e36;
}

.gantt-shell .wx-gantt .my-marker {
	background-color: rgba(255, 84, 84, 0.77);
}
</style>
```

#### Recipes

##### Basic Gantt With Theme

```vue
<script setup>
import { Gantt, Willow } from "@svar-ui/vue-gantt";

const tasks = [
	{ id: 1, text: "Planning", type: "summary", parent: 0, open: true },
	{
		id: 10,
		text: "Research",
		type: "task",
		parent: 1,
		start: new Date(2026, 3, 2),
		duration: 3,
		progress: 50,
	},
];
const links = [];
</script>

<template>
  <div class="gtcell">
    <Willow>
      <Gantt :tasks="tasks" :links="links" />
    </Willow>
  </div>
</template>

<style scoped>
.gtcell {
	height: 100%;
}
</style>
```

##### Toolbar, Context Menu, And Editor

```vue
<script setup>
import { ref } from "vue";
import { Gantt, Toolbar, ContextMenu, Editor } from "@svar-ui/vue-gantt";

const api = ref();
</script>

<template>
  <Toolbar :api="api" />

  <div class="gtcell">
    <ContextMenu :api="api">
      <Gantt ref="api" :tasks="tasks" :links="links" :scales="scales" undo />
    </ContextMenu>
    <Editor :api="api" />
  </div>
</template>

<style scoped>
.gtcell {
	height: calc(100% - 50px);
	border-top: var(--wx-gantt-border);
}
</style>
```

##### Initialize API And Handle Actions

```vue
<script setup>
import { ref } from "vue";
import { Gantt, Editor } from "@svar-ui/vue-gantt";

const api = ref();

function init(ganttApi) {
	api.value = ganttApi;

	api.value.on("add-task", ({ id }) => {
		api.value.exec("show-editor", { id });
	});

	api.value.intercept("sort-tasks", ev => {
		return ev.key === "text";
	});
}
</script>

<template>
  <Gantt
    :init="init"
    :tasks="tasks"
    :links="links"
    :onupdatetask="ev => console.log(ev.id, ev.task)"
  />
  <Editor :api="api" />
</template>
```

##### Custom Columns And Inline Editors

```vue
<script setup>
import { Gantt } from "@svar-ui/vue-gantt";
import AvatarCell from "./AvatarCell.vue";

const columns = [
	{ id: "text", header: "Task name", width: 220, editor: "text" },
	{ id: "assigned", header: "Assigned", width: 160, cell: AvatarCell },
	{
		id: "start",
		header: ["Start date", { filter: { type: "datepicker" } }],
		align: "center",
		width: 130,
		editor: "datepicker",
	},
	{ id: "add-task", header: "Add task", width: 50, align: "center" },
];
</script>

<template>
  <Gantt :tasks="tasks" :links="links" :columns="columns" :cellHeight="40" />
</template>
```

##### Custom Task Content And Custom Event

```vue
<!-- TaskContent.vue -->
<script setup>
const props = defineProps({
  data: {},
  onaction: { type: Function },
});

function toggle(ev) {
	ev.stopPropagation();
	props.onaction?.({
		action: "custom-click",
		data: { id: props.data.id, clicked: !props.data.clicked },
	});
}
</script>

<template>
  <button :onclick="toggle">{{ props.data.clicked ? "Clicked" : "Click" }}</button>
</template>
```

```vue
<script setup>
import { ref } from "vue";
import { Gantt } from "@svar-ui/vue-gantt";
import TaskContent from "./TaskContent.vue";

const api = ref();
</script>

<template>
  <Gantt
    ref="api"
    :tasks="tasks"
    :links="links"
    :taskTemplate="TaskContent"
    :oncustomclick="ev =>
      api.exec('update-task', {
        id: ev.id,
        task: { clicked: ev.clicked },
      })"
  />
</template>
```

##### Custom Editor Items

```vue
<script setup>
import { ref } from "vue";
import {
	Gantt,
	Editor,
	getEditorItems,
	registerEditorItem,
	defaultTaskTypes,
} from "@svar-ui/vue-gantt";
import { RadioButtonGroup } from "@svar-ui/vue-core";

registerEditorItem("radio", RadioButtonGroup);

const base = getEditorItems();
const items = base.map(item =>
	item.key === "type"
		? {
				key: "type",
				comp: "radio",
				label: "Type",
				options: defaultTaskTypes.map(type => ({
					...type,
					value: type.id,
				})),
				config: { type: "inline" },
			}
		: item
);

const api = ref();
</script>

<template>
  <Gantt ref="api" :tasks="tasks" :links="links" />
  <Editor :api="api" :items="items" placement="modal" :autoSave="false" />
</template>
```

##### Custom Menu Options

```vue
<script setup>
import { ref } from "vue";
import { Gantt, ContextMenu, Editor, getMenuOptions } from "@svar-ui/vue-gantt";

const api = ref();
const ids = ["cut-task", "copy-task", "paste-task", "delete-task"];
const options = [
	{ id: "add-task:after", text: "Add below", icon: "wxi-plus" },
	...getMenuOptions().filter(op => ids.includes(op.id)),
	{
		id: "custom-action",
		text: "Custom action",
		icon: "wxi-empty",
		handler: () => console.log("custom action"),
	},
];
</script>

<template>
  <ContextMenu
    :api="api"
    :options="options"
    :onclick="({ context, action }) => console.log(context?.id, action?.id)"
  >
    <Gantt ref="api" :tasks="tasks" :links="links" />
  </ContextMenu>
  <Editor :api="api" />
</template>
```

##### Scales, Zoom, Markers, And Holidays

```vue
<script setup>
import { Gantt } from "@svar-ui/vue-gantt";

const scales = [
	{ unit: "year", step: 1, format: "%Y" },
	{ unit: "month", step: 1, format: "%F" },
	{ unit: "day", step: 1, format: "%j" },
];

const markers = [
	{ start: new Date(2026, 3, 2), text: "Start" },
	{ start: new Date(2026, 3, 8), text: "Review", css: "my-marker" },
];

function highlightTime(date, unit) {
	const weekend = date.getDay() === 0 || date.getDay() === 6;
	return unit === "day" && weekend ? "wx-weekend" : "";
}
</script>

<template>
  <Gantt
    :tasks="tasks"
    :links="links"
    :scales="scales"
    :markers="markers"
    :highlightTime="highlightTime"
    :start="new Date(2026, 3, 1)"
    :end="new Date(2026, 4, 1)"
    :cellWidth="60"
    zoom
  />
</template>
```

##### Pro Feature Bundle

```vue
<script setup>
import { ref } from "vue";
import {
	Gantt,
	ContextMenu,
	Editor,
	Toolbar,
	Tooltip,
} from "@svar-ui/vue-gantt";
import { Calendar } from "@svar-ui/gantt-store";
import TooltipContent from "./TooltipContent.vue";

const calendar = new Calendar({
	weekHours: {
		monday: 8,
		tuesday: 8,
		wednesday: 8,
		thursday: 8,
		friday: 8,
		saturday: 0,
		sunday: 0,
	},
});

const api = ref();
</script>

<template>
  <Toolbar :api="api" />
  <div class="gtcell">
    <ContextMenu :api="api">
      <Tooltip :api="api" :content="TooltipContent">
        <Gantt
          ref="api"
          :tasks="tasks"
          :links="links"
          :calendar="calendar"
          baselines
          splitTasks
          :rollups="{ type: 'closest' }"
          :criticalPath="{ type: 'flexible' }"
          :summary="{ autoProgress: true }"
          undo
        />
      </Tooltip>
    </ContextMenu>
    <Editor :api="api" />
  </div>
</template>
```

##### Server Provider And Lazy Data

```vue
<script setup>
import { ref } from "vue";
import { Gantt, ContextMenu, Editor } from "@svar-ui/vue-gantt";
import { RestDataProvider } from "@svar-ui/gantt-data-provider";

const provider = new RestDataProvider("/api/gantt");
const api = ref();
const tasks = ref([]);
const links = ref([]);

provider.getData().then(data => {
	tasks.value = data.tasks;
	links.value = data.links;
});

function init(ganttApi) {
	api.value = ganttApi;
	api.value.setNext(provider);
	api.value.on("request-data", ev => {
		provider.getData(ev.id).then(data => {
			api.value.exec("provide-data", { id: ev.id, data });
		});
	});
}
</script>

<template>
  <ContextMenu :api="api">
    <Gantt :init="init" ref="api" :tasks="tasks" :links="links" />
  </ContextMenu>
  <Editor :api="api" />
</template>
```

#### Implementation Notes

- `Tooltip.content` is typed as receiving only `{ data }`, but source also passes `segmentIndex` for split-task segment tooltips.
- `show-editor` public action type is `{ id: TID }`, but split-task source also passes `segmentIndex`.
- `Gantt` mutates task objects during date normalization; clone `tasks` before passing them if caller-owned data must remain unchanged.
- `columns` can be `false` for no grid; it is normalized to an empty column set by the store.
- date column templates are added automatically for `start`, `end`, and `duration` unless a column has a custom `template`.
- default `add-task` actions create `{ type: "task", text: _("New Task") }` and usually select or show the new task depending on caller.


## File: locales.md

> Source: `locales.md`

i18n patterns common to all SVAR Vue components - Locale wrapper, bundled language packs, extending words and formats

### Localizing SVAR Vue Components

All `@svar-ui/vue-*` widgets read locale data from a single Vue inject key (`wx-i18n`). The mechanics live in `@svar-ui/vue-core`; every other package consumes them.

#### Locale Wrapper

Wrap the subtree you want to localize. With no wrapper, widgets fall back to English.

```vue
<script setup>
import { Calendar, Locale } from "@svar-ui/vue-core";
import { de } from "@svar-ui/core-locales";
</script>

<template>
  <Locale :words="de">
    <Calendar :value="new Date(2025, 4, 1)" />
  </Locale>
</template>
```

Wrap the smallest subtree that needs the alternative locale - nested `Locale` blocks let different parts of the app render in different languages.

`Locale` does not render any DOM wrapper; it only mutates the injected context, so it never affects layout.

#### Bundled Language Packs

Core packs ship in `@svar-ui/core-locales`:

```js
import { en, cn, de, es, fr, it, ja, pt, ru } from "@svar-ui/core-locales";
```

Standalone widget packages ship their own dictionaries alongside the core pack - each exports locale objects keyed by language code (`cn`, `de`, `fr`, ...):

- `@svar-ui/core-locales` - core widgets (always include)
- `@svar-ui/editor-locales` - Editor
- `@svar-ui/filter-locales` - Filter
- `@svar-ui/gantt-locales` - Gantt
- `@svar-ui/filemanager-locales` - File Manager
- `@svar-ui/grid-locales` - Grid

If you see English fallbacks in a localized UI, the missing terms come from the package's own locale module - merge them in via `<Locale :words="..." />`.

To localize a standalone widget, merge the matching package locale with the core locale:

```vue
<script setup>
import { Gantt } from "@svar-ui/vue-gantt";
import { Locale } from "@svar-ui/vue-core";
import { cn } from "@svar-ui/gantt-locales";
import { cn as cnCore } from "@svar-ui/core-locales";
</script>

<template>
  <Locale :words="{ ...cn, ...cnCore }">
    <Gantt v-bind="settings" />
  </Locale>
</template>
```

#### Extending Or Overriding Words

`Locale words` accepts a partial pack and extends the current context. Spread an existing pack to keep its formats and override only what you need:

```vue
<script setup>
import { Calendar, Locale } from "@svar-ui/vue-core";
import { cn } from "@svar-ui/core-locales";

const words = {
    ...cn,
    formats: {
        ...cn.formats,
        monthYearFormat: "%Y年%F",
        yearFormat: "%Y年",
    },
};
</script>

<template>
  <Locale :words="words">
    <Calendar :value="new Date(2025, 4, 1)" />
  </Locale>
</template>
```

Pass `:optional="true"` to make merged terms additive fallbacks rather than overrides - useful for layering app-specific strings on top of a full pack.

#### Affected Surfaces

Locale changes calendar labels, date/time formats, modal buttons, pager strings, empty-list text, notice/modal helpers, color-board select text - any widget that displays static strings or formats values reads them through this context.

#### Direct Helper

For non-component code, use the `locale` helper to build a translator:

```js
import { en, locale } from "@svar-ui/vue-core";

const i18n = locale(en).extend(
    { core: { "Rows per page": "Rows" } },
    true
);
const _ = i18n.getGroup("core");
_("Rows per page"); // "Rows"
```


## File: themes.md

> Source: `themes.md`

### Styling SVAR Vue Components

All `@svar-ui/vue-*` widgets share the same theming pipeline. The mechanics live in `@svar-ui/vue-core`; every other package consumes them.

#### Per widget css files

Each package ships `style.css` (this component only) and `all.css` (this component plus all dependencies).

```css
@import "@svar-ui/vue-gantt/style.css";
```

#### Theme Wrapper

Wrap the part of the app that uses SVAR widgets in a theme component from `@svar-ui/vue-core`:

```vue
<script setup>
import { Willow } from "@svar-ui/vue-core";
</script>

<template>
  <Willow>
    <App />
  </Willow>
</template>
```

Available themes: `Willow`, `WillowDark`. The wrapper:

- provides the Vue inject key `wx-theme`
- renders `.wx-theme.wx-{name}-theme` with `height:100%`
- loads Open Sans + the `wxi` icon CSS by default; pass `:fonts="false"` to skip when the host app manages fonts itself

Without a theme wrapper widgets still render but lose theme variables and font/icon CSS.

#### Per-widget Willow / WillowDark themes

Several widgets ship their **own** `Willow` / `WillowDark` components on top of the core base. The widget version wraps the core theme and layers in widget-specific CSS variables (bar colors, grid borders, timescale fonts, etc.). When using such a widget, import the theme from the widget package - not from core - so both layers apply.

Widgets that expose custom `Willow` / `WillowDark` themes:

- `@svar-ui/vue-core` - base
- `@svar-ui/vue-gantt`
- `@svar-ui/vue-grid`
- `@svar-ui/vue-editor`
- `@svar-ui/vue-filter`
- `@svar-ui/vue-filemanager`
- `@svar-ui/vue-comments`
- `@svar-ui/vue-kanban`

The widget theme delegates to core and adds extra rules scoped to `.wx-willow-theme` (or `.wx-willow-dark-theme`):

```vue
<script setup>
import { Willow } from "@svar-ui/vue-core";
defineProps({ fonts: { type: Boolean, default: true } });
</script>

<template>
  <Willow :fonts="fonts">
    <slot v-if="$slots.default" />
  </Willow>
</template>

<style scoped>
:global(.wx-willow-theme) {
    --wx-gantt-border-color: #e6e6e6;
    --wx-gantt-task-color: #3983eb;
    /* ...widget-specific overrides... */
}
</style>
```

Mount the widget's own theme once at the app root. The wrapper internally renders the core `Willow`, so a separate core import is not needed:

```vue
<script setup>
import { Willow, Gantt } from "@svar-ui/vue-gantt";
</script>

<template>
  <Willow />
  <Gantt v-bind="settings" />
</template>
```

#### CSS Variables

Theme styling is variable-driven. Override variables on the theme wrapper or on any ancestor of the widgets you want to restyle - overrides cascade to every SVAR widget in the subtree.

```vue
<template>
  <Willow>
    <div class="brand">
      <App />
    </div>
  </Willow>
</template>

<style scoped>
.brand {
    --wx-color-primary: #0f766e;
    --wx-input-width: 280px;
    --wx-button-border-radius: 4px;
    --wx-calendar-cell-size: 30px;
}
</style>
```

Nest different wrapper blocks for per-section restyling without forking the theme.

#### `css` Prop Convention

Most widgets accept a `css` prop. The string is appended to the widget's root class, so it works as a parent styling hook:

```vue
<template>
  <Toolbar css="my-toolbar" :items="items" />
</template>

<style scoped>
.my-toolbar {
    padding: 8px 12px;
}
</style>
```

Composite widgets often expose secondary css props for nested popups (`menuCss` on `Toolbar`/`MenuBar`, etc.). Check the per-component file for the exact set.

#### Class Hooks

The per-component file lists the exact selectors that widget exposes.

#### Custom CSS class overrides

When writing custom rules to override widget styles, always use **at least two selectors** (e.g. `.a .b {}`). Vue scopes its component styles by appending a hash attribute which has higher specificity than a plain `.b`. A two-selector rule (`.a .b`) matches or beats that specificity and wins.

Convention: the first selector is a container/wrapper of the widget instance, the second is the inner class you want to alter:

```css
.my-gantt-host .wx-bar-task {
    background: #ff8800;
}
```

#### Override Order

Prefer in this order:

1. **CSS variables on a wrapper** - propagates consistently to every widget in the subtree.
2. **`css` prop class** - a stable parent hook that survives internal markup changes.
3. **Direct `.wx-*` selectors** - targeted overrides; tightest coupling to widget internals, use sparingly.

#### Core Vars

##### Base Colors

| Variable | Default | Use for |
|---|---|---|
| `--wx-color-primary` | `#37a9ef` | Primary accent - active states, selected items, links |
| `--wx-color-primary-selected` | `#d5eaf7` | Selected/highlighted row or item background |
| `--wx-color-primary-font` | `#fff` | Text on primary-colored backgrounds |
| `--wx-color-secondary` | `transparent` | Secondary/ghost element background |
| `--wx-color-secondary-hover` | `rgba(55, 169, 239, 0.12)` | Secondary hover background |
| `--wx-color-secondary-font` | `#37a9ef` | Secondary element text |
| `--wx-color-secondary-border` | `#37a9ef` | Secondary element border |
| `--wx-color-success` | `#77d257` | Success indicator |
| `--wx-color-warning` | `#fcba2e` | Warning indicator |
| `--wx-color-info` | `#37a9ef` | Info indicator |
| `--wx-color-danger` | `#fe6158` | Error/destructive state, error borders |
| `--wx-color-disabled` | `#f2f3f7` | Disabled element background |
| `--wx-color-disabled-alt` | `#e9e9e9` | Alternate disabled background |
| `--wx-color-font` | `#2c2f3c` | Primary text |
| `--wx-color-font-alt` | `#9fa1ae` | Secondary/muted text, placeholders |
| `--wx-color-font-disabled` | `#c0c3ce` | Disabled text |
| `--wx-color-link` | `#37a9ef` | Link text |
| `--wx-background` | `#ffffff` | Main surface |
| `--wx-background-alt` | `#f2f3f7` | Alternate surface (cards, tags, odd/even areas) |
| `--wx-background-hover` | `#eaedf5` | Hover state background |

##### Typography

| Variable | Default | Use for |
|---|---|---|
| `--wx-font-family` | `"Open Sans", Arial, Helvetica, sans-serif` | All text |
| `--wx-font-size` | `14px` | Body text |
| `--wx-line-height` | `20px` | Body line height |
| `--wx-font-size-md` | `14px` | Medium text |
| `--wx-line-height-md` | `24px` | Medium line height |
| `--wx-font-size-hd` | `16px` | Headings |
| `--wx-line-height-hd` | `30px` | Heading line height |
| `--wx-font-size-sm` | `12px` | Captions, small text |
| `--wx-line-height-sm` | `16px` | Small line height |
| `--wx-font-weight` | `400` | Normal weight |
| `--wx-font-weight-md` | `600` | Semi-bold (labels, buttons) |
| `--wx-font-weight-b` | `700` | Bold (modal headers) |

##### Icons

| Variable | Default | Use for |
|---|---|---|
| `--wx-icon-color` | `#9fa1ae` | Default icon tint |
| `--wx-icon-size` | `20px` | Icon dimensions |
| `--wx-icon-border-radius` | `2px` | Icon hover-state rounding |

##### Borders, Shadows, Spacing

| Variable | Default | Use for |
|---|---|---|
| `--wx-border` | `1px solid #e6e6e6` | Standard border |
| `--wx-border-radius` | `3px` | Default corner radius |
| `--wx-radius-major` | `6px` | Larger radius (cards, panels) |
| `--wx-border-light` | `none` | Subtle divider |
| `--wx-border-medium` | `1px solid #eaedf5` | Medium divider |
| `--wx-shadow-light` | `0px 3px 10px ...` | Elevated panels (popups, dropdowns) |
| `--wx-shadow-medium` | `0px 4px 20px ...` | High-elevation surfaces (modals) |
| `--wx-padding` | `8px` | Base spacing unit |

##### Layout

| Variable | Default | Use for |
|---|---|---|
| `--wx-field-gutter` | `16px` | Vertical gap between form rows |
| `--wx-field-width` | `400px` | Max width of a form field row |

##### Z-index Scale

| Layer | Value |
|---|---|
| Popups / dropdowns | `100` |
| Modals | `1000` |
| Notices / toasts | `1010` |
