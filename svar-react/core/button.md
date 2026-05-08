# SVAR React Core Button

Package: `@svar-ui/react-core`

## Package

```js
import { Button } from "@svar-ui/react-core";
```

## Supported Functionality

- Renders a native `<button class="wx-button">`.
- `type` is split on spaces and each part becomes a `wx-*` class.
- Typed values are `primary`, `secondary`, `danger`, `link`, and each with `block`.
- `css` is appended to the button class list.
- `icon` renders an `<i class={icon}>` before content.
- When `icon` is set and no `children` are supplied, the button also gets `.wx-icon` icon-only styling.
- Renders `children` when provided; otherwise renders `text`.
- `onClick` receives the native `MouseEvent`.

## Public Types

```ts
import type { ComponentType, ReactNode, MouseEvent } from "react";

export declare const Button: ComponentType<{
	type?:
		| "primary"
		| "secondary"
		| "danger"
		| "link"
		| "primary block"
		| "secondary block"
		| "danger block"
		| "link block";
	css?: string;
	icon?: string;
	disabled?: boolean;
	title?: string;
	text?: string;
	children?: ReactNode;
	onClick?: (ev: MouseEvent) => void;
}>;
```

## Styling

- Button class: `.wx-button`
- Type/state classes: `.wx-primary`, `.wx-secondary`, `.wx-danger`, `.wx-link`, `.wx-block`, `.wx-pressed`, `.wx-icon`
- Disabled styling uses the native `[disabled]` attribute.
- Icon child selector is `i`.

```jsx
<Button css="save-button" type="primary" icon="wxi-check">Save</Button>
```

```css
:.wx-button.save-button {
	min-width: 120px;
}
```

## Recipes

### Variants And Click Handler

```jsx
import { Button } from "@svar-ui/react-core";

function Demo() {
	function save(ev) {
		console.log(ev.currentTarget);
	}

	return (
		<>
			<Button type="primary" icon="wxi-check" onClick={save}>Save</Button>
			<Button type="secondary block">Full Width</Button>
			<Button type="danger" disabled>Delete</Button>
			<Button type="link">Details</Button>
		</>
	);
}
```

### Icon-Only Button

```jsx
import { Button } from "@svar-ui/react-core";

function Demo() {
	return (
		<Button
			icon="wxi-search"
			title="Search"
			onClick={() => console.log("search")}
		/>
	);
}
```

## Implementation Notes

- Source has `.wx-square` styles, but `square` is not in the public `type` union.
- `Button` does not call `preventDefault` or stop propagation; handler receives the raw event.
