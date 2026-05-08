Use when building, configuring, styling, localizing, or integrating SVAR React Comments / @svar-ui/react-comments components

## Package

```js
import { Comments, Willow, WillowDark } from "@svar-ui/react-comments";
import "@svar-ui/react-comments/all.css";
```

Top-level exports:

- `Comments` - comments list with add, edit, delete, async data loading, built-in message layouts, and text/markdown rendering
- `Willow`, `WillowDark` - theme wrappers that forward to `@svar-ui/react-core` themes and add comments CSS variables

## Supported functionality

### Data And Users

- `value` is either an `IComment[]` or a truthy key passed to `ondata(value)`
- `ondata(value)` may return `IComment[]` or `Promise<IComment[]>`; while pending, the layout renders with `data=[]`
- `IComment.author` object wins when present; otherwise `IComment.user` is resolved against `users`
- users without `color` get a generated HSL color from `id + name`
- unknown users render as `{ id: 0, name: "Unknown", color: "hsl(0, 0%, 85%)" }`
- `activeUser` can be a user id or an `IUser`; new comments use it for `author` and `user`
- source date formatting uses `comments.dateFormat` or locale specific
-
Common data objects:

```js
const users = [
	{ id: 1, name: "Alice Smith", avatar: "/avatars/alice.png" },
	{ id: 2, name: "Marta Kowalska", color: "#e23a43" },
];

const value = [
	{ id: 1, user: 1, content: "Plain text", date: new Date() },
	{ id: 2, author: users[1], content: "**Markdown**", format: "markdown" },
];
```

### Change Flow

- add creates `{ id: uid(), content, author, user: author.id, date: new Date() }`
- add/update/delete replace internal data with a new array before calling `onchange`
- add payload: `{ action: "add", value, comment, originalValue }`
- update payload: `{ action: "update", value, id, comment, originalValue }`
- delete payload: `{ action: "delete", value, id, originalValue }`
- if add `onchange` returns an object or promise, returned fields are merged into the newly added comment
- `value` is not two-way bound; keep parent state or backend state synchronized from `onchange`

### Rendering Modes

- `render="flow"` is the default layout
- `render="bubbles"` uses chat-style bubbles
- custom `render` component receives `owned`, `edit`, `author`, `date`, and `children` from source
- `format="text"` is the default content renderer
- `format="markdown"` renders markdown content through the bundled Lima renderer
- custom `format` component receives `{ content }`
- per-comment `comment.format` overrides the component-level `format`

Built-ins:

```js
{ render: "flow" }
{ render: "bubbles" }
{ format: "text" }
{ format: "markdown" }
```

### Editing And Deleting

- owned comments are comments where `message.author.id === active author id`
- only owned comments get the visible menu icon
- internal action menu options are `edit-comment` and `delete-comment`
- edit mode replaces message content with the same textarea component used for posting
- `Ctrl+Enter` or `Cmd+Enter` posts textarea content
- empty textarea content is ignored

## Public Types

```ts
import type { ComponentType, ReactNode } from "react";

export interface IUser {
	id: string | number;
	name?: string;
	avatar?: string;
	color?: string;
}

export interface IComment {
	id?: string | number;
	content: string;
	author?: IUser;
	user?: string | number;
	date?: Date;
	format?: "text" | "markdown" | FormatComponent;
}

export interface IChange {
	action: "add" | "update" | "delete";
	id?: string | number;
	comment?: IComment;
	value: IComment[];
	originalValue: IComment[] | string | number;
}

export type FormatComponent = ComponentType<{
	content: string;
}>;

export type RenderComponent = ComponentType<{
	owned?: string | number;
	edit?: string | number;
	author: IUser;
	date: Date;
	children?: ReactNode;
}>;

export declare const Comments: ComponentType<{
	ondata?: (value: string | number) => Promise<IComment[]> | IComment[];
	onChange?: (ev: IChange) => void;
	value?: IComment[] | string | number;
	readonly?: boolean;
	render?: "bubbles" | "flow" | RenderComponent;
	format?: "text" | "markdown" | FormatComponent;
	users?: IUser[];
	activeUser?: string | number | IUser;
	focus?: boolean;
}>;

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

Import the package CSS before using the component (`all.css` includes dependency styles, `style.css` is this component only)

- root list: `.wx-comments-list` is `height: 100%`
- scroll body: `.wx-list` is flex column
- message stack: `.wx-messages`
- flow layout: `.wx-flow`, `.wx-flow.wx-owned`, `.wx-flow-toolbar`, `.wx-message`, `.wx-menu-icon`, `.wx-comment-date`
- bubble layout: `.wx-bubble`, `.wx-bubble.wx-owned`, `.wx-bubble-wrapper`, `.wx-main-bubble`, `.wx-agent-message`, `.wx-avatar`, `.wx-message`
- shared message hooks: `.wx-author-name`, `.wx-menu-icon`, `.wx-comment-date`, `.wx-owned`
- composer hooks: `.wx-comments-textarea`, `.wx-comments-textarea.wx-flow`, `.wx-textarea-wrapper`, `.wx-textarea-avatar`, `.wx-textarea-bottombar`
- avatar hooks: `.wx-user`, `.wx-user.wx-small`, `.wx-user.wx-normal`, `.wx-border`, `.wx-comments-avatar-color-light`, `.wx-comments-avatar-color-dark`
- edit/delete menu is rendered by `@svar-ui/react-menu`
- package CSS variables: `--wx-comments-msg-background`, `--wx-comments-msg-background-agent`, `--wx-avatar-color-dark`

```jsx
import "./CommentsPane.css";

<div className="comments-pane">
	<Comments value={comments} users={users} activeUser={1} />
</div>

/* CommentsPane.css
.comments-pane {
	height: 480px;
	max-width: 760px;
}

.comments-pane .wx-comments-list {
	border: var(--wx-border);
}

.comments-pane .wx-flow {
	padding: 12px 16px;
}

.comments-pane .wx-comments-textarea {
	padding-top: 8px;
}
*/
```

## Recipes

### Basic Comments

```jsx
import { useState } from "react";
import { Comments } from "@svar-ui/react-comments";

function BasicComments() {
	const [comments, setComments] = useState([
		{ id: 1, user: 1, content: "First comment", date: new Date() },
	]);

	const users = [
		{ id: 1, name: "Alice Smith", avatar: "/avatars/alice.png" },
		{ id: 2, name: "Marta Kowalska", color: "#e23a43" },
	];

	return <Comments value={comments} users={users} activeUser={1} focus={true} />;
}
```

### Persist Changes

```jsx
import { useState } from "react";
import { Comments } from "@svar-ui/react-comments";

function PersistedComments() {
	const [comments, setComments] = useState([]);
	const activeUser = { id: 1, name: "Alice Smith" };

	async function saveChange(ev) {
		setComments(ev.value);

		if (ev.action === "add") {
			return await api.createComment(ev.comment);
		}

		if (ev.action === "update") {
			await api.updateComment(ev.id, ev.comment);
		}

		if (ev.action === "delete") {
			await api.deleteComment(ev.id);
		}
	}

	return <Comments value={comments} onChange={saveChange} activeUser={activeUser} />;
}
```

### Load By External Key

```jsx
import { useState } from "react";
import { Comments } from "@svar-ui/react-comments";

function LoadByKey() {
	const [pageId, setPageId] = useState(1);
	const users = [{ id: 1, name: "Alice Smith" }];

	function loadComments(id) {
		return api.getComments(id);
	}

	function saveComment({ action, comment, id, originalValue }) {
		return api.forPage(originalValue).save(action, comment, id);
	}

	return (
		<Comments
			value={pageId}
			ondata={loadComments}
			onChange={saveComment}
			users={users}
			activeUser={1}
		/>
	);
}
```

### Switch Layout Or Markdown

```jsx
import { useState } from "react";
import { Comments } from "@svar-ui/react-comments";

function LayoutSwitch() {
	const [render, setRender] = useState("flow");
	const comments = [
		{ id: 1, user: 1, content: "### Title\n\n**Markdown** text" },
	];
	const users = [{ id: 1, name: "Alice Smith" }];

	return (
		<Comments
			value={comments}
			users={users}
			activeUser={1}
			render={render}
			format="markdown"
		/>
	);
}
```

### Custom Message And Content Renderers

```jsx
// MessageRenderer.jsx
function MessageRenderer({ owned, author, date, children }) {
	return (
		<div className={owned ? "owned" : ""} style={{ paddingLeft: 8 }}>
			<b>{author.name}</b>
			<span>{date.toLocaleString()}</span>
			{children}
		</div>
	);
}

export default MessageRenderer;
```

```jsx
// ContentRenderer.jsx
function ContentRenderer({ content }) {
	return <span className="content">{content.toUpperCase()}</span>;
}

export default ContentRenderer;
```

```jsx
import { Comments } from "@svar-ui/react-comments";
import MessageRenderer from "./MessageRenderer.jsx";
import ContentRenderer from "./ContentRenderer.jsx";

function CustomRenderers() {
	const users = [{ id: 1, name: "Alice Smith" }];
	const comments = [{ id: 1, user: 1, content: "Hello", date: new Date() }];

	return (
		<Comments
			value={comments}
			users={users}
			activeUser={1}
			render={MessageRenderer}
			format={ContentRenderer}
		/>
	);
}
```

## Implementation Notes

- there is no public item registration API; custom renderers are passed directly through `render` and `format`
