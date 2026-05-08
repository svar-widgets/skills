# SVAR React Core RangeCalendar

Package: `@svar-ui/react-core`

## Package

```js
import { RangeCalendar } from "@svar-ui/react-core";
```

## Supported Functionality

- Date range calendar with controlled `start` and `end`.
- `months` is `1` or `2`; default is `2`.
- Two-month mode renders left and right panels with synchronized months.
- `buttons` defaults to `["clear", "today"]`; arrays can include `"done"`.
- When `buttons` includes `"done"`, selection changes are held until the done action emits the final value.
- Selection order is normalized: selecting an end before the start swaps `start` and `end`.
- `markers(date)` can return a class string appended to `.wx-day`.
- `onChange` receives `{ start: Date | null, end: Date | null }`.

## Public Types

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

## Styling

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

## Recipes

### Two-Month Range With Done Button

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

### Single-Month Range

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

## Implementation Notes

- Source initializes the visible month from `start`, then `current`, then `new Date()`.
- Clearing emits `{ start: null, end: null }`.
