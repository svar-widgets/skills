# SVAR React Core Modal

Package: `@svar-ui/react-core`

## Package

```js
import { Modal } from "@svar-ui/react-core";
```

## Supported Functionality

- Fixed-position backdrop and centered window.
- `title` renders the default header unless a `header` render function is supplied.
- `children` renders the modal body.
- `footer` render function replaces the default button row.
- `buttons` defaults to `["cancel", "ok"]`; pass `false` to hide default buttons.
- Button id `"cancel"` calls `onCancel`; every other button id calls `onConfirm`.
- Button labels are localized through locale group `core`.
- Modal focuses itself on mount.
- Enter calls `onConfirm` unless focus is inside a `TEXTAREA` or `BUTTON`; Escape calls `onCancel`.

## Public Types

```ts
import type { FC, ReactNode } from "react";

export declare const Modal: FC<{
	title?: string;
	buttons?: boolean | string[];
	header?: () => ReactNode;
	footer?: () => ReactNode;
	children?: ReactNode;
	onConfirm?: (ev: { button?: string; event: MouseEvent }) => void;
	onCancel?: (ev: { button?: string; event: MouseEvent }) => void;
}>;
```

## Styling

- Backdrop: `.wx-modal`
- Window: `.wx-window`
- Header: `.wx-header`
- Button row: `.wx-buttons`
- Button cell: `.wx-button`

```jsx
<Modal title="Confirm">
	<div>Continue?</div>
</Modal>
```

```css
.wx-modal .wx-window {
	--wx-modal-width: 360px;
}
```

## Recipes

### Portal Modal With Default Buttons

```jsx
import { useState } from "react";
import { Button, Modal, Portal } from "@svar-ui/react-core";

function Example() {
	const [open, setOpen] = useState(false);

	return (
		<>
			<Button type="primary" onClick={() => setOpen(true)}>Show</Button>

			{open && (
				<Portal>
					<Modal
						title="Confirm"
						onConfirm={() => setOpen(false)}
						onCancel={() => setOpen(false)}
					>
						Continue?
					</Modal>
				</Portal>
			)}
		</>
	);
}
```

### Custom Header And Footer

```jsx
import { Button, Modal } from "@svar-ui/react-core";

function Example() {
	return (
		<Modal
			buttons={false}
			header={() => <h2>Custom Title</h2>}
			footer={() => <Button type="primary">Apply</Button>}
		>
			<div>Body</div>
		</Modal>
	);
}
```

## Implementation Notes

- Keyboard Enter/Escape handlers pass a keyboard event, while public types declare `MouseEvent`.
- Button click handlers pass `{ button, event }`.
- Default `"ok"` button is rendered as `type="block primary"`; other default buttons use `type="block secondary"`.
