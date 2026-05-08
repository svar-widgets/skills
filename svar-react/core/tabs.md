# SVAR React Core Tabs

Package: `@svar-ui/react-core`

## Package

```js
import { Tabs } from "@svar-ui/react-core";
```

## Supported Functionality

- Renders a tab strip only; render the tab panel yourself based on `value`.
- `options` are `{ id, label?, title?, icon? }`.
- `value` is the active tab id and is controlled.
- Clicking a tab sets `value = option.id` and emits `onChange({ value })`.
- `type` is `top` or `bottom`; default is `top`.
- Icons use the same icon class pattern as other core controls.

## Public Types

```ts
import type { ComponentType } from "react";

export declare const Tabs: ComponentType<{
	options?: {
		id: string | number;
		label?: string;
		title?: string;
		icon?: string;
	}[];
	value?: string | number;
	type?: "top" | "bottom";
	onChange?: (ev: { value: string | number }) => void;
}>;
```

## Styling

- Wrapper: `.wx-tabs`, plus `.wx-top` or `.wx-bottom`
- Active button: `.wx-active`
- Default icon: `.wx-icon`, icon-only modifier `.wx-only`
- Default label: `.wx-label`

```jsx
<Tabs options={tabs} value={active} onChange={ev => setActive(ev.value)} />
```

```css
.wx-tabs {
	--wx-tabs-cell-min-width: 80px;
}
```

## Recipes

### Tabs With Panels

```jsx
import { useState } from "react";
import { Tabs } from "@svar-ui/react-core";

function Demo() {
	const tabs = [
		{ id: "info", label: "Info", icon: "wxi-alert" },
		{ id: "audit", label: "Audit" },
		{ id: "done", icon: "wxi-check", title: "Done" },
	];

	const [active, setActive] = useState("info");

	return (
		<>
			<Tabs options={tabs} value={active} onChange={ev => setActive(ev.value)} />

			{active === "info" ? (
				<div>Info panel</div>
			) : active === "audit" ? (
				<div>Audit panel</div>
			) : (
				<div>Done panel</div>
			)}

			<Tabs options={tabs} value={active} onChange={ev => setActive(ev.value)} type="bottom" />
		</>
	);
}
```

## Implementation Notes

- `Tabs` has no `css` prop; style with an enclosing parent/global selector or theme variables.
