# SVAR React Core Calendar

Package: `@svar-ui/react-core`

## Package

```js
import { Calendar } from "@svar-ui/react-core";
```

## Supported Functionality

- Full single-date calendar with header navigation and optional action buttons.
- `value` is controlled and is a `Date` or `null`.
- `current` is controlled and controls the visible month; source normalizes it to the first day of that month.
- `buttons` defaults to `["clear", "today"]`; pass `false` to hide buttons or `true` for the default set.
- `markers(date)` can return a CSS class string appended to the matching `.wx-day`.
- `onChange` receives `{ value: Date | null }`.
- Internally wraps the calendar panel in `Locale`, so it can work without an outer locale provider.

## Public Types

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

## Styling

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

## Recipes

### Mark Dates And Keep Visible Month Bound

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

### Hide Action Buttons

```jsx
import { Calendar } from "@svar-ui/react-core";

function Demo() {
	return (
		<Calendar buttons={false} onChange={ev => console.log(ev.value)} />
	);
}
```

## Implementation Notes

- Selecting a date clones it with `new Date(...)` before assigning `value`.
- Clearing sets `value` to `null`.
- Source calls `onChange` after updating the value.
