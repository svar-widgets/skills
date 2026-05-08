# SVAR React Core Fullscreen

Package: `@svar-ui/react-core`

## Package

```js
import { Fullscreen } from "@svar-ui/react-core";
```

## Supported Functionality

- Wraps content in a fullscreen-capable container.
- Default toggle button uses `Button` with `css="wx-fullscreen-button"`.
- Default icon switches between `wxi-expand` and `wxi-collapse`.
- Custom `toggleButton` render function receives `(toggleFullscreen, inFullscreen)`.
- `hotkey` configures a scoped hotkey on the fullscreen wrapper through `@svar-ui/lib-dom` hotkeys.
- Tracks native `fullscreenchange` to keep `inFullscreen` in sync.

## Public Types

```ts
import type { ComponentType, ReactNode } from "react";

export declare const Fullscreen: ComponentType<{
	toggleButton?: (
		toggle: (ev: MouseEvent) => void,
		inFullscreen: boolean
	) => ReactNode;
	children?: ReactNode;
	hotkey?: string;
}>;
```

## Styling

- Wrapper: `.wx-fullscreen`
- Default button: `.wx-fullscreen-button`
- Default icon: `.wx-fullscreen-icon`
- Fullscreen backdrop selector: `.wx-fullscreen::backdrop`
- Wrapper is `position: relative`, `height: 100%`, `width: 100%`, `tabindex="-1"`.
- Default button is absolutely positioned at bottom right.

```jsx
<Fullscreen>
	<div className="report">Report content</div>
</Fullscreen>
```

```css
.wx-fullscreen .wx-fullscreen-button {
	right: 12px;
	bottom: 12px;
}
```

## Recipes

### Custom Toggle Button

```jsx
import { Button, Fullscreen } from "@svar-ui/react-core";

function Example() {
	return (
		<Fullscreen
			hotkey="ctrl+shift+f"
			toggleButton={(toggle, inFullscreen) => (
				<Button onClick={toggle}>
					{inFullscreen ? "Exit fullscreen" : "Enter fullscreen"}
				</Button>
			)}
		>
			<div className="panel">Report content</div>
		</Fullscreen>
	);
}
```

## Implementation Notes

- `toggleFullscreen` calls `node.requestFullscreen()` and `document.exitFullscreen()`.
