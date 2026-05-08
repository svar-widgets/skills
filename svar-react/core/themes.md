# SVAR React Core Themes

Package: `@svar-ui/react-core`

## Package

```js
import { Willow, WillowDark } from "@svar-ui/react-core";
```

## Supported Functionality

- Theme components provide React context `wx-theme`.
- `Willow` sets `wx-theme` to `"willow"`.
- `WillowDark` sets `wx-theme` to `"willow-dark"`.
- When `children` are supplied, each theme renders `.wx-theme.wx-*-theme` with `height:100%`.
- `fonts` defaults to `true`.
- `Willow` and `WillowDark` load Open Sans font files and the `wxi` icon CSS.
- Use `fonts={false}` when fonts/icons are already loaded or the app manages font loading.
- Theme styling is CSS-variable driven; override variables on the theme wrapper or an ancestor around specific controls.

## Public Types

```ts
import type { ComponentType, ReactNode } from "react";

export declare const Willow: ComponentType<{
	fonts?: boolean;
	children?: ReactNode;
}>;

export declare const WillowDark: ComponentType<{
	fonts?: boolean;
	children?: ReactNode;
}>;
```

## Styling


```jsx
<Willow fonts={false}>
	<div className="app-theme">
		<App />
	</div>
</Willow>
```

```css
.app-theme {
	--wx-color-primary: #0f766e;
	--wx-input-width: 280px;
	--wx-button-border-radius: 4px;
	--wx-calendar-cell-size: 30px;
}
```

## Recipes

### Wrap An App In A Theme

```jsx
import { Willow } from "@svar-ui/react-core";
import AppRoutes from "./AppRoutes.jsx";

function Demo() {
	return (
		<Willow>
			<AppRoutes />
		</Willow>
	);
}
```

### Dark Theme Without CDN Font Injection

```jsx
import { WillowDark } from "@svar-ui/react-core";

function Demo() {
	return (
		<WillowDark fonts={false}>
			<div className="screen">Dark UI</div>
		</WillowDark>
	);
}
```

## Other information

extra details about themes can be obtained from `../themes.md`
