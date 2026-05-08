# svar-react — core

_Generated 2026-05-08T13:35:37.052Z_

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

Use when building, configuring, styling, or modifying SVAR React Core / @svar-ui/react-core widgets, themes, locale, forms, popups, selectors, calendars, buttons, and display components

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
} from "@svar-ui/react-core";
import "@svar-ui/react-menu/all.css";
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

- Most controls expose a controlled `value` prop and an `onChange` callback. Event payloads differ by widget and are documented in each file.
- Option-based widgets generally use `{ id, label }` options and emit selected ids as values.
- Dropdown-backed widgets share `DropdownOptions` for position, align, width, inline mode, scroll tracking, and virtualization.


## File: core/avatar.md

> Source: `core/avatar.md`

### SVAR React Core Avatar

Package: `@svar-ui/react-core`

#### Package

```js
import { Avatar } from "@svar-ui/react-core";
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
import type { ComponentType } from "react";

export interface IUser {
	id: string | number;
	name?: string;
	avatar?: string;
	color?: string;
}

export declare const Avatar: ComponentType<{
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

```jsx
<div className="people">
	<Avatar value={users} size={36} limit={5} />
</div>
```

```css
.people {
	width: 180px;
}

.people .wx-avatar {
	border: 2px solid var(--wx-background);
}
```

#### Recipes

##### User Stack With Responsive Overflow

```jsx
import { Avatar } from "@svar-ui/react-core";

const users = [
	{ id: 1, name: "Jane Smith", avatar: "/avatars/jane.png" },
	{ id: 2, name: "Lee Park", color: "#2ecc71" },
	{ id: 3, name: "Ana Stone", color: "#e74c3c" },
	{ id: 4, name: "Kai Wong", color: "#37a9ef" },
];

function Demo() {
	return (
		<div style={{ width: 160 }}>
			<Avatar value={users} size={32} limit={4} />
		</div>
	);
}
```

##### Single Initial Avatar

```jsx
import { Avatar } from "@svar-ui/react-core";

function Demo() {
	return (
		<Avatar value={{ id: 1, name: "Jane Smith", color: "#2f77e3" }} size={40} />
	);
}
```


## File: core/button.md

> Source: `core/button.md`

### SVAR React Core Button

Package: `@svar-ui/react-core`

#### Package

```js
import { Button } from "@svar-ui/react-core";
```

#### Supported Functionality

- Renders a native `<button class="wx-button">`.
- `type` is split on spaces and each part becomes a `wx-*` class.
- Typed values are `primary`, `secondary`, `danger`, `link`, and each with `block`.
- `css` is appended to the button class list.
- `icon` renders an `<i class={icon}>` before content.
- When `icon` is set and no `children` are supplied, the button also gets `.wx-icon` icon-only styling.
- Renders `children` when provided; otherwise renders `text`.
- `onClick` receives the native `MouseEvent`.

#### Public Types

```ts
import type { ComponentType, ReactNode, MouseEvent } from "react";

export declare const Button: ComponentType<{
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
	children?: ReactNode;
	onClick?: (ev: MouseEvent) => void;
}>;
```

#### Styling

- Button class: `.wx-button`
- Type/state classes: `.wx-primary`, `.wx-secondary`, `.wx-danger`, `.wx-link`, `.wx-block`, `.wx-pressed`, `.wx-icon`
- Disabled styling uses the native `[disabled]` attribute.
- Icon child selector is `i`.

```jsx
<Button css="save-button" type="primary" icon="wxi-check">Save</Button>
```

```css
:.wx-button.save-button {
	min-width: 120px;
}
```

#### Recipes

##### Variants And Click Handler

```jsx
import { Button } from "@svar-ui/react-core";

function Demo() {
	function save(ev) {
		console.log(ev.currentTarget);
	}

	return (
		<>
			<Button type="primary" icon="wxi-check" onClick={save}>Save</Button>
			<Button type="secondary block">Full Width</Button>
			<Button type="danger" disabled>Delete</Button>
			<Button type="link">Details</Button>
		</>
	);
}
```

##### Icon-Only Button

```jsx
import { Button } from "@svar-ui/react-core";

function Demo() {
	return (
		<Button
			icon="wxi-search"
			title="Search"
			onClick={() => console.log("search")}
		/>
	);
}
```

#### Implementation Notes

- Source has `.wx-square` styles, but `square` is not in the public `type` union.
- `Button` does not call `preventDefault` or stop propagation; handler receives the raw event.


## File: core/calendar.md

> Source: `core/calendar.md`

### SVAR React Core Calendar

Package: `@svar-ui/react-core`

#### Package

```js
import { Calendar } from "@svar-ui/react-core";
```

#### Supported Functionality

- Full single-date calendar with header navigation and optional action buttons.
- `value` is controlled and is a `Date` or `null`.
- `current` is controlled and controls the visible month; source normalizes it to the first day of that month.
- `buttons` defaults to `["clear", "today"]`; pass `false` to hide buttons or `true` for the default set.
- `markers(date)` can return a CSS class string appended to the matching `.wx-day`.
- `onChange` receives `{ value: Date | null }`.
- Internally wraps the calendar panel in `Locale`, so it can work without an outer locale provider.

#### Public Types

```ts
import type { ComponentType } from "react";

export declare const Calendar: ComponentType<{
	value?: Date;
	current?: Date;
	markers?: (date: Date) => string;
	buttons?: boolean | ("clear" | "today")[];
	onChange?: (ev: { value: Date | null }) => void;
}>;
```

#### Styling

- Calendar wrapper: `.wx-calendar`
- Layout: `.wx-wrap`, `.wx-buttons`, `.wx-button-item`
- Header: `.wx-header`, `.wx-pager`, `.wx-spacer`, `.wx-label`
- Month grid comes from `Month`: `.wx-weekdays`, `.wx-weekday`, `.wx-days`, `.wx-day`, `.wx-out`, `.wx-selected`, `.wx-weekend`, `.wx-inactive`
- Year/month pickers: `.wx-months`, `.wx-month`, `.wx-years`, `.wx-year`, `.wx-current`, `.wx-prev-decade`, `.wx-next-decade`

```jsx
<div className="compact-calendar">
	<Calendar value={new Date(2025, 4, 1)} />
</div>
```

```css
.compact-calendar {
	--wx-calendar-cell-size: 28px;
	--wx-calendar-padding: 8px;
}

.compact-calendar .holiday {
	outline: 1px solid var(--wx-color-warning);
}
```

#### Recipes

##### Mark Dates And Keep Visible Month Bound

```jsx
import { useState } from "react";
import { Calendar } from "@svar-ui/react-core";

function Demo() {
	const [value, setValue] = useState(new Date(2025, 4, 1));
	const [current, setCurrent] = useState(new Date(2025, 4, 1));

	function markers(date) {
		return date.getDay() === 0 ? "holiday" : "";
	}

	return (
		<Calendar
			value={value}
			current={current}
			markers={markers}
			buttons={["today"]}
			onChange={ev => {
				setValue(ev.value);
				console.log(ev.value);
			}}
		/>
	);
}
```

##### Hide Action Buttons

```jsx
import { Calendar } from "@svar-ui/react-core";

function Demo() {
	return (
		<Calendar buttons={false} onChange={ev => console.log(ev.value)} />
	);
}
```

#### Implementation Notes

- Selecting a date clones it with `new Date(...)` before assigning `value`.
- Clearing sets `value` to `null`.
- Source calls `onChange` after updating the value.


## File: core/checkbox.md

> Source: `core/checkbox.md`

### SVAR React Core Checkbox

Package: `@svar-ui/react-core`

Use this file standalone for `Checkbox` and `CheckboxGroup`.

#### Package

```js
import { Checkbox, CheckboxGroup } from "@svar-ui/react-core";
```

#### Supported Functionality

- `Checkbox.value` is a controlled boolean.
- `Checkbox.inputValue` is emitted alongside the checked state; default is an empty string.
- `Checkbox.onChange` emits `{ value, inputValue }`.
- `CheckboxGroup.options` are `{ id, label }`.
- `CheckboxGroup.value` is a controlled array of selected option ids.
- Group `onChange` emits `{ value }`.
- Group `type` supports `inline` and `grid`; default layout is one item per row.

#### Public Types

```ts
import type { ComponentType } from "react";

export declare const Checkbox: ComponentType<{
	id?: string | number;
	label?: string;
	inputValue?: string | number;
	value?: boolean;
	style?: string;
	disabled?: boolean;
	onChange?: (ev: { value: boolean; inputValue: string | number }) => void;
}>;

export declare const CheckboxGroup: ComponentType<{
	options?: { id: string | number; label: string }[];
	value?: (string | number)[];
	type?: "inline" | "grid";
	onChange?: (ev: { value: (string | number)[] }) => void;
}>;
```

#### Styling

- Checkbox wrapper: `.wx-checkbox`
- `style` prop is applied to the checkbox wrapper.
- Group wrapper: `.wx-checkboxgroup`, `.wx-checkboxgroup.wx-inline`, `.wx-checkboxgroup.wx-grid`
- Group item wrapper: `.wx-item`

```jsx
<div className="todo-checks">
	<CheckboxGroup options={options} value={value} onChange={ev => setValue(ev.value)} />
</div>
```

```css
.todo-checks .wx-checkboxgroup .wx-item {
	margin-top: 8px;
}
```

#### Recipes

##### Single Checkbox

```jsx
import { useState } from "react";
import { Checkbox } from "@svar-ui/react-core";

function Demo() {
	const [done, setDone] = useState(false);

	return (
		<Checkbox
			label="Done"
			inputValue="done"
			value={done}
			onChange={ev => {
				setDone(ev.value);
				console.log(ev.value, ev.inputValue);
			}}
		/>
	);
}
```

##### Checkbox Group

```jsx
import { useState } from "react";
import { CheckboxGroup } from "@svar-ui/react-core";

const options = [
	{ id: "new", label: "New" },
	{ id: "open", label: "Open" },
	{ id: "done", label: "Done" },
];

function Demo() {
	const [selected, setSelected] = useState(["new"]);

	return (
		<CheckboxGroup
			options={options}
			value={selected}
			onChange={ev => setSelected(ev.value)}
			type="inline"
		/>
	);
}
```

#### Implementation Notes

- `CheckboxGroup` does not pass disabled state through option objects.


## File: core/colorboard.md

> Source: `core/colorboard.md`

### SVAR React Core ColorBoard

Package: `@svar-ui/react-core`

#### Package

```js
import { ColorBoard } from "@svar-ui/react-core";
```

#### Supported Functionality

- HSV color board with hue line, saturation/value block, text input, preview, and optional select button.
- `value` is controlled and defaults to `"#65D3B3"`.
- Valid typed hex is normalized to uppercase `#RRGGBB`; 3-digit hex is expanded.
- Moving sliders or typing a valid color emits `{ value, input: true }`.
- With `button={true}`, clicking the select button emits a final `{ value }`.
- Keyboard arrow keys move the focused block/line slider.

#### Public Types

```ts
import type { ComponentType } from "react";

export declare const ColorBoard: ComponentType<{
	value?: string;
	button?: boolean;
	onChange?: (ev: { value: string; input?: boolean }) => void;
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

```jsx
<div className="picker-board">
	<ColorBoard value={value} onChange={ev => setValue(ev.value)} />
</div>
```

```css
.picker-board .wx-color-block {
	height: 180px;
}
```

#### Recipes

##### Inline Color Board

```jsx
import { useState } from "react";
import { ColorBoard } from "@svar-ui/react-core";

function Demo() {
	const [value, setValue] = useState("#48C8E2");

	return (
		<div style={{ width: 300 }}>
			<ColorBoard
				value={value}
				onChange={ev => {
					setValue(ev.value);
					if (!ev.input) console.log(ev.value);
				}}
			/>
		</div>
	);
}
```


## File: core/colorpicker.md

> Source: `core/colorpicker.md`

### SVAR React Core ColorPicker

Package: `@svar-ui/react-core`

#### Package

```js
import { ColorPicker } from "@svar-ui/react-core";
```

#### Supported Functionality

- Input-like color picker that opens `ColorBoard` in a `Dropdown`.
- `value` is a controlled color string.
- The inner `ColorBoard` is rendered with `button="true"`.
- `ColorPicker` ignores `ColorBoard` input events and updates only on the final select event.
- Final selection closes the popup and emits `{ value }`.
- `clear` shows a close icon when value is set and not disabled.
- `dropdown` is forwarded to `Dropdown`.

#### Public Types

```ts
import type { ComponentType } from "react";

export interface DropdownOptions {
	inline?: boolean;
	position?: "top" | "right" | "bottom" | "left";
	align?: "start" | "center" | "end";
	css?: string;
	width?: string | "unset" | "auto";
	trackScroll?: boolean;
	virtualized?: boolean;
}

export declare const ColorPicker: ComponentType<{
	value?: string;
	id?: string | number;
	placeholder?: string;
	title?: string;
	disabled?: boolean;
	error?: boolean;
	clear?: boolean;
	dropdown?: DropdownOptions;
	onChange?: (ev: { value: string }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-colorpicker`
- Selected swatch: `.wx-color`
- Clear icon: `.wxi-close`
- Input state classes: `.wx-focus`, `.wx-error`
- Dropdown content uses `ColorBoard` hooks such as `.wx-colorboard`, `.wx-color-block`, `.wx-color-line`.


```jsx
<ColorPicker dropdown={{ css: "color-popup", width: "300px" }} />
```

```css
.wx-popup.color-popup {
	width: 300px;
}
```

#### Recipes

##### Color Picker In A Field

```jsx
import { useState } from "react";
import { ColorPicker, Field } from "@svar-ui/react-core";

function Demo() {
	const [color, setColor] = useState("#65D3B3");

	return (
		<Field label="Color" position="left">
			<ColorPicker
				value={color}
				placeholder="Select a color"
				clear
				onChange={ev => {
					setColor(ev.value);
					console.log(ev.value);
				}}
			/>
		</Field>
	);
}
```

#### Implementation Notes

- `ColorPicker` displays the current `value` as swatch background without validating it.


## File: core/colorselect.md

> Source: `core/colorselect.md`

### SVAR React Core ColorSelect

Package: `@svar-ui/react-core`

#### Package

```js
import { ColorSelect } from "@svar-ui/react-core";
```

#### Supported Functionality

- Input-like color palette selector.
- `value` is a controlled hex color string or empty string.
- Default colors are `#00a037`, `#37a9ef`, `#f5a623`, `#ff4c3b`, `#a0a0a0`, `#000000`, `#ffffff`.
- Clicking the input opens a `Dropdown` unless disabled.
- Palette includes an empty color item that selects `""`.
- `clear` shows a close icon when value is set and not disabled.
- `onChange` emits `{ value }`.

#### Public Types

```ts
import type { ComponentType } from "react";

export declare const ColorSelect: ComponentType<{
	colors?: string[];
	value?: string;
	id?: string | number;
	clear?: boolean;
	placeholder?: string;
	title?: string;
	disabled?: boolean;
	error?: boolean;
	onChange?: (ev: { value: string }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-colorselect`
- Selected swatch: `.wx-selected`
- Dropdown palette: `.wx-colors`
- Swatch: `.wx-color`
- Empty swatch: `.wx-empty`
- Clear icon: `.wx-clear.wxi-close`


```jsx
<ColorSelect colors={colors} value={value} onChange={ev => setValue(ev.value)} clear />
```

```css
.wx-colorselect .wx-color {
	border-radius: 50%;
}
```

#### Recipes

##### Custom Palette

```jsx
import { useState } from "react";
import { ColorSelect, Field } from "@svar-ui/react-core";

function Demo() {
	const [color, setColor] = useState("");

	return (
		<Field label="Color" position="left">
			<ColorSelect
				colors={["#65D3B3", "#FFC975", "#58C3FE"]}
				value={color}
				onChange={ev => setColor(ev.value)}
				placeholder="Select a color"
				clear
			/>
		</Field>
	);
}
```


## File: core/combo.md

> Source: `core/combo.md`

### SVAR React Core Combo

Package: `@svar-ui/react-core`

#### Package

```js
import { Combo } from "@svar-ui/react-core";
```

#### Supported Functionality

- Searchable single-select input backed by `SuggestDropdown`.
- `options` are `{ id, label }` by default.
- `textField` controls display/filter field; default is `"label"`.
- `textOptions` can provide selected display objects when visible `options` are filtered or partial.
- Typing filters `options` case-insensitively by `textField`.
- Blur selects exact text match first, then first containing match, then previous value or first option.
- Dropdown selection updates the controlled `value` and emits `{ value }`.
- `children` render function receives `{ option }` for custom list row content.
- `dropdown` is forwarded to `SuggestDropdown`/`Dropdown`.

#### Public Types

```ts
import type { ComponentType, ReactNode } from "react";

export interface DropdownOptions {
	inline?: boolean;
	position?: "top" | "right" | "bottom" | "left";
	align?: "start" | "center" | "end";
	css?: string;
	width?: string | "unset" | "auto";
	trackScroll?: boolean;
	virtualized?: boolean;
}

export declare const Combo: ComponentType<{
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
	children?: (params: { option: any }) => ReactNode;
	onChange?: (ev: { value: string | number }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-combo`
- Icon: `.wx-icon`, close icon `.wxi-close`
- Error class is applied to the input as `.wx-error`.
- Dropdown list hooks from `SuggestDropdown`: `.wx-list`, `.wx-item`, `.wx-focus`, `.wx-no-data`.
- Non-inline dropdown `css` is appended to `.wx-popup`.


```jsx
<Combo options={users} dropdown={{ css: "users-popup", width: "320px" }} />
```

```css
.wx-popup.users-popup .wx-list {
	max-height: 360px;
}
```

#### Recipes

##### Custom Option Template And Virtualized List

```jsx
import { useState } from "react";
import { Combo } from "@svar-ui/react-core";

const users = Array.from({ length: 10000 }, (_, id) => ({
	id,
	label: `User ${id}`,
	email: `user${id}@example.com`,
}));

function Demo() {
	const [value, setValue] = useState(9000);

	return (
		<Combo
			options={users}
			value={value}
			onChange={ev => setValue(ev.value)}
			dropdown={{ virtualized: true, width: "320px" }}
		>
			{({ option }) => (
				<div className="user-option">
					<strong>{option.label}</strong>
					<span>{option.email}</span>
				</div>
			)}
		</Combo>
	);
}
```

##### Hidden Selected Option

```jsx
import { Combo } from "@svar-ui/react-core";

const allUsers = [
	{ id: 87, label: "Berni Mayou" },
	{ id: 103, label: "Ned Stark" },
];

const visibleUsers = [{ id: 103, label: "Ned Stark" }];

function Demo() {
	return (
		<Combo textOptions={allUsers} options={visibleUsers} value={87} clear />
	);
}
```

#### Implementation Notes

- Filtering assumes `option[textField]` is a string


## File: core/counter.md

> Source: `core/counter.md`

### SVAR React Core Counter

Package: `@svar-ui/react-core`

#### Package

```js
import { Counter } from "@svar-ui/react-core";
```

#### Supported Functionality

- Numeric input with decrement and increment buttons.
- Controlled `value`, default `0`.
- `step` defaults to `1`, `min` defaults to `0`, `max` defaults to `Infinity`.
- Button clicks update `value` and emit `{ value }`.
- Typing emits `{ value, input: true }` without immediately mutating the bound value in the handler payload path.
- Blur normalizes the bound value to min/max and step, then emits `{ value }`.
- `readonly` blocks button changes and blur normalization.
- `disabled` disables the input and both buttons.

#### Public Types

```ts
import type { ComponentType } from "react";

export declare const Counter: ComponentType<{
	id?: string | number;
	value?: number;
	step?: number;
	min?: number;
	max?: number;
	error?: boolean;
	disabled?: boolean;
	readonly?: boolean;
	onChange?: (ev: { value: number; input?: boolean }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-counter`
- State classes: `.wx-disabled`, `.wx-readonly`, `.wx-error`
- Input: `.wx-input`
- Buttons: `.wx-btn`, `.wx-btn-dec`, `.wx-btn-inc`
- SVG icons: `.wx-dec`, `.wx-inc`

```jsx
<Counter value={value} onChange={ev => setValue(ev.value)} min={0} max={30} />
```

```css
.wx-counter .wx-input {
	width: 64px;
}
```

#### Recipes

##### Counter With Final Change Handling

```jsx
import { useState } from "react";
import { Counter, Field } from "@svar-ui/react-core";

function Demo() {
	const [count, setCount] = useState(5);

	return (
		<Field label="Quantity">
			<Counter
				value={count}
				min={0}
				max={30}
				step={3}
				onChange={ev => {
					setCount(ev.value);
					if (!ev.input) console.log(ev.value);
				}}
			/>
		</Field>
	);
}
```


## File: core/datepicker.md

> Source: `core/datepicker.md`

### SVAR React Core DatePicker

Package: `@svar-ui/react-core`

#### Package

```js
import { DatePicker } from "@svar-ui/react-core";
```

#### Supported Functionality

- Input-like single-date picker backed by `Text`, `Dropdown`, and `Calendar`.
- `value` is a controlled prop and is a `Date` or `null`.
- `format` can be a date format string or `(value: Date) => string`; locale date format is used by default.
- `editable={true}` parses committed text with `new Date(text)`.
- `editable={fn}` uses the custom parser and expects `Date | null`.
- `clear` passes through to the inner `Text` clear icon.
- `buttons` is forwarded to `Calendar`; default is `["clear", "today"]`.
- `dropdown` is forwarded to `Dropdown`; date dropdowns default width to `"unset"` when no width is provided.
- Popup closes on window scroll.
- `onChange` receives `{ value: Date | null }` after the value is updated.

#### Public Types

```ts
import type { ComponentType } from "react";

export interface DropdownOptions {
	inline?: boolean;
	position?: "top" | "right" | "bottom" | "left";
	align?: "start" | "center" | "end";
	css?: string;
	width?: string | "unset" | "auto";
	trackScroll?: boolean;
	virtualized?: boolean;
}

export declare const DatePicker: ComponentType<{
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
	onChange?: (ev: { value: Date | null }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-datepicker`
- `css` is passed to the inner `Text`; use `css="wx-icon-left"` for the left-icon input variant.
- Inner input classes come from `Text`: `.wx-text`, `.wx-input`, `.wx-icon`, `.wx-error`, `.wx-disabled`, `.wx-focus`.
- Popup surface uses `Dropdown`/`Popup` hooks such as `.wx-popup`.
- Calendar hooks come from `Calendar` and `Month`.


```jsx
<DatePicker css="wx-icon-left date-input" dropdown={{ css: "date-popup" }} />
```

```css
.wx-text.date-input {
	--wx-input-width: 220px;
}

.wx-popup.date-popup {
	padding: 4px;
}
```

#### Recipes

##### Bound Date In A Field

```jsx
import { useState } from "react";
import { DatePicker, Field } from "@svar-ui/react-core";

function Example() {
	const [value, setValue] = useState(new Date(2025, 4, 1));

	return (
		<Field label="Date" position="left">
			<DatePicker
				value={value}
				clear
				onChange={ev => {
					setValue(ev.value);
					console.log(ev.value);
				}}
			/>
		</Field>
	);
}
```

##### Editable Date With Custom Parser

```jsx
import { useState } from "react";
import { DatePicker } from "@svar-ui/react-core";

function parseDate(text) {
	const p = text.match(/(..)(..)(.+)/);
	return p ? new Date(p.slice(1, 4).join("/")) : null;
}

function Example() {
	const [value, setValue] = useState(new Date(2025, 4, 1));

	return (
		<DatePicker
			value={value}
			editable={parseDate}
			format="%m%d%Y"
			clear
			dropdown={{ width: "280px", align: "start" }}
			onChange={ev => setValue(ev.value)}
		/>
	);
}
```

#### Implementation Notes

- Public types include `width` and `align`, but source does not use those props directly; use `dropdown={{ width, align }}`.
- Selecting the same date value does not emit `onChange`.


## File: core/daterangepicker.md

> Source: `core/daterangepicker.md`

### SVAR React Core DateRangePicker

Package: `@svar-ui/react-core`

#### Package

```js
import { DateRangePicker } from "@svar-ui/react-core";
```

#### Supported Functionality

- Input-like date range picker backed by `Text`, `Dropdown`, and `RangeCalendar`.
- `value` is a controlled prop and is `{ start: Date; end?: Date }` or `null`.
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
- `onChange` receives `{ value: { start: Date; end: Date | null } | null }`.

#### Public Types

```ts
import type { ComponentType } from "react";

export interface DropdownOptions {
	inline?: boolean;
	position?: "top" | "right" | "bottom" | "left";
	align?: "start" | "center" | "end";
	css?: string;
	width?: string | "unset" | "auto";
	trackScroll?: boolean;
	virtualized?: boolean;
}

export declare const DateRangePicker: ComponentType<{
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
	onChange?: (ev: {
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

```jsx
<DateRangePicker css="range-input" dropdown={{ css: "range-popup" }} />
```

```css
.wx-text.range-input {
	--wx-input-width: 280px;
}
```

#### Recipes

##### Two-Month Range Picker

```jsx
import { useState } from "react";
import { DateRangePicker, Field } from "@svar-ui/react-core";

function Example() {
	const [value, setValue] = useState({
		start: new Date(2025, 4, 1),
		end: new Date(2025, 4, 7),
	});

	return (
		<Field label="Range" position="left">
			<DateRangePicker
				value={value}
				months={2}
				buttons={["done", "clear", "today"]}
				clear
				onChange={ev => {
					setValue(ev.value);
					console.log(ev.value);
				}}
			/>
		</Field>
	);
}
```

##### Editable Range

```jsx
import { useState } from "react";
import { DateRangePicker } from "@svar-ui/react-core";

function Example() {
	const [value, setValue] = useState();

	return (
		<DateRangePicker
			value={value}
			editable
			placeholder="Start - end"
			dropdown={{ width: "unset", align: "start" }}
			onChange={ev => setValue(ev.value)}
		/>
	);
}
```

#### Implementation Notes

- Public types include `width` and `align`, but source does not use those props directly; use `dropdown={{ width, align }}`.
- If the popup closes while only `start` is selected, source emits the pending single-start range.
- With a `"done"` button, `RangeCalendar` holds intermediate selection changes until done is pressed.


## File: core/dropdown.md

> Source: `core/dropdown.md`

### SVAR React Core Dropdown

Package: `@svar-ui/react-core`

#### Package

```js
import { Dropdown } from "@svar-ui/react-core";
```

#### Supported Functionality

- Anchored dropdown surface for arbitrary child content.
- `position` is `top`, `right`, `bottom`, or `left`; default is `bottom`.
- `align` is `start`, `center`, or `end`; default is `start`.
- `width` defaults to `"100%"`.
- Non-inline mode renders a `Portal` containing `Popup` anchored to the trigger's parent node.
- `inline={true}` renders `.wx-dropdown` in place without `Portal`.
- `trackScroll` is passed to `Popup` in non-inline mode.
- `onCancel` is called by click-outside behavior and scroll tracking where enabled.

#### Public Types

```ts
import type { ComponentType, ReactNode } from "react";

export interface DropdownOptions {
	inline?: boolean;
	position?: "top" | "right" | "bottom" | "left";
	align?: "start" | "center" | "end";
	css?: string;
	width?: string | "unset" | "auto";
	trackScroll?: boolean;
	virtualized?: boolean;
}

export declare const Dropdown: ComponentType<
	DropdownOptions & {
		children?: ReactNode;
		onCancel?: (ev: MouseEvent) => void;
	}
>;
```

#### Styling

- Inline dropdown container: `.wx-dropdown`
- Inline position classes: `.wx-top-start`, `.wx-top-center`, `.wx-top-end`, `.wx-bottom-start`, `.wx-bottom-center`, `.wx-bottom-end`, `.wx-left-start`, `.wx-left-center`, `.wx-left-end`, `.wx-right-start`, `.wx-right-center`, `.wx-right-end`
- Non-inline dropdown uses `Popup`; `css` is appended to `.wx-popup`.
- Hidden anchor marker: `.wx-portal-node`


```jsx
<Dropdown css="calendar-popup" width="300px">
	<div>Content</div>
</Dropdown>
```

```css
.wx-popup.calendar-popup {
	padding: 8px;
}
```

#### Recipes

##### Anchored Dropdown

```jsx
import { useState } from "react";
import { Button, Calendar, Dropdown } from "@svar-ui/react-core";

function Example() {
	const [open, setOpen] = useState(false);

	return (
		<>
			<Button onClick={() => setOpen(true)}>Open</Button>
			{open && (
				<Dropdown
					width="300px"
					position="bottom"
					align="start"
					css="calendar-popup"
					onCancel={() => setOpen(false)}
				>
					<Calendar />
				</Dropdown>
			)}
		</>
	);
}
```

##### Inline Dropdown

```jsx
import { Dropdown } from "@svar-ui/react-core";

function Example() {
	return (
		<div style={{ position: "relative" }}>
			<Dropdown inline width="200px" position="bottom" align="end">
				<div style={{ padding: 8 }}>Inline content</div>
			</Dropdown>
		</div>
	);
}
```

#### Implementation Notes

- Source supports `autoFit = true` for inline dropdowns; `DropdownOptions` does not declare `autoFit`.
- `virtualized` is part of `DropdownOptions` for list helpers; `Dropdown` itself does not implement list virtualization.


## File: core/field.md

> Source: `core/field.md`

### SVAR React Core Field

Package: `@svar-ui/react-core`

#### Package

```js
import { Field } from "@svar-ui/react-core";
```

#### Supported Functionality

- Wraps controls with label and control layout.
- Default label position is top; `position="left"` creates a side label layout.
- `width` sets inline width on the `.wx-field` wrapper.
- `error` adds `.wx-error` and colors the label.
- `required` adds `.wx-required` and appends a red `*` to the label.
- `type="checkbox" | "slider" | "switch"` adjusts vertical padding for those controls in left-label layout.
- Sets React context `wx-input-id`; child controls that call `getInputId` share the generated id with the label.

#### Public Types

```ts
import type { ComponentType, ReactNode } from "react";

export declare const Field: ComponentType<{
	label?: string;
	position?: "left";
	width?: string;
	error?: boolean;
	type?: "checkbox" | "slider" | "switch";
	required?: boolean;
	children?: ReactNode;
}>;
```

#### Styling

- Wrapper: `.wx-field`
- Side label modifier: `.wx-left`
- State classes: `.wx-error`, `.wx-required`
- Label: `.wx-label`
- Control wrapper: `.wx-field-control`
- Control type modifiers: `.wx-field-control.wx-checkbox`, `.wx-field-control.wx-slider`, `.wx-field-control.wx-switch`


```jsx
<Field label="Owner" position="left" width="480px">
	{children}
</Field>
```

```css
.wx-field.wx-left > .wx-label {
	width: 140px;
}
```

#### Recipes

##### Labeled Control

```jsx
import { useState } from "react";
import { Field, Text } from "@svar-ui/react-core";

function Example() {
	const [name, setName] = useState("");

	return (
		<Field label="Name" required>
			<Text value={name} onChange={ev => setName(ev.value)} />
		</Field>
	);
}
```

##### Nested Fields

```jsx
import { Field, Text } from "@svar-ui/react-core";

function Example() {
	return (
		<Field label="Name">
			<Field label="First" position="left">
				<Text />
			</Field>
			<Field label="Last" position="left">
				<Text />
			</Field>
		</Field>
	);
}
```


## File: core/fullscreen.md

> Source: `core/fullscreen.md`

### SVAR React Core Fullscreen

Package: `@svar-ui/react-core`

#### Package

```js
import { Fullscreen } from "@svar-ui/react-core";
```

#### Supported Functionality

- Wraps content in a fullscreen-capable container.
- Default toggle button uses `Button` with `css="wx-fullscreen-button"`.
- Default icon switches between `wxi-expand` and `wxi-collapse`.
- Custom `toggleButton` render function receives `(toggleFullscreen, inFullscreen)`.
- `hotkey` configures a scoped hotkey on the fullscreen wrapper through `@svar-ui/lib-dom` hotkeys.
- Tracks native `fullscreenchange` to keep `inFullscreen` in sync.

#### Public Types

```ts
import type { ComponentType, ReactNode } from "react";

export declare const Fullscreen: ComponentType<{
	toggleButton?: (
		toggle: (ev: MouseEvent) => void,
		inFullscreen: boolean
	) => ReactNode;
	children?: ReactNode;
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

```jsx
<Fullscreen>
	<div className="report">Report content</div>
</Fullscreen>
```

```css
.wx-fullscreen .wx-fullscreen-button {
	right: 12px;
	bottom: 12px;
}
```

#### Recipes

##### Custom Toggle Button

```jsx
import { Button, Fullscreen } from "@svar-ui/react-core";

function Example() {
	return (
		<Fullscreen
			hotkey="ctrl+shift+f"
			toggleButton={(toggle, inFullscreen) => (
				<Button onClick={toggle}>
					{inFullscreen ? "Exit fullscreen" : "Enter fullscreen"}
				</Button>
			)}
		>
			<div className="panel">Report content</div>
		</Fullscreen>
	);
}
```

#### Implementation Notes

- `toggleFullscreen` calls `node.requestFullscreen()` and `document.exitFullscreen()`.


## File: core/globals.md

> Source: `core/globals.md`

### SVAR React Core Globals

Package: `@svar-ui/react-core`

#### Package

```js
import { Globals } from "@svar-ui/react-core";
```

#### Supported Functionality

- Renders children and installs React context `context.helpers`.
- `helpers.showNotice(msg)` appends a notice.
- `helpers.showModal(msg)` renders a `Modal` and returns a Promise.
- `showNotice` payload fields used by source include `text`, `type`, `expire`, and optional `id`.
- Notice `type` can be empty or classes such as `info`, `warning`, `success`, and `danger`.
- `showNotice` default expiry is `5100ms`; `expire: -1` keeps the notice until the close icon is clicked.
- `showModal` payload fields used by source include `title`, `message`, and `buttons`.
- Confirm resolves the modal Promise; cancel rejects it.
- `Notice` and `Notices` are source components but are not top-level exports.

#### Public Types

```ts
import type { ComponentType, ReactNode } from "react";

export declare const Globals: ComponentType<{
	children?: ReactNode;
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

```jsx
<Globals>
	<App />
</Globals>
```

```css
.wx-notices {
	top: 12px;
	right: 12px;
}
```

#### Recipes

##### Install Globals At App Root

```jsx
import { Globals } from "@svar-ui/react-core";
import Actions from "./Actions.jsx";

function App() {
	return (
		<Globals>
			<Actions />
		</Globals>
	);
}
```

##### Use Notice And Modal Helpers In A Child

```jsx
import { useContext } from "react";
import { Button, context } from "@svar-ui/react-core";

function Actions() {
	const { showNotice, showModal } = useContext(context.helpers);

	async function confirmDelete() {
		try {
			await showModal({ title: "Confirm", message: "Delete item?" });
			showNotice({ type: "success", text: "Deleted" });
		} catch {
			showNotice({ type: "info", text: "Canceled" });
		}
	}

	return (
		<>
			<Button type="danger" onClick={confirmDelete}>Delete</Button>
			<Button onClick={() => showNotice({ type: "info", text: "Saved" })}>
				Notice
			</Button>
		</>
	);
}
```

#### Implementation Notes

- `showModal` stores one active modal at a time.


## File: core/icon.md

> Source: `core/icon.md`

### SVAR React Core Icon

Package: `@svar-ui/react-core`

#### Package

```js
import { Icon } from "@svar-ui/react-core";
```

#### Supported Functionality

- Renders `<i className="wx-icon {css}">`.
- Use `css` for icon font classes such as `wxi-search`.
- `title` is forwarded to the `<i>`.
- `onClick` is forwarded to the `<i>`.
- If `children` is provided, it is rendered inside the `<i>` and `role="img"` is added.

#### Public Types

```ts
import type { ComponentType, ReactNode } from "react";

export declare const Icon: ComponentType<{
	css?: string;
	title?: string;
	children?: ReactNode;
	onClick?: (ev: MouseEvent) => void;
}>;
```

#### Styling

- Icon class: `.wx-icon`
- `css` is appended to `.wx-icon`.

```jsx
<Icon css="wxi-search app-icon" title="Search" />
```

```css
.wx-icon.app-icon {
	color: var(--wx-color-primary);
}
```

#### Recipes

##### Clickable Icon

```jsx
import { Icon } from "@svar-ui/react-core";

function Example() {
	return (
		<Icon
			css="wxi-information-outline"
			title="Info"
			onClick={() => console.log("info")}
		/>
	);
}
```

#### Implementation Notes

- The component intentionally uses an `<i>` rather than a button


## File: core/locale.md

> Source: `core/locale.md`

### SVAR React Core Locale

Package: `@svar-ui/react-core`

#### Package

```js
import { Locale, locale, en } from "@svar-ui/react-core";
```

For all bundled language packs, import from `@svar-ui/core-locales`:

```js
import { en, cn, de, es, fr, it, ja, pt, ru } from "@svar-ui/core-locales";
```

#### Supported Functionality

- `Locale` reads React context `context.i18n` (use `useContext(context.i18n)` from `@svar-ui/react-core`).
- If no locale context exists, it creates one from English words.
- If `words` is not `null`, it extends the current locale with `words`.
- `optional` is passed to the locale `extend` call.
- Use `Locale` around the smallest subtree that needs different words or formats.
- Locale affects calendar labels, date/time formats, modal buttons, pager labels, empty-list text, notices/modal helper strings, and color board select text.
- `locale` is re-exported in JS from `@svar-ui/lib-dom`.
- `en` is re-exported in JS from `@svar-ui/core-locales`.

#### Public Types

```ts
import type { FC, ReactNode } from "react";

export declare const Locale: FC<{
	words?: any;
	optional?: boolean;
	children?: ReactNode;
}>;

export type { ILocale, Terms, TPosition } from "@svar-ui/lib-dom";
```

#### Styling

- `Locale` does not render a wrapper element or public classes.
- It only changes locale context for children.
- Styling changes that depend on locale direction or content length must be handled by app CSS or theme variables.

#### Recipes

##### Localize A Calendar Subtree

```jsx
import { Calendar, Locale } from "@svar-ui/react-core";
import { de } from "@svar-ui/core-locales";

function Example() {
	return (
		<Locale words={de}>
			<Calendar value={new Date(2025, 4, 1)} />
		</Locale>
	);
}
```

##### Override Date Formats

```jsx
import { Calendar, Locale } from "@svar-ui/react-core";
import { cn } from "@svar-ui/core-locales";

const words = {
	...cn,
	formats: {
		...cn.formats,
		monthYearFormat: "%Y年%F",
		yearFormat: "%Y年",
	},
};

function Example() {
	return (
		<Locale words={words}>
			<Calendar value={new Date(2025, 4, 1)} />
		</Locale>
	);
}
```

##### Use The Locale Helper Directly

```jsx
import { en, locale } from "@svar-ui/react-core";

function Example() {
	const i18n = locale(en).extend(
		{
			core: {
				"Rows per page": "Rows",
			},
		},
		true
	);
	const _ = i18n.getGroup("core");

	return <span>{_("Rows per page")}</span>;
}
```

##### Read Locale From Context

```jsx
import { useContext } from "react";
import { context } from "@svar-ui/react-core";

function Example() {
	const locale = useContext(context.i18n);
	const _ = locale.getGroup("core");
	return <span>{_("Rows per page")}</span>;
}
```

#### Implementation Notes

- `Locale` renders only `children`; it has no DOM wrapper.

#### Other information

extra details about locales can be obtained from `../locales.md`


## File: core/modal.md

> Source: `core/modal.md`

### SVAR React Core Modal

Package: `@svar-ui/react-core`

#### Package

```js
import { Modal } from "@svar-ui/react-core";
```

#### Supported Functionality

- Fixed-position backdrop and centered window.
- `title` renders the default header unless a `header` render function is supplied.
- `children` renders the modal body.
- `footer` render function replaces the default button row.
- `buttons` defaults to `["cancel", "ok"]`; pass `false` to hide default buttons.
- Button id `"cancel"` calls `onCancel`; every other button id calls `onConfirm`.
- Button labels are localized through locale group `core`.
- Modal focuses itself on mount.
- Enter calls `onConfirm` unless focus is inside a `TEXTAREA` or `BUTTON`; Escape calls `onCancel`.

#### Public Types

```ts
import type { FC, ReactNode } from "react";

export declare const Modal: FC<{
	title?: string;
	buttons?: boolean | string[];
	header?: () => ReactNode;
	footer?: () => ReactNode;
	children?: ReactNode;
	onConfirm?: (ev: { button?: string; event: MouseEvent }) => void;
	onCancel?: (ev: { button?: string; event: MouseEvent }) => void;
}>;
```

#### Styling

- Backdrop: `.wx-modal`
- Window: `.wx-window`
- Header: `.wx-header`
- Button row: `.wx-buttons`
- Button cell: `.wx-button`

```jsx
<Modal title="Confirm">
	<div>Continue?</div>
</Modal>
```

```css
.wx-modal .wx-window {
	--wx-modal-width: 360px;
}
```

#### Recipes

##### Portal Modal With Default Buttons

```jsx
import { useState } from "react";
import { Button, Modal, Portal } from "@svar-ui/react-core";

function Example() {
	const [open, setOpen] = useState(false);

	return (
		<>
			<Button type="primary" onClick={() => setOpen(true)}>Show</Button>

			{open && (
				<Portal>
					<Modal
						title="Confirm"
						onConfirm={() => setOpen(false)}
						onCancel={() => setOpen(false)}
					>
						Continue?
					</Modal>
				</Portal>
			)}
		</>
	);
}
```

##### Custom Header And Footer

```jsx
import { Button, Modal } from "@svar-ui/react-core";

function Example() {
	return (
		<Modal
			buttons={false}
			header={() => <h2>Custom Title</h2>}
			footer={() => <Button type="primary">Apply</Button>}
		>
			<div>Body</div>
		</Modal>
	);
}
```

#### Implementation Notes

- Keyboard Enter/Escape handlers pass a keyboard event, while public types declare `MouseEvent`.
- Button click handlers pass `{ button, event }`.
- Default `"ok"` button is rendered as `type="block primary"`; other default buttons use `type="block secondary"`.


## File: core/modalarea.md

> Source: `core/modalarea.md`

### SVAR React Core ModalArea

Package: `@svar-ui/react-core`

#### Package

```js
import { ModalArea } from "@svar-ui/react-core";
```

#### Supported Functionality

- Local absolute-position modal backdrop and centered window.
- Intended for modal content inside the current layout rather than a viewport-level fixed modal.
- Renders only `children`; it has no built-in header, footer, buttons, or cancel handler.
- Uses a short fade transition.
- Parent layout should provide a positioned containing block when local placement matters.

#### Public Types

```ts
import type { FC, ReactNode } from "react";

export declare const ModalArea: FC<{
	children?: ReactNode;
}>;
```

#### Styling

- Backdrop: `.wx-modal`
- Window: `.wx-window`
- Backdrop is `position: absolute`, fills the containing block, and uses `--wx-modal-backdrop`.
- Window uses modal background, shadow, border, radius, and min width variables.

```jsx
<div className="local-area">
	<ModalArea>
		<div className="inner">Local modal content</div>
	</ModalArea>
</div>
```

```css
.local-area {
	position: relative;
	min-height: 300px;
}
```

#### Recipes

##### Local Modal Overlay

```jsx
import { useState } from "react";
import { Button, ModalArea } from "@svar-ui/react-core";

function Example() {
	const [open, setOpen] = useState(false);

	return (
		<div style={{ position: "relative", minHeight: 300 }}>
			<Button onClick={() => setOpen(true)}>Open local modal</Button>

			{open && (
				<ModalArea>
					<Button onClick={() => setOpen(false)}>Close</Button>
				</ModalArea>
			)}
		</div>
	);
}
```

#### Implementation Notes

- `ModalArea` does not trap focus or handle Escape.
- Use `Modal` when you need built-in title, buttons, confirmation, or cancellation behavior.


## File: core/month.md

> Source: `core/month.md`

### SVAR React Core Month

Package: `@svar-ui/react-core`

#### Package

```js
import { Month } from "@svar-ui/react-core";
```

#### Supported Functionality

- Low-level month grid used by `Calendar` and `RangeCalendar`.
- `current` is the visible month; pass a date inside the month to render.
- `part="normal"` is required for standalone single-date selection with `value={Date}`.
- Range rendering uses `value={{ start, end }}` and `part` values such as `"left"`, `"right"`, or `"both"`.
- `markers(date)` can return a CSS class string appended to `.wx-day`.
- `onChange` receives a `Date` directly, not an object.
- After selecting a date, source calls `onCancel()` if provided.
- Weekday labels and week start come from locale context, falling back to the default locale.

#### Public Types

```ts
import type { FC } from "react";

export declare const Month: FC<{
	value?: { start: Date; end: Date } | Date;
	current?: Date;
	part?: string;
	markers?: (date: Date) => string;
	onCancel?: () => void;
	onChange?: (ev: Date) => void;
}>;
```

#### Styling

- Weekday row: `.wx-weekdays`, `.wx-weekday`
- Day grid: `.wx-days`, `.wx-day`
- Date state classes: `.wx-out`, `.wx-selected`, `.wx-left`, `.wx-right`, `.wx-inrange`, `.wx-weekend`, `.wx-inactive`
- Marker classes from `markers(date)` are appended to `.wx-day`.

```jsx
<Month current={new Date(2025, 4, 1)} part="normal" markers={markers} />
```

```css
.wx-day.payday {
	font-weight: 700;
}
```

#### Recipes

##### Standalone Single-Month Picker

```jsx
import { useState } from "react";
import { Month } from "@svar-ui/react-core";

function Example() {
	const [value, setValue] = useState(new Date(2025, 4, 15));
	const [current, setCurrent] = useState(new Date(2025, 4, 1));

	return (
		<Month
			value={value}
			current={current}
			part="normal"
			onChange={date => setValue(date)}
		/>
	);
}
```

##### Range Markup Preview

```jsx
import { Month } from "@svar-ui/react-core";

const value = {
	start: new Date(2025, 4, 10),
	end: new Date(2025, 4, 18),
};

function Example() {
	return (
		<Month
			value={value}
			current={value.start}
			part="both"
			onChange={date => console.log(date)}
		/>
	);
}
```

#### Implementation Notes

- Source default `part` is `""`; that path treats `value` as a range object. Use `part="normal"` for a plain `Date`.
- Days outside the current month get `.wx-out` and `.wx-inactive`.
- `Month` does not render calendar header or action buttons; use `Calendar` or `RangeCalendar` for those.


## File: core/multicombo.md

> Source: `core/multicombo.md`

### SVAR React Core MultiCombo

Package: `@svar-ui/react-core`

#### Package

```js
import { MultiCombo } from "@svar-ui/react-core";
```

#### Supported Functionality

- Multi-select searchable input backed by `SuggestDropdown`.
- `value` is an array of selected ids; pair with `onChange` to keep state in sync.
- `options` are `{ id, label }` by default.
- `textField` controls display/filter field; default is `"label"`.
- `textOptions` can provide selected tag display objects when visible `options` are partial.
- Typing filters options case-insensitively by `textField`.
- Selected options render as tags with remove icons.
- `checkboxes` shows non-interactive checkboxes in dropdown rows.
- `children` render function receives `{ option }` for both tags and list rows.
- `onChange` emits `{ value }`.

#### Public Types

```ts
import type { FC, ReactNode } from "react";

export interface DropdownOptions {
	inline?: boolean;
	position?: "top" | "right" | "bottom" | "left";
	align?: "start" | "center" | "end";
	css?: string;
	width?: string | "unset" | "auto";
	trackScroll?: boolean;
	virtualized?: boolean;
}

export declare const MultiCombo: FC<{
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
	children?: (ctx: { option: any }) => ReactNode;
	onChange?: (ev: { value: (string | number)[] }) => void;
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

```jsx
<MultiCombo
	options={options}
	value={value}
	onChange={ev => setValue(ev.value)}
	dropdown={{ css: "roles-popup" }}
/>
```

```css
.wx-multicombo .wx-tag {
	max-width: 180px;
}
```

#### Recipes

##### Multi Select With Checkboxes

```jsx
import { useState } from "react";
import { MultiCombo } from "@svar-ui/react-core";

const options = [
	{ id: "editor", label: "Editor" },
	{ id: "owner", label: "Owner" },
	{ id: "viewer", label: "Viewer" },
];

function Example() {
	const [roles, setRoles] = useState(["viewer"]);

	return (
		<MultiCombo
			options={options}
			value={roles}
			onChange={ev => setRoles(ev.value)}
			checkboxes
			placeholder="Select roles"
		/>
	);
}
```

##### Custom Tag And Row Content

```jsx
import { MultiCombo } from "@svar-ui/react-core";

const users = [
	{ id: 104, label: "Lord Varys", email: "little.birds@mail" },
];

function Example() {
	return (
		<MultiCombo options={users} value={[104]}>
			{({ option }) => <strong>{option.label}</strong>}
		</MultiCombo>
	);
}
```

#### Implementation Notes

- Filtering assumes `option[textField]` is a string
- The source `onselect` path ignores falsy ids; avoid empty-string ids for selected options.


## File: core/pager.md

> Source: `core/pager.md`

### SVAR React Core Pager

Package: `@svar-ui/react-core`

#### Package

```js
import { Pager } from "@svar-ui/react-core";
```

#### Supported Functionality

- Pagination control with rows-per-page input, page navigation icons, current page input, and total page count.
- `value` is the current page; default is `1`. Pair with `onChange` to keep state in sync.
- `pageSize` is controlled; default is `20`.
- `pageCount` is `Math.ceil(total / pageSize)`.
- `from` is the zero-based row offset: `(value - 1) * pageSize`.
- `to` is capped by `total`: `Math.min(value * pageSize, total)`.
- Page navigation emits `{ value, from, to }` after updating the bound page.
- Labels come from locale group `core`.

#### Public Types

```ts
import type { FC } from "react";

export declare const Pager: FC<{
	total?: number;
	pageSize?: number;
	value?: number;
	onChange?: (ev: { value: number; from: number; to: number }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-pager`
- Sections: `.wx-left`, `.wx-center`, `.wx-right`
- Navigation icons: `.wx-icon`, icon font classes `wxi-angle-dbl-left`, `wxi-angle-left`, `wxi-angle-right`, `wxi-angle-dbl-right`
- Disabled icons: `.wx-disabled`
- Inputs use local `input` styles inside the component.

```jsx
<div className="grid-footer">
	<Pager total={100} />
</div>
```

```css
.grid-footer .wx-pager {
	justify-content: flex-end;
}
```

#### Recipes

##### Bound Page And Page Size

```jsx
import { useState } from "react";
import { Pager } from "@svar-ui/react-core";

function Example() {
	const [page, setPage] = useState(2);
	const [pageSize, setPageSize] = useState(10);

	return (
		<Pager
			total={100}
			value={page}
			pageSize={pageSize}
			onChange={ev => {
				setPage(ev.value);
				console.log(ev.value, ev.from, ev.to);
			}}
		/>
	);
}
```

#### Implementation Notes

- Page-size input calls `onChange` with `value` equal to the entered page size, not the active page.
- Page navigation calls `onChange` with `value` equal to the active page.
- Current-page input rejects values below `1`, above `pageCount`, or `NaN`.


## File: core/popup.md

> Source: `core/popup.md`

### SVAR React Core Popup

Package: `@svar-ui/react-core`

#### Package

```js
import { Popup } from "@svar-ui/react-core";
```

#### Supported Functionality

- Low-level absolutely positioned popup surface.
- Position is calculated with `calculatePosition` from `@svar-ui/lib-dom`.
- Use `parent` to anchor to an element, or use `left`/`top` with an `at` position.
- `at` defaults to `"bottom"` in source.
- `onCancel` is called by click-outside behavior.
- `width` can be number, "auto" or percentage like `100%` - calculated from `parent.offsetWidth`.
- `trackScroll`; when enabled hides on scroll outside of popup.

#### Public Types

```ts
import { TPosition } from "@svar-ui/lib-dom";
import type { FC, ReactNode } from "react";

export declare const Popup: FC<{
	left?: number;
	top?: number;
	at?: TPosition;
	css: string;
	width: number | string;
	trackScroll: boolean;
	parent?: HTMLElement;
	children?: ReactNode;
	onCancel?: (ev: MouseEvent) => void;
}>;
```

#### Styling

- Container: `.wx-popup`
- Source appends `css` to `.wx-popup`.
- Inline style sets `position:absolute`, calculated `top`, `left`, and `width`.

```jsx
<Popup parent={buttonNode} css="help-popup">
	<div className="body">Help</div>
</Popup>
```

```css
.wx-popup.help-popup {
	padding: 12px;
}
```

#### Recipes

##### Popup Anchored To A Button

```jsx
import { useRef, useState } from "react";
import { Button, Popup } from "@svar-ui/react-core";

function Example() {
	const parentRef = useRef(null);
	const [open, setOpen] = useState(false);

	return (
		<>
			<div ref={parentRef}>
				<Button onClick={() => setOpen(true)}>Anchor</Button>
			</div>

			{open && parentRef.current && (
				<Popup
					parent={parentRef.current}
					at="bottom"
					onCancel={() => setOpen(false)}
				>
					<div style={{ padding: 12 }}>Popup content</div>
				</Popup>
			)}
		</>
	);
}
```

#### Implementation Notes

- Use `Dropdown` for the common anchored dropdown case; it handles `Portal` and parent discovery.


## File: core/portal.md

> Source: `core/portal.md`

### SVAR React Core Portal

Package: `@svar-ui/react-core`

#### Package

```js
import { Portal, popupContainer } from "@svar-ui/react-core";
```

#### Supported Functionality

- `Portal` moves its themed child node to `target` or the nearest `data-wx-portal-root` ancestor.
- If no local portal root exists, source appends to the top node from `@svar-ui/lib-dom` environment.
- `theme` defaults from `context.skin` (read via `useContext(context.skin)` from `@svar-ui/react-core`) when not supplied.
- Children are rendered into the portal target as standard JSX children.
- `popupContainer(node)` marks a local portal root with a generated `data-wx-portal-root` attribute.

#### Public Types

```ts
import type { FC, ReactNode } from "react";

export declare const Portal: FC<{
	theme?: "willow" | "willow-dark";
	target?: HTMLElement;
	children?: ReactNode;
}>;

export declare function popupContainer(node: HTMLElement): void;
```

#### Styling

- Source wrapper `.wx-portal` is `display: none`.
- Moved node receives `.wx-{theme}-theme`, such as `.wx-willow-theme`.
- `popupContainer` has no class; it sets a data attribute.

```jsx
import { useEffect, useRef } from "react";
import { popupContainer } from "@svar-ui/react-core";

function LocalRoot({ children }) {
	const ref = useRef(null);
	useEffect(() => {
		if (ref.current) popupContainer(ref.current);
	}, []);
	return <div ref={ref} className="local-root">{children}</div>;
}
```

#### Recipes

##### Render A Modal Through Portal

```jsx
import { useState } from "react";
import { Button, Modal, Portal } from "@svar-ui/react-core";

function Example() {
	const [open, setOpen] = useState(false);

	return (
		<>
			<Button onClick={() => setOpen(true)}>Open</Button>

			{open && (
				<Portal>
					<Modal title="Portal Modal" onCancel={() => setOpen(false)}>
						Content
					</Modal>
				</Portal>
			)}
		</>
	);
}
```

##### Local Portal Root

```jsx
import { useEffect, useRef } from "react";
import { DatePicker, popupContainer } from "@svar-ui/react-core";

function Example() {
	const ref = useRef(null);
	useEffect(() => {
		if (ref.current) popupContainer(ref.current);
	}, []);

	return (
		<div ref={ref} className="local-root">
			<DatePicker />
		</div>
	);
}
```


## File: core/radio.md

> Source: `core/radio.md`

### SVAR React Core Radio

Package: `@svar-ui/react-core`

Use this file standalone for `RadioButton` and `RadioButtonGroup`.

#### Package

```js
import { RadioButton, RadioButtonGroup } from "@svar-ui/react-core";
```

#### Supported Functionality

- `RadioButton.value` is a controlled boolean checked state.
- `RadioButton.onChange` fires only when the radio becomes checked and emits `{ value: true, inputValue }`.
- Standalone radio buttons need a shared `name` to behave as one browser radio group.
- `RadioButtonGroup.options` are `{ id, label }`.
- `RadioButtonGroup.value` is the selected option id.
- Group `onChange` emits `{ value }`.
- Group `type` supports `inline` and `grid`; default layout is one item per row.

#### Public Types

```ts
import type { ComponentType } from "react";

export declare const RadioButton: ComponentType<{
	id?: string | number;
	label?: string;
	value?: boolean;
	name?: string;
	inputValue?: string | number;
	disabled?: boolean;
	onChange?: (ev: { value: boolean; inputValue: string | number }) => void;
}>;

export declare const RadioButtonGroup: ComponentType<{
	options?: { id: string | number; label: string }[];
	value?: string | number;
	type?: "inline" | "grid";
	onChange?: (ev: { value: string | number }) => void;
}>;
```

#### Styling

- Radio wrapper: `.wx-radio`
- Group wrapper: `.wx-radiogroup`, `.wx-radiogroup.wx-inline`, `.wx-radiogroup.wx-grid`
- Group item wrapper: `.wx-item`

```jsx
<RadioButtonGroup options={options} value={value} onChange={ev => setValue(ev.value)} type="grid" />
```

```css
.wx-radiogroup.wx-grid .wx-item {
	flex-basis: 33.333%;
	max-width: 33.333%;
}
```

#### Recipes

##### Standalone Radio Buttons

```jsx
import { RadioButton } from "@svar-ui/react-core";

function Demo() {
	return (
		<>
			<RadioButton label="One" name="mode" inputValue="one" value={true} />
			<RadioButton label="Two" name="mode" inputValue="two" />
		</>
	);
}
```

##### Radio Group

```jsx
import { useState } from "react";
import { RadioButtonGroup } from "@svar-ui/react-core";

function Demo() {
	const options = [
		{ id: 1, label: "Option 1" },
		{ id: 2, label: "Option 2" },
		{ id: 3, label: "Option 3" },
	];

	const [value, setValue] = useState(1);

	return (
		<RadioButtonGroup
			options={options}
			value={value}
			onChange={ev => setValue(ev.value)}
			type="inline"
		/>
	);
}
```

#### Implementation Notes

- `RadioButtonGroup` does not pass disabled state through option objects.


## File: core/rangecalendar.md

> Source: `core/rangecalendar.md`

### SVAR React Core RangeCalendar

Package: `@svar-ui/react-core`

#### Package

```js
import { RangeCalendar } from "@svar-ui/react-core";
```

#### Supported Functionality

- Date range calendar with controlled `start` and `end`.
- `months` is `1` or `2`; default is `2`.
- Two-month mode renders left and right panels with synchronized months.
- `buttons` defaults to `["clear", "today"]`; arrays can include `"done"`.
- When `buttons` includes `"done"`, selection changes are held until the done action emits the final value.
- Selection order is normalized: selecting an end before the start swaps `start` and `end`.
- `markers(date)` can return a class string appended to `.wx-day`.
- `onChange` receives `{ start: Date | null, end: Date | null }`.

#### Public Types

```ts
import type { ComponentType } from "react";

export declare const RangeCalendar: ComponentType<{
	start?: Date;
	end?: Date;
	current?: Date;
	months?: 1 | 2;
	markers?: (date: Date) => string;
	buttons?: boolean | ("clear" | "today" | "done")[];
	onChange?: (ev: { start: Date | null; end: Date | null }) => void;
}>;
```

#### Styling

- Two-month wrapper: `.wx-rangecalendar`
- Panel wrapper: `.wx-half`
- Calendar panels use `.wx-calendar`, `.wx-wrap`, `.wx-buttons`, `.wx-button-item`
- Month range states: `.wx-selected`, `.wx-left`, `.wx-right`, `.wx-inrange`

```jsx
<div className="range-shell">
	<RangeCalendar months={2} />
</div>
```

```css
.range-shell {
	--wx-calendar-cell-size: 30px;
}
```

#### Recipes

##### Two-Month Range With Done Button

```jsx
import { useState } from "react";
import { RangeCalendar } from "@svar-ui/react-core";

function Demo() {
	const [start, setStart] = useState(new Date(2025, 4, 1));
	const [end, setEnd] = useState(new Date(2025, 4, 7));

	return (
		<RangeCalendar
			start={start}
			end={end}
			months={2}
			buttons={["done", "clear", "today"]}
			onChange={ev => {
				setStart(ev.start);
				setEnd(ev.end);
				console.log(ev.start, ev.end);
			}}
		/>
	);
}
```

##### Single-Month Range

```jsx
import { useState } from "react";
import { RangeCalendar } from "@svar-ui/react-core";

function Demo() {
	const [start, setStart] = useState();
	const [end, setEnd] = useState();

	return (
		<RangeCalendar
			start={start}
			end={end}
			months={1}
			buttons={false}
			onChange={ev => {
				setStart(ev.start);
				setEnd(ev.end);
				console.log(ev.start, ev.end);
			}}
		/>
	);
}
```

#### Implementation Notes

- Source initializes the visible month from `start`, then `current`, then `new Date()`.
- Clearing emits `{ start: null, end: null }`.


## File: core/richselect.md

> Source: `core/richselect.md`

### SVAR React Core RichSelect

Package: `@svar-ui/react-core`

#### Package

```js
import { RichSelect } from "@svar-ui/react-core";
```

#### Supported Functionality

- Non-input single-select control backed by `SuggestDropdown`.
- `value` is the selected id and is controlled.
- `options` are `{ id, label }` by default.
- `textField` controls display field; default is `"label"`.
- `textOptions` can provide selected display objects when visible `options` are partial.
- `clear` shows a close icon when value is set and not disabled.
- `children` render function receives the option object directly for both selected content and list rows.
- `onChange` emits `{ value }`.

#### Public Types

```ts
import type { ComponentType, ReactNode } from "react";

export interface DropdownOptions {
	inline?: boolean;
	position?: "top" | "right" | "bottom" | "left";
	align?: "start" | "center" | "end";
	css?: string;
	width?: string | "unset" | "auto";
	trackScroll?: boolean;
	virtualized?: boolean;
}

export declare const RichSelect: ComponentType<{
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
	children?: (option: any) => ReactNode;
	onChange?: (ev: { value: string | number }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-richselect`
- State classes: `.wx-disabled`, `.wx-error`, `.wx-nowrap`
- Content label: `.wx-label`
- Placeholder: `.wx-placeholder`
- Icon: `.wx-icon`, close icon `.wxi-close`
- Dropdown list hooks: `.wx-list`, `.wx-item`, `.wx-focus`

```jsx
<RichSelect
	options={users}
	value={104}
	dropdown={{ css: "user-select-menu" }}
/>
```

```css
.wx-popup.user-select-menu .wx-item {
	min-height: 40px;
}
```

#### Recipes

##### Rich Select With Custom Template

```jsx
import { RichSelect } from "@svar-ui/react-core";

function Demo() {
	const users = [
		{ id: 104, label: "Lord Varys", email: "little.birds@mail" },
		{ id: 103, label: "Ned Stark", email: "winterhell@mail" },
	];

	return (
		<RichSelect options={users} value={104}>
			{option => (
				<div>
					<strong>{option.label}</strong>
					<span>{option.email}</span>
				</div>
			)}
		</RichSelect>
	);
}
```

##### Hidden Selected Option

```jsx
import { RichSelect } from "@svar-ui/react-core";

function Demo() {
	const allUsers = [
		{ id: 87, label: "Berni Mayou" },
		{ id: 103, label: "Ned Stark" },
	];

	const visibleUsers = [{ id: 103, label: "Ned Stark" }];

	return (
		<RichSelect textOptions={allUsers} options={visibleUsers} value={87} clear />
	);
}
```

#### Implementation Notes

- Without a custom render function, `.wx-nowrap` is added to ellipsize the selected label.


## File: core/segmented.md

> Source: `core/segmented.md`

### SVAR React Core Segmented

Package: `@svar-ui/react-core`

#### Package

```js
import { Segmented } from "@svar-ui/react-core";
```

#### Supported Functionality

- Renders an inline segmented button group.
- `options` are `{ id, label, icon?, title? }`.
- `value` is the selected id and is controlled.
- Clicking an option sets `value = option.id` and emits `onChange({ value })`.
- `css` is appended to `.wx-segmented`.
- Default content renders `option.icon` and `option.label`.
- `children` render function receives `{ option }` for custom option content.

#### Public Types

```ts
import type { ComponentType, ReactNode } from "react";

export declare const Segmented: ComponentType<{
	options?: {
		id: string | number;
		label: string;
		icon?: string;
		title?: string;
	}[];
	value?: string | number;
	css?: string;
	children?: (ctx: { option: any }) => ReactNode;
	onChange?: (ev: { value: string | number }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-segmented`
- Selected button: `.wx-selected`
- Default icon: `.wx-icon`, icon-only modifier `.wx-only`
- Default label: `.wx-label`

```jsx
<Segmented css="view-mode" options={options} value={value} onChange={ev => setValue(ev.value)} />
```

```css
.wx-segmented.view-mode {
	--wx-segmented-padding: 3px;
}
```

#### Recipes

##### Basic Segmented Control

```jsx
import { useState } from "react";
import { Segmented } from "@svar-ui/react-core";

function Demo() {
	const options = [
		{ id: "list", label: "List", icon: "wxi-view-sequential" },
		{ id: "grid", label: "Grid", icon: "wxi-view-grid" },
	];

	const [value, setValue] = useState("list");

	return (
		<Segmented
			options={options}
			value={value}
			onChange={ev => {
				setValue(ev.value);
				console.log(ev.value);
			}}
		/>
	);
}
```

##### Custom Option Content

```jsx
import { Segmented } from "@svar-ui/react-core";

function Demo() {
	const options = [
		{ id: "left", label: "Left", icon: "wxi-align-left" },
		{ id: "right", label: "Right", icon: "wxi-align-right" },
	];

	return (
		<Segmented options={options} value="left">
			{({ option }) => (
				<>
					<i className={option.icon}></i>
					<span>{option.label}</span>
				</>
			)}
		</Segmented>
	);
}
```


## File: core/select.md

> Source: `core/select.md`

### SVAR React Core Select

Package: `@svar-ui/react-core`

#### Package

```js
import { Select } from "@svar-ui/react-core";
```

#### Supported Functionality

- Renders a native `<select>` inside `.wx-select`.
- `options` are `{ id, label }` by default.
- `textField` changes the displayed field; default is `"label"`.
- `value` is controlled and stores the selected option id.
- `placeholder` is shown as an overlay when value is empty and not `0`.
- `clear` shows a close icon when the component has a value and is not disabled.
- `onChange` emits `{ value }`.

#### Public Types

```ts
import type { ComponentType } from "react";

export declare const Select: ComponentType<{
	value?: string | number;
	options?: { id: string | number; label: string }[];
	placeholder?: string;
	title?: string;
	disabled?: boolean;
	error?: boolean;
	textField?: string;
	clear?: boolean;
	id?: string | number;
	onChange?: (ev: { value: string | number }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-select`
- Placeholder overlay: `.wx-placeholder`
- Icon: `.wx-icon`, close icon `.wxi-close`
- Error class is applied to the native `select` as `.wx-error`.

```jsx
<div className="owner-select">
	<Select options={users} value={value} onChange={ev => setValue(ev.value)} clear />
</div>
```

```css
.owner-select .wx-select {
	--wx-input-width: 280px;
}
```

#### Recipes

##### Native Select With Clear

```jsx
import { useState } from "react";
import { Field, Select } from "@svar-ui/react-core";

function Demo() {
	const users = [
		{ id: 103, label: "Ned Stark" },
		{ id: 104, label: "Lord Varys" },
	];

	const [owner, setOwner] = useState("");

	return (
		<Field label="Owner" position="left">
			<Select
				options={users}
				value={owner}
				onChange={ev => setOwner(ev.value)}
				placeholder="Select owner"
				clear
			/>
		</Field>
	);
}
```

#### Implementation Notes

- `Select` has no `css` prop; use a parent/global selector for styling.


## File: core/sidearea.md

> Source: `core/sidearea.md`

### SVAR React Core SideArea

Package: `@svar-ui/react-core`

#### Package

```js
import { SideArea } from "@svar-ui/react-core";
```

#### Supported Functionality

- Absolute-position side panel for local layouts.
- `position` public type supports only `"right"`; source defaults to `"right"`.
- Clicking outside the panel calls `onCancel`.
- Uses a fly transition from the right.
- Renders arbitrary `children`.

#### Public Types

```ts
import type { ComponentType, ReactNode } from "react";

export declare const SideArea: ComponentType<{
	position?: "right";
	children?: ReactNode;
	onCancel?: () => void;
}>;
```

#### Styling

- Panel: `.wx-sidearea`
- Right position: `.wx-pos-right`

```jsx
<div className="side-host">
	<SideArea>
		<div className="side-content">Panel</div>
	</SideArea>
</div>
```

```css
.side-host {
	position: relative;
	min-height: 300px;
}

.side-content {
	width: 400px;
	padding: 20px;
}
```

#### Recipes

##### Right-Side Local Panel

```jsx
import { useState } from "react";
import { Button, SideArea } from "@svar-ui/react-core";

function Demo() {
	const [open, setOpen] = useState(false);

	return (
		<div style={{ position: "relative", minHeight: "300px" }}>
			<Button onClick={() => setOpen(true)}>Open side panel</Button>

			{open && (
				<SideArea onCancel={() => setOpen(false)}>
					<div style={{ width: "400px", padding: "20px" }}>Panel content</div>
				</SideArea>
			)}
		</div>
	);
}
```


## File: core/slider.md

> Source: `core/slider.md`

### SVAR React Core Slider

Package: `@svar-ui/react-core`

#### Package

```js
import { Slider } from "@svar-ui/react-core";
```

#### Supported Functionality

- Renders an input range with optional label.
- Controlled `value`, default `0`.
- `min` defaults to `0`, `max` to `100`, `step` to `1`.
- `width` sets inline width on `.wx-slider`.
- During drag, `onChange` emits `{ value, previous, input: true }`.
- On final change, `onChange` emits `{ value, previous }`.
- `previous` tracks the previous input/final value separately for drag and final changes.

#### Public Types

```ts
import type { ComponentType } from "react";

export declare const Slider: ComponentType<{
	id?: string | number;
	label?: string;
	width?: string;
	min?: number;
	max?: number;
	value?: number;
	step?: number;
	title?: string;
	disabled?: boolean;
	onChange?: (ev: {
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

```jsx
<Slider width="240px" value={value} onChange={ev => setValue(ev.value)} />
```

```css
.wx-slider {
	--wx-slider-thumb-size: 18px;
}
```

#### Recipes

##### Slider With Drag And Final Events

```jsx
import { useState } from "react";
import { Field, Slider } from "@svar-ui/react-core";

function Demo() {
	const [progress, setProgress] = useState(50);

	return (
		<Field label="Progress" position="left" type="slider">
			<Slider
				label={`Progress: ${progress}%`}
				value={progress}
				min={0}
				max={100}
				onChange={ev => {
					setProgress(ev.value);
					if (ev.input) console.log("drag", ev.previous, ev.value);
					else console.log("final", ev.previous, ev.value);
				}}
			/>
		</Field>
	);
}
```


## File: core/suggest-dropdown.md

> Source: `core/suggest-dropdown.md`

### SVAR React Core SuggestDropdown

Package: `@svar-ui/react-core`

#### Package

```js
import { SuggestDropdown } from "@svar-ui/react-core";
```

#### Supported Functionality

- Low-level dropdown list helper used by `Combo`, `MultiCombo`, and `RichSelect`.
- Renders only when navigation index is not `null`; callers open it through `onReady.navigate`.
- `items` are `{ id, label }`.
- `onReady` receives navigation helpers: `navigate`, `keydown`, and `move`.
- `onSelect` emits `{ id }`; in multiselect mode `id` is the next selected id array.
- `multiselect` toggles id arrays instead of a single id.
- `checkboxes` renders a non-interactive `Checkbox` in each row.
- `virtualized` renders only visible rows with fixed measured item height and overscan.
- `children` render function receives `{ option }`.

#### Public Types

```ts
import type { ComponentType, ReactNode } from "react";

export interface DropdownOptions {
	inline?: boolean;
	position?: "top" | "right" | "bottom" | "left";
	align?: "start" | "center" | "end";
	css?: string;
	width?: string | "unset" | "auto";
	trackScroll?: boolean;
	virtualized?: boolean;
}

export declare const SuggestDropdown: ComponentType<
	DropdownOptions & {
		items?: { id: string | number; label: string }[];
		children?: (ctx: { option: any }) => ReactNode;
		onSelect?: (ev: { id: string | number | (string | number)[] }) => void;
		onReady?: (ev: {
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

```jsx
<SuggestDropdown items={items} css="suggest-menu" />
```

```css
.wx-popup.suggest-menu .wx-list {
	max-height: 180px;
}
```

#### Recipes

##### Controlled Suggest Dropdown

```jsx
import { useRef } from "react";
import { SuggestDropdown } from "@svar-ui/react-core";

function Demo() {
	const items = [
		{ id: 1, label: "One" },
		{ id: 2, label: "Two" },
	];

	const apiRef = useRef(null);

	return (
		<>
			<button onClick={() => apiRef.current?.navigate(0)}>Open</button>

			<SuggestDropdown
				items={items}
				onReady={ev => (apiRef.current = ev)}
				onSelect={ev => console.log(ev.id)}
			/>
		</>
	);
}
```

#### Implementation Notes

- Keyboard handlers use `ev.code` values `Enter`, `Space`, `Escape`, `Tab`, `ArrowDown`, and `ArrowUp`.
- Virtual mode measures the first rendered item and assumes all rows have that height.


## File: core/switch.md

> Source: `core/switch.md`

### SVAR React Core Switch

Package: `@svar-ui/react-core`

#### Package

```js
import { Switch } from "@svar-ui/react-core";
```

#### Supported Functionality

- Renders a labeled checkbox styled as a switch.
- `value` is a controlled boolean.
- `disabled` is forwarded to the hidden checkbox input.
- `onChange` emits `{ value }` after the checked state changes.
- `id` is used through the shared input id helper, so it can connect with a surrounding `Field`.

#### Public Types

```ts
import type { ComponentType } from "react";

export declare const Switch: ComponentType<{
	id?: string | number;
	value?: boolean;
	disabled?: boolean;
	onChange?: (ev: { value: boolean }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-switch`
- Internal elements are an invisible checkbox input and a visual `span`.

```jsx
<Switch value={value} onChange={ev => setValue(ev.value)} />
```

```css
.wx-switch {
	--wx-switch-width: 56px;
}
```

#### Recipes

##### Bound Switch In A Field

```jsx
import { useState } from "react";
import { Field, Switch } from "@svar-ui/react-core";

function Demo() {
	const [enabled, setEnabled] = useState(true);

	return (
		<Field label={`Enabled: ${enabled}`} position="left" type="switch">
			<Switch
				value={enabled}
				onChange={ev => {
					setEnabled(ev.value);
					console.log(ev.value);
				}}
			/>
		</Field>
	);
}
```

#### Implementation Notes

- The component does not expose `css`; style through parent/global selectors or theme variables.


## File: core/tabs.md

> Source: `core/tabs.md`

### SVAR React Core Tabs

Package: `@svar-ui/react-core`

#### Package

```js
import { Tabs } from "@svar-ui/react-core";
```

#### Supported Functionality

- Renders a tab strip only; render the tab panel yourself based on `value`.
- `options` are `{ id, label?, title?, icon? }`.
- `value` is the active tab id and is controlled.
- Clicking a tab sets `value = option.id` and emits `onChange({ value })`.
- `type` is `top` or `bottom`; default is `top`.
- Icons use the same icon class pattern as other core controls.

#### Public Types

```ts
import type { ComponentType } from "react";

export declare const Tabs: ComponentType<{
	options?: {
		id: string | number;
		label?: string;
		title?: string;
		icon?: string;
	}[];
	value?: string | number;
	type?: "top" | "bottom";
	onChange?: (ev: { value: string | number }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-tabs`, plus `.wx-top` or `.wx-bottom`
- Active button: `.wx-active`
- Default icon: `.wx-icon`, icon-only modifier `.wx-only`
- Default label: `.wx-label`

```jsx
<Tabs options={tabs} value={active} onChange={ev => setActive(ev.value)} />
```

```css
.wx-tabs {
	--wx-tabs-cell-min-width: 80px;
}
```

#### Recipes

##### Tabs With Panels

```jsx
import { useState } from "react";
import { Tabs } from "@svar-ui/react-core";

function Demo() {
	const tabs = [
		{ id: "info", label: "Info", icon: "wxi-alert" },
		{ id: "audit", label: "Audit" },
		{ id: "done", icon: "wxi-check", title: "Done" },
	];

	const [active, setActive] = useState("info");

	return (
		<>
			<Tabs options={tabs} value={active} onChange={ev => setActive(ev.value)} />

			{active === "info" ? (
				<div>Info panel</div>
			) : active === "audit" ? (
				<div>Audit panel</div>
			) : (
				<div>Done panel</div>
			)}

			<Tabs options={tabs} value={active} onChange={ev => setActive(ev.value)} type="bottom" />
		</>
	);
}
```

#### Implementation Notes

- `Tabs` has no `css` prop; style with an enclosing parent/global selector or theme variables.


## File: core/text.md

> Source: `core/text.md`

### SVAR React Core Text

Package: `@svar-ui/react-core`

#### Package

```js
import { Text } from "@svar-ui/react-core";
```

#### Supported Functionality

- Controlled `value`, with `string | number` public type.
- `type` supports `text`, `number`, and `password`; default is `text`.
- `onChange` fires `{ value, input: true }` on input and `{ value }` on native change.
- `focus` and `select` focus/select the input after mount.
- `clear` shows a close icon when the input has a value; clicking it sets `value = ""` and emits `{ value }`.
- `icon` renders inside the input. It is right-aligned unless `css` includes `wx-icon-left`.
- `inputStyle` is applied to the inner `<input>`.
- `readonly`, `disabled`, `error`, `placeholder`, and `title` are forwarded to the input/wrapper.

#### Public Types

```ts
import type { ComponentType } from "react";

export declare const Text: ComponentType<{
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
	onChange?: (ev: { value: string | number; input?: boolean }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-text`
- State/classes: `.wx-error`, `.wx-disabled`, `.wx-clear`, `.wx-icon-left`, `.wx-icon-right`
- Icon: `.wx-icon`; clear icon: `.wx-icon.wxi-close`
- `css` is appended to `.wx-text`.

```jsx
<Text css="search-input wx-icon-left" icon="wxi-search" clear />
```

```css
.wx-text.search-input {
	--wx-input-width: 320px;
}
```

#### Recipes

##### Text With Clear And Left Icon

```jsx
import { useState } from "react";
import { Field, Text } from "@svar-ui/react-core";

function Demo() {
	const [query, setQuery] = useState("");

	return (
		<Field label="Search" position="left">
			<Text
				value={query}
				onChange={ev => {
					setQuery(ev.value);
					if (!ev.input) console.log("final", ev.value);
				}}
				placeholder="Type here"
				icon="wxi-search"
				css="wx-icon-left"
				clear
			/>
		</Field>
	);
}
```

##### Focus And Select On Mount

```jsx
import { Text } from "@svar-ui/react-core";

function Demo() {
	return <Text value="Some value" focus select />;
}
```

#### Implementation Notes

- `type="number"` still binds through the input value; account for string/number conversion in your app logic.


## File: core/textarea.md

> Source: `core/textarea.md`

### SVAR React Core TextArea

Package: `@svar-ui/react-core`

#### Package

```js
import { TextArea } from "@svar-ui/react-core";
```

#### Supported Functionality

- Renders a native `<textarea class="wx-textarea">`.
- `value` is controlled.
- `onChange` fires `{ value, input: true }` on input and `{ value }` on native change.
- Supports `id`, `placeholder`, `title`, `disabled`, `error`, and `readonly`.
- The textarea is vertically resizable unless disabled.

#### Public Types

```ts
import type { ComponentType } from "react";

export declare const TextArea: ComponentType<{
	value?: string;
	id?: string | number;
	placeholder?: string;
	title?: string;
	disabled?: boolean;
	error?: boolean;
	readonly?: boolean;
	onChange?: (ev: { value: string; input?: boolean }) => void;
}>;
```

#### Styling

- Textarea: `.wx-textarea`
- Error state: `.wx-textarea.wx-error`
- Disabled state uses `[disabled]`.

```jsx
<TextArea placeholder="Details" />
```

```css
.wx-textarea {
	min-height: 140px;
}
```

#### Recipes

##### TextArea In A Field

```jsx
import { useState } from "react";
import { Field, TextArea } from "@svar-ui/react-core";

function Demo() {
	const [details, setDetails] = useState("");

	return (
		<Field label="Details" error>
			<TextArea
				value={details}
				onChange={ev => setDetails(ev.value)}
				error
				title="Details are required"
				placeholder="Type here"
			/>
		</Field>
	);
}
```

#### Implementation Notes

- There is no `css` prop; style through a parent/global selector or theme variables.


## File: core/themes.md

> Source: `core/themes.md`

### SVAR React Core Themes

Package: `@svar-ui/react-core`

#### Package

```js
import { Willow, WillowDark } from "@svar-ui/react-core";
```

#### Supported Functionality

- Theme components provide React context `wx-theme`.
- `Willow` sets `wx-theme` to `"willow"`.
- `WillowDark` sets `wx-theme` to `"willow-dark"`.
- When `children` are supplied, each theme renders `.wx-theme.wx-*-theme` with `height:100%`.
- `fonts` defaults to `true`.
- `Willow` and `WillowDark` load Open Sans font files and the `wxi` icon CSS.
- Use `fonts={false}` when fonts/icons are already loaded or the app manages font loading.
- Theme styling is CSS-variable driven; override variables on the theme wrapper or an ancestor around specific controls.

#### Public Types

```ts
import type { ComponentType, ReactNode } from "react";

export declare const Willow: ComponentType<{
	fonts?: boolean;
	children?: ReactNode;
}>;

export declare const WillowDark: ComponentType<{
	fonts?: boolean;
	children?: ReactNode;
}>;
```

#### Styling


```jsx
<Willow fonts={false}>
	<div className="app-theme">
		<App />
	</div>
</Willow>
```

```css
.app-theme {
	--wx-color-primary: #0f766e;
	--wx-input-width: 280px;
	--wx-button-border-radius: 4px;
	--wx-calendar-cell-size: 30px;
}
```

#### Recipes

##### Wrap An App In A Theme

```jsx
import { Willow } from "@svar-ui/react-core";
import AppRoutes from "./AppRoutes.jsx";

function Demo() {
	return (
		<Willow>
			<AppRoutes />
		</Willow>
	);
}
```

##### Dark Theme Without CDN Font Injection

```jsx
import { WillowDark } from "@svar-ui/react-core";

function Demo() {
	return (
		<WillowDark fonts={false}>
			<div className="screen">Dark UI</div>
		</WillowDark>
	);
}
```

#### Other information

extra details about themes can be obtained from `../themes.md`


## File: core/timepicker.md

> Source: `core/timepicker.md`

### SVAR React Core TimePicker

Package: `@svar-ui/react-core`

#### Package

```js
import { TimePicker } from "@svar-ui/react-core";
```

#### Supported Functionality

- Input-like time picker backed by `Text`, `Dropdown`, `Slider`, and optional `TwoState`.
- `value` is controlled and is a `Date`; only hours and minutes are used.
- Default value is `new Date(0, 0, 0, 0, 0)` when `value` is nullish.
- `format` can be a time format string or `(value: Date) => string`; locale time format is used by default.
- Locale `calendar.clockFormat == 12` enables the AM/PM `TwoState`.
- Hour and minute text inputs update on blur.
- Hour and minute sliders update through `Slider.onChange`.
- `dropdown` is forwarded to `Dropdown`; date/time dropdowns default width to `"unset"` when no width is provided.
- `onChange` receives `{ value: Date }` after assigning the new value.

#### Public Types

```ts
import type { ComponentType } from "react";

export interface DropdownOptions {
	inline?: boolean;
	position?: "top" | "right" | "bottom" | "left";
	align?: "start" | "center" | "end";
	css?: string;
	width?: string | "unset" | "auto";
	trackScroll?: boolean;
	virtualized?: boolean;
}

export declare const TimePicker: ComponentType<{
	value?: Date;
	id?: string | number;
	title?: string;
	css?: string;
	disabled?: boolean;
	error?: boolean;
	format?: string | ((value: Date) => string);
	dropdown?: DropdownOptions;
	onChange?: (ev: { value: Date }) => void;
}>;
```

#### Styling

- Wrapper: `.wx-timepicker`
- State classes: `.wx-disabled`, `.wx-error`
- `css` is passed to the inner `Text`.
- Popup content: `.wx-wrapper`, `.wx-timer`, `.wx-digit`, `.wx-separator`
- Slider rows use `Field` and `Slider` classes.
- AM/PM toggle uses `TwoState`/`Button` classes.

```jsx
<TimePicker css="time-input" dropdown={{ css: "time-popup", width: "260px" }} />
```

```css
.wx-text.time-input {
	--wx-input-width: 180px;
}
```

#### Recipes

##### Bound Time

```jsx
import { useState } from "react";
import { Field, TimePicker } from "@svar-ui/react-core";

function Demo() {
	const [value, setValue] = useState(new Date(0, 0, 0, 14, 30));

	return (
		<Field label="Time" position="left">
			<TimePicker
				value={value}
				onChange={ev => {
					setValue(ev.value);
					console.log(ev.value);
				}}
			/>
		</Field>
	);
}
```

##### Twelve-Hour Locale

```jsx
import { useState } from "react";
import { Field, Locale, TimePicker } from "@svar-ui/react-core";

function Demo() {
	const [value, setValue] = useState(new Date(0, 0, 0, 14, 30));

	return (
		<Locale
			words={{
				formats: { timeFormat: "%g:%i %a" },
				calendar: { clockFormat: 12 },
			}}
		>
			<Field label="Time" position="left">
				<TimePicker
					value={value}
					onChange={ev => setValue(ev.value)}
					dropdown={{ width: "100%" }}
				/>
			</Field>
		</Locale>
	);
}
```

#### Implementation Notes

- The visible text is readonly; typed hour/minute edits happen only inside the popup.


## File: core/twostate.md

> Source: `core/twostate.md`

### SVAR React Core TwoState

Package: `@svar-ui/react-core`

#### Package

```js
import { TwoState } from "@svar-ui/react-core";
```

#### Supported Functionality

- Wraps `Button` and toggles controlled boolean `value`.
- When active, adds `pressed` to the forwarded `type`.
- `textActive` and `iconActive` replace `text` and `icon` while active.
- `children` renders inactive/default content; `active` render function prop renders active content when `value` is true.
- Click order: `onClick(ev)` first, then value toggle and `onChange({ value })`.
- Calling `ev.preventDefault()` inside `onClick` prevents the toggle and `onChange`.

#### Public Types

```ts
import type { ComponentType, ReactNode } from "react";

export declare const TwoState: ComponentType<{
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
	active?: () => ReactNode;
	children?: ReactNode;
	onClick?: (ev: MouseEvent) => void;
	onChange?: (ev: { value: boolean }) => void;
}>;
```

#### Styling

- Uses `Button`, so styling hooks are `.wx-button` plus `.wx-pressed` when active.
- `css` is passed to the inner `Button`.
- Button type variables such as `--wx-button-pressed`, `--wx-button-primary-pressed`, and `--wx-button-box-shadow` control active state.

```jsx
<TwoState css="favorite-button" icon="wxi-star" iconActive="wxi-check" />
```

```css
.wx-button.favorite-button.wx-pressed {
	font-weight: 700;
}
```

#### Recipes

##### Toggle With Active Content

```jsx
import { useState } from "react";
import { TwoState } from "@svar-ui/react-core";

function Demo() {
	const [active, setActive] = useState(false);

	return (
		<TwoState
			value={active}
			onChange={ev => {
				setActive(ev.value);
				console.log(ev.value);
			}}
			type="primary"
			icon="wxi-star"
			iconActive="wxi-check"
			active={() => "Favorited"}
		>
			Favorite
		</TwoState>
	);
}
```

##### Prevent Toggle

```jsx
import { TwoState } from "@svar-ui/react-core";

function Demo() {
	function beforeToggle(ev) {
		if (!confirm("Toggle?")) ev.preventDefault();
	}

	return <TwoState onClick={beforeToggle}>Toggle</TwoState>;
}
```

#### Implementation Notes

- The active render function is invoked only when `value` is true.
- If `active` is not supplied, the component reuses `children` or `text` with active icon/text substitutions.


## File: locales.md

> Source: `locales.md`

i18n patterns common to all SVAR React components - Locale wrapper, bundled language packs, extending words and formats

### Localizing SVAR React Components

All `@svar-ui/react-*` widgets read locale data from a single React context (`wx-i18n`). The mechanics live in `@svar-ui/react-core`; every other package consumes them.

#### Locale Wrapper

Wrap the subtree you want to localize. With no wrapper, widgets fall back to English.

```jsx
import { Calendar, Locale } from "@svar-ui/react-core";
import { de } from "@svar-ui/core-locales";

function App() {
    return (
        <Locale words={de}>
            <Calendar value={new Date(2025, 4, 1)} />
        </Locale>
    );
}
```

Wrap the smallest subtree that needs the alternative locale - nested `Locale` blocks let different parts of the app render in different languages.

`Locale` does not render any DOM wrapper; it only mutates context, so it never affects layout.

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

If you see English fallbacks in a localized UI, the missing terms come from the package's own locale module - merge them in via `Locale words={...}`.

To localize a standalone widget, merge the matching package locale with the core locale:

```jsx
import { Gantt } from "@svar-ui/react-gantt";
import { Locale } from "@svar-ui/react-core";
import { cn } from "@svar-ui/gantt-locales";
import { cn as cnCore } from "@svar-ui/core-locales";

function App() {
    return (
        <Locale words={{ ...cn, ...cnCore }}>
            <Gantt {...settings} />
        </Locale>
    );
}
```

#### Extending Or Overriding Words

`Locale words` accepts a partial pack and extends the current context. Spread an existing pack to keep its formats and override only what you need:

```jsx
import { Calendar, Locale } from "@svar-ui/react-core";
import { cn } from "@svar-ui/core-locales";

function App() {
    const words = {
        ...cn,
        formats: {
            ...cn.formats,
            monthYearFormat: "%Y年%F",
            yearFormat: "%Y年",
        },
    };

    return (
        <Locale words={words}>
            <Calendar value={new Date(2025, 4, 1)} />
        </Locale>
    );
}
```

Pass `optional={true}` to make merged terms additive fallbacks rather than overrides - useful for layering app-specific strings on top of a full pack.

#### Affected Surfaces

Locale changes calendar labels, date/time formats, modal buttons, pager strings, empty-list text, notice/modal helpers, color-board select text - any widget that displays static strings or formats values reads them through this context.

#### Direct Helper

For non-component code, use the `locale` helper to build a translator:

```js
import { en, locale } from "@svar-ui/react-core";

const i18n = locale(en).extend(
    { core: { "Rows per page": "Rows" } },
    true
);
const _ = i18n.getGroup("core");
_("Rows per page"); // "Rows"
```


## File: themes.md

> Source: `themes.md`

### Styling SVAR React Components

All `@svar-ui/react-*` widgets share the same theming pipeline. The mechanics live in `@svar-ui/react-core`; every other package consumes them.

#### Per widget css files

Each package ships `style.css` (this component only) and `all.css` (this component plus all dependencies).

```css
@import "@svar-ui/react-gantt/style.css";
```

#### Theme Wrapper

Wrap the part of the app that uses SVAR widgets in a theme component from `@svar-ui/react-core`:

```jsx
import { Willow } from "@svar-ui/react-core";

function Root() {
    return (
        <Willow>
            <App />
        </Willow>
    );
}
```

Available themes: `Willow`, `WillowDark`. The wrapper:

- sets the React context `wx-theme`
- renders `.wx-theme.wx-{name}-theme` with `height:100%`
- loads Open Sans + the `wxi` icon CSS by default; pass `fonts={false}` to skip when the host app manages fonts itself

Without a theme wrapper widgets still render but lose theme variables and font/icon CSS.

#### Per-widget Willow / WillowDark themes

Several widgets ship their **own** `Willow` / `WillowDark` components on top of the core base. The widget version wraps the core theme and layers in widget-specific CSS variables (bar colors, grid borders, timescale fonts, etc.). When using such a widget, import the theme from the widget package - not from core - so both layers apply.

Widgets that expose custom `Willow` / `WillowDark` themes:

- `@svar-ui/react-core` - base
- `@svar-ui/react-gantt`
- `@svar-ui/react-grid`
- `@svar-ui/react-editor`
- `@svar-ui/react-filter`
- `@svar-ui/react-filemanager`
- `@svar-ui/react-comments`
- `@svar-ui/react-kanban`

The widget theme delegates to core and adds extra rules scoped to `.wx-willow-theme` (or `.wx-willow-dark-theme`):

```jsx
import "./WidgetTheme.css";
import { Willow } from "@svar-ui/react-core";

function WidgetTheme({ fonts = true, children }) {
    return children
        ? <Willow fonts={fonts}>{children}</Willow>
        : <Willow fonts={fonts} />;
}

/* WidgetTheme.css
.wx-willow-theme {
    --wx-gantt-border-color: #e6e6e6;
    --wx-gantt-task-color: #3983eb;
    /* ...widget-specific overrides... *\/
}
*/
```

Mount the widget's own theme once at the app root. The wrapper internally renders the core `Willow`, so a separate core import is not needed:

```jsx
import { Willow, Gantt } from "@svar-ui/react-gantt";

function App() {
    return (
        <>
            <Willow />
            <Gantt {...settings} />
        </>
    );
}
```

#### CSS Variables

Theme styling is variable-driven. Override variables on the theme wrapper or on any ancestor of the widgets you want to restyle - overrides cascade to every SVAR widget in the subtree.

```jsx
import "./Brand.css";

<Willow>
    <div className="brand">
        <App />
    </div>
</Willow>

/* Brand.css
.brand {
    --wx-color-primary: #0f766e;
    --wx-input-width: 280px;
    --wx-button-border-radius: 4px;
    --wx-calendar-cell-size: 30px;
}
*/
```

Nest different wrapper blocks for per-section restyling without forking the theme.

#### `css` Prop Convention

Most widgets accept a `css` prop. The string is appended to the widget's root class, so it works as a parent styling hook:

```jsx
<Toolbar css="my-toolbar" items={items} />

/* CSS
.my-toolbar {
    padding: 8px 12px;
}
*/
```

Composite widgets often expose secondary css props for nested popups (`menuCss` on `Toolbar`/`MenuBar`, etc.). Check the per-component file for the exact set.

#### Class Hooks

The per-component file lists the exact selectors that widget exposes.

#### Custom CSS class overrides

When writing custom rules to override widget styles, always use **at least two selectors** (e.g. `.a .b {}`). Component styles in the bundled SVAR widgets carry higher specificity than a plain `.b`. A two-selector rule (`.a .b`) matches or beats that specificity and wins.

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
