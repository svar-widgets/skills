# SVAR React Core SuggestDropdown

Package: `@svar-ui/react-core`

## Package

```js
import { SuggestDropdown } from "@svar-ui/react-core";
```

## Supported Functionality

- Low-level dropdown list helper used by `Combo`, `MultiCombo`, and `RichSelect`.
- Renders only when navigation index is not `null`; callers open it through `onReady.navigate`.
- `items` are `{ id, label }`.
- `onReady` receives navigation helpers: `navigate`, `keydown`, and `move`.
- `onSelect` emits `{ id }`; in multiselect mode `id` is the next selected id array.
- `multiselect` toggles id arrays instead of a single id.
- `checkboxes` renders a non-interactive `Checkbox` in each row.
- `virtualized` renders only visible rows with fixed measured item height and overscan.
- `children` render function receives `{ option }`.

## Public Types

```ts
import type { ComponentType, ReactNode } from "react";

export interface DropdownOptions {
	inline?: boolean;
	position?: "top" | "right" | "bottom" | "left";
	align?: "start" | "center" | "end";
	css?: string;
	width?: string | "unset" | "auto";
	trackScroll?: boolean;
	virtualized?: boolean;
}

export declare const SuggestDropdown: ComponentType<
	DropdownOptions & {
		items?: { id: string | number; label: string }[];
		children?: (ctx: { option: any }) => ReactNode;
		onSelect?: (ev: { id: string | number | (string | number)[] }) => void;
		onReady?: (ev: {
			navigate?: (dir: number | null, ev?: KeyboardEvent) => void;
			keydown?: (ev: KeyboardEvent, dir: number) => void;
			move?: (ev: KeyboardEvent) => void;
		}) => void;
		multiselect?: boolean;
		checkboxes?: boolean;
		value?: string | number | (string | number)[];
		virtualized?: boolean;
	}
>;
```

## Styling

- List container: `.wx-list`
- Virtual wrapper/content: `.wx-list-wrapper`, `.wx-list-content`
- Row: `.wx-item`
- Focus row: `.wx-item.wx-focus`
- Empty state: `.wx-no-data`
- Non-inline dropdown `css` is appended to `.wx-popup`.

```jsx
<SuggestDropdown items={items} css="suggest-menu" />
```

```css
.wx-popup.suggest-menu .wx-list {
	max-height: 180px;
}
```

## Recipes

### Controlled Suggest Dropdown

```jsx
import { useRef } from "react";
import { SuggestDropdown } from "@svar-ui/react-core";

function Demo() {
	const items = [
		{ id: 1, label: "One" },
		{ id: 2, label: "Two" },
	];

	const apiRef = useRef(null);

	return (
		<>
			<button onClick={() => apiRef.current?.navigate(0)}>Open</button>

			<SuggestDropdown
				items={items}
				onReady={ev => (apiRef.current = ev)}
				onSelect={ev => console.log(ev.id)}
			/>
		</>
	);
}
```

## Implementation Notes

- Keyboard handlers use `ev.code` values `Enter`, `Space`, `Escape`, `Tab`, `ArrowDown`, and `ArrowUp`.
- Virtual mode measures the first rendered item and assumes all rows have that height.
