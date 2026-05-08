# svar-svelte — filemanager

_Generated 2026-05-08T13:35:37.017Z_

## Contents

- [`filemanager/index.md`](#file-filemanager-index-md)
- [`locales.md`](#file-locales-md)
- [`themes.md`](#file-themes-md)


## File: filemanager/index.md

> Source: `filemanager/index.md`

Use when building, configuring, styling, or modifying SVAR Svelte Filemanager / @svar-ui/svelte-filemanager components, menus, themes, store actions, or backend data provider integration.

#### Package

```js
import {
	Filemanager,
	Willow,
	WillowDark,
	getMenuOptions,
} from "@svar-ui/svelte-filemanager";
```

#### Supported functionality

##### Components and themes

- `Filemanager` renders the full file explorer: toolbar, search, sidebar tree, cards/table/panels views, preview/info panel, context/action menus, upload drop area, and modals.
- `Willow`, and `WillowDark` wrap matching `@svar-ui/svelte-core` themes and add filemanager CSS variables.
- Theme components accept `fonts?: boolean` and optional Svelte children.
- `Filemanager` has no `children` snippet, slot, `class`, `style`, or `css` passthrough prop.

##### Data model

- `data` is a flat `IEntity[]`; each item must have path-like `id`, such as `"/Code/Button.js"`.
- Root `"/"` is generated internally as a folder named `"My files"`.
- `FileTree.parseId` derives `parent`, `name`, and `ext` from `id`; missing `type` defaults to `"file"`.
- Folder items are the only records rendered in the sidebar tree.
- `date` is expected as a `Date` object for built-in formatting.
- `lazy: true` on a folder triggers `request-data` when the folder path is opened.
- Duplicate create/copy names are made unique by appending `.new` before the extension, for example `"/file.new.txt"`.
- `drive` is optional and only renders storage info when both `used` and `total` are present.

##### Modes and layout

- `mode` supports `"cards"`, `"table"`, `"panels"`, and `"search"`.
- Toolbar mode buttons only expose `"table"`, `"cards"`, and `"panels"`.
- Search runs `filter-files`; non-empty text switches to `"search"` mode and clearing text restores previous `mode` and `panels`.
- `preview` toggles the info pane; on containers narrower than `768px`, preview uses a narrow full-content layout.
- `panels` accepts partial panel state; common fields are `path` and `selected`.
- `activePanel` is `0` or `1` and is used in panels mode and upload drop handling.

##### API and events

- Use `init(api)` for first-time API setup; it is called once after initial store setup.
- `bind:this={api}` exposes the same public methods: `exec`, `on`, `intercept`, `detach`, `setNext`, `getState`, `getReactiveState`, `getStores`, `getFile`, and `serialize`.
- Component event props are generated from store action names by removing hyphens and prefixing `on`, for example `onrequestdata`, `ondownloadfile`, `onopenfile`, `oncreatefile`.
- Event callback payloads are the same objects passed to `api.exec(action, payload)`.
- Action flow is store first, then component event props, then any next bus set by `api.setNext(...)`.
- `api.intercept(action, callback)` can cancel or replace built-in behavior by returning `false`, as shown by backend filtering demos.
- The store mutates some action payloads before downstream handlers/providers: `rename-file.newId`, `create-file.newId`, `copy-files.newIds`, `move-files.newIds`, and `skipProvider` when copy/move into self is rejected.

##### Built-in actions

- Selection/navigation: `select-file`, `set-path`, `set-active-panel`, `open-tree-folder`.
- View/search/sort: `show-preview`, `filter-files`, `set-mode`, `sort-files`.
- File operations: `create-file`, `rename-file`, `delete-files`, `copy-files`, `move-files`.
- Backend/user hooks: `request-data`, `provide-data`, `download-file`, `open-file`.
- Hotkeys use the current `menuOptions` result, so removed menu items also remove their default hotkey behavior.
- Built-in hotkeys include `Ctrl/Cmd+C`, `Ctrl/Cmd+X`, `Ctrl/Cmd+V`, `Ctrl/Cmd+R`, `Ctrl/Cmd+D`, `Delete`, `Enter`, and arrow navigation with Ctrl/Cmd or Shift selection modifiers.

##### Menus

- `menuOptions(mode, item)` receives one of `"folder"`, `"file"`, `"body"`, `"add"`, or `"multiselect"` plus the current item when applicable.
- Return `false`, `null`, `undefined`, or an empty array to suppress a menu for that context.
- Default `"add"` menu: `add-file`, `add-folder`, and `upload` with `comp: "upload"`.
- Default `"body"` menu: `paste`.
- Default `"multiselect"` menu: `copy`, `move`, separator, `delete`.
- Default file menu: `download`, `copy`, `move`, `paste`, separator, `rename`, `delete`.
- Default folder menu omits `download`.
- Root folder context menu is filtered to `paste` only.
- Search mode filters out `paste`.
- Readonly mode hides add controls and edit menus; desktop readonly file menus include only `download`, while narrow mode prepends `preview`.
- Before menu display, item text is localized and `hotkey` is copied to `subtext`; tree-context menu options have `hotkey` cleared.
- Custom menu option `handler` receives a menu pack with `context`; use `context.id` for file operations.
- Filemanager registers the custom menu item type `"upload"` internally through `registerMenuItem("upload", UploadButton)`.

##### Icons, previews, and info

- `icons(file, size)` is used for image URLs in cards/table/info; `size` is `"big"` or `"small"`.
- `icons="simple"` is supported by source and demos and disables image icon URLs, falling back to icon font classes.
- Default icons use `https://cdn.svar.dev/icons/filemanager/vivid/${size}/${icon}.svg`.
- `previews(file, width, height)` is used for card thumbnails and info preview; return a URL string or a falsy value.
- `extraInfo(file)` runs for a single selected item in the info pane; it may return an object, a promise, or null.
- Extra info object entries are appended to the info grid as name/value rows.

##### Saving

- `RestDataProvider` from `@svar-ui/filemanager-data-provider` persists data changes to a REST backend.
- Wire it once with `api.setNext(provider)` in `init`; the provider then forwards every data action (`create-file`, `rename-file`, `move-files`, `copy-files`, `delete-files`) emitted on the event bus as the matching REST call. No per-action save handlers needed.
- Uploads are sent from `create-file` when `ev.file.file` exists; otherwise create sends JSON.
- Initial load and lazy folders use `provider.loadFiles(id)` / `loadInfo(id)`; dispatch results back through `provide-data` for `request-data`.
- Provider emits `"file-renamed"` when backend-generated ids differ from local ids - re-emit `rename-file` with `skipProvider: true` to sync the store.

```js
import { RestDataProvider } from "@svar-ui/filemanager-data-provider";

const provider = new RestDataProvider("/api/files");

function init(api) {
	api.setNext(provider); // forwards all file mutations to REST
}
```

#### Public Types

```ts
import type { Component } from "svelte";
import type { IMenuOption } from "@svar-ui/svelte-menu";

import type {
	TMethodsConfig,
	IApi,
	IConfig,
	TContextMenuType,
	IExtraInfo,
	IParsedEntity,
} from "@svar-ui/filemanager-store";

export * from "@svar-ui/filemanager-store";

export interface IFileMenuOption extends IMenuOption {
	hotkey: string;
}

export type FilePreview = IParsedEntity & {
	type: "file" | "folder" | "search" | "multiple" | "none";
};

export declare const Filemanager: Component<
	{
		readonly?: boolean;
		menuOptions?: (
			mode: TContextMenuType,
			item?: IParsedEntity
		) => IFileMenuOption[];
		extraInfo?: (
			file: IParsedEntity
		) => Promise<IExtraInfo> | IExtraInfo | null;
		icons?: (file: IParsedEntity, size: "big" | "small") => string;
		previews?: (
			file: FilePreview,
			width: number,
			height: number
		) => string | null;
		init?: (api: IApi) => void;
	} & IConfig &
		FilemanagerActions<TMethodsConfig>
>;

export declare const Willow: Component<{
	fonts?: boolean;
	children?: () => any;
}>;

export declare const WillowDark: Component<{
	fonts?: boolean;
	children?: () => any;
}>;

/* get component events from store actions*/
type RemoveHyphen<S extends string> = S extends `${infer Head}-${infer Tail}`
	? `${Head}${RemoveHyphen<Tail>}`
	: S;

type EventName<K extends string> = `on${RemoveHyphen<K>}`;

export type FilemanagerActions<TMethodsConfig extends Record<string, any>> = {
	[K in keyof TMethodsConfig as EventName<K & string>]?: (
		ev: TMethodsConfig[K]
	) => void;
} & {
	[key: `on${string}`]: (ev?: any) => void;
};
```

Important store shapes for wiring handlers, condensed from `store/dist/types`:

```ts
export type TID = string;
export type TContextMenuType =
	| "folder"
	| "file"
	| "body"
	| "add"
	| "multiselect";

export interface IEntity {
	id: TID;
	type?: "file" | "folder";
	size?: number;
	lazy?: boolean;
	date?: Date;
	[key: string]: any;
}

export interface IParsedEntity extends IEntity {
	parent: TID;
	name: string;
	ext: string;
	$level: number;
	open?: boolean;
	data?: IParsedEntity[];
}

export interface IFile {
	name: string;
	date?: Date;
	type?: "file" | "folder";
	size?: number;
	file?: File;
}

export type TMode = "cards" | "table" | "panels" | "search";
export type TActivePanel = 0 | 1;

export interface IPanel {
	path: TID;
	selected: TID[];
	_selected: IParsedEntity[];
	_files: IParsedEntity[];
	_crumbs: IParsedEntity[];
	_sorts: { [key: TID]: { key: string; order: "asc" | "desc" } };
	_lastSelected: TID;
	_selectNavigation: boolean;
}

export interface IConfig {
	data?: IEntity[];
	mode?: TMode;
	drive?: IDrive;
	preview?: boolean;
	panels?: Partial<IPanel>[];
	activePanel?: TActivePanel;
}

export interface IDrive {
	used?: number;
	total?: number;
}

export interface IExtraInfo {
	Size: string;
	Count: string;
	[key: string]: any;
}

type WithActionMeta<T> = T & {
	skipProvider?: boolean;
	[key: string]: any;
};

export type TMethodsConfig = {
	["select-file"]: WithActionMeta<{
		id?: TID;
		toggle?: boolean;
		range?: boolean;
		panel?: TActivePanel;
		type?: "navigation";
	}>;
	["set-path"]: WithActionMeta<{
		id: TID;
		selected?: TID[];
		panel?: TActivePanel;
	}>;
	["set-active-panel"]: WithActionMeta<{ panel: TActivePanel }>;
	["open-tree-folder"]: WithActionMeta<{ id: TID; mode: boolean }>;
	["show-preview"]: WithActionMeta<{ mode: boolean }>;
	["filter-files"]: WithActionMeta<{ text: string }>;
	["set-mode"]: WithActionMeta<{ mode: TMode }>;
	["rename-file"]: WithActionMeta<{ id: TID; name: string; newId?: string }>;
	["create-file"]: WithActionMeta<{
		file: IFile;
		parent: TID;
		newId?: string;
	}>;
	["delete-files"]: WithActionMeta<{ ids: TID[] }>;
	["move-files"]: WithActionMeta<{
		ids: TID[];
		target: TID;
		newIds?: TID[];
	}>;
	["copy-files"]: WithActionMeta<{
		ids: TID[];
		target: TID;
		newIds?: TID[];
	}>;
	["request-data"]: WithActionMeta<{ id: TID }>;
	["provide-data"]: WithActionMeta<{ id: TID; data: IEntity[] }>;
	["download-file"]: WithActionMeta<{ id: TID }>;
	["open-file"]: WithActionMeta<{ id: TID }>;
	["sort-files"]: WithActionMeta<{
		key: string;
		order: "asc" | "desc";
		panel?: TActivePanel;
		path?: string;
	}>;
};
```

#### Styling

- `Filemanager` does not accept `css`, `class`, `className`, or `style`; wrap it in a parent element and target global classes from that parent.
- The root component class is `.wx-filemanager`; it is `display: flex`, `flex-direction: column`, `height: 100%`, `max-width: 100vw`, `max-height: 100vh`, and `overflow: hidden`.
- The parent container must provide a usable height, usually `height: 100%` or a fixed height.
- Theme variables defined by package themes: `--wx-fm-background`, `--wx-fm-box-shadow`, `--wx-fm-select-background`, `--wx-fm-grid-border`, `--wx-fm-grid-header-color`, `--wx-fm-button-font-color`, `--wx-fm-toolbar-height`.
- Other consumed variables include core/theme variables such as `--wx-background`, `--wx-border`, `--wx-color-primary`, `--wx-color-primary-selected`, `--wx-color-font-alt`, `--wx-icon-color`, `--wx-button-background`, `--wx-table-select-background`, and `--wx-table-select-focus-background`.
- Toolbar: `.wx-toolbar`, `.wx-left`, `.wx-right`, `.wx-preview-icon`, `.wx-modes`; height comes from `--wx-fm-toolbar-height`, default theme value `56px`, with `gap: 8px` and `padding: 0 12px`.
- Layout: `.wx-content-wrapper` has `margin-top: 10px`; `.wx-sidebar` is `width: 238px` with `padding: 0 10px 10px`; `.wx-content-item` uses `width: 67%`; `.wx-info` uses `width: 38%`.
- Cards: `.wx-cards` uses flex wrapping and `padding: 30px 20px 10px`; card `.wx-item` is `210px x 200px` with `margin: 0 20px 20px 0`.
- Cards item hooks: `.wx-preview`, `.wx-file-preview`, `.wx-file-icon`, `.wx-card-preview`, `.wx-info`, `.wx-folder-name`, `.wx-file-name`, `.wx-more`, `.wx-back`, `.wx-selected`.
- Table hooks: `.wx-list`, `.wx-grid`, `.wx-row`, `.wx-header`, `.wx-cell`, `.wx-each-cell`; row/header height is configured as `42px`.
- Tree hooks: `.wx-tree`, `.wx-folder`, `.wx-toggle`, `.wx-toggle-placeholder`, `.wx-selected`; folder indentation is inline `padding-left` based on tree level.
- Breadcrumb hooks: `.wx-breadcrumbs`, `.wx-refresh-icon`, `.wx-item`.
- Search hooks: `.wx-search`, `.wx-search-input`, `.wx-icon`, `.wx-text`.
- Preview/info hooks: `.wx-info`, `.wx-info-narrow`, `.wx-wrapper`, `.wx-preview`, `.wx-info-panel`, `.wx-no-info-panel`, `.wx-img-wrapper`, `.wx-icon-wrapper`, `.wx-title`, `.wx-list`, `.wx-name`, `.wx-value`.
- Panels mode hooks: `.wx-panels`; child `.wx-item` uses `width: calc(50% - 10px)` and the first panel has `margin-right: 10px`.
- Upload hooks: `.wx-upload-area`, `.wx-upload-area.wx-active`; active drop background uses `--wx-color-primary-selected`.
- Menu popups come from `@svar-ui/svelte-menu` and use `.wx-menu`, `.wx-option`, `.wx-separator`, `.wx-subtext`, and related menu hooks; the popup is portaled outside the filemanager layout.
- Several classes are generic (`.wx-list`, `.wx-item`, `.wx-wrapper`, `.wx-name`); always scope selectors from a wrapper or a more specific filemanager section.

```svelte
<div class="filemanager">
	<Filemanager {data} {drive} />
</div>

<style>
	.filemanager {
		height: 100%;
		width: 100%;
		--wx-color-primary: rgb(11, 162, 208);
		--wx-fm-background: rgb(207, 209, 221);
		--wx-fm-select-background: rgb(235, 235, 255);
		--wx-table-select-background: rgba(33, 195, 255, 0.1);
		--wx-table-select-focus-background: rgba(33, 195, 255, 0.1);
	}

	.filemanager > .wx-filemanager .wx-cards .wx-back {
		color: rgb(74, 93, 237);
	}
</style>
```

#### Recipes

##### Basic Filemanager

```svelte
<script>
	import { Filemanager, Willow } from "@svar-ui/svelte-filemanager";

	const data = [
		{ id: "/Code", type: "folder", date: new Date(2023, 11, 2, 17, 25) },
		{ id: "/Code/Button.js", type: "file", size: 1177, date: new Date() },
	];

	const drive = {
		used: 15200000000,
		total: 50000000000,
	};
</script>

<Willow>
	<Filemanager {data} {drive} />
</Willow>
```

##### Initial Mode, Path, Selection, And Preview

```svelte
<script>
	import { Filemanager } from "@svar-ui/svelte-filemanager";

	const panels = [
		{ path: "/Code", selected: ["/Code/Button.js"] },
		{ path: "/", selected: ["/Music"] },
	];
</script>

<Filemanager
	{data}
	{drive}
	mode="panels"
	{panels}
	activePanel={0}
	preview
/>
```

##### Handle API And Component Events

```svelte
<script>
	import { Filemanager } from "@svar-ui/svelte-filemanager";

	let api;
	let saved = [];

	function init(fm) {
		api = fm;

		api.on("download-file", ({ id }) => {
			window.open(`/download?id=${encodeURIComponent(id)}`, "_self");
		});

		api.on("open-file", ({ id }) => {
			window.open(`/direct?id=${encodeURIComponent(id)}`, "_blank");
		});
	}

	function serializeCode() {
		saved = api.serialize("/Code");
		api.exec("provide-data", { id: "/Code", data: [] });
	}

	function loadLazy({ id }) {
		fetch(`/files/${encodeURIComponent(id)}`)
			.then(res => res.json())
			.then(data => api.exec("provide-data", { id, data }));
	}
</script>

<button onclick={serializeCode}>Serialize /Code</button>

<Filemanager
	bind:this={api}
	{init}
	{data}
	{drive}
	onrequestdata={loadLazy}
/>
```

##### Customize Context Menus

```svelte
<script>
	import { Filemanager, getMenuOptions } from "@svar-ui/svelte-filemanager";

	let api;

	function init(fm) {
		api = fm;
	}

	function menuOptions(mode, item) {
		if ((mode === "file" || mode === "folder") && item.id === "/Code") {
			return false;
		}

		if (mode === "file" || mode === "folder") {
			return [
				...getMenuOptions(mode),
				{ comp: "separator" },
				{
					id: "clone",
					text: "Clone",
					icon: "wxi-content-copy",
					hotkey: "Ctrl+Shift+V",
					handler: ({ context }) => {
						const { panels, activePanel } = api.getState();
						api.exec("copy-files", {
							ids: [context.id],
							target: panels[activePanel].path,
						});
					},
				},
			];
		}

		return getMenuOptions(mode);
	}
</script>

<Filemanager {data} {drive} {init} {menuOptions} />
```

##### Use Server Data And RestDataProvider

```svelte
<script>
	import { Filemanager } from "@svar-ui/svelte-filemanager";
	import { RestDataProvider } from "@svar-ui/filemanager-data-provider";

	const server = "https://example.com/api";
	const provider = new RestDataProvider(server);

	let api;
	let data = $state([]);
	let drive = $state({});

	function init(fm) {
		api = fm;
		api.setNext(provider);

		api.on("download-file", ({ id }) => {
			window.open(`${server}/direct?id=${encodeURIComponent(id)}&download=true`, "_self");
		});

		api.on("open-file", ({ id }) => {
			window.open(`${server}/direct?id=${encodeURIComponent(id)}`, "_blank");
		});
	}

	function loadData({ id }) {
		provider.loadFiles(id).then(files => {
			api.exec("provide-data", { id, data: files });
		});
	}

	provider.on("file-renamed", ({ id, newId }) => {
		const name = newId.slice(newId.lastIndexOf("/") + 1);
		api.exec("rename-file", { id, name, skipProvider: true });
	});

	Promise.all([provider.loadFiles(), provider.loadInfo()]).then(([files, info]) => {
		data = files;
		drive = info;
	});
</script>

<Filemanager {init} {data} {drive} onrequestdata={loadData} />
```

##### Custom Icons, Previews, And Extra Info

```svelte
<script>
	import { Filemanager } from "@svar-ui/svelte-filemanager";
	import { formatSize } from "@svar-ui/filemanager-store";

	const server = "https://example.com/api";

	function icons(file, size) {
		const name = file.type === "file" ? file.ext : file.type;
		return `${server}/icons/${size}/${name}.svg`;
	}

	function previews(file, width, height) {
		if (file.ext === "png" || file.ext === "jpg" || file.ext === "jpeg") {
			return `${server}/preview?width=${width}&height=${height}&id=${encodeURIComponent(file.id)}`;
		}
		return null;
	}

	function extraInfo(file) {
		if (file.type === "folder") {
			return { Size: formatSize(file.size || 0), Count: "folder" };
		}
		return null;
	}
</script>

<Filemanager {data} {drive} {icons} {previews} {extraInfo} preview />
```

##### Backend Search Intercept

```svelte
<script>
	import { Filemanager } from "@svar-ui/svelte-filemanager";

	let api;

	function init(fm) {
		api = fm;

		api.intercept("filter-files", ({ text }) => {
			const { panels, activePanel } = api.getState();
			const id = panels[activePanel].path;

			fetch(`/files/${encodeURIComponent(id)}?text=${text || ""}`)
				.then(res => res.json())
				.then(data => {
					api.exec("set-mode", { mode: text ? "search" : "cards" });
					api.exec("provide-data", { id, data });
				});

			return false;
		});
	}
</script>

<Filemanager {init} {data} {drive} />
```

##### Localize Filemanager

```svelte
<script>
	import { Locale } from "@svar-ui/svelte-core";
	import { cn } from "@svar-ui/filemanager-locales";
	import { cn as cnCore } from "@svar-ui/core-locales";
	import { Filemanager } from "@svar-ui/svelte-filemanager";
</script>

<Locale words={{ ...cn, ...cnCore }}>
	<Filemanager {data} {drive} />
</Locale>
```

#### Implementation Notes

- `Filemanager.svelte` stores all unknown props in `restProps` for generated action callbacks; unknown props are not spread onto DOM.
- Source supports `icons="simple"`, but the declaration types `icons` only as a function.
- Source default `icons` can return `false` for folders, but the declaration says `string`.
- Source accepts falsy `previews` return values, but the declaration says `string | null`.
- `menuOptions` can suppress menus with falsy returns, but the declaration says it returns `IFileMenuOption[]`.
- Store source `IMenuOption.id` is `string | number`, while generated `store/dist/types/types.d.ts` has `id?: string`.
- `RestDataProvider.loadFiles()` and `loadInfo()` are called without arguments in demos, but generated provider declarations require `id: TID`.
- `DataStore` mutates the input file objects during parse by adding `parent`, `name`, `ext`, default `type`, and tree state fields.
- Context/action menus and tests rely on ids encoded by `setID`; use raw file ids in app code and let the library set data attributes.
- `registerMenuItem("upload", UploadButton)` runs inside `Sidebar.svelte`; a custom `"upload"` add item only works through the built-in sidebar add menu.
- `extraInfo` errors are caught and logged, then ignored.
- In readonly mode, hotkeys use readonly menu options, so edit hotkeys do not open modals.


## File: locales.md

> Source: `locales.md`

i18n patterns common to all SVAR Svelte components - Locale wrapper, bundled language packs, extending words and formats

### Localizing SVAR Svelte Components

All `@svar-ui/svelte-*` widgets read locale data from a single Svelte context (`wx-i18n`). The mechanics live in `@svar-ui/svelte-core`; every other package consumes them.

#### Locale Wrapper

Wrap the subtree you want to localize. With no wrapper, widgets fall back to English.

```svelte
<script>
    import { Calendar, Locale } from "@svar-ui/svelte-core";
    import { de } from "@svar-ui/core-locales";
</script>

<Locale words={de}>
    <Calendar value={new Date(2025, 4, 1)} />
</Locale>
```

Wrap the smallest subtree that needs the alternative locale - nested `Locale` blocks let different parts of the app render in different languages.

`Locale` does not render any DOM wrapper; it only mutates context, so it never affects layout.

#### Bundled Language Packs

Core packs ship in `@svar-ui/core-locales`:

```js
import { en, cn, de, es, fr, it, ja, pt, ru } from "@svar-ui/core-locales";
```

Standalone widget packages ship their own dictionaries alongside the core pack - each exports locale objects keyed by language code (`cn`, `de`, `fr`, ...):

- `@svar-ui/core-locales` - core widgets (always include)
- `@svar-ui/editor-locales` - Editor
- `@svar-ui/filter-locales` - Filter
- `@svar-ui/gantt-locales` - Gantt
- `@svar-ui/filemanager-locales` - File Manager
- `@svar-ui/grid-locales` - Grid

If you see English fallbacks in a localized UI, the missing terms come from the package's own locale module - merge them in via `Locale words={...}`.

To localize a standalone widget, merge the matching package locale with the core locale:

```svelte
<script>
    import { Gantt } from "@svar-ui/svelte-gantt";
    import { Locale } from "@svar-ui/svelte-core";
    import { cn } from "@svar-ui/gantt-locales";
    import { cn as cnCore } from "@svar-ui/core-locales";
</script>

<Locale words={{ ...cn, ...cnCore }}>
    <Gantt {...settings} />
</Locale>
```

#### Extending Or Overriding Words

`Locale words` accepts a partial pack and extends the current context. Spread an existing pack to keep its formats and override only what you need:

```svelte
<script>
    import { Calendar, Locale } from "@svar-ui/svelte-core";
    import { cn } from "@svar-ui/core-locales";

    const words = {
        ...cn,
        formats: {
            ...cn.formats,
            monthYearFormat: "%Y年%F",
            yearFormat: "%Y年",
        },
    };
</script>

<Locale {words}>
    <Calendar value={new Date(2025, 4, 1)} />
</Locale>
```

Pass `optional={true}` to make merged terms additive fallbacks rather than overrides - useful for layering app-specific strings on top of a full pack.

#### Affected Surfaces

Locale changes calendar labels, date/time formats, modal buttons, pager strings, empty-list text, notice/modal helpers, color-board select text - any widget that displays static strings or formats values reads them through this context.

#### Direct Helper

For non-component code, use the `locale` helper to build a translator:

```js
import { en, locale } from "@svar-ui/svelte-core";

const i18n = locale(en).extend(
    { core: { "Rows per page": "Rows" } },
    true
);
const _ = i18n.getGroup("core");
_("Rows per page"); // "Rows"
```


## File: themes.md

> Source: `themes.md`

### Styling SVAR Svelte Components

All `@svar-ui/svelte-*` widgets share the same theming pipeline. The mechanics live in `@svar-ui/svelte-core`; every other package consumes them.

#### Theme Wrapper

Wrap the part of the app that uses SVAR widgets in a theme component from `@svar-ui/svelte-core`:

```svelte
<script>
    import { Willow } from "@svar-ui/svelte-core";
</script>

<Willow>
    <App />
</Willow>
```

Available themes: `Willow`, `WillowDark`. The wrapper:

- sets the Svelte context `wx-theme`
- renders `.wx-theme.wx-{name}-theme` with `height:100%`
- loads Open Sans + the `wxi` icon CSS by default; pass `fonts={false}` to skip when the host app manages fonts itself

Without a theme wrapper widgets still render but lose theme variables and font/icon CSS.

#### Per-widget Willow / WillowDark themes

Several widgets ship their **own** `Willow` / `WillowDark` components on top of the core base. The widget version wraps the core theme and layers in widget-specific CSS variables (bar colors, grid borders, timescale fonts, etc.). When using such a widget, import the theme from the widget package - not from core - so both layers apply.

Widgets that expose custom `Willow` / `WillowDark` themes:

- `@svar-ui/svelte-core` - base
- `@svar-ui/svelte-gantt`
- `@svar-ui/svelte-grid`
- `@svar-ui/svelte-editor`
- `@svar-ui/svelte-filter`
- `@svar-ui/svelte-filemanager`
- `@svar-ui/svelte-comments`
- `@svar-ui/svelte-kanban`

The widget theme delegates to core and adds extra rules scoped to `.wx-willow-theme` (or `.wx-willow-dark-theme`):

```svelte
<script>
    import { Willow } from "@svar-ui/svelte-core";
    let { fonts = true, children } = $props();
</script>

{#if children}
    <Willow {fonts}>{@render children()}</Willow>
{:else}
    <Willow {fonts} />
{/if}

<style>
    :global(.wx-willow-theme) {
        --wx-gantt-border-color: #e6e6e6;
        --wx-gantt-task-color: #3983eb;
        /* ...widget-specific overrides... */
    }
</style>
```

Mount the widget's own theme once at the app root. The wrapper internally renders the core `Willow`, so a separate core import is not needed:

```svelte
<script>
    import { Willow } from "@svar-ui/svelte-gantt";
    import { Gantt } from "@svar-ui/svelte-gantt";
</script>

<Willow />
<Gantt {...settings} />
```

#### CSS Variables

Theme styling is variable-driven. Override variables on the theme wrapper or on any ancestor of the widgets you want to restyle - overrides cascade to every SVAR widget in the subtree.

```svelte
<Willow>
    <div class="brand">
        <App />
    </div>
</Willow>

<style>
    .brand {
        --wx-color-primary: #0f766e;
        --wx-input-width: 280px;
        --wx-button-border-radius: 4px;
        --wx-calendar-cell-size: 30px;
    }
</style>
```

Nest different wrapper blocks for per-section restyling without forking the theme.

#### `css` Prop Convention

Most widgets accept a `css` prop. The string is appended to the widget's root class, so it works as a parent styling hook:

```svelte
<Toolbar css="my-toolbar" {items} />

<style>
    .my-toolbar {
        padding: 8px 12px;
    }
</style>
```

Composite widgets often expose secondary css props for nested popups (`menuCss` on `Toolbar`/`MenuBar`, etc.). Check the per-component file for the exact set.

#### Class Hooks

The per-component file lists the exact selectors that widget exposes.

#### Custom CSS class overrides

When writing custom rules to override widget styles, always use **at least two selectors** (e.g. `.a .b {}`). Svelte scopes its component styles by appending a hash class which has higher specificity than a plain `.b`. A two-selector rule (`.a .b`) matches or beats that specificity and wins.

Convention: the first selector is a container/wrapper of the widget instance, the second is the inner class you want to alter:

```css
.my-gantt-host .wx-bar-task {
    background: #ff8800;
}
```

#### Override Order

Prefer in this order:

1. **CSS variables on a wrapper** - propagates consistently to every widget in the subtree.
2. **`css` prop class** - a stable parent hook that survives internal markup changes.
3. **Direct `.wx-*` selectors** - targeted overrides; tightest coupling to widget internals, use sparingly.

#### Core Vars

##### Base Colors

| Variable | Default | Use for |
|---|---|---|
| `--wx-color-primary` | `#37a9ef` | Primary accent - active states, selected items, links |
| `--wx-color-primary-selected` | `#d5eaf7` | Selected/highlighted row or item background |
| `--wx-color-primary-font` | `#fff` | Text on primary-colored backgrounds |
| `--wx-color-secondary` | `transparent` | Secondary/ghost element background |
| `--wx-color-secondary-hover` | `rgba(55, 169, 239, 0.12)` | Secondary hover background |
| `--wx-color-secondary-font` | `#37a9ef` | Secondary element text |
| `--wx-color-secondary-border` | `#37a9ef` | Secondary element border |
| `--wx-color-success` | `#77d257` | Success indicator |
| `--wx-color-warning` | `#fcba2e` | Warning indicator |
| `--wx-color-info` | `#37a9ef` | Info indicator |
| `--wx-color-danger` | `#fe6158` | Error/destructive state, error borders |
| `--wx-color-disabled` | `#f2f3f7` | Disabled element background |
| `--wx-color-disabled-alt` | `#e9e9e9` | Alternate disabled background |
| `--wx-color-font` | `#2c2f3c` | Primary text |
| `--wx-color-font-alt` | `#9fa1ae` | Secondary/muted text, placeholders |
| `--wx-color-font-disabled` | `#c0c3ce` | Disabled text |
| `--wx-color-link` | `#37a9ef` | Link text |
| `--wx-background` | `#ffffff` | Main surface |
| `--wx-background-alt` | `#f2f3f7` | Alternate surface (cards, tags, odd/even areas) |
| `--wx-background-hover` | `#eaedf5` | Hover state background |

##### Typography

| Variable | Default | Use for |
|---|---|---|
| `--wx-font-family` | `"Open Sans", Arial, Helvetica, sans-serif` | All text |
| `--wx-font-size` | `14px` | Body text |
| `--wx-line-height` | `20px` | Body line height |
| `--wx-font-size-md` | `14px` | Medium text |
| `--wx-line-height-md` | `24px` | Medium line height |
| `--wx-font-size-hd` | `16px` | Headings |
| `--wx-line-height-hd` | `30px` | Heading line height |
| `--wx-font-size-sm` | `12px` | Captions, small text |
| `--wx-line-height-sm` | `16px` | Small line height |
| `--wx-font-weight` | `400` | Normal weight |
| `--wx-font-weight-md` | `600` | Semi-bold (labels, buttons) |
| `--wx-font-weight-b` | `700` | Bold (modal headers) |

##### Icons

| Variable | Default | Use for |
|---|---|---|
| `--wx-icon-color` | `#9fa1ae` | Default icon tint |
| `--wx-icon-size` | `20px` | Icon dimensions |
| `--wx-icon-border-radius` | `2px` | Icon hover-state rounding |

##### Borders, Shadows, Spacing

| Variable | Default | Use for |
|---|---|---|
| `--wx-border` | `1px solid #e6e6e6` | Standard border |
| `--wx-border-radius` | `3px` | Default corner radius |
| `--wx-radius-major` | `6px` | Larger radius (cards, panels) |
| `--wx-border-light` | `none` | Subtle divider |
| `--wx-border-medium` | `1px solid #eaedf5` | Medium divider |
| `--wx-shadow-light` | `0px 3px 10px ...` | Elevated panels (popups, dropdowns) |
| `--wx-shadow-medium` | `0px 4px 20px ...` | High-elevation surfaces (modals) |
| `--wx-padding` | `8px` | Base spacing unit |

##### Layout

| Variable | Default | Use for |
|---|---|---|
| `--wx-field-gutter` | `16px` | Vertical gap between form rows |
| `--wx-field-width` | `400px` | Max width of a form field row |

##### Z-index Scale

| Layer | Value |
|---|---|
| Popups / dropdowns | `100` |
| Modals | `1000` |
| Notices / toasts | `1010` |
