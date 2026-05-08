# SVAR React Core Switch

Package: `@svar-ui/react-core`

## Package

```js
import { Switch } from "@svar-ui/react-core";
```

## Supported Functionality

- Renders a labeled checkbox styled as a switch.
- `value` is a controlled boolean.
- `disabled` is forwarded to the hidden checkbox input.
- `onChange` emits `{ value }` after the checked state changes.
- `id` is used through the shared input id helper, so it can connect with a surrounding `Field`.

## Public Types

```ts
import type { ComponentType } from "react";

export declare const Switch: ComponentType<{
	id?: string | number;
	value?: boolean;
	disabled?: boolean;
	onChange?: (ev: { value: boolean }) => void;
}>;
```

## Styling

- Wrapper: `.wx-switch`
- Internal elements are an invisible checkbox input and a visual `span`.

```jsx
<Switch value={value} onChange={ev => setValue(ev.value)} />
```

```css
.wx-switch {
	--wx-switch-width: 56px;
}
```

## Recipes

### Bound Switch In A Field

```jsx
import { useState } from "react";
import { Field, Switch } from "@svar-ui/react-core";

function Demo() {
	const [enabled, setEnabled] = useState(true);

	return (
		<Field label={`Enabled: ${enabled}`} position="left" type="switch">
			<Switch
				value={enabled}
				onChange={ev => {
					setEnabled(ev.value);
					console.log(ev.value);
				}}
			/>
		</Field>
	);
}
```

## Implementation Notes

- The component does not expose `css`; style through parent/global selectors or theme variables.
