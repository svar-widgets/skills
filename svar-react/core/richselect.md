# SVAR React Core RichSelect

Package: `@svar-ui/react-core`

## Package

```js
import { RichSelect } from "@svar-ui/react-core";
```

## Supported Functionality

- Non-input single-select control backed by `SuggestDropdown`.
- `value` is the selected id and is controlled.
- `options` are `{ id, label }` by default.
- `textField` controls display field; default is `"label"`.
- `textOptions` can provide selected display objects when visible `options` are partial.
- `clear` shows a close icon when value is set and not disabled.
- `children` render function receives the option object directly for both selected content and list rows.
- `onChange` emits `{ value }`.

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

export declare const RichSelect: ComponentType<{
	value?: string | number;
	options?: { id: string | number; label: string }[];
	textOptions?: { id: string | number; label: string }[];
	placeholder?: string;
	disabled?: boolean;
	error?: boolean;
	title?: string;
	textField?: string;
	clear?: boolean;
	dropdown?: DropdownOptions & {
		virtualized?: boolean;
	};
	children?: (option: any) => ReactNode;
	onChange?: (ev: { value: string | number }) => void;
}>;
```

## Styling

- Wrapper: `.wx-richselect`
- State classes: `.wx-disabled`, `.wx-error`, `.wx-nowrap`
- Content label: `.wx-label`
- Placeholder: `.wx-placeholder`
- Icon: `.wx-icon`, close icon `.wxi-close`
- Dropdown list hooks: `.wx-list`, `.wx-item`, `.wx-focus`

```jsx
<RichSelect
	options={users}
	value={104}
	dropdown={{ css: "user-select-menu" }}
/>
```

```css
.wx-popup.user-select-menu .wx-item {
	min-height: 40px;
}
```

## Recipes

### Rich Select With Custom Template

```jsx
import { RichSelect } from "@svar-ui/react-core";

function Demo() {
	const users = [
		{ id: 104, label: "Lord Varys", email: "little.birds@mail" },
		{ id: 103, label: "Ned Stark", email: "winterhell@mail" },
	];

	return (
		<RichSelect options={users} value={104}>
			{option => (
				<div>
					<strong>{option.label}</strong>
					<span>{option.email}</span>
				</div>
			)}
		</RichSelect>
	);
}
```

### Hidden Selected Option

```jsx
import { RichSelect } from "@svar-ui/react-core";

function Demo() {
	const allUsers = [
		{ id: 87, label: "Berni Mayou" },
		{ id: 103, label: "Ned Stark" },
	];

	const visibleUsers = [{ id: 103, label: "Ned Stark" }];

	return (
		<RichSelect textOptions={allUsers} options={visibleUsers} value={87} clear />
	);
}
```

## Implementation Notes

- Without a custom render function, `.wx-nowrap` is added to ellipsize the selected label.
