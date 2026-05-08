# SVAR React Core TwoState

Package: `@svar-ui/react-core`

## Package

```js
import { TwoState } from "@svar-ui/react-core";
```

## Supported Functionality

- Wraps `Button` and toggles controlled boolean `value`.
- When active, adds `pressed` to the forwarded `type`.
- `textActive` and `iconActive` replace `text` and `icon` while active.
- `children` renders inactive/default content; `active` render function prop renders active content when `value` is true.
- Click order: `onClick(ev)` first, then value toggle and `onChange({ value })`.
- Calling `ev.preventDefault()` inside `onClick` prevents the toggle and `onChange`.

## Public Types

```ts
import type { ComponentType, ReactNode } from "react";

export declare const TwoState: ComponentType<{
	value?: boolean;
	type?:
		| "primary"
		| "secondary"
		| "danger"
		| "link"
		| "primary block"
		| "secondary block"
		| "danger block"
		| "link block";
	icon?: string;
	disabled?: boolean;
	iconActive?: string;
	title?: string;
	css?: string;
	text?: string;
	textActive?: string;
	active?: () => ReactNode;
	children?: ReactNode;
	onClick?: (ev: MouseEvent) => void;
	onChange?: (ev: { value: boolean }) => void;
}>;
```

## Styling

- Uses `Button`, so styling hooks are `.wx-button` plus `.wx-pressed` when active.
- `css` is passed to the inner `Button`.
- Button type variables such as `--wx-button-pressed`, `--wx-button-primary-pressed`, and `--wx-button-box-shadow` control active state.

```jsx
<TwoState css="favorite-button" icon="wxi-star" iconActive="wxi-check" />
```

```css
.wx-button.favorite-button.wx-pressed {
	font-weight: 700;
}
```

## Recipes

### Toggle With Active Content

```jsx
import { useState } from "react";
import { TwoState } from "@svar-ui/react-core";

function Demo() {
	const [active, setActive] = useState(false);

	return (
		<TwoState
			value={active}
			onChange={ev => {
				setActive(ev.value);
				console.log(ev.value);
			}}
			type="primary"
			icon="wxi-star"
			iconActive="wxi-check"
			active={() => "Favorited"}
		>
			Favorite
		</TwoState>
	);
}
```

### Prevent Toggle

```jsx
import { TwoState } from "@svar-ui/react-core";

function Demo() {
	function beforeToggle(ev) {
		if (!confirm("Toggle?")) ev.preventDefault();
	}

	return <TwoState onClick={beforeToggle}>Toggle</TwoState>;
}
```

## Implementation Notes

- The active render function is invoked only when `value` is true.
- If `active` is not supplied, the component reuses `children` or `text` with active icon/text substitutions.
