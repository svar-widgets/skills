# SVAR React Core Text

Package: `@svar-ui/react-core`

## Package

```js
import { Text } from "@svar-ui/react-core";
```

## Supported Functionality

- Controlled `value`, with `string | number` public type.
- `type` supports `text`, `number`, and `password`; default is `text`.
- `onChange` fires `{ value, input: true }` on input and `{ value }` on native change.
- `focus` and `select` focus/select the input after mount.
- `clear` shows a close icon when the input has a value; clicking it sets `value = ""` and emits `{ value }`.
- `icon` renders inside the input. It is right-aligned unless `css` includes `wx-icon-left`.
- `inputStyle` is applied to the inner `<input>`.
- `readonly`, `disabled`, `error`, `placeholder`, and `title` are forwarded to the input/wrapper.

## Public Types

```ts
import type { ComponentType } from "react";

export declare const Text: ComponentType<{
	value?: string | number;
	id?: string | number;
	readonly?: boolean;
	focus?: boolean;
	select?: boolean;
	type?: "text" | "number" | "password";
	placeholder?: string;
	disabled?: boolean;
	error?: boolean;
	inputStyle?: string;
	title?: string;
	css?: string;
	icon?: string;
	clear?: boolean;
	onChange?: (ev: { value: string | number; input?: boolean }) => void;
}>;
```

## Styling

- Wrapper: `.wx-text`
- State/classes: `.wx-error`, `.wx-disabled`, `.wx-clear`, `.wx-icon-left`, `.wx-icon-right`
- Icon: `.wx-icon`; clear icon: `.wx-icon.wxi-close`
- `css` is appended to `.wx-text`.

```jsx
<Text css="search-input wx-icon-left" icon="wxi-search" clear />
```

```css
.wx-text.search-input {
	--wx-input-width: 320px;
}
```

## Recipes

### Text With Clear And Left Icon

```jsx
import { useState } from "react";
import { Field, Text } from "@svar-ui/react-core";

function Demo() {
	const [query, setQuery] = useState("");

	return (
		<Field label="Search" position="left">
			<Text
				value={query}
				onChange={ev => {
					setQuery(ev.value);
					if (!ev.input) console.log("final", ev.value);
				}}
				placeholder="Type here"
				icon="wxi-search"
				css="wx-icon-left"
				clear
			/>
		</Field>
	);
}
```

### Focus And Select On Mount

```jsx
import { Text } from "@svar-ui/react-core";

function Demo() {
	return <Text value="Some value" focus select />;
}
```

## Implementation Notes

- `type="number"` still binds through the input value; account for string/number conversion in your app logic.
