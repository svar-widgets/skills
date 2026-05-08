# SVAR React Core Segmented

Package: `@svar-ui/react-core`

## Package

```js
import { Segmented } from "@svar-ui/react-core";
```

## Supported Functionality

- Renders an inline segmented button group.
- `options` are `{ id, label, icon?, title? }`.
- `value` is the selected id and is controlled.
- Clicking an option sets `value = option.id` and emits `onChange({ value })`.
- `css` is appended to `.wx-segmented`.
- Default content renders `option.icon` and `option.label`.
- `children` render function receives `{ option }` for custom option content.

## Public Types

```ts
import type { ComponentType, ReactNode } from "react";

export declare const Segmented: ComponentType<{
	options?: {
		id: string | number;
		label: string;
		icon?: string;
		title?: string;
	}[];
	value?: string | number;
	css?: string;
	children?: (ctx: { option: any }) => ReactNode;
	onChange?: (ev: { value: string | number }) => void;
}>;
```

## Styling

- Wrapper: `.wx-segmented`
- Selected button: `.wx-selected`
- Default icon: `.wx-icon`, icon-only modifier `.wx-only`
- Default label: `.wx-label`

```jsx
<Segmented css="view-mode" options={options} value={value} onChange={ev => setValue(ev.value)} />
```

```css
.wx-segmented.view-mode {
	--wx-segmented-padding: 3px;
}
```

## Recipes

### Basic Segmented Control

```jsx
import { useState } from "react";
import { Segmented } from "@svar-ui/react-core";

function Demo() {
	const options = [
		{ id: "list", label: "List", icon: "wxi-view-sequential" },
		{ id: "grid", label: "Grid", icon: "wxi-view-grid" },
	];

	const [value, setValue] = useState("list");

	return (
		<Segmented
			options={options}
			value={value}
			onChange={ev => {
				setValue(ev.value);
				console.log(ev.value);
			}}
		/>
	);
}
```

### Custom Option Content

```jsx
import { Segmented } from "@svar-ui/react-core";

function Demo() {
	const options = [
		{ id: "left", label: "Left", icon: "wxi-align-left" },
		{ id: "right", label: "Right", icon: "wxi-align-right" },
	];

	return (
		<Segmented options={options} value="left">
			{({ option }) => (
				<>
					<i className={option.icon}></i>
					<span>{option.label}</span>
				</>
			)}
		</Segmented>
	);
}
```
