# SVAR React Core Radio

Package: `@svar-ui/react-core`

Use this file standalone for `RadioButton` and `RadioButtonGroup`.

## Package

```js
import { RadioButton, RadioButtonGroup } from "@svar-ui/react-core";
```

## Supported Functionality

- `RadioButton.value` is a controlled boolean checked state.
- `RadioButton.onChange` fires only when the radio becomes checked and emits `{ value: true, inputValue }`.
- Standalone radio buttons need a shared `name` to behave as one browser radio group.
- `RadioButtonGroup.options` are `{ id, label }`.
- `RadioButtonGroup.value` is the selected option id.
- Group `onChange` emits `{ value }`.
- Group `type` supports `inline` and `grid`; default layout is one item per row.

## Public Types

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

## Styling

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

## Recipes

### Standalone Radio Buttons

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

### Radio Group

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

## Implementation Notes

- `RadioButtonGroup` does not pass disabled state through option objects.
