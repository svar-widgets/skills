# SVAR React Core Combo

Package: `@svar-ui/react-core`

## Package

```js
import { Combo } from "@svar-ui/react-core";
```

## Supported Functionality

- Searchable single-select input backed by `SuggestDropdown`.
- `options` are `{ id, label }` by default.
- `textField` controls display/filter field; default is `"label"`.
- `textOptions` can provide selected display objects when visible `options` are filtered or partial.
- Typing filters `options` case-insensitively by `textField`.
- Blur selects exact text match first, then first containing match, then previous value or first option.
- Dropdown selection updates the controlled `value` and emits `{ value }`.
- `children` render function receives `{ option }` for custom list row content.
- `dropdown` is forwarded to `SuggestDropdown`/`Dropdown`.

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

export declare const Combo: ComponentType<{
	value?: string | number;
	id?: string | number;
	options?: { id: string | number; label: string }[];
	textOptions?: { id: string | number; label: string }[];
	textField?: string;
	placeholder?: string;
	title?: string;
	disabled?: boolean;
	error?: boolean;
	clear?: boolean;
	dropdown?: DropdownOptions & {
		virtualized?: boolean;
	};
	children?: (params: { option: any }) => ReactNode;
	onChange?: (ev: { value: string | number }) => void;
}>;
```

## Styling

- Wrapper: `.wx-combo`
- Icon: `.wx-icon`, close icon `.wxi-close`
- Error class is applied to the input as `.wx-error`.
- Dropdown list hooks from `SuggestDropdown`: `.wx-list`, `.wx-item`, `.wx-focus`, `.wx-no-data`.
- Non-inline dropdown `css` is appended to `.wx-popup`.


```jsx
<Combo options={users} dropdown={{ css: "users-popup", width: "320px" }} />
```

```css
.wx-popup.users-popup .wx-list {
	max-height: 360px;
}
```

## Recipes

### Custom Option Template And Virtualized List

```jsx
import { useState } from "react";
import { Combo } from "@svar-ui/react-core";

const users = Array.from({ length: 10000 }, (_, id) => ({
	id,
	label: `User ${id}`,
	email: `user${id}@example.com`,
}));

function Demo() {
	const [value, setValue] = useState(9000);

	return (
		<Combo
			options={users}
			value={value}
			onChange={ev => setValue(ev.value)}
			dropdown={{ virtualized: true, width: "320px" }}
		>
			{({ option }) => (
				<div className="user-option">
					<strong>{option.label}</strong>
					<span>{option.email}</span>
				</div>
			)}
		</Combo>
	);
}
```

### Hidden Selected Option

```jsx
import { Combo } from "@svar-ui/react-core";

const allUsers = [
	{ id: 87, label: "Berni Mayou" },
	{ id: 103, label: "Ned Stark" },
];

const visibleUsers = [{ id: 103, label: "Ned Stark" }];

function Demo() {
	return (
		<Combo textOptions={allUsers} options={visibleUsers} value={87} clear />
	);
}
```

## Implementation Notes

- Filtering assumes `option[textField]` is a string
