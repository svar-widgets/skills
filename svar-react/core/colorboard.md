# SVAR React Core ColorBoard

Package: `@svar-ui/react-core`

## Package

```js
import { ColorBoard } from "@svar-ui/react-core";
```

## Supported Functionality

- HSV color board with hue line, saturation/value block, text input, preview, and optional select button.
- `value` is controlled and defaults to `"#65D3B3"`.
- Valid typed hex is normalized to uppercase `#RRGGBB`; 3-digit hex is expanded.
- Moving sliders or typing a valid color emits `{ value, input: true }`.
- With `button={true}`, clicking the select button emits a final `{ value }`.
- Keyboard arrow keys move the focused block/line slider.

## Public Types

```ts
import type { ComponentType } from "react";

export declare const ColorBoard: ComponentType<{
	value?: string;
	button?: boolean;
	onChange?: (ev: { value: string; input?: boolean }) => void;
}>;
```

## Styling

- Wrapper: `.wx-colorboard`
- Saturation/value block: `.wx-color-block`
- Block slider: `.wx-color-block-slider.wx-slider`
- Hue line: `.wx-color-line`
- Hue slider: `.wx-color-line-slider.wx-slider`
- Controls row: `.wx-color-controls`
- Preview: `.wx-color`
- Text input: `.wx-text`

```jsx
<div className="picker-board">
	<ColorBoard value={value} onChange={ev => setValue(ev.value)} />
</div>
```

```css
.picker-board .wx-color-block {
	height: 180px;
}
```

## Recipes

### Inline Color Board

```jsx
import { useState } from "react";
import { ColorBoard } from "@svar-ui/react-core";

function Demo() {
	const [value, setValue] = useState("#48C8E2");

	return (
		<div style={{ width: 300 }}>
			<ColorBoard
				value={value}
				onChange={ev => {
					setValue(ev.value);
					if (!ev.input) console.log(ev.value);
				}}
			/>
		</div>
	);
}
```
