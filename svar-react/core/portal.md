# SVAR React Core Portal

Package: `@svar-ui/react-core`

## Package

```js
import { Portal, popupContainer } from "@svar-ui/react-core";
```

## Supported Functionality

- `Portal` moves its themed child node to `target` or the nearest `data-wx-portal-root` ancestor.
- If no local portal root exists, source appends to the top node from `@svar-ui/lib-dom` environment.
- `theme` defaults from `context.skin` (read via `useContext(context.skin)` from `@svar-ui/react-core`) when not supplied.
- Children are rendered into the portal target as standard JSX children.
- `popupContainer(node)` marks a local portal root with a generated `data-wx-portal-root` attribute.

## Public Types

```ts
import type { FC, ReactNode } from "react";

export declare const Portal: FC<{
	theme?: "willow" | "willow-dark";
	target?: HTMLElement;
	children?: ReactNode;
}>;

export declare function popupContainer(node: HTMLElement): void;
```

## Styling

- Source wrapper `.wx-portal` is `display: none`.
- Moved node receives `.wx-{theme}-theme`, such as `.wx-willow-theme`.
- `popupContainer` has no class; it sets a data attribute.

```jsx
import { useEffect, useRef } from "react";
import { popupContainer } from "@svar-ui/react-core";

function LocalRoot({ children }) {
	const ref = useRef(null);
	useEffect(() => {
		if (ref.current) popupContainer(ref.current);
	}, []);
	return <div ref={ref} className="local-root">{children}</div>;
}
```

## Recipes

### Render A Modal Through Portal

```jsx
import { useState } from "react";
import { Button, Modal, Portal } from "@svar-ui/react-core";

function Example() {
	const [open, setOpen] = useState(false);

	return (
		<>
			<Button onClick={() => setOpen(true)}>Open</Button>

			{open && (
				<Portal>
					<Modal title="Portal Modal" onCancel={() => setOpen(false)}>
						Content
					</Modal>
				</Portal>
			)}
		</>
	);
}
```

### Local Portal Root

```jsx
import { useEffect, useRef } from "react";
import { DatePicker, popupContainer } from "@svar-ui/react-core";

function Example() {
	const ref = useRef(null);
	useEffect(() => {
		if (ref.current) popupContainer(ref.current);
	}, []);

	return (
		<div ref={ref} className="local-root">
			<DatePicker />
		</div>
	);
}
```
