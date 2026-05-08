# SVAR React Core SideArea

Package: `@svar-ui/react-core`

## Package

```js
import { SideArea } from "@svar-ui/react-core";
```

## Supported Functionality

- Absolute-position side panel for local layouts.
- `position` public type supports only `"right"`; source defaults to `"right"`.
- Clicking outside the panel calls `onCancel`.
- Uses a fly transition from the right.
- Renders arbitrary `children`.

## Public Types

```ts
import type { ComponentType, ReactNode } from "react";

export declare const SideArea: ComponentType<{
	position?: "right";
	children?: ReactNode;
	onCancel?: () => void;
}>;
```

## Styling

- Panel: `.wx-sidearea`
- Right position: `.wx-pos-right`

```jsx
<div className="side-host">
	<SideArea>
		<div className="side-content">Panel</div>
	</SideArea>
</div>
```

```css
.side-host {
	position: relative;
	min-height: 300px;
}

.side-content {
	width: 400px;
	padding: 20px;
}
```

## Recipes

### Right-Side Local Panel

```jsx
import { useState } from "react";
import { Button, SideArea } from "@svar-ui/react-core";

function Demo() {
	const [open, setOpen] = useState(false);

	return (
		<div style={{ position: "relative", minHeight: "300px" }}>
			<Button onClick={() => setOpen(true)}>Open side panel</Button>

			{open && (
				<SideArea onCancel={() => setOpen(false)}>
					<div style={{ width: "400px", padding: "20px" }}>Panel content</div>
				</SideArea>
			)}
		</div>
	);
}
```
