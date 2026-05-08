# SVAR React Core MultiCombo

Package: `@svar-ui/react-core`

## Package

```js
import { MultiCombo } from "@svar-ui/react-core";
```

## Supported Functionality

- Multi-select searchable input backed by `SuggestDropdown`.
- `value` is an array of selected ids; pair with `onChange` to keep state in sync.
- `options` are `{ id, label }` by default.
- `textField` controls display/filter field; default is `"label"`.
- `textOptions` can provide selected tag display objects when visible `options` are partial.
- Typing filters options case-insensitively by `textField`.
- Selected options render as tags with remove icons.
- `checkboxes` shows non-interactive checkboxes in dropdown rows.
- `children` render function receives `{ option }` for both tags and list rows.
- `onChange` emits `{ value }`.

## Public Types

```ts
import type { FC, ReactNode } from "react";

export interface DropdownOptions {
	inline?: boolean;
	position?: "top" | "right" | "bottom" | "left";
	align?: "start" | "center" | "end";
	css?: string;
	width?: string | "unset" | "auto";
	trackScroll?: boolean;
	virtualized?: boolean;
}

export declare const MultiCombo: FC<{
	id?: string | number;
	value?: (string | number)[];
	options?: { id: string | number; label: string }[];
	textOptions?: { id: string | number; label: string }[];
	textField?: string;
	placeholder?: string;
	title?: string;
	disabled?: boolean;
	error?: boolean;
	checkboxes?: boolean;
	dropdown?: DropdownOptions & {
		virtualized?: boolean;
	};
	children?: (ctx: { option: any }) => ReactNode;
	onChange?: (ev: { value: (string | number)[] }) => void;
}>;
```

## Styling

- Wrapper: `.wx-multicombo`
- State classes: `.wx-focus`, `.wx-disabled`, `.wx-error`, `.wx-not-empty`
- Border wrapper: `.wx-wrapper`
- Tags wrapper: `.wx-tags`, tag `.wx-tag`
- Input row: `.wx-select`
- Icons: `.wx-icon`, `.wxi-close`
- Dropdown list hooks: `.wx-list`, `.wx-item`, `.wx-focus`

```jsx
<MultiCombo
	options={options}
	value={value}
	onChange={ev => setValue(ev.value)}
	dropdown={{ css: "roles-popup" }}
/>
```

```css
.wx-multicombo .wx-tag {
	max-width: 180px;
}
```

## Recipes

### Multi Select With Checkboxes

```jsx
import { useState } from "react";
import { MultiCombo } from "@svar-ui/react-core";

const options = [
	{ id: "editor", label: "Editor" },
	{ id: "owner", label: "Owner" },
	{ id: "viewer", label: "Viewer" },
];

function Example() {
	const [roles, setRoles] = useState(["viewer"]);

	return (
		<MultiCombo
			options={options}
			value={roles}
			onChange={ev => setRoles(ev.value)}
			checkboxes
			placeholder="Select roles"
		/>
	);
}
```

### Custom Tag And Row Content

```jsx
import { MultiCombo } from "@svar-ui/react-core";

const users = [
	{ id: 104, label: "Lord Varys", email: "little.birds@mail" },
];

function Example() {
	return (
		<MultiCombo options={users} value={[104]}>
			{({ option }) => <strong>{option.label}</strong>}
		</MultiCombo>
	);
}
```

## Implementation Notes

- Filtering assumes `option[textField]` is a string
- The source `onselect` path ignores falsy ids; avoid empty-string ids for selected options.
