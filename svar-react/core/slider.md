# SVAR React Core Slider

Package: `@svar-ui/react-core`

## Package

```js
import { Slider } from "@svar-ui/react-core";
```

## Supported Functionality

- Renders an input range with optional label.
- Controlled `value`, default `0`.
- `min` defaults to `0`, `max` to `100`, `step` to `1`.
- `width` sets inline width on `.wx-slider`.
- During drag, `onChange` emits `{ value, previous, input: true }`.
- On final change, `onChange` emits `{ value, previous }`.
- `previous` tracks the previous input/final value separately for drag and final changes.

## Public Types

```ts
import type { ComponentType } from "react";

export declare const Slider: ComponentType<{
	id?: string | number;
	label?: string;
	width?: string;
	min?: number;
	max?: number;
	value?: number;
	step?: number;
	title?: string;
	disabled?: boolean;
	onChange?: (ev: {
		value: number;
		previous: number;
		input?: boolean;
	}) => void;
}>;
```

## Styling

- Wrapper: `.wx-slider`
- Inner range input is styled through input pseudo-elements.
- Label is a native `label` inside `.wx-slider`.

```jsx
<Slider width="240px" value={value} onChange={ev => setValue(ev.value)} />
```

```css
.wx-slider {
	--wx-slider-thumb-size: 18px;
}
```

## Recipes

### Slider With Drag And Final Events

```jsx
import { useState } from "react";
import { Field, Slider } from "@svar-ui/react-core";

function Demo() {
	const [progress, setProgress] = useState(50);

	return (
		<Field label="Progress" position="left" type="slider">
			<Slider
				label={`Progress: ${progress}%`}
				value={progress}
				min={0}
				max={100}
				onChange={ev => {
					setProgress(ev.value);
					if (ev.input) console.log("drag", ev.previous, ev.value);
					else console.log("final", ev.previous, ev.value);
				}}
			/>
		</Field>
	);
}
```
