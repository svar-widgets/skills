Use when building, configuring, styling, or modifying SVAR Svelte Layout / @svar-ui/svelte-layout components

## Package

```js
import { Layout, Cell, Panel } from "@svar-ui/svelte-layout";
```

Top-level exports:

- `Layout` - flex container with direction, spacing presets, padding, and optional drag resizing
- `Cell` - direct layout child with fixed or grow-based sizing and optional header
- `Panel` - collapsible `Cell` variant with an expanded header and collapsed bar

## Supported functionality

### Components

- `Layout` renders a full-size flex container with `direction="column"` by default; use `direction="row"` for horizontal panes.
- `Cell` and `Panel` emit `.wx-cell`; only direct `.wx-cell` children of a resizable `Layout` participate in drag resizing

### Sizing

- `width` or `height` on `Cell`/`Panel` sets a fixed pixel size and `flex:none`.
- Without `width` and `height`, `Cell`/`Panel` uses `flex:{grow}`; `grow` defaults to `1`.
- `minWidth` and `minHeight` set CSS minimums and are read by the resizer to clamp drag ranges.
- In row layouts, fixed `width` is the usual main-axis control; in column layouts, fixed `height` is the usual main-axis control.

### Layout spacing

- Presets are `clean`, `line`, `wide`, and `space`.
- Preset values in source: `clean` = gap 0/padding 0, `line` = gap 1/padding 0, `wide` = gap 10/padding 0, `space` = gap 10/padding 10.
- `gap` and `padding` override preset values when provided.
- When `resizable` is true, CSS gap is not rendered; 6px `.wx-resizer` elements are injected between direct cells. `padding` still applies.

### Events and state

- if at least one cell is not flexible, it will have new size set after resizing
- resize between two flexibles cell must be resolved by `oncellresize` handler ( setting new size / flex )
- `Panel` accepts `oncollapse?: (collapsed: boolean) => void`, called after the internal collapsed state toggles.

### Panel collapse

- Expanded `Panel` always renders `.wx-cell-header` with a toggle button; custom `header` snippet replaces label text but not the toggle.
- Collapsed row panels become a vertical bar; collapsed column panels become a horizontal bar.
- Collapsed size is controlled by `--wx-panel-collapsed-size`, default `24px`.
- Collapsed panels can't be resized

## Public Types

```ts
import { type Snippet, type Component } from "svelte";

interface ILayoutProps {
	direction?: "column" | "row";
	preset?: "clean" | "line" | "wide" | "space";
	gap?: number;
	padding?: number;
	resizable?: boolean;
	css?: string;
	children: Snippet;
	oncellresize?: (sizes: number[]) => void;
}

interface ICellProps {
	label?: string;
	width?: number;
	height?: number;
	minWidth?: number;
	minHeight?: number;
	grow?: number;
	scroll?: boolean;
	css?: string;
	children: Snippet;
	header?: Snippet;
}

interface IPanelProps {
	label?: string;
	collapsed?: boolean;
	width?: number;
	height?: number;
	minWidth?: number;
	minHeight?: number;
	grow?: number;
	scroll?: boolean;
	css?: string;
	children: Snippet;
	header?: Snippet;
	oncollapse?: (collapsed: boolean) => void;
}

export declare const Layout: Component<ILayoutProps>;
export declare const Cell: Component<ICellProps>;
export declare const Panel: Component<IPanelProps>;
```

## Styling

- `css` is appended to the component root: `.wx-layout`, `.wx-cell`, or `.wx-cell.wx-panel`.
- Layout hooks: `.wx-layout`, `.wx-layout-{preset}`, `.wx-column`, `.wx-row`.
- Cell hooks: `.wx-cell`, `.wx-cell-header`, `.wx-cell-body`.
- Panel hooks: `.wx-panel`, `.wx-panel-collapsed`, `.wx-panel-animating`, `.wx-panel-row`, `.wx-panel-column`, `.wx-panel-collapsed-bar`, `.wx-panel-toggle`, `.wx-panel-icon`, `.wx-panel-label`.
- Resizer hooks: `.wx-resizer` is inserted between direct cells; `.wx-resize-overlay` is a temporary fixed overlay during drag.
- global `.wx-scroll` sets `overflow:auto` on the component root.
- global `.wx-border` adds border
- Built-in variables: `--wx-layout-gap-color`, `--wx-layout-line-color`, `--wx-layout-resizer-hover`, `--wx-layout-resizer-active`, `--wx-panel-collapsed-size`.

```svelte
<Layout direction="row" preset="line" css="app-layout">
	<Cell label="Files" width={220} css="app-pane">Files</Cell>
	<Cell label="Editor">Editor</Cell>
</Layout>

<style>
	.app-layout {
		--wx-layout-line-color: #d7dee8;
		--wx-layout-resizer-hover: rgba(40, 95, 170, 0.18);
		--wx-panel-collapsed-size: 30px;
	}

	.app-pane .wx-cell-header {
		padding: 6px 10px;
	}
</style>
```

## Recipes

### Basic Fixed And Flexible Panes

```svelte
<script>
	import { Layout, Cell } from "@svar-ui/svelte-layout";
</script>

<div class="workspace">
	<Layout direction="row" preset="line">
		<Cell label="Sidebar" width={240} minWidth={160}>
			<nav>Navigation</nav>
		</Cell>
		<Cell label="Main" grow={3}>
			<main>Content</main>
		</Cell>
	</Layout>
</div>

<style>
	.workspace {
		width: 100%;
		height: 100vh;
	}
</style>
```

### Resizable IDE Layout

```svelte
<script>
	import { Layout, Cell, Panel } from "@svar-ui/svelte-layout";

	let sidebarWidth = $state(220);
</script>

<Layout
	direction="row"
	padding={6}
	resizable
	oncellresize={sizes => (sidebarWidth = sizes[0])}
>
	<Panel label="Files" width={sidebarWidth} minWidth={120}>
		<div>File tree</div>
	</Panel>

	<Cell>
		<Layout preset="line">
			<Cell grow={3}>
				{#snippet header()}<span>Editor</span>{/snippet}
				<div>Editor area</div>
			</Cell>
			<Panel grow={1} label="Terminal">
				<div>Terminal</div>
			</Panel>
		</Layout>
	</Cell>
</Layout>
```

### Controlled Panel Collapse

```svelte
<script>
	import { Layout, Cell, Panel } from "@svar-ui/svelte-layout";

	let collapsed = $state(false);
</script>

<Layout direction="row" preset="line">
	<Panel
		label="Sidebar"
		width={220}
		minWidth={140}
		{collapsed}
		oncollapse={value => (collapsed = value)}
	>
		<div>Sidebar content</div>
	</Panel>
	<Cell>
		<div>Main content</div>
	</Cell>
</Layout>
```

### Custom Header Snippet

```svelte
<script>
	import { Layout, Cell } from "@svar-ui/svelte-layout";
</script>

<Layout>
	<Cell height={48}>
		{#snippet header()}
			<div class="bar">
				<span>Toolbar</span>
				<button>Save</button>
			</div>
		{/snippet}
		<div>Body</div>
	</Cell>
	<Cell scroll>
		<div>Long content</div>
	</Cell>
</Layout>
```

### Presets And Explicit Spacing

```svelte
<script>
	import { Layout, Cell } from "@svar-ui/svelte-layout";
</script>

<Layout direction="row" preset="space" gap={12} padding={16}>
	<Cell css="wx-border">Left</Cell>
	<Cell css="wx-border">Right</Cell>
</Layout>
```

## Implementation Notes

- `Cell` renders `.wx-cell-header` and `.wx-cell-body` only when `header` or `label` is provided.
- `Panel` detects row vs column from the parent DOM class `.wx-row`; outside a `Layout`, it behaves as column-oriented.
- Resizable layouts query only `:scope > .wx-cell`, so wrapping a `Cell` or `Panel` in another element prevents it from being resized.
- Drag resizing mutates inline styles on the adjacent cells during the pointer drag. Originally flexible cells are restored after pointer up; originally fixed cells keep their dragged pixel size.
