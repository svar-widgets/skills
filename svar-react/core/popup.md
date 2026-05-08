# SVAR React Core Popup

Package: `@svar-ui/react-core`

## Package

```js
import { Popup } from "@svar-ui/react-core";
```

## Supported Functionality

- Low-level absolutely positioned popup surface.
- Position is calculated with `calculatePosition` from `@svar-ui/lib-dom`.
- Use `parent` to anchor to an element, or use `left`/`top` with an `at` position.
- `at` defaults to `"bottom"` in source.
- `onCancel` is called by click-outside behavior.
- `width` can be number, "auto" or percentage like `100%` - calculated from `parent.offsetWidth`.
- `trackScroll`; when enabled hides on scroll outside of popup.

## Public Types

```ts
import { TPosition } from "@svar-ui/lib-dom";
import type { FC, ReactNode } from "react";

export declare const Popup: FC<{
	left?: number;
	top?: number;
	at?: TPosition;
	css: string;
	width: number | string;
	trackScroll: boolean;
	parent?: HTMLElement;
	children?: ReactNode;
	onCancel?: (ev: MouseEvent) => void;
}>;
```

## Styling

- Container: `.wx-popup`
- Source appends `css` to `.wx-popup`.
- Inline style sets `position:absolute`, calculated `top`, `left`, and `width`.

```jsx
<Popup parent={buttonNode} css="help-popup">
	<div className="body">Help</div>
</Popup>
```

```css
.wx-popup.help-popup {
	padding: 12px;
}
```

## Recipes

### Popup Anchored To A Button

```jsx
import { useRef, useState } from "react";
import { Button, Popup } from "@svar-ui/react-core";

function Example() {
	const parentRef = useRef(null);
	const [open, setOpen] = useState(false);

	return (
		<>
			<div ref={parentRef}>
				<Button onClick={() => setOpen(true)}>Anchor</Button>
			</div>

			{open && parentRef.current && (
				<Popup
					parent={parentRef.current}
					at="bottom"
					onCancel={() => setOpen(false)}
				>
					<div style={{ padding: 12 }}>Popup content</div>
				</Popup>
			)}
		</>
	);
}
```

## Implementation Notes

- Use `Dropdown` for the common anchored dropdown case; it handles `Portal` and parent discovery.
