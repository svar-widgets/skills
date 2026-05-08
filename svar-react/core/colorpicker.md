# SVAR React Core ColorPicker

Package: `@svar-ui/react-core`

## Package

```js
import { ColorPicker } from "@svar-ui/react-core";
```

## Supported Functionality

- Input-like color picker that opens `ColorBoard` in a `Dropdown`.
- `value` is a controlled color string.
- The inner `ColorBoard` is rendered with `button="true"`.
- `ColorPicker` ignores `ColorBoard` input events and updates only on the final select event.
- Final selection closes the popup and emits `{ value }`.
- `clear` shows a close icon when value is set and not disabled.
- `dropdown` is forwarded to `Dropdown`.

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

## Styling

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

## Recipes

### Color Picker In A Field

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

## Implementation Notes

- `ColorPicker` displays the current `value` as swatch background without validating it.
