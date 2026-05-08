# SVAR React Core ModalArea

Package: `@svar-ui/react-core`

## Package

```js
import { ModalArea } from "@svar-ui/react-core";
```

## Supported Functionality

- Local absolute-position modal backdrop and centered window.
- Intended for modal content inside the current layout rather than a viewport-level fixed modal.
- Renders only `children`; it has no built-in header, footer, buttons, or cancel handler.
- Uses a short fade transition.
- Parent layout should provide a positioned containing block when local placement matters.

## Public Types

```ts
import type { FC, ReactNode } from "react";

export declare const ModalArea: FC<{
	children?: ReactNode;
}>;
```

## Styling

- Backdrop: `.wx-modal`
- Window: `.wx-window`
- Backdrop is `position: absolute`, fills the containing block, and uses `--wx-modal-backdrop`.
- Window uses modal background, shadow, border, radius, and min width variables.

```jsx
<div className="local-area">
	<ModalArea>
		<div className="inner">Local modal content</div>
	</ModalArea>
</div>
```

```css
.local-area {
	position: relative;
	min-height: 300px;
}
```

## Recipes

### Local Modal Overlay

```jsx
import { useState } from "react";
import { Button, ModalArea } from "@svar-ui/react-core";

function Example() {
	const [open, setOpen] = useState(false);

	return (
		<div style={{ position: "relative", minHeight: 300 }}>
			<Button onClick={() => setOpen(true)}>Open local modal</Button>

			{open && (
				<ModalArea>
					<Button onClick={() => setOpen(false)}>Close</Button>
				</ModalArea>
			)}
		</div>
	);
}
```

## Implementation Notes

- `ModalArea` does not trap focus or handle Escape.
- Use `Modal` when you need built-in title, buttons, confirmation, or cancellation behavior.
