# svar-vue — core

_Generated 2026-05-08T13:35:37.091Z_

## Contents

- [`core/index.md`](#file-core-index-md)
- [`core/avatar.md`](#file-core-avatar-md)
- [`core/button.md`](#file-core-button-md)
- [`core/calendar.md`](#file-core-calendar-md)
- [`core/checkbox.md`](#file-core-checkbox-md)
- [`core/colorboard.md`](#file-core-colorboard-md)
- [`core/colorpicker.md`](#file-core-colorpicker-md)
- [`core/colorselect.md`](#file-core-colorselect-md)
- [`core/combo.md`](#file-core-combo-md)
- [`core/counter.md`](#file-core-counter-md)
- [`core/datepicker.md`](#file-core-datepicker-md)
- [`core/daterangepicker.md`](#file-core-daterangepicker-md)
- [`core/dropdown.md`](#file-core-dropdown-md)
- [`core/field.md`](#file-core-field-md)
- [`core/fullscreen.md`](#file-core-fullscreen-md)
- [`core/globals.md`](#file-core-globals-md)
- [`core/icon.md`](#file-core-icon-md)
- [`core/locale.md`](#file-core-locale-md)
- [`core/modal.md`](#file-core-modal-md)
- [`core/modalarea.md`](#file-core-modalarea-md)
- [`core/month.md`](#file-core-month-md)
- [`core/multicombo.md`](#file-core-multicombo-md)
- [`core/pager.md`](#file-core-pager-md)
- [`core/popup.md`](#file-core-popup-md)
- [`core/portal.md`](#file-core-portal-md)
- [`core/radio.md`](#file-core-radio-md)
- [`core/rangecalendar.md`](#file-core-rangecalendar-md)
- [`core/richselect.md`](#file-core-richselect-md)
- [`core/segmented.md`](#file-core-segmented-md)
- [`core/select.md`](#file-core-select-md)
- [`core/sidearea.md`](#file-core-sidearea-md)
- [`core/slider.md`](#file-core-slider-md)
- [`core/suggest-dropdown.md`](#file-core-suggest-dropdown-md)
- [`core/switch.md`](#file-core-switch-md)
- [`core/tabs.md`](#file-core-tabs-md)
- [`core/text.md`](#file-core-text-md)
- [`core/textarea.md`](#file-core-textarea-md)
- [`core/themes.md`](#file-core-themes-md)
- [`core/timepicker.md`](#file-core-timepicker-md)
- [`core/twostate.md`](#file-core-twostate-md)
- [`locales.md`](#file-locales-md)
- [`themes.md`](#file-themes-md)


## File: core/index.md

> Source: `core/index.md`

Use when building, configuring, styling, or modifying SVAR Vue Core / @svar-ui/vue-core widgets, themes, locale, forms, popups, selectors, calendars, buttons, and display components

This is an index file. Open the focused widget file that matches the component you are using. Each child file is standalone and contain all critical info needed for that widget.

#### Package

```js
import {
	TextArea,
	Button,
	Checkbox,
	CheckboxGroup,
	ColorSelect,
	ColorBoard,
	ColorPicker,
	Combo,
	DatePicker,
	DateRangePicker,
	Fullscreen,
	Avatar,
	Icon,
	MultiCombo,
	Popup,
	Dropdown,
	Pager,
	RadioButton,
	RadioButtonGroup,
	RichSelect,
	Segmented,
	Select,
	Slider,
	Switch,
	Tabs,
	Text,
	Counter,
	Globals,
	Field,
	Calendar,
	Month,
	RangeCalendar,
	TimePicker,
	TwoState,
	Modal,
	ModalArea,
	SideArea,
	Portal,
	Willow,
	WillowDark,
	Locale,
	locale,
	popupContainer,
	SuggestDropdown,
	en,
} from "@svar-ui/vue-core";

import "@svar-ui/vue-core/all.css";
```

#### Widget Index

- `button.md` - `Button`
- `twostate.md` - `TwoState`
- `icon.md` - `Icon`
- `checkbox.md` - `Checkbox`, `CheckboxGroup`
- `radio.md` - `RadioButton`, `RadioButtonGroup`
- `switch.md` - `Switch`
- `segmented.md` - `Segmented`
- `tabs.md` - `Tabs`
- `field.md` - `Field`
- `text.md` - `Text`
- `textarea.md` - `TextArea`
- `counter.md` - `Counter`
- `slider.md` - `Slider`
- `select.md` - `Select`
- `combo.md` - `Combo`
- `multicombo.md` - `MultiCombo`
- `richselect.md` - `RichSelect`
- `suggest-dropdown.md` - `SuggestDropdown`
- `dropdown.md` - `Dropdown`
- `popup.md` - `Popup`
- `portal.md` - `Portal`, `popupContainer`
- `colorselect.md` - `ColorSelect`
- `colorboard.md` - `ColorBoard`
- `colorpicker.md` - `ColorPicker`
- `calendar.md` - `Calendar`
- `month.md` - `Month`
- `rangecalendar.md` - `RangeCalendar`
- `datepicker.md` - `DatePicker`
- `daterangepicker.md` - `DateRangePicker`
- `timepicker.md` - `TimePicker`
- `avatar.md` - `Avatar`
- `pager.md` - `Pager`
- `fullscreen.md` - `Fullscreen`
- `modal.md` - `Modal`
- `modalarea.md` - `ModalArea`
- `sidearea.md` - `SideArea`
- `globals.md` - `Globals`, `showNotice`, `showModal`
- `themes.md` - `Willow`, `WillowDark`, theme CSS variables
- `locale.md` - `Locale`, `locale`, `en`, bundled locale imports

#### Shared Contracts

- Most controls expose bindable `value` and an `onchange` callback. Event payloads differ by widget and are documented in each file.
- Option-based widgets generally use `{ id, label }` options and emit selected ids as values.
- Dropdown-backed widgets share `DropdownOptions` for position, align, width, inline mode, scroll tracking, and virtualization.


## File: core/avatar.md

> Source: `core/avatar.md`

### SVAR Vue Core Avatar

Package: `@svar-ui/vue-core`

#### Package

```js
import { Avatar } from "@svar-ui/vue-core";
```

#### Supported Functionality

- Displays one user or a stack of users.
- User object fields are `id`, `name`, `avatar`, and `color`.
- `size` controls circle size and computed font size; default is `32`.
- `limit` caps visible users before responsive fitting is applied.
- When users are hidden, the last visible avatar shows a `+N` overlay.
- If `avatar` is present, it renders an image; otherwise initials are derived from `name`.

#### Public Types

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

#### Styling

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

#### Recipes

##### User Stack With Responsive Overflow

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

##### Single Initial Avatar

```vue
<script setup>
import { Avatar } from "@svar-ui/vue-core";
</script>

<template>
  <Avatar :value="{ id: 1, name: 'Jane Smith', color: '#2f77e3' }" :size="40" />
</template>
```


## File: core/button.md

> Source: `core/button.md`

### SVAR Vue Core Button

Package: `@svar-ui/vue-core`

#### Package

```js
import { Button } from "@svar-ui/vue-core";
```

#### Supported Functionality

- Renders a native `<button class="wx-button">`.
- `type` is split on spaces and each part becomes a `wx-*` class.
- Typed values are `primary`, `secondary`, `danger`, `link`, and each with `block`.
- `css` is appended to the button class list.
- `icon` renders an `<i class={icon}>` before content.
- When `icon` is set and no `children` are supplied, the button also gets `.wx-icon` icon-only styling.
- Renders `children` slot when provided; otherwise renders `text`.
- `onclick` receives the native `MouseEvent`.

#### Public Types

```ts
import type { Component } from "vue";

export declare const Button: Component<{
	type?:
		| "primary"
		| "secondary"
		| "danger"
		| "link"
		| "primary block"
		| "secondary block"
		| "danger block"
		| "link block";
	css?: string;
	icon?: string;
	disabled?: boolean;
	title?: string;
	text?: string;
	children?: () => any;
	onclick?: (ev: MouseEvent) => void;
}>;
```

#### Styling

- Button class: `.wx-button`
- Type/state classes: `.wx-primary`, `.wx-secondary`, `.wx-danger`, `.wx-link`, `.wx-block`, `.wx-pressed`, `.wx-icon`
- Disabled styling uses the native `[disabled]` attribute.
- Icon child selector is `i`.

```vue
<template>
  <Button css="save-button" type="primary" icon="wxi-check">Save</Button>
</template>

<style scoped>
:.wx-button.save-button {
	min-width: 120px;
}
</style>
```

#### Recipes

##### Variants And Click Handler

```vue
<script setup>
import { Button } from "@svar-ui/vue-core";

function save(ev) {
	console.log(ev.currentTarget);
}
</script>

<template>
  <Button type="primary" icon="wxi-check" :onclick="save">Save</Button>
  <Button type="secondary block">Full Width</Button>
  <Button type="danger" disabled>Delete</Button>
  <Button type="link">Details</Button>
</template>
```

##### Icon-Only Button

```vue
<script setup>
import { Button } from "@svar-ui/vue-core";
</script>

<template>
  <Button
    icon="wxi-search"
    title="Search"
    :onclick="() => console.log('search')"
  />
</template>
```

#### Implementation Notes

- Source has `.wx-square` styles, but `square` is not in the public `type` union.
- `Button` does not call `preventDefault` or stop propagation; handler receives the raw event.


## File: core/calendar.md

> Source: `core/calendar.md`

### SVAR Vue Core Calendar

Package: `@svar-ui/vue-core`

#### Package

```js
import { Calendar } from "@svar-ui/vue-core";
```

#### Supported Functionality

- Full single-date calendar with header navigation and optional action buttons.
- `value` is bindable and is a `Date` or `null`.
- `current` is bindable and controls the visible month; source normalizes it to the first day of that month.
- `buttons` defaults to `["clear", "today"]`; pass `false` to hide buttons or `true` for the default set.
- `markers(date)` can return a CSS class string appended to the matching `.wx-day`.
- `onchange` receives `{ value: Date | null }`.
- Internally wraps the calendar panel in `Locale`, so it can work without an outer locale provider.

#### Public Types

```ts
import type { Component } from "vue";

export declare const Calendar: Component<{
	value?: Date;
	current?: Date;
	markers?: (date: Date) => string;
	buttons?: boolean | ("clear" | "today")[];
	onchange?: (ev: { value: Date | null }) => void;
}>;
```

#### Styling

- Calendar wrapper: `.wx-calendar`
- Layout: `.wx-wrap`, `.wx-buttons`, `.wx-button-item`
- Header: `.wx-header`, `.wx-pager`, `.wx-spacer`, `.wx-label`
- Month grid comes from `Month`: `.wx-weekdays`, `.wx-weekday`, `.wx-days`, `.wx-day`, `.wx-out`, `.wx-selected`, `.wx-weekend`, `.wx-inactive`
- Year/month pickers: `.wx-months`, `.wx-month`, `.wx-years`, `.wx-year`, `.wx-current`, `.wx-prev-decade`, `.wx-next-decade`

```vue
<template>
  <div class="compact-calendar">
    <Calendar :value="new Date(2025, 4, 1)" />
  </div>
</template>

<style scoped>
.compact-calendar {
	--wx-calendar-cell-size: 28px;
	--wx-calendar-padding: 8px;
}

.compact-calendar .holiday {
	outline: 1px solid var(--wx-color-warning);
}
</style>
```

#### Recipes

##### Mark Dates And Keep Visible Month Bound

```vue
<script setup>
import { ref } from "vue";
import { Calendar } from "@svar-ui/vue-core";

const value = ref(new Date(2025, 4, 1));
const current = ref(new Date(2025, 4, 1));

function markers(date) {
	return date.getDay() === 0 ? "holiday" : "";
}
</script>

<template>
  <Calendar
    v-model:value="value"
    v-model:current="current"
    :markers="markers"
    :buttons="['today']"
    :onchange="ev => console.log(ev.value)"
  />
</template>
```

##### Hide Action Buttons

```vue
<script setup>
import { Calendar } from "@svar-ui/vue-core";
</script>

<template>
  <Calendar :buttons="false" :onchange="ev => console.log(ev.value)" />
</template>
```

#### Implementation Notes

- Selecting a date clones it with `new Date(...)` before assigning `value`.
- Clearing sets `value` to `null`.
- Source calls `onchange` after updating the bindable `value`.


## File: core/checkbox.md

> Source: `core/checkbox.md`

### SVAR Vue Core Checkbox

Package: `@svar-ui/vue-core`

Use this file standalone for `Checkbox` and `CheckboxGroup`.

#### Package

```js
import { Checkbox, CheckboxGroup } from "@svar-ui/vue-core";
```

#### Supported Functionality

- `Checkbox.value` is a bindable boolean.
- `Checkbox.inputValue` is emitted alongside the checked state; default is an empty string.
- `Checkbox.onchange` emits `{ value, inputValue }`.
- `CheckboxGroup.options` are `{ id, label }`.
- `CheckboxGroup.value` is a bindable array of selected option ids.
- Group `onchange` emits `{ value }`.
- Group `type` supports `inline` and `grid`; default layout is one item per row.

#### Public Types

```ts
import type { Component } from "vue";

export declare const Checkbox: Component<{
	id?: string | number;
	label?: string;
	inputValue?: string | number;
	value?: boolean;
	style?: string;
	disabled?: boolean;
	onchange?: (ev: { value: boolean; inputValue: string | number }) => void;
}>;

export declare const CheckboxGroup: Component<{
	options?: { id: string | number; label: string }[];
	value?: (string | number)[];
	type?: "inline" | "grid";
	onchange?: (ev: { value: (string | number)[] }) => void;
}>;
```

#### Styling

- Checkbox wrapper: `.wx-checkbox`
- `style` prop is applied to the checkbox wrapper.
- Group wrapper: `.wx-checkboxgroup`, `.wx-checkboxgroup.wx-inline`, `.wx-checkboxgroup.wx-grid`
- Group item wrapper: `.wx-item`

```vue
<template>
  <div class="todo-checks">
    <CheckboxGroup :options="options" v-model:value="value" />
  </div>
</template>

<style scoped>
.todo-checks .wx-checkboxgroup .wx-item {
	margin-top: 8px;
}
</style>
```

#### Recipes

##### Single Checkbox

```vue
<script setup>
import { ref } from "vue";
import { Checkbox } from "@svar-ui/vue-core";

const done = ref(false);
</script>

<template>
  <Checkbox
    label="Done"
    inputValue="done"
    v-model:value="done"
    :onchange="ev => console.log(ev.value, ev.inputValue)"
  />
</template>
```

##### Checkbox Group

```vue
<script setup>
import { ref } from "vue";
import { CheckboxGroup } from "@svar-ui/vue-core";

const options = [
	{ id: "new", label: "New" },
	{ id: "open", label: "Open" },
	{ id: "done", label: "Done" },
];

const selected = ref(["new"]);
</script>

<template>
  <CheckboxGroup :options="options" v-model:value="selected" type="inline" />
</template>
```

#### Implementation Notes

- `CheckboxGroup` does not pass disabled state through option objects.


## File: core/colorboard.md

> Source: `core/colorboard.md`

### SVAR Vue Core ColorBoard

Package: `@svar-ui/vue-core`

#### Package

```js
import { ColorBoard } from "@svar-ui/vue-core";
```

#### Supported Functionality

- HSV color board with hue line, saturation/value block, text input, preview, and optional select button.
- `value` is bindable and defaults to `"#65D3B3"`.
- Valid typed hex is normalized to uppercase `#RRGGBB`; 3-digit hex is expanded.
- Moving sliders or typing a valid color emits `{ value, input: true }`.
- With `button={true}`, clicking the select button emits a final `{ value }`.
- Keyboard arrow keys move the focused block/line slider.

#### Public Types

```ts
import type { Component } from "vue";

export declare const ColorBoard: Component<{
	value?: string;
	button?: boolean;
	onchange?: (ev: { value: string; input?: boolean }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-colorboard`
- Saturation/value block: `.wx-color-block`
- Block slider: `.wx-color-block-slider.wx-slider`
- Hue line: `.wx-color-line`
- Hue slider: `.wx-color-line-slider.wx-slider`
- Controls row: `.wx-color-controls`
- Preview: `.wx-color`
- Text input: `.wx-text`

```vue
<template>
  <div class="picker-board">
    <ColorBoard v-model:value="value" />
  </div>
</template>

<style scoped>
.picker-board .wx-color-block {
	height: 180px;
}
</style>
```

#### Recipes

##### Inline Color Board

```vue
<script setup>
import { ref } from "vue";
import { ColorBoard } from "@svar-ui/vue-core";

const value = ref("#48C8E2");
</script>

<template>
  <div style="width: 300px">
    <ColorBoard
      v-model:value="value"
      :onchange="ev => {
        if (!ev.input) console.log(ev.value);
      }"
    />
  </div>
</template>
```


## File: core/colorpicker.md

> Source: `core/colorpicker.md`

### SVAR Vue Core ColorPicker

Package: `@svar-ui/vue-core`

#### Package

```js
import { ColorPicker } from "@svar-ui/vue-core";
```

#### Supported Functionality

- Input-like color picker that opens `ColorBoard` in a `Dropdown`.
- `value` is a bindable color string.
- The inner `ColorBoard` is rendered with `button="true"`.
- `ColorPicker` ignores `ColorBoard` input events and updates only on the final select event.
- Final selection closes the popup and emits `{ value }`.
- `clear` shows a close icon when value is set and not disabled.
- `dropdown` is forwarded to `Dropdown`.

#### Public Types

```ts
import type { Component } from "vue";

export interface DropdownOptions {
	inline?: boolean;
	position?: "top" | "right" | "bottom" | "left";
	align?: "start" | "center" | "end";
	css?: string;
	width?: string | "unset" | "auto";
	trackScroll?: boolean;
	virtualized?: boolean;
}

export declare const ColorPicker: Component<{
	value?: string;
	id?: string | number;
	placeholder?: string;
	title?: string;
	disabled?: boolean;
	error?: boolean;
	clear?: boolean;
	dropdown?: DropdownOptions;
	onchange?: (ev: { value: string }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-colorpicker`
- Selected swatch: `.wx-color`
- Clear icon: `.wxi-close`
- Input state classes: `.wx-focus`, `.wx-error`
- Dropdown content uses `ColorBoard` hooks such as `.wx-colorboard`, `.wx-color-block`, `.wx-color-line`.


```vue
<template>
  <ColorPicker :dropdown="{ css: 'color-popup', width: '300px' }" />
</template>

<style scoped>
.wx-popup.color-popup {
	width: 300px;
}
</style>
```

#### Recipes

##### Color Picker In A Field

```vue
<script setup>
import { ref } from "vue";
import { ColorPicker, Field } from "@svar-ui/vue-core";

const color = ref("#65D3B3");
</script>

<template>
  <Field label="Color" position="left">
    <ColorPicker
      v-model:value="color"
      placeholder="Select a color"
      clear
      :onchange="ev => console.log(ev.value)"
    />
  </Field>
</template>
```

#### Implementation Notes

- `ColorPicker` displays the current `value` as swatch background without validating it.


## File: core/colorselect.md

> Source: `core/colorselect.md`

### SVAR Vue Core ColorSelect

Package: `@svar-ui/vue-core`

#### Package

```js
import { ColorSelect } from "@svar-ui/vue-core";
```

#### Supported Functionality

- Input-like color palette selector.
- `value` is a bindable hex color string or empty string.
- Default colors are `#00a037`, `#37a9ef`, `#f5a623`, `#ff4c3b`, `#a0a0a0`, `#000000`, `#ffffff`.
- Clicking the input opens a `Dropdown` unless disabled.
- Palette includes an empty color item that selects `""`.
- `clear` shows a close icon when value is set and not disabled.
- `onchange` emits `{ value }`.

#### Public Types

```ts
import type { Component } from "vue";

export declare const ColorSelect: Component<{
	colors?: string[];
	value?: string;
	id?: string | number;
	clear?: boolean;
	placeholder?: string;
	title?: string;
	disabled?: boolean;
	error?: boolean;
	onchange?: (ev: { value: string }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-colorselect`
- Selected swatch: `.wx-selected`
- Dropdown palette: `.wx-colors`
- Swatch: `.wx-color`
- Empty swatch: `.wx-empty`
- Clear icon: `.wx-clear.wxi-close`


```vue
<template>
  <ColorSelect :colors="colors" v-model:value="value" clear />
</template>

<style scoped>
.wx-colorselect .wx-color {
	border-radius: 50%;
}
</style>
```

#### Recipes

##### Custom Palette

```vue
<script setup>
import { ref } from "vue";
import { ColorSelect, Field } from "@svar-ui/vue-core";

const color = ref("");
</script>

<template>
  <Field label="Color" position="left">
    <ColorSelect
      :colors="['#65D3B3', '#FFC975', '#58C3FE']"
      v-model:value="color"
      placeholder="Select a color"
      clear
    />
  </Field>
</template>
```


## File: core/combo.md

> Source: `core/combo.md`

### SVAR Vue Core Combo

Package: `@svar-ui/vue-core`

#### Package

```js
import { Combo } from "@svar-ui/vue-core";
```

#### Supported Functionality

- Searchable single-select input backed by `SuggestDropdown`.
- `options` are `{ id, label }` by default.
- `textField` controls display/filter field; default is `"label"`.
- `textOptions` can provide selected display objects when visible `options` are filtered or partial.
- Typing filters `options` case-insensitively by `textField`.
- Blur selects exact text match first, then first containing match, then previous value or first option.
- Dropdown selection updates bindable `value` and emits `{ value }`.
- `children` slot receives `{ option }` for custom list row content.
- `dropdown` is forwarded to `SuggestDropdown`/`Dropdown`.

#### Public Types

```ts
import type { Component } from "vue";

export interface DropdownOptions {
	inline?: boolean;
	position?: "top" | "right" | "bottom" | "left";
	align?: "start" | "center" | "end";
	css?: string;
	width?: string | "unset" | "auto";
	trackScroll?: boolean;
	virtualized?: boolean;
}

export declare const Combo: Component<{
	value?: string | number;
	id?: string | number;
	options?: { id: string | number; label: string }[];
	textOptions?: { id: string | number; label: string }[];
	textField?: string;
	placeholder?: string;
	title?: string;
	disabled?: boolean;
	error?: boolean;
	clear?: boolean;
	dropdown?: DropdownOptions & {
		virtualized?: boolean;
	};
	children?: () => any;
	onchange?: (ev: { value: string | number }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-combo`
- Icon: `.wx-icon`, close icon `.wxi-close`
- Error class is applied to the input as `.wx-error`.
- Dropdown list hooks from `SuggestDropdown`: `.wx-list`, `.wx-item`, `.wx-focus`, `.wx-no-data`.
- Non-inline dropdown `css` is appended to `.wx-popup`.


```vue
<template>
  <Combo :options="users" :dropdown="{ css: 'users-popup', width: '320px' }" />
</template>

<style scoped>
.wx-popup.users-popup .wx-list {
	max-height: 360px;
}
</style>
```

#### Recipes

##### Custom Option Template And Virtualized List

```vue
<script setup>
import { ref } from "vue";
import { Combo } from "@svar-ui/vue-core";

const users = Array.from({ length: 10000 }, (_, id) => ({
	id,
	label: `User ${id}`,
	email: `user${id}@example.com`,
}));

const value = ref(9000);
</script>

<template>
  <Combo
    :options="users"
    v-model:value="value"
    :dropdown="{ virtualized: true, width: '320px' }"
  >
    <template #children="{ option }">
      <div class="user-option">
        <strong>{{ option.label }}</strong>
        <span>{{ option.email }}</span>
      </div>
    </template>
  </Combo>
</template>
```

##### Hidden Selected Option

```vue
<script setup>
import { Combo } from "@svar-ui/vue-core";

const allUsers = [
	{ id: 87, label: "Berni Mayou" },
	{ id: 103, label: "Ned Stark" },
];

const visibleUsers = [{ id: 103, label: "Ned Stark" }];
</script>

<template>
  <Combo :textOptions="allUsers" :options="visibleUsers" :value="87" clear />
</template>
```

#### Implementation Notes

- Filtering assumes `option[textField]` is a string


## File: core/counter.md

> Source: `core/counter.md`

### SVAR Vue Core Counter

Package: `@svar-ui/vue-core`

#### Package

```js
import { Counter } from "@svar-ui/vue-core";
```

#### Supported Functionality

- Numeric input with decrement and increment buttons.
- Bindable `value`, default `0`.
- `step` defaults to `1`, `min` defaults to `0`, `max` defaults to `Infinity`.
- Button clicks update `value` and emit `{ value }`.
- Typing emits `{ value, input: true }` without immediately mutating the bound value in the handler payload path.
- Blur normalizes the bound value to min/max and step, then emits `{ value }`.
- `readonly` blocks button changes and blur normalization.
- `disabled` disables the input and both buttons.

#### Public Types

```ts
import type { Component } from "vue";

export declare const Counter: Component<{
	id?: string | number;
	value?: number;
	step?: number;
	min?: number;
	max?: number;
	error?: boolean;
	disabled?: boolean;
	readonly?: boolean;
	onchange?: (ev: { value: number; input?: boolean }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-counter`
- State classes: `.wx-disabled`, `.wx-readonly`, `.wx-error`
- Input: `.wx-input`
- Buttons: `.wx-btn`, `.wx-btn-dec`, `.wx-btn-inc`
- SVG icons: `.wx-dec`, `.wx-inc`

```vue
<template>
  <Counter v-model:value="value" :min="0" :max="30" />
</template>

<style scoped>
.wx-counter .wx-input {
	width: 64px;
}
</style>
```

#### Recipes

##### Counter With Final Change Handling

```vue
<script setup>
import { ref } from "vue";
import { Counter, Field } from "@svar-ui/vue-core";

const count = ref(5);
</script>

<template>
  <Field label="Quantity">
    <Counter
      v-model:value="count"
      :min="0"
      :max="30"
      :step="3"
      :onchange="ev => {
        if (!ev.input) console.log(ev.value);
      }"
    />
  </Field>
</template>
```


## File: core/datepicker.md

> Source: `core/datepicker.md`

### SVAR Vue Core DatePicker

Package: `@svar-ui/vue-core`

#### Package

```js
import { DatePicker } from "@svar-ui/vue-core";
```

#### Supported Functionality

- Input-like single-date picker backed by `Text`, `Dropdown`, and `Calendar`.
- `value` is bindable and is a `Date` or `null`.
- `format` can be a date format string or `(value: Date) => string`; locale date format is used by default.
- `editable={true}` parses committed text with `new Date(text)`.
- `editable={fn}` uses the custom parser and expects `Date | null`.
- `clear` passes through to the inner `Text` clear icon.
- `buttons` is forwarded to `Calendar`; default is `["clear", "today"]`.
- `dropdown` is forwarded to `Dropdown`; date dropdowns default width to `"unset"` when no width is provided.
- Popup closes on window scroll.
- `onchange` receives `{ value: Date | null }` after the bindable value is updated.

#### Public Types

```ts
import type { Component } from "vue";

export interface DropdownOptions {
	inline?: boolean;
	position?: "top" | "right" | "bottom" | "left";
	align?: "start" | "center" | "end";
	css?: string;
	width?: string | "unset" | "auto";
	trackScroll?: boolean;
	virtualized?: boolean;
}

export declare const DatePicker: Component<{
	value?: Date;
	id?: string | number;
	disabled?: boolean;
	error?: boolean;
	width?: string;
	align?: "start" | "center" | "end";
	placeholder?: string;
	format?: string | ((value: Date) => string);
	buttons?: boolean | ("clear" | "today")[];
	css?: string;
	title?: string;
	editable?: boolean | ((value: string) => Date | null);
	clear?: boolean;
	dropdown?: DropdownOptions;
	onchange?: (ev: { value: Date | null }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-datepicker`
- `css` is passed to the inner `Text`; use `css="wx-icon-left"` for the left-icon input variant.
- Inner input classes come from `Text`: `.wx-text`, `.wx-input`, `.wx-icon`, `.wx-error`, `.wx-disabled`, `.wx-focus`.
- Popup surface uses `Dropdown`/`Popup` hooks such as `.wx-popup`.
- Calendar hooks come from `Calendar` and `Month`.


```vue
<template>
  <DatePicker css="wx-icon-left date-input" :dropdown="{ css: 'date-popup' }" />
</template>

<style scoped>
.wx-text.date-input {
	--wx-input-width: 220px;
}

.wx-popup.date-popup {
	padding: 4px;
}
</style>
```

#### Recipes

##### Bound Date In A Field

```vue
<script setup>
import { ref } from "vue";
import { DatePicker, Field } from "@svar-ui/vue-core";

const value = ref(new Date(2025, 4, 1));
</script>

<template>
  <Field label="Date" position="left">
    <DatePicker v-model:value="value" clear :onchange="ev => console.log(ev.value)" />
  </Field>
</template>
```

##### Editable Date With Custom Parser

```vue
<script setup>
import { ref } from "vue";
import { DatePicker } from "@svar-ui/vue-core";

const value = ref(new Date(2025, 4, 1));

function parseDate(text) {
	const p = text.match(/(..)(..)(.+)/);
	return p ? new Date(p.slice(1, 4).join("/")) : null;
}
</script>

<template>
  <DatePicker
    v-model:value="value"
    :editable="parseDate"
    format="%m%d%Y"
    clear
    :dropdown="{ width: '280px', align: 'start' }"
  />
</template>
```

#### Implementation Notes

- Public types include `width` and `align`, but source does not use those props directly; use `dropdown={{ width, align }}`.
- Selecting the same date value does not emit `onchange`.


## File: core/daterangepicker.md

> Source: `core/daterangepicker.md`

### SVAR Vue Core DateRangePicker

Package: `@svar-ui/vue-core`

#### Package

```js
import { DateRangePicker } from "@svar-ui/vue-core";
```

#### Supported Functionality

- Input-like date range picker backed by `Text`, `Dropdown`, and `RangeCalendar`.
- `value` is bindable and is `{ start: Date; end?: Date }` or `null`.
- `format` can be a date format string or `(date: Date) => string`; locale date format is used by default.
- Display text is `start - end`; missing `end` displays only the start.
- `months` is forwarded to `RangeCalendar` and is `1` or `2`.
- `buttons` is forwarded to `RangeCalendar`; arrays can include `"done"`.
- `editable={true}` parses committed text with `new Date(text)`.
- `editable={fn}` uses the custom parser and expects `Date | null`.
- Editable parsing splits text on `" -"`.
- `clear` passes through to the inner `Text` clear icon.
- `dropdown` is forwarded to `Dropdown`; date dropdowns default width to `"unset"` when no width is provided.
- Popup closes on window scroll.
- `onchange` receives `{ value: { start: Date; end: Date | null } | null }`.

#### Public Types

```ts
import type { Component } from "vue";

export interface DropdownOptions {
	inline?: boolean;
	position?: "top" | "right" | "bottom" | "left";
	align?: "start" | "center" | "end";
	css?: string;
	width?: string | "unset" | "auto";
	trackScroll?: boolean;
	virtualized?: boolean;
}

export declare const DateRangePicker: Component<{
	value?: { start: Date; end?: Date };
	id?: string | number;
	disabled?: boolean;
	error?: boolean;
	width?: string;
	align?: "start" | "center" | "end";
	placeholder?: string;
	css?: string;
	title?: string;
	format?: string | ((date: Date) => string);
	months?: 1 | 2;
	buttons?: boolean | ("clear" | "today" | "done")[];
	editable?: boolean | ((value: string) => Date | null);
	clear?: boolean;
	dropdown?: DropdownOptions;
	onchange?: (ev: {
		value: { start: Date; end: Date | null } | null;
	}) => void;
}>;
```

#### Styling

- Wrapper: `.wx-daterangepicker`
- State classes: `.wx-disabled`, `.wx-error`
- `css` is passed to the inner `Text`.
- Inner input classes come from `Text`: `.wx-text`, `.wx-input`, `.wx-icon`.
- Popup surface uses `Dropdown`/`Popup` hooks such as `.wx-popup`.
- Calendar hooks come from `RangeCalendar`, `Calendar`, and `Month`.

```vue
<template>
  <DateRangePicker css="range-input" :dropdown="{ css: 'range-popup' }" />
</template>

<style scoped>
.wx-text.range-input {
	--wx-input-width: 280px;
}
</style>
```

#### Recipes

##### Two-Month Range Picker

```vue
<script setup>
import { ref } from "vue";
import { DateRangePicker, Field } from "@svar-ui/vue-core";

const value = ref({
	start: new Date(2025, 4, 1),
	end: new Date(2025, 4, 7),
});
</script>

<template>
  <Field label="Range" position="left">
    <DateRangePicker
      v-model:value="value"
      :months="2"
      :buttons="['done', 'clear', 'today']"
      clear
      :onchange="ev => console.log(ev.value)"
    />
  </Field>
</template>
```

##### Editable Range

```vue
<script setup>
import { ref } from "vue";
import { DateRangePicker } from "@svar-ui/vue-core";

const value = ref();
</script>

<template>
  <DateRangePicker
    v-model:value="value"
    editable
    placeholder="Start - end"
    :dropdown="{ width: 'unset', align: 'start' }"
  />
</template>
```

#### Implementation Notes

- Public types include `width` and `align`, but source does not use those props directly; use `dropdown={{ width, align }}`.
- If the popup closes while only `start` is selected, source emits the pending single-start range.
- With a `"done"` button, `RangeCalendar` holds intermediate selection changes until done is pressed.


## File: core/dropdown.md

> Source: `core/dropdown.md`

### SVAR Vue Core Dropdown

Package: `@svar-ui/vue-core`

#### Package

```js
import { Dropdown } from "@svar-ui/vue-core";
```

#### Supported Functionality

- Anchored dropdown surface for arbitrary child content.
- `position` is `top`, `right`, `bottom`, or `left`; default is `bottom`.
- `align` is `start`, `center`, or `end`; default is `start`.
- `width` defaults to `"100%"`.
- Non-inline mode renders a `Portal` containing `Popup` anchored to the trigger's parent node.
- `inline={true}` renders `.wx-dropdown` in place without `Portal`.
- `trackScroll` is passed to `Popup` in non-inline mode.
- `oncancel` is called by click-outside behavior and scroll tracking where enabled.

#### Public Types

```ts
import type { Component } from "vue";

export interface DropdownOptions {
	inline?: boolean;
	position?: "top" | "right" | "bottom" | "left";
	align?: "start" | "center" | "end";
	css?: string;
	width?: string | "unset" | "auto";
	trackScroll?: boolean;
	virtualized?: boolean;
}

export declare const Dropdown: Component<
	DropdownOptions & {
		children?: () => any;
		oncancel?: (ev: MouseEvent) => void;
	}
>;
```

#### Styling

- Inline dropdown container: `.wx-dropdown`
- Inline position classes: `.wx-top-start`, `.wx-top-center`, `.wx-top-end`, `.wx-bottom-start`, `.wx-bottom-center`, `.wx-bottom-end`, `.wx-left-start`, `.wx-left-center`, `.wx-left-end`, `.wx-right-start`, `.wx-right-center`, `.wx-right-end`
- Non-inline dropdown uses `Popup`; `css` is appended to `.wx-popup`.
- Hidden anchor marker: `.wx-portal-node`


```vue
<template>
  <Dropdown css="calendar-popup" width="300px">
    <div>Content</div>
  </Dropdown>
</template>

<style scoped>
.wx-popup.calendar-popup {
	padding: 8px;
}
</style>
```

#### Recipes

##### Anchored Dropdown

```vue
<script setup>
import { ref } from "vue";
import { Button, Calendar, Dropdown } from "@svar-ui/vue-core";

const open = ref(false);
</script>

<template>
  <Button :onclick="() => (open = true)">Open</Button>
  <Dropdown
    v-if="open"
    width="300px"
    position="bottom"
    align="start"
    css="calendar-popup"
    :oncancel="() => (open = false)"
  >
    <Calendar />
  </Dropdown>
</template>
```

##### Inline Dropdown

```vue
<script setup>
import { Dropdown } from "@svar-ui/vue-core";
</script>

<template>
  <div style="position: relative">
    <Dropdown inline width="200px" position="bottom" align="end">
      <div style="padding: 8px">Inline content</div>
    </Dropdown>
  </div>
</template>
```

#### Implementation Notes

- Source supports `autoFit = true` for inline dropdowns; `DropdownOptions` does not declare `autoFit`.
- `virtualized` is part of `DropdownOptions` for list helpers; `Dropdown` itself does not implement list virtualization.


## File: core/field.md

> Source: `core/field.md`

### SVAR Vue Core Field

Package: `@svar-ui/vue-core`

#### Package

```js
import { Field } from "@svar-ui/vue-core";
```

#### Supported Functionality

- Wraps controls with label and control layout.
- Default label position is top; `position="left"` creates a side label layout.
- `width` sets inline width on the `.wx-field` wrapper.
- `error` adds `.wx-error` and colors the label.
- `required` adds `.wx-required` and appends a red `*` to the label.
- `type="checkbox" | "slider" | "switch"` adjusts vertical padding for those controls in left-label layout.
- Sets Vue inject key `wx-input-id`; child controls that call `getInputId` share the generated id with the label.

#### Public Types

```ts
import type { Component } from "vue";

export declare const Field: Component<{
	label?: string;
	position?: "left";
	width?: string;
	error?: boolean;
	type?: "checkbox" | "slider" | "switch";
	required?: boolean;
	children?: () => any;
}>;
```

#### Styling

- Wrapper: `.wx-field`
- Side label modifier: `.wx-left`
- State classes: `.wx-error`, `.wx-required`
- Label: `.wx-label`
- Control wrapper: `.wx-field-control`
- Control type modifiers: `.wx-field-control.wx-checkbox`, `.wx-field-control.wx-slider`, `.wx-field-control.wx-switch`


```vue
<template>
  <Field label="Owner" position="left" width="480px">
    <slot />
  </Field>
</template>

<style scoped>
.wx-field.wx-left > .wx-label {
	width: 140px;
}
</style>
```

#### Recipes

##### Labeled Control

```vue
<script setup>
import { ref } from "vue";
import { Field, Text } from "@svar-ui/vue-core";

const name = ref("");
</script>

<template>
  <Field label="Name" required>
    <Text v-model:value="name" />
  </Field>
</template>
```

##### Nested Fields

```vue
<script setup>
import { Field, Text } from "@svar-ui/vue-core";
</script>

<template>
  <Field label="Name">
    <Field label="First" position="left">
      <Text />
    </Field>
    <Field label="Last" position="left">
      <Text />
    </Field>
  </Field>
</template>
```


## File: core/fullscreen.md

> Source: `core/fullscreen.md`

### SVAR Vue Core Fullscreen

Package: `@svar-ui/vue-core`

#### Package

```js
import { Fullscreen } from "@svar-ui/vue-core";
```

#### Supported Functionality

- Wraps content in a fullscreen-capable container.
- Default toggle button uses `Button` with `css="wx-fullscreen-button"`.
- Default icon switches between `wxi-expand` and `wxi-collapse`.
- Custom `toggleButton` slot receives `(toggleFullscreen, inFullscreen)`.
- `hotkey` configures a scoped hotkey on the fullscreen wrapper through `@svar-ui/lib-dom` hotkeys.
- Tracks native `fullscreenchange` to keep `inFullscreen` in sync.

#### Public Types

```ts
import type { Component, Slot } from "vue";

export declare const Fullscreen: Component<{
	toggleButton?: Slot<[(ev: MouseEvent) => void, boolean]>;
	children?: () => any;
	hotkey?: string;
}>;
```

#### Styling

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

#### Recipes

##### Custom Toggle Button

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

#### Implementation Notes

- `toggleFullscreen` calls `node.requestFullscreen()` and `document.exitFullscreen()`.


## File: core/globals.md

> Source: `core/globals.md`

### SVAR Vue Core Globals

Package: `@svar-ui/vue-core`

#### Package

```js
import { Globals } from "@svar-ui/vue-core";
```

#### Supported Functionality

- Renders children and installs Vue inject key `wx-helpers`.
- `wx-helpers.showNotice(msg)` appends a notice.
- `wx-helpers.showModal(msg)` renders a `Modal` and returns a Promise.
- `showNotice` payload fields used by source include `text`, `type`, `expire`, and optional `id`.
- Notice `type` can be empty or classes such as `info`, `warning`, `success`, and `danger`.
- `showNotice` default expiry is `5100ms`; `expire: -1` keeps the notice until the close icon is clicked.
- `showModal` payload fields used by source include `title`, `message`, and `buttons`.
- Confirm resolves the modal Promise; cancel rejects it.
- `Notice` and `Notices` are source components but are not top-level exports.

#### Public Types

```ts
import type { Component } from "vue";

export declare const Globals: Component<{
	children?: () => any;
}>;
```

#### Source Helper Shapes

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

#### Styling

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

#### Recipes

##### Install Globals At App Root

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

##### Use Notice And Modal Helpers In A Child

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

#### Implementation Notes

- `showModal` stores one active modal at a time.


## File: core/icon.md

> Source: `core/icon.md`

### SVAR Vue Core Icon

Package: `@svar-ui/vue-core`

#### Package

```js
import { Icon } from "@svar-ui/vue-core";
```

#### Supported Functionality

- Renders `<i class="wx-icon {css}">`.
- Use `css` for icon font classes such as `wxi-search`.
- `title` is forwarded to the `<i>`.
- `onclick` is forwarded to the `<i>`.
- If `children` slot is provided, it is rendered inside the `<i>` and `role="img"` is added.

#### Public Types

```ts
import type { Component } from "vue";

export declare const Icon: Component<{
	css?: string;
	title?: string;
	children?: () => any;
	onclick?: (ev: MouseEvent) => void;
}>;
```

#### Styling

- Icon class: `.wx-icon`
- `css` is appended to `.wx-icon`.

```vue
<template>
  <Icon css="wxi-search app-icon" title="Search" />
</template>

<style scoped>
.wx-icon.app-icon {
	color: var(--wx-color-primary);
}
</style>
```

#### Recipes

##### Clickable Icon

```vue
<script setup>
import { Icon } from "@svar-ui/vue-core";
</script>

<template>
  <Icon
    css="wxi-information-outline"
    title="Info"
    :onclick="() => console.log('info')"
  />
</template>
```

#### Implementation Notes

- The component intentionally uses an `<i>` rather than a button


## File: core/locale.md

> Source: `core/locale.md`

### SVAR Vue Core Locale

Package: `@svar-ui/vue-core`

#### Package

```js
import { Locale, locale, en } from "@svar-ui/vue-core";
```

For all bundled language packs, import from `@svar-ui/core-locales`:

```js
import { en, cn, de, es, fr, it, ja, pt, ru } from "@svar-ui/core-locales";
```

#### Supported Functionality

- `Locale` reads Vue inject key `wx-i18n`.
- If no locale context exists, it creates one from English words.
- If `words` is not `null`, it extends the current locale with `words`.
- `optional` is passed to the locale `extend` call.
- Use `Locale` around the smallest subtree that needs different words or formats.
- Locale affects calendar labels, date/time formats, modal buttons, pager labels, empty-list text, notices/modal helper strings, and color board select text.
- `locale` is re-exported in JS from `@svar-ui/lib-dom`.
- `en` is re-exported in JS from `@svar-ui/core-locales`.

#### Public Types

```ts
import type { Component } from "vue";

export declare const Locale: Component<{
	words?: any;
	optional?: boolean;
	children?: () => any;
}>;

export type { ILocale, Terms, TPosition } from "@svar-ui/lib-dom";
```

#### Styling

- `Locale` does not render a wrapper element or public classes.
- It only changes locale context for children.
- Styling changes that depend on locale direction or content length must be handled by app CSS or theme variables.

#### Recipes

##### Localize A Calendar Subtree

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

##### Override Date Formats

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

##### Use The Locale Helper Directly

```vue
<script setup>
import { en, locale } from "@svar-ui/vue-core";

const i18n = locale(en).extend(
	{
		core: {
			"Rows per page": "Rows",
		},
	},
	true
);
const _ = i18n.getGroup("core");
</script>

<template>
  <span>{{ _("Rows per page") }}</span>
</template>
```

#### Implementation Notes

- `Locale` renders only `children`; it has no DOM wrapper.

#### Other information

extra details about locales can be obtained from `../locales.md`


## File: core/modal.md

> Source: `core/modal.md`

### SVAR Vue Core Modal

Package: `@svar-ui/vue-core`

#### Package

```js
import { Modal } from "@svar-ui/vue-core";
```

#### Supported Functionality

- Fixed-position backdrop and centered window.
- `title` renders the default header unless a `header` slot is supplied.
- `children` renders the modal body.
- `footer` slot replaces the default button row.
- `buttons` defaults to `["cancel", "ok"]`; pass `false` to hide default buttons.
- Button id `"cancel"` calls `oncancel`; every other button id calls `onconfirm`.
- Button labels are localized through locale group `core`.
- Modal focuses itself on mount.
- Enter calls `onconfirm` unless focus is inside a `TEXTAREA` or `BUTTON`; Escape calls `oncancel`.

#### Public Types

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

#### Styling

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

#### Recipes

##### Portal Modal With Default Buttons

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

##### Custom Header And Footer

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

#### Implementation Notes

- Keyboard Enter/Escape handlers pass a keyboard event, while public types declare `MouseEvent`.
- Button click handlers pass `{ button, event }`.
- Default `"ok"` button is rendered as `type="block primary"`; other default buttons use `type="block secondary"`.


## File: core/modalarea.md

> Source: `core/modalarea.md`

### SVAR Vue Core ModalArea

Package: `@svar-ui/vue-core`

#### Package

```js
import { ModalArea } from "@svar-ui/vue-core";
```

#### Supported Functionality

- Local absolute-position modal backdrop and centered window.
- Intended for modal content inside the current layout rather than a viewport-level fixed modal.
- Renders only `children`; it has no built-in header, footer, buttons, or cancel handler.
- Uses a short fade transition.
- Parent layout should provide a positioned containing block when local placement matters.

#### Public Types

```ts
import type { Component } from "vue";

export declare const ModalArea: Component<{
	children?: () => any;
}>;
```

#### Styling

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

#### Recipes

##### Local Modal Overlay

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

#### Implementation Notes

- `ModalArea` does not trap focus or handle Escape.
- Use `Modal` when you need built-in title, buttons, confirmation, or cancellation behavior.


## File: core/month.md

> Source: `core/month.md`

### SVAR Vue Core Month

Package: `@svar-ui/vue-core`

#### Package

```js
import { Month } from "@svar-ui/vue-core";
```

#### Supported Functionality

- Low-level month grid used by `Calendar` and `RangeCalendar`.
- `current` is the visible month; pass a date inside the month to render.
- `part="normal"` is required for standalone single-date selection with `value={Date}`.
- Range rendering uses `value={{ start, end }}` and `part` values such as `"left"`, `"right"`, or `"both"`.
- `markers(date)` can return a CSS class string appended to `.wx-day`.
- `onchange` receives a `Date` directly, not an object.
- After selecting a date, source calls `oncancel()` if provided.
- Weekday labels and week start come from locale context, falling back to the default locale.

#### Public Types

```ts
import type { Component } from "vue";

export declare const Month: Component<{
	value?: { start: Date; end: Date } | Date;
	current?: Date;
	part?: string;
	markers?: (date: Date) => string;
	oncancel?: () => void;
	onchange?: (ev: Date) => void;
}>;
```

#### Styling

- Weekday row: `.wx-weekdays`, `.wx-weekday`
- Day grid: `.wx-days`, `.wx-day`
- Date state classes: `.wx-out`, `.wx-selected`, `.wx-left`, `.wx-right`, `.wx-inrange`, `.wx-weekend`, `.wx-inactive`
- Marker classes from `markers(date)` are appended to `.wx-day`.

```vue
<template>
  <Month :current="new Date(2025, 4, 1)" part="normal" :markers="markers" />
</template>

<style scoped>
.wx-day.payday {
	font-weight: 700;
}
</style>
```

#### Recipes

##### Standalone Single-Month Picker

```vue
<script setup>
import { ref } from "vue";
import { Month } from "@svar-ui/vue-core";

const value = ref(new Date(2025, 4, 15));
const current = ref(new Date(2025, 4, 1));
</script>

<template>
  <Month
    v-model:value="value"
    v-model:current="current"
    part="normal"
    :onchange="date => (value = date)"
  />
</template>
```

##### Range Markup Preview

```vue
<script setup>
import { Month } from "@svar-ui/vue-core";

const value = {
	start: new Date(2025, 4, 10),
	end: new Date(2025, 4, 18),
};
</script>

<template>
  <Month
    :value="value"
    :current="value.start"
    part="both"
    :onchange="date => console.log(date)"
  />
</template>
```

#### Implementation Notes

- Source default `part` is `""`; that path treats `value` as a range object. Use `part="normal"` for a plain `Date`.
- Days outside the current month get `.wx-out` and `.wx-inactive`.
- `Month` does not render calendar header or action buttons; use `Calendar` or `RangeCalendar` for those.


## File: core/multicombo.md

> Source: `core/multicombo.md`

### SVAR Vue Core MultiCombo

Package: `@svar-ui/vue-core`

#### Package

```js
import { MultiCombo } from "@svar-ui/vue-core";
```

#### Supported Functionality

- Multi-select searchable input backed by `SuggestDropdown`.
- `value` is a bindable array of selected ids.
- `options` are `{ id, label }` by default.
- `textField` controls display/filter field; default is `"label"`.
- `textOptions` can provide selected tag display objects when visible `options` are partial.
- Typing filters options case-insensitively by `textField`.
- Selected options render as tags with remove icons.
- `checkboxes` shows non-interactive checkboxes in dropdown rows.
- `children` slot receives `{ option }` for both tags and list rows.
- `onchange` emits `{ value }`.

#### Public Types

```ts
import type { Component } from "vue";

export interface DropdownOptions {
	inline?: boolean;
	position?: "top" | "right" | "bottom" | "left";
	align?: "start" | "center" | "end";
	css?: string;
	width?: string | "unset" | "auto";
	trackScroll?: boolean;
	virtualized?: boolean;
}

export declare const MultiCombo: Component<{
	id?: string | number;
	value?: (string | number)[];
	options?: { id: string | number; label: string }[];
	textOptions?: { id: string | number; label: string }[];
	textField?: string;
	placeholder?: string;
	title?: string;
	disabled?: boolean;
	error?: boolean;
	checkboxes?: boolean;
	dropdown?: DropdownOptions & {
		virtualized?: boolean;
	};
	children?: () => any;
	onchange?: (ev: { value: (string | number)[] }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-multicombo`
- State classes: `.wx-focus`, `.wx-disabled`, `.wx-error`, `.wx-not-empty`
- Border wrapper: `.wx-wrapper`
- Tags wrapper: `.wx-tags`, tag `.wx-tag`
- Input row: `.wx-select`
- Icons: `.wx-icon`, `.wxi-close`
- Dropdown list hooks: `.wx-list`, `.wx-item`, `.wx-focus`

```vue
<template>
  <MultiCombo :options="options" v-model:value="value" :dropdown="{ css: 'roles-popup' }" />
</template>

<style scoped>
.wx-multicombo .wx-tag {
	max-width: 180px;
}
</style>
```

#### Recipes

##### Multi Select With Checkboxes

```vue
<script setup>
import { ref } from "vue";
import { MultiCombo } from "@svar-ui/vue-core";

const options = [
	{ id: "editor", label: "Editor" },
	{ id: "owner", label: "Owner" },
	{ id: "viewer", label: "Viewer" },
];

const roles = ref(["viewer"]);
</script>

<template>
  <MultiCombo
    :options="options"
    v-model:value="roles"
    checkboxes
    placeholder="Select roles"
  />
</template>
```

##### Custom Tag And Row Content

```vue
<script setup>
import { MultiCombo } from "@svar-ui/vue-core";

const users = [
	{ id: 104, label: "Lord Varys", email: "little.birds@mail" },
];
</script>

<template>
  <MultiCombo :options="users" :value="[104]">
    <template #children="{ option }">
      <strong>{{ option.label }}</strong>
    </template>
  </MultiCombo>
</template>
```

#### Implementation Notes

- Filtering assumes `option[textField]` is a string
- The source `onselect` path ignores falsy ids; avoid empty-string ids for selected options.


## File: core/pager.md

> Source: `core/pager.md`

### SVAR Vue Core Pager

Package: `@svar-ui/vue-core`

#### Package

```js
import { Pager } from "@svar-ui/vue-core";
```

#### Supported Functionality

- Pagination control with rows-per-page input, page navigation icons, current page input, and total page count.
- `value` is the bindable current page; default is `1`.
- `pageSize` is bindable; default is `20`.
- `pageCount` is `Math.ceil(total / pageSize)`.
- `from` is the zero-based row offset: `(value - 1) * pageSize`.
- `to` is capped by `total`: `Math.min(value * pageSize, total)`.
- Page navigation emits `{ value, from, to }` after updating the bound page.
- Labels come from locale group `core`.

#### Public Types

```ts
import type { Component } from "vue";

export declare const Pager: Component<{
	total?: number;
	pageSize?: number;
	value?: number;
	onchange?: (ev: { value: number; from: number; to: number }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-pager`
- Sections: `.wx-left`, `.wx-center`, `.wx-right`
- Navigation icons: `.wx-icon`, icon font classes `wxi-angle-dbl-left`, `wxi-angle-left`, `wxi-angle-right`, `wxi-angle-dbl-right`
- Disabled icons: `.wx-disabled`
- Inputs use local `input` styles inside the component.

```vue
<template>
  <div class="grid-footer">
    <Pager :total="100" />
  </div>
</template>

<style scoped>
.grid-footer .wx-pager {
	justify-content: flex-end;
}
</style>
```

#### Recipes

##### Bound Page And Page Size

```vue
<script setup>
import { ref } from "vue";
import { Pager } from "@svar-ui/vue-core";

const page = ref(2);
const pageSize = ref(10);
</script>

<template>
  <Pager
    :total="100"
    v-model:value="page"
    v-model:pageSize="pageSize"
    :onchange="ev => console.log(ev.value, ev.from, ev.to)"
  />
</template>
```

#### Implementation Notes

- Page-size input calls `onchange` with `value` equal to the entered page size, not the active page.
- Page navigation calls `onchange` with `value` equal to the active page.
- Current-page input rejects values below `1`, above `pageCount`, or `NaN`.


## File: core/popup.md

> Source: `core/popup.md`

### SVAR Vue Core Popup

Package: `@svar-ui/vue-core`

#### Package

```js
import { Popup } from "@svar-ui/vue-core";
```

#### Supported Functionality

- Low-level absolutely positioned popup surface.
- Position is calculated with `calculatePosition` from `@svar-ui/lib-dom`.
- Use `parent` to anchor to an element, or use `left`/`top` with an `at` position.
- `at` defaults to `"bottom"` in source.
- `oncancel` is called by click-outside behavior.
- `width` can be number, "auto" or percentage like `100%` - calculated from `parent.offsetWidth`.
- `trackScroll`; when enabled hides on scroll outside of popup.

#### Public Types

```ts
import { TPosition } from "@svar-ui/lib-dom";
import type { Component } from "vue";

export declare const Popup: Component<{
	left?: number;
	top?: number;
	at?: TPosition;
	css: string;
	width: number | string;
	trackScroll: boolean;
	parent?: HTMLElement;
	children?: () => any;
	oncancel?: (ev: MouseEvent) => void;
}>;
```

#### Styling

- Container: `.wx-popup`
- Source appends `css` to `.wx-popup`.
- Inline style sets `position:absolute`, calculated `top`, `left`, and `width`.

```vue
<template>
  <Popup :parent="buttonNode" css="help-popup">
    <div class="body">Help</div>
  </Popup>
</template>

<style scoped>
.wx-popup.help-popup {
	padding: 12px;
}
</style>
```

#### Recipes

##### Popup Anchored To A Button

```vue
<script setup>
import { ref } from "vue";
import { Button, Popup } from "@svar-ui/vue-core";

const parent = ref(null);
</script>

<template>
  <div ref="parent">
    <Button>Anchor</Button>
  </div>

  <Popup v-if="parent" :parent="parent" at="bottom" :oncancel="() => (parent = null)">
    <div style="padding: 12px">Popup content</div>
  </Popup>
</template>
```

#### Implementation Notes

- Use `Dropdown` for the common anchored dropdown case; it handles `Portal` and parent discovery.


## File: core/portal.md

> Source: `core/portal.md`

### SVAR Vue Core Portal

Package: `@svar-ui/vue-core`

#### Package

```js
import { Portal, popupContainer } from "@svar-ui/vue-core";
```

#### Supported Functionality

- `Portal` moves its themed child node to `target` or the nearest `data-wx-portal-root` ancestor.
- If no local portal root exists, source appends to the top node from `@svar-ui/lib-dom` environment.
- `theme` defaults from `wx-theme` context when not supplied.
- Children receive an internal `{ mount }` callback argument in source.
- `popupContainer(node)` marks a local portal root with a generated `data-wx-portal-root` attribute.

#### Public Types

```ts
import type { Component } from "vue";

export declare const Portal: Component<{
	theme?: "willow" | "willow-dark";
	target?: HTMLElement;
	children?: () => any;
}>;

export declare function popupContainer(node: HTMLElement): void;
```

#### Styling

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

#### Recipes

##### Render A Modal Through Portal

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

##### Local Portal Root

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


## File: core/radio.md

> Source: `core/radio.md`

### SVAR Vue Core Radio

Package: `@svar-ui/vue-core`

Use this file standalone for `RadioButton` and `RadioButtonGroup`.

#### Package

```js
import { RadioButton, RadioButtonGroup } from "@svar-ui/vue-core";
```

#### Supported Functionality

- `RadioButton.value` is a bindable boolean checked state.
- `RadioButton.onchange` fires only when the radio becomes checked and emits `{ value: true, inputValue }`.
- Standalone radio buttons need a shared `name` to behave as one browser radio group.
- `RadioButtonGroup.options` are `{ id, label }`.
- `RadioButtonGroup.value` is the selected option id.
- Group `onchange` emits `{ value }`.
- Group `type` supports `inline` and `grid`; default layout is one item per row.

#### Public Types

```ts
import type { Component } from "vue";

export declare const RadioButton: Component<{
	id?: string | number;
	label?: string;
	value?: boolean;
	name?: string;
	inputValue?: string | number;
	disabled?: boolean;
	onchange?: (ev: { value: boolean; inputValue: string | number }) => void;
}>;

export declare const RadioButtonGroup: Component<{
	options?: { id: string | number; label: string }[];
	value?: string | number;
	type?: "inline" | "grid";
	onchange?: (ev: { value: string | number }) => void;
}>;
```

#### Styling

- Radio wrapper: `.wx-radio`
- Group wrapper: `.wx-radiogroup`, `.wx-radiogroup.wx-inline`, `.wx-radiogroup.wx-grid`
- Group item wrapper: `.wx-item`

```vue
<template>
  <RadioButtonGroup :options="options" v-model:value="value" type="grid" />
</template>

<style scoped>
.wx-radiogroup.wx-grid .wx-item {
	flex-basis: 33.333%;
	max-width: 33.333%;
}
</style>
```

#### Recipes

##### Standalone Radio Buttons

```vue
<script setup>
import { RadioButton } from "@svar-ui/vue-core";
</script>

<template>
  <RadioButton label="One" name="mode" inputValue="one" :value="true" />
  <RadioButton label="Two" name="mode" inputValue="two" />
</template>
```

##### Radio Group

```vue
<script setup>
import { ref } from "vue";
import { RadioButtonGroup } from "@svar-ui/vue-core";

const options = [
	{ id: 1, label: "Option 1" },
	{ id: 2, label: "Option 2" },
	{ id: 3, label: "Option 3" },
];

const value = ref(1);
</script>

<template>
  <RadioButtonGroup :options="options" v-model:value="value" type="inline" />
</template>
```

#### Implementation Notes

- `RadioButtonGroup` does not pass disabled state through option objects.


## File: core/rangecalendar.md

> Source: `core/rangecalendar.md`

### SVAR Vue Core RangeCalendar

Package: `@svar-ui/vue-core`

#### Package

```js
import { RangeCalendar } from "@svar-ui/vue-core";
```

#### Supported Functionality

- Date range calendar with bindable `start` and `end`.
- `months` is `1` or `2`; default is `2`.
- Two-month mode renders left and right panels with synchronized months.
- `buttons` defaults to `["clear", "today"]`; arrays can include `"done"`.
- When `buttons` includes `"done"`, selection changes are held until the done action emits the final value.
- Selection order is normalized: selecting an end before the start swaps `start` and `end`.
- `markers(date)` can return a class string appended to `.wx-day`.
- `onchange` receives `{ start: Date | null, end: Date | null }`.

#### Public Types

```ts
import type { Component } from "vue";

export declare const RangeCalendar: Component<{
	start?: Date;
	end?: Date;
	current?: Date;
	months?: 1 | 2;
	markers?: (date: Date) => string;
	buttons?: boolean | ("clear" | "today" | "done")[];
	onchange?: (ev: { start: Date | null; end: Date | null }) => void;
}>;
```

#### Styling

- Two-month wrapper: `.wx-rangecalendar`
- Panel wrapper: `.wx-half`
- Calendar panels use `.wx-calendar`, `.wx-wrap`, `.wx-buttons`, `.wx-button-item`
- Month range states: `.wx-selected`, `.wx-left`, `.wx-right`, `.wx-inrange`

```vue
<template>
  <div class="range-shell">
    <RangeCalendar :months="2" />
  </div>
</template>

<style scoped>
.range-shell {
	--wx-calendar-cell-size: 30px;
}
</style>
```

#### Recipes

##### Two-Month Range With Done Button

```vue
<script setup>
import { ref } from "vue";
import { RangeCalendar } from "@svar-ui/vue-core";

const start = ref(new Date(2025, 4, 1));
const end = ref(new Date(2025, 4, 7));
</script>

<template>
  <RangeCalendar
    v-model:start="start"
    v-model:end="end"
    :months="2"
    :buttons="['done', 'clear', 'today']"
    :onchange="ev => console.log(ev.start, ev.end)"
  />
</template>
```

##### Single-Month Range

```vue
<script setup>
import { ref } from "vue";
import { RangeCalendar } from "@svar-ui/vue-core";

const start = ref();
const end = ref();
</script>

<template>
  <RangeCalendar
    v-model:start="start"
    v-model:end="end"
    :months="1"
    :buttons="false"
    :onchange="ev => console.log(ev.start, ev.end)"
  />
</template>
```

#### Implementation Notes

- Source initializes the visible month from `start`, then `current`, then `new Date()`.
- Clearing emits `{ start: null, end: null }`.


## File: core/richselect.md

> Source: `core/richselect.md`

### SVAR Vue Core RichSelect

Package: `@svar-ui/vue-core`

#### Package

```js
import { RichSelect } from "@svar-ui/vue-core";
```

#### Supported Functionality

- Non-input single-select control backed by `SuggestDropdown`.
- `value` is the selected id and is bindable.
- `options` are `{ id, label }` by default.
- `textField` controls display field; default is `"label"`.
- `textOptions` can provide selected display objects when visible `options` are partial.
- `clear` shows a close icon when value is set and not disabled.
- `children` slot receives the option object directly for both selected content and list rows.
- `onchange` emits `{ value }`.

#### Public Types

```ts
import type { Component } from "vue";

export interface DropdownOptions {
	inline?: boolean;
	position?: "top" | "right" | "bottom" | "left";
	align?: "start" | "center" | "end";
	css?: string;
	width?: string | "unset" | "auto";
	trackScroll?: boolean;
	virtualized?: boolean;
}

export declare const RichSelect: Component<{
	value?: string | number;
	options?: { id: string | number; label: string }[];
	textOptions?: { id: string | number; label: string }[];
	placeholder?: string;
	disabled?: boolean;
	error?: boolean;
	title?: string;
	textField?: string;
	clear?: boolean;
	dropdown?: DropdownOptions & {
		virtualized?: boolean;
	};
	children?: () => any;
	onchange?: (ev: { value: string | number }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-richselect`
- State classes: `.wx-disabled`, `.wx-error`, `.wx-nowrap`
- Content label: `.wx-label`
- Placeholder: `.wx-placeholder`
- Icon: `.wx-icon`, close icon `.wxi-close`
- Dropdown list hooks: `.wx-list`, `.wx-item`, `.wx-focus`

```vue
<template>
  <RichSelect
    :options="users"
    :value="104"
    :dropdown="{ css: 'user-select-menu' }"
  />
</template>

<style scoped>
.wx-popup.user-select-menu .wx-item {
	min-height: 40px;
}
</style>
```

#### Recipes

##### Rich Select With Custom Template

```vue
<script setup>
import { RichSelect } from "@svar-ui/vue-core";

const users = [
	{ id: 104, label: "Lord Varys", email: "little.birds@mail" },
	{ id: 103, label: "Ned Stark", email: "winterhell@mail" },
];
</script>

<template>
  <RichSelect :options="users" :value="104">
    <template #children="option">
      <div>
        <strong>{{ option.label }}</strong>
        <span>{{ option.email }}</span>
      </div>
    </template>
  </RichSelect>
</template>
```

##### Hidden Selected Option

```vue
<script setup>
import { RichSelect } from "@svar-ui/vue-core";

const allUsers = [
	{ id: 87, label: "Berni Mayou" },
	{ id: 103, label: "Ned Stark" },
];

const visibleUsers = [{ id: 103, label: "Ned Stark" }];
</script>

<template>
  <RichSelect :textOptions="allUsers" :options="visibleUsers" :value="87" clear />
</template>
```

#### Implementation Notes

- Without a custom slot, `.wx-nowrap` is added to ellipsize the selected label.


## File: core/segmented.md

> Source: `core/segmented.md`

### SVAR Vue Core Segmented

Package: `@svar-ui/vue-core`

#### Package

```js
import { Segmented } from "@svar-ui/vue-core";
```

#### Supported Functionality

- Renders an inline segmented button group.
- `options` are `{ id, label, icon?, title? }`.
- `value` is the selected id and is bindable.
- Clicking an option sets `value = option.id` and emits `onchange({ value })`.
- `css` is appended to `.wx-segmented`.
- Default content renders `option.icon` and `option.label`.
- `children` slot receives `{ option }` for custom option content.

#### Public Types

```ts
import type { Component } from "vue";

export declare const Segmented: Component<{
	options?: {
		id: string | number;
		label: string;
		icon?: string;
		title?: string;
	}[];
	value?: string | number;
	css?: string;
	children?: () => any;
	onchange?: (ev: { value: string | number }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-segmented`
- Selected button: `.wx-selected`
- Default icon: `.wx-icon`, icon-only modifier `.wx-only`
- Default label: `.wx-label`

```vue
<template>
  <Segmented css="view-mode" :options="options" v-model:value="value" />
</template>

<style scoped>
.wx-segmented.view-mode {
	--wx-segmented-padding: 3px;
}
</style>
```

#### Recipes

##### Basic Segmented Control

```vue
<script setup>
import { ref } from "vue";
import { Segmented } from "@svar-ui/vue-core";

const options = [
	{ id: "list", label: "List", icon: "wxi-view-sequential" },
	{ id: "grid", label: "Grid", icon: "wxi-view-grid" },
];

const value = ref("list");
</script>

<template>
  <Segmented :options="options" v-model:value="value" :onchange="ev => console.log(ev.value)" />
</template>
```

##### Custom Option Content

```vue
<script setup>
import { Segmented } from "@svar-ui/vue-core";

const options = [
	{ id: "left", label: "Left", icon: "wxi-align-left" },
	{ id: "right", label: "Right", icon: "wxi-align-right" },
];
</script>

<template>
  <Segmented :options="options" value="left">
    <template #children="{ option }">
      <i :class="option.icon"></i>
      <span>{{ option.label }}</span>
    </template>
  </Segmented>
</template>
```


## File: core/select.md

> Source: `core/select.md`

### SVAR Vue Core Select

Package: `@svar-ui/vue-core`

#### Package

```js
import { Select } from "@svar-ui/vue-core";
```

#### Supported Functionality

- Renders a native `<select>` inside `.wx-select`.
- `options` are `{ id, label }` by default.
- `textField` changes the displayed field; default is `"label"`.
- `value` is bindable and stores the selected option id.
- `placeholder` is shown as an overlay when value is empty and not `0`.
- `clear` shows a close icon when the component has a value and is not disabled.
- `onchange` emits `{ value }`.

#### Public Types

```ts
import type { Component } from "vue";

export declare const Select: Component<{
	value?: string | number;
	options?: { id: string | number; label: string }[];
	placeholder?: string;
	title?: string;
	disabled?: boolean;
	error?: boolean;
	textField?: string;
	clear?: boolean;
	id?: string | number;
	onchange?: (ev: { value: string | number }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-select`
- Placeholder overlay: `.wx-placeholder`
- Icon: `.wx-icon`, close icon `.wxi-close`
- Error class is applied to the native `select` as `.wx-error`.

```vue
<template>
  <div class="owner-select">
    <Select :options="users" v-model:value="value" clear />
  </div>
</template>

<style scoped>
.owner-select .wx-select {
	--wx-input-width: 280px;
}
</style>
```

#### Recipes

##### Native Select With Clear

```vue
<script setup>
import { ref } from "vue";
import { Field, Select } from "@svar-ui/vue-core";

const users = [
	{ id: 103, label: "Ned Stark" },
	{ id: 104, label: "Lord Varys" },
];

const owner = ref("");
</script>

<template>
  <Field label="Owner" position="left">
    <Select
      :options="users"
      v-model:value="owner"
      placeholder="Select owner"
      clear
    />
  </Field>
</template>
```

#### Implementation Notes

- `Select` has no `css` prop; use a parent/global selector for styling.


## File: core/sidearea.md

> Source: `core/sidearea.md`

### SVAR Vue Core SideArea

Package: `@svar-ui/vue-core`

#### Package

```js
import { SideArea } from "@svar-ui/vue-core";
```

#### Supported Functionality

- Absolute-position side panel for local layouts.
- `position` public type supports only `"right"`; source defaults to `"right"`.
- Clicking outside the panel calls `oncancel`.
- Uses a fly transition from the right.
- Renders arbitrary `children`.

#### Public Types

```ts
import type { Component } from "vue";

export declare const SideArea: Component<{
	position?: "right";
	children?: () => any;
	oncancel?: () => void;
}>;
```

#### Styling

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

#### Recipes

##### Right-Side Local Panel

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


## File: core/slider.md

> Source: `core/slider.md`

### SVAR Vue Core Slider

Package: `@svar-ui/vue-core`

#### Package

```js
import { Slider } from "@svar-ui/vue-core";
```

#### Supported Functionality

- Renders an input range with optional label.
- Bindable `value`, default `0`.
- `min` defaults to `0`, `max` to `100`, `step` to `1`.
- `width` sets inline width on `.wx-slider`.
- During drag, `onchange` emits `{ value, previous, input: true }`.
- On final change, `onchange` emits `{ value, previous }`.
- `previous` tracks the previous input/final value separately for drag and final changes.

#### Public Types

```ts
import type { Component } from "vue";

export declare const Slider: Component<{
	id?: string | number;
	label?: string;
	width?: string;
	min?: number;
	max?: number;
	value?: number;
	step?: number;
	title?: string;
	disabled?: boolean;
	onchange?: (ev: {
		value: number;
		previous: number;
		input?: boolean;
	}) => void;
}>;
```

#### Styling

- Wrapper: `.wx-slider`
- Inner range input is styled through input pseudo-elements.
- Label is a native `label` inside `.wx-slider`.

```vue
<template>
  <Slider width="240px" v-model:value="value" />
</template>

<style scoped>
.wx-slider {
	--wx-slider-thumb-size: 18px;
}
</style>
```

#### Recipes

##### Slider With Drag And Final Events

```vue
<script setup>
import { ref } from "vue";
import { Field, Slider } from "@svar-ui/vue-core";

const progress = ref(50);
</script>

<template>
  <Field label="Progress" position="left" type="slider">
    <Slider
      :label="`Progress: ${progress}%`"
      v-model:value="progress"
      :min="0"
      :max="100"
      :onchange="ev => {
        if (ev.input) console.log('drag', ev.previous, ev.value);
        else console.log('final', ev.previous, ev.value);
      }"
    />
  </Field>
</template>
```


## File: core/suggest-dropdown.md

> Source: `core/suggest-dropdown.md`

### SVAR Vue Core SuggestDropdown

Package: `@svar-ui/vue-core`

#### Package

```js
import { SuggestDropdown } from "@svar-ui/vue-core";
```

#### Supported Functionality

- Low-level dropdown list helper used by `Combo`, `MultiCombo`, and `RichSelect`.
- Renders only when navigation index is not `null`; callers open it through `onready.navigate`.
- `items` are `{ id, label }`.
- `onready` receives navigation helpers: `navigate`, `keydown`, and `move`.
- `onselect` emits `{ id }`; in multiselect mode `id` is the next selected id array.
- `multiselect` toggles id arrays instead of a single id.
- `checkboxes` renders a non-interactive `Checkbox` in each row.
- `virtualized` renders only visible rows with fixed measured item height and overscan.
- `children` slot receives `{ option }`.

#### Public Types

```ts
import type { Component } from "vue";

export interface DropdownOptions {
	inline?: boolean;
	position?: "top" | "right" | "bottom" | "left";
	align?: "start" | "center" | "end";
	css?: string;
	width?: string | "unset" | "auto";
	trackScroll?: boolean;
	virtualized?: boolean;
}

export declare const SuggestDropdown: Component<
	DropdownOptions & {
		items?: { id: string | number; label: string }[];
		children?: () => any;
		onselect?: (ev: { id: string | number | (string | number)[] }) => void;
		onready?: (ev: {
			navigate?: (dir: number | null, ev?: KeyboardEvent) => void;
			keydown?: (ev: KeyboardEvent, dir: number) => void;
			move?: (ev: KeyboardEvent) => void;
		}) => void;
		multiselect?: boolean;
		checkboxes?: boolean;
		value?: string | number | (string | number)[];
		virtualized?: boolean;
	}
>;
```

#### Styling

- List container: `.wx-list`
- Virtual wrapper/content: `.wx-list-wrapper`, `.wx-list-content`
- Row: `.wx-item`
- Focus row: `.wx-item.wx-focus`
- Empty state: `.wx-no-data`
- Non-inline dropdown `css` is appended to `.wx-popup`.

```vue
<template>
  <SuggestDropdown :items="items" css="suggest-menu" />
</template>

<style scoped>
.wx-popup.suggest-menu .wx-list {
	max-height: 180px;
}
</style>
```

#### Recipes

##### Controlled Suggest Dropdown

```vue
<script setup>
import { ref } from "vue";
import { SuggestDropdown } from "@svar-ui/vue-core";

const items = [
	{ id: 1, label: "One" },
	{ id: 2, label: "Two" },
];

let api;
</script>

<template>
  <button :onclick="() => api.navigate(0)">Open</button>

  <SuggestDropdown
    :items="items"
    :onready="ev => (api = ev)"
    :onselect="ev => console.log(ev.id)"
  />
</template>
```

#### Implementation Notes

- Keyboard handlers use `ev.code` values `Enter`, `Space`, `Escape`, `Tab`, `ArrowDown`, and `ArrowUp`.
- Virtual mode measures the first rendered item and assumes all rows have that height.


## File: core/switch.md

> Source: `core/switch.md`

### SVAR Vue Core Switch

Package: `@svar-ui/vue-core`

#### Package

```js
import { Switch } from "@svar-ui/vue-core";
```

#### Supported Functionality

- Renders a labeled checkbox styled as a switch.
- `value` is a bindable boolean.
- `disabled` is forwarded to the hidden checkbox input.
- `onchange` emits `{ value }` after the checked state changes.
- `id` is used through the shared input id helper, so it can connect with a surrounding `Field`.

#### Public Types

```ts
import type { Component } from "vue";

export declare const Switch: Component<{
	id?: string | number;
	value?: boolean;
	disabled?: boolean;
	onchange?: (ev: { value: boolean }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-switch`
- Internal elements are an invisible checkbox input and a visual `span`.

```vue
<template>
  <Switch v-model:value="value" />
</template>

<style scoped>
.wx-switch {
	--wx-switch-width: 56px;
}
</style>
```

#### Recipes

##### Bound Switch In A Field

```vue
<script setup>
import { ref } from "vue";
import { Field, Switch } from "@svar-ui/vue-core";

const enabled = ref(true);
</script>

<template>
  <Field :label="`Enabled: ${enabled}`" position="left" type="switch">
    <Switch v-model:value="enabled" :onchange="ev => console.log(ev.value)" />
  </Field>
</template>
```

#### Implementation Notes

- The component does not expose `css`; style through parent/global selectors or theme variables.


## File: core/tabs.md

> Source: `core/tabs.md`

### SVAR Vue Core Tabs

Package: `@svar-ui/vue-core`

#### Package

```js
import { Tabs } from "@svar-ui/vue-core";
```

#### Supported Functionality

- Renders a tab strip only; render the tab panel yourself based on `value`.
- `options` are `{ id, label?, title?, icon? }`.
- `value` is the active tab id and is bindable.
- Clicking a tab sets `value = option.id` and emits `onchange({ value })`.
- `type` is `top` or `bottom`; default is `top`.
- Icons use the same icon class pattern as other core controls.

#### Public Types

```ts
import type { Component } from "vue";

export declare const Tabs: Component<{
	options?: {
		id: string | number;
		label?: string;
		title?: string;
		icon?: string;
	}[];
	value?: string | number;
	type?: "top" | "bottom";
	onchange?: (ev: { value: string | number }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-tabs`, plus `.wx-top` or `.wx-bottom`
- Active button: `.wx-active`
- Default icon: `.wx-icon`, icon-only modifier `.wx-only`
- Default label: `.wx-label`

```vue
<template>
  <Tabs :options="tabs" v-model:value="active" />
</template>

<style scoped>
.wx-tabs {
	--wx-tabs-cell-min-width: 80px;
}
</style>
```

#### Recipes

##### Tabs With Panels

```vue
<script setup>
import { ref } from "vue";
import { Tabs } from "@svar-ui/vue-core";

const tabs = [
	{ id: "info", label: "Info", icon: "wxi-alert" },
	{ id: "audit", label: "Audit" },
	{ id: "done", icon: "wxi-check", title: "Done" },
];

const active = ref("info");
</script>

<template>
  <Tabs :options="tabs" v-model:value="active" />

  <div v-if="active === 'info'">Info panel</div>
  <div v-else-if="active === 'audit'">Audit panel</div>
  <div v-else>Done panel</div>

  <Tabs :options="tabs" v-model:value="active" type="bottom" />
</template>
```

#### Implementation Notes

- `Tabs` has no `css` prop; style with an enclosing parent/global selector or theme variables.


## File: core/text.md

> Source: `core/text.md`

### SVAR Vue Core Text

Package: `@svar-ui/vue-core`

#### Package

```js
import { Text } from "@svar-ui/vue-core";
```

#### Supported Functionality

- Bindable `value`, with `string | number` public type.
- `type` supports `text`, `number`, and `password`; default is `text`.
- `onchange` fires `{ value, input: true }` on input and `{ value }` on native change.
- `focus` and `select` focus/select the input after mount.
- `clear` shows a close icon when the input has a value; clicking it sets `value = ""` and emits `{ value }`.
- `icon` renders inside the input. It is right-aligned unless `css` includes `wx-icon-left`.
- `inputStyle` is applied to the inner `<input>`.
- `readonly`, `disabled`, `error`, `placeholder`, and `title` are forwarded to the input/wrapper.

#### Public Types

```ts
import type { Component } from "vue";

export declare const Text: Component<{
	value?: string | number;
	id?: string | number;
	readonly?: boolean;
	focus?: boolean;
	select?: boolean;
	type?: "text" | "number" | "password";
	placeholder?: string;
	disabled?: boolean;
	error?: boolean;
	inputStyle?: string;
	title?: string;
	css?: string;
	icon?: string;
	clear?: boolean;
	onchange?: (ev: { value: string | number; input?: boolean }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-text`
- State/classes: `.wx-error`, `.wx-disabled`, `.wx-clear`, `.wx-icon-left`, `.wx-icon-right`
- Icon: `.wx-icon`; clear icon: `.wx-icon.wxi-close`
- `css` is appended to `.wx-text`.

```vue
<template>
  <Text css="search-input wx-icon-left" icon="wxi-search" clear />
</template>

<style scoped>
.wx-text.search-input {
	--wx-input-width: 320px;
}
</style>
```

#### Recipes

##### Text With Clear And Left Icon

```vue
<script setup>
import { ref } from "vue";
import { Field, Text } from "@svar-ui/vue-core";

const query = ref("");
</script>

<template>
  <Field label="Search" position="left">
    <Text
      v-model:value="query"
      placeholder="Type here"
      icon="wxi-search"
      css="wx-icon-left"
      clear
      :onchange="ev => {
        if (!ev.input) console.log('final', ev.value);
      }"
    />
  </Field>
</template>
```

##### Focus And Select On Mount

```vue
<script setup>
import { Text } from "@svar-ui/vue-core";
</script>

<template>
  <Text value="Some value" focus select />
</template>
```

#### Implementation Notes

- `type="number"` still binds through the input value; account for string/number conversion in your app logic.


## File: core/textarea.md

> Source: `core/textarea.md`

### SVAR Vue Core TextArea

Package: `@svar-ui/vue-core`

#### Package

```js
import { TextArea } from "@svar-ui/vue-core";
```

#### Supported Functionality

- Renders a native `<textarea class="wx-textarea">`.
- `value` is bindable.
- `onchange` fires `{ value, input: true }` on input and `{ value }` on native change.
- Supports `id`, `placeholder`, `title`, `disabled`, `error`, and `readonly`.
- The textarea is vertically resizable unless disabled.

#### Public Types

```ts
import type { Component } from "vue";

export declare const TextArea: Component<{
	value?: string;
	id?: string | number;
	placeholder?: string;
	title?: string;
	disabled?: boolean;
	error?: boolean;
	readonly?: boolean;
	onchange?: (ev: { value: string; input?: boolean }) => void;
}>;
```

#### Styling

- Textarea: `.wx-textarea`
- Error state: `.wx-textarea.wx-error`
- Disabled state uses `[disabled]`.

```vue
<template>
  <TextArea placeholder="Details" />
</template>

<style scoped>
.wx-textarea {
	min-height: 140px;
}
</style>
```

#### Recipes

##### TextArea In A Field

```vue
<script setup>
import { ref } from "vue";
import { Field, TextArea } from "@svar-ui/vue-core";

const details = ref("");
</script>

<template>
  <Field label="Details" error>
    <TextArea
      v-model:value="details"
      error
      title="Details are required"
      placeholder="Type here"
    />
  </Field>
</template>
```

#### Implementation Notes

- There is no `css` prop; style through a parent/global selector or theme variables.


## File: core/themes.md

> Source: `core/themes.md`

### SVAR Vue Core Themes

Package: `@svar-ui/vue-core`

#### Package

```js
import { Willow, WillowDark } from "@svar-ui/vue-core";
```

#### Supported Functionality

- Theme components provide Vue inject key `wx-theme`.
- `Willow` sets `wx-theme` to `"willow"`.
- `WillowDark` sets `wx-theme` to `"willow-dark"`.
- When `children` are supplied, each theme renders `.wx-theme.wx-*-theme` with `height:100%`.
- `fonts` defaults to `true`.
- `Willow` and `WillowDark` load Open Sans font files and the `wxi` icon CSS.
- Use `fonts={false}` when fonts/icons are already loaded or the app manages font loading.
- Theme styling is CSS-variable driven; override variables on the theme wrapper or an ancestor around specific controls.

#### Public Types

```ts
import type { Component } from "vue";

export declare const Willow: Component<{
	fonts?: boolean;
	children?: () => any;
}>;

export declare const WillowDark: Component<{
	fonts?: boolean;
	children?: () => any;
}>;
```

#### Styling


```vue
<template>
  <Willow :fonts="false">
    <div class="app-theme">
      <App />
    </div>
  </Willow>
</template>

<style scoped>
.app-theme {
	--wx-color-primary: #0f766e;
	--wx-input-width: 280px;
	--wx-button-border-radius: 4px;
	--wx-calendar-cell-size: 30px;
}
</style>
```

#### Recipes

##### Wrap An App In A Theme

```vue
<script setup>
import { Willow } from "@svar-ui/vue-core";
import AppRoutes from "./AppRoutes.vue";
</script>

<template>
  <Willow>
    <AppRoutes />
  </Willow>
</template>
```

##### Dark Theme Without CDN Font Injection

```vue
<script setup>
import { WillowDark } from "@svar-ui/vue-core";
</script>

<template>
  <WillowDark :fonts="false">
    <div class="screen">Dark UI</div>
  </WillowDark>
</template>
```

#### Other information

extra details about themes can be obtained from `../themes.md`


## File: core/timepicker.md

> Source: `core/timepicker.md`

### SVAR Vue Core TimePicker

Package: `@svar-ui/vue-core`

#### Package

```js
import { TimePicker } from "@svar-ui/vue-core";
```

#### Supported Functionality

- Input-like time picker backed by `Text`, `Dropdown`, `Slider`, and optional `TwoState`.
- `value` is bindable and is a `Date`; only hours and minutes are used.
- Default value is `new Date(0, 0, 0, 0, 0)` when `value` is nullish.
- `format` can be a time format string or `(value: Date) => string`; locale time format is used by default.
- Locale `calendar.clockFormat == 12` enables the AM/PM `TwoState`.
- Hour and minute text inputs update on blur.
- Hour and minute sliders update through `Slider.onchange`.
- `dropdown` is forwarded to `Dropdown`; date/time dropdowns default width to `"unset"` when no width is provided.
- `onchange` receives `{ value: Date }` after assigning the new bindable value.

#### Public Types

```ts
import type { Component } from "vue";

export interface DropdownOptions {
	inline?: boolean;
	position?: "top" | "right" | "bottom" | "left";
	align?: "start" | "center" | "end";
	css?: string;
	width?: string | "unset" | "auto";
	trackScroll?: boolean;
	virtualized?: boolean;
}

export declare const TimePicker: Component<{
	value?: Date;
	id?: string | number;
	title?: string;
	css?: string;
	disabled?: boolean;
	error?: boolean;
	format?: string | ((value: Date) => string);
	dropdown?: DropdownOptions;
	onchange?: (ev: { value: Date }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-timepicker`
- State classes: `.wx-disabled`, `.wx-error`
- `css` is passed to the inner `Text`.
- Popup content: `.wx-wrapper`, `.wx-timer`, `.wx-digit`, `.wx-separator`
- Slider rows use `Field` and `Slider` classes.
- AM/PM toggle uses `TwoState`/`Button` classes.

```vue
<template>
  <TimePicker css="time-input" :dropdown="{ css: 'time-popup', width: '260px' }" />
</template>

<style scoped>
.wx-text.time-input {
	--wx-input-width: 180px;
}
</style>
```

#### Recipes

##### Bound Time

```vue
<script setup>
import { ref } from "vue";
import { Field, TimePicker } from "@svar-ui/vue-core";

const value = ref(new Date(0, 0, 0, 14, 30));
</script>

<template>
  <Field label="Time" position="left">
    <TimePicker v-model:value="value" :onchange="ev => console.log(ev.value)" />
  </Field>
</template>
```

##### Twelve-Hour Locale

```vue
<script setup>
import { ref } from "vue";
import { Field, Locale, TimePicker } from "@svar-ui/vue-core";

const value = ref(new Date(0, 0, 0, 14, 30));
</script>

<template>
  <Locale
    :words="{
      formats: { timeFormat: '%g:%i %a' },
      calendar: { clockFormat: 12 },
    }"
  >
    <Field label="Time" position="left">
      <TimePicker v-model:value="value" :dropdown="{ width: '100%' }" />
    </Field>
  </Locale>
</template>
```

#### Implementation Notes

- The visible text is readonly; typed hour/minute edits happen only inside the popup.


## File: core/twostate.md

> Source: `core/twostate.md`

### SVAR Vue Core TwoState

Package: `@svar-ui/vue-core`

#### Package

```js
import { TwoState } from "@svar-ui/vue-core";
```

#### Supported Functionality

- Wraps `Button` and toggles bindable boolean `value`.
- When active, adds `pressed` to the forwarded `type`.
- `textActive` and `iconActive` replace `text` and `icon` while active.
- `children` renders inactive/default content; `active` slot renders active content when `value` is true.
- Click order: `onclick(ev)` first, then value toggle and `onchange({ value })`.
- Calling `ev.preventDefault()` inside `onclick` prevents the toggle and `onchange`.

#### Public Types

```ts
import type { Component, Slot } from "vue";

export declare const TwoState: Component<{
	value?: boolean;
	type?:
		| "primary"
		| "secondary"
		| "danger"
		| "link"
		| "primary block"
		| "secondary block"
		| "danger block"
		| "link block";
	icon?: string;
	disabled?: boolean;
	iconActive?: string;
	title?: string;
	css?: string;
	text?: string;
	textActive?: string;
	active?: Slot<[]>;
	children?: () => any;
	onclick?: (ev: MouseEvent) => void;
	onchange?: (ev: { value: boolean }) => void;
}>;
```

#### Styling

- Uses `Button`, so styling hooks are `.wx-button` plus `.wx-pressed` when active.
- `css` is passed to the inner `Button`.
- Button type variables such as `--wx-button-pressed`, `--wx-button-primary-pressed`, and `--wx-button-box-shadow` control active state.

```vue
<template>
  <TwoState css="favorite-button" icon="wxi-star" iconActive="wxi-check" />
</template>

<style scoped>
.wx-button.favorite-button.wx-pressed {
	font-weight: 700;
}
</style>
```

#### Recipes

##### Toggle With Active Content

```vue
<script setup>
import { ref } from "vue";
import { TwoState } from "@svar-ui/vue-core";

const active = ref(false);
</script>

<template>
  <TwoState
    v-model:value="active"
    type="primary"
    icon="wxi-star"
    iconActive="wxi-check"
    :onchange="ev => console.log(ev.value)"
  >
    Favorite
    <template #active>
      Favorited
    </template>
  </TwoState>
</template>
```

##### Prevent Toggle

```vue
<script setup>
import { TwoState } from "@svar-ui/vue-core";

function beforeToggle(ev) {
	if (!confirm("Toggle?")) ev.preventDefault();
}
</script>

<template>
  <TwoState :onclick="beforeToggle">Toggle</TwoState>
</template>
```

#### Implementation Notes

- The active slot is rendered only when `value` is true.
- If `active` is not supplied, the component reuses `children` or `text` with active icon/text substitutions.


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
