# SVAR React Core ColorSelect

Package: `@svar-ui/react-core`

## Package

```js
import { ColorSelect } from "@svar-ui/react-core";
```

## Supported Functionality

- Input-like color palette selector.
- `value` is a controlled hex color string or empty string.
- Default colors are `#00a037`, `#37a9ef`, `#f5a623`, `#ff4c3b`, `#a0a0a0`, `#000000`, `#ffffff`.
- Clicking the input opens a `Dropdown` unless disabled.
- Palette includes an empty color item that selects `""`.
- `clear` shows a close icon when value is set and not disabled.
- `onChange` emits `{ value }`.

## Public Types

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

## Styling

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

## Recipes

### Custom Palette

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
