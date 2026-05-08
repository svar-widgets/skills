# SVAR React Core Counter

Package: `@svar-ui/react-core`

## Package

```js
import { Counter } from "@svar-ui/react-core";
```

## Supported Functionality

- Numeric input with decrement and increment buttons.
- Controlled `value`, default `0`.
- `step` defaults to `1`, `min` defaults to `0`, `max` defaults to `Infinity`.
- Button clicks update `value` and emit `{ value }`.
- Typing emits `{ value, input: true }` without immediately mutating the bound value in the handler payload path.
- Blur normalizes the bound value to min/max and step, then emits `{ value }`.
- `readonly` blocks button changes and blur normalization.
- `disabled` disables the input and both buttons.

## Public Types

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

## Styling

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

## Recipes

### Counter With Final Change Handling

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
