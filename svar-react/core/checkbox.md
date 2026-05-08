# SVAR React Core Checkbox

Package: `@svar-ui/react-core`

Use this file standalone for `Checkbox` and `CheckboxGroup`.

## Package

```js
import { Checkbox, CheckboxGroup } from "@svar-ui/react-core";
```

## Supported Functionality

- `Checkbox.value` is a controlled boolean.
- `Checkbox.inputValue` is emitted alongside the checked state; default is an empty string.
- `Checkbox.onChange` emits `{ value, inputValue }`.
- `CheckboxGroup.options` are `{ id, label }`.
- `CheckboxGroup.value` is a controlled array of selected option ids.
- Group `onChange` emits `{ value }`.
- Group `type` supports `inline` and `grid`; default layout is one item per row.

## Public Types

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

## Styling

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

## Recipes

### Single Checkbox

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

### Checkbox Group

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

## Implementation Notes

- `CheckboxGroup` does not pass disabled state through option objects.
