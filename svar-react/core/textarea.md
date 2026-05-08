# SVAR React Core TextArea

Package: `@svar-ui/react-core`

## Package

```js
import { TextArea } from "@svar-ui/react-core";
```

## Supported Functionality

- Renders a native `<textarea class="wx-textarea">`.
- `value` is controlled.
- `onChange` fires `{ value, input: true }` on input and `{ value }` on native change.
- Supports `id`, `placeholder`, `title`, `disabled`, `error`, and `readonly`.
- The textarea is vertically resizable unless disabled.

## Public Types

```ts
import type { ComponentType } from "react";

export declare const TextArea: ComponentType<{
	value?: string;
	id?: string | number;
	placeholder?: string;
	title?: string;
	disabled?: boolean;
	error?: boolean;
	readonly?: boolean;
	onChange?: (ev: { value: string; input?: boolean }) => void;
}>;
```

## Styling

- Textarea: `.wx-textarea`
- Error state: `.wx-textarea.wx-error`
- Disabled state uses `[disabled]`.

```jsx
<TextArea placeholder="Details" />
```

```css
.wx-textarea {
	min-height: 140px;
}
```

## Recipes

### TextArea In A Field

```jsx
import { useState } from "react";
import { Field, TextArea } from "@svar-ui/react-core";

function Demo() {
	const [details, setDetails] = useState("");

	return (
		<Field label="Details" error>
			<TextArea
				value={details}
				onChange={ev => setDetails(ev.value)}
				error
				title="Details are required"
				placeholder="Type here"
			/>
		</Field>
	);
}
```

## Implementation Notes

- There is no `css` prop; style through a parent/global selector or theme variables.
