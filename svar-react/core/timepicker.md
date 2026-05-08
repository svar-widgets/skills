# SVAR React Core TimePicker

Package: `@svar-ui/react-core`

## Package

```js
import { TimePicker } from "@svar-ui/react-core";
```

## Supported Functionality

- Input-like time picker backed by `Text`, `Dropdown`, `Slider`, and optional `TwoState`.
- `value` is controlled and is a `Date`; only hours and minutes are used.
- Default value is `new Date(0, 0, 0, 0, 0)` when `value` is nullish.
- `format` can be a time format string or `(value: Date) => string`; locale time format is used by default.
- Locale `calendar.clockFormat == 12` enables the AM/PM `TwoState`.
- Hour and minute text inputs update on blur.
- Hour and minute sliders update through `Slider.onChange`.
- `dropdown` is forwarded to `Dropdown`; date/time dropdowns default width to `"unset"` when no width is provided.
- `onChange` receives `{ value: Date }` after assigning the new value.

## Public Types

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

## Styling

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

## Recipes

### Bound Time

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

### Twelve-Hour Locale

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

## Implementation Notes

- The visible text is readonly; typed hour/minute edits happen only inside the popup.
