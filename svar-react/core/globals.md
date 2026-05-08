# SVAR React Core Globals

Package: `@svar-ui/react-core`

## Package

```js
import { Globals } from "@svar-ui/react-core";
```

## Supported Functionality

- Renders children and installs React context `context.helpers`.
- `helpers.showNotice(msg)` appends a notice.
- `helpers.showModal(msg)` renders a `Modal` and returns a Promise.
- `showNotice` payload fields used by source include `text`, `type`, `expire`, and optional `id`.
- Notice `type` can be empty or classes such as `info`, `warning`, `success`, and `danger`.
- `showNotice` default expiry is `5100ms`; `expire: -1` keeps the notice until the close icon is clicked.
- `showModal` payload fields used by source include `title`, `message`, and `buttons`.
- Confirm resolves the modal Promise; cancel rejects it.
- `Notice` and `Notices` are source components but are not top-level exports.

## Public Types

```ts
import type { ComponentType, ReactNode } from "react";

export declare const Globals: ComponentType<{
	children?: ReactNode;
}>;
```

## Source Helper Shapes

These helper payloads are source behavior, not exported public TypeScript declarations.

```ts
type NoticeMessage = {
	id?: string | number;
	text?: string;
	type?: "" | "info" | "warning" | "success" | "danger" | string;
	expire?: number;
};

type ModalMessage = {
	title?: string;
	message?: any;
	buttons?: boolean | string[];
};
```

## Styling

- Notice list: `.wx-notices`
- Notice item: `.wx-notice`
- Notice content: `.wx-text`
- Notice close button: `.wx-button`
- Notice type classes: `.wx-info`, `.wx-warning`, `.wx-success`, `.wx-danger`
- Modals rendered by `showModal` use `Modal` classes: `.wx-modal`, `.wx-window`, `.wx-header`, `.wx-buttons`, `.wx-button`

```jsx
<Globals>
	<App />
</Globals>
```

```css
.wx-notices {
	top: 12px;
	right: 12px;
}
```

## Recipes

### Install Globals At App Root

```jsx
import { Globals } from "@svar-ui/react-core";
import Actions from "./Actions.jsx";

function App() {
	return (
		<Globals>
			<Actions />
		</Globals>
	);
}
```

### Use Notice And Modal Helpers In A Child

```jsx
import { useContext } from "react";
import { Button, context } from "@svar-ui/react-core";

function Actions() {
	const { showNotice, showModal } = useContext(context.helpers);

	async function confirmDelete() {
		try {
			await showModal({ title: "Confirm", message: "Delete item?" });
			showNotice({ type: "success", text: "Deleted" });
		} catch {
			showNotice({ type: "info", text: "Canceled" });
		}
	}

	return (
		<>
			<Button type="danger" onClick={confirmDelete}>Delete</Button>
			<Button onClick={() => showNotice({ type: "info", text: "Saved" })}>
				Notice
			</Button>
		</>
	);
}
```

## Implementation Notes

- `showModal` stores one active modal at a time.
