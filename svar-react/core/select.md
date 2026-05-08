# SVAR React Core Select

Package: `@svar-ui/react-core`

## Package

```js
import { Select } from "@svar-ui/react-core";
```

## Supported Functionality

- Renders a native `<select>` inside `.wx-select`.
- `options` are `{ id, label }` by default.
- `textField` changes the displayed field; default is `"label"`.
- `value` is controlled and stores the selected option id.
- `placeholder` is shown as an overlay when value is empty and not `0`.
- `clear` shows a close icon when the component has a value and is not disabled.
- `onChange` emits `{ value }`.

## Public Types

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

## Styling

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

## Recipes

### Native Select With Clear

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

## Implementation Notes

- `Select` has no `css` prop; use a parent/global selector for styling.
