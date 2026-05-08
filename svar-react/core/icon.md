# SVAR React Core Icon

Package: `@svar-ui/react-core`

## Package

```js
import { Icon } from "@svar-ui/react-core";
```

## Supported Functionality

- Renders `<i className="wx-icon {css}">`.
- Use `css` for icon font classes such as `wxi-search`.
- `title` is forwarded to the `<i>`.
- `onClick` is forwarded to the `<i>`.
- If `children` is provided, it is rendered inside the `<i>` and `role="img"` is added.

## Public Types

```ts
import type { ComponentType, ReactNode } from "react";

export declare const Icon: ComponentType<{
	css?: string;
	title?: string;
	children?: ReactNode;
	onClick?: (ev: MouseEvent) => void;
}>;
```

## Styling

- Icon class: `.wx-icon`
- `css` is appended to `.wx-icon`.

```jsx
<Icon css="wxi-search app-icon" title="Search" />
```

```css
.wx-icon.app-icon {
	color: var(--wx-color-primary);
}
```

## Recipes

### Clickable Icon

```jsx
import { Icon } from "@svar-ui/react-core";

function Example() {
	return (
		<Icon
			css="wxi-information-outline"
			title="Info"
			onClick={() => console.log("info")}
		/>
	);
}
```

## Implementation Notes

- The component intentionally uses an `<i>` rather than a button
