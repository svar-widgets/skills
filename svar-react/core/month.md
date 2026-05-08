# SVAR React Core Month

Package: `@svar-ui/react-core`

## Package

```js
import { Month } from "@svar-ui/react-core";
```

## Supported Functionality

- Low-level month grid used by `Calendar` and `RangeCalendar`.
- `current` is the visible month; pass a date inside the month to render.
- `part="normal"` is required for standalone single-date selection with `value={Date}`.
- Range rendering uses `value={{ start, end }}` and `part` values such as `"left"`, `"right"`, or `"both"`.
- `markers(date)` can return a CSS class string appended to `.wx-day`.
- `onChange` receives a `Date` directly, not an object.
- After selecting a date, source calls `onCancel()` if provided.
- Weekday labels and week start come from locale context, falling back to the default locale.

## Public Types

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

## Styling

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

## Recipes

### Standalone Single-Month Picker

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

### Range Markup Preview

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

## Implementation Notes

- Source default `part` is `""`; that path treats `value` as a range object. Use `part="normal"` for a plain `Date`.
- Days outside the current month get `.wx-out` and `.wx-inactive`.
- `Month` does not render calendar header or action buttons; use `Calendar` or `RangeCalendar` for those.
