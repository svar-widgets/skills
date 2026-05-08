Use when building, configuring, styling, or modifying SVAR React Filemanager / @svar-ui/react-filemanager components, menus, themes, store actions, or backend data provider integration.

## Package

```js
import {
	Filemanager,
	Willow,
	WillowDark,
	getMenuOptions,
} from "@svar-ui/react-filemanager";
import "@svar-ui/react-filemanager/all.css";
```

## Supported functionality

### Components and themes

- `Filemanager` renders the full file explorer: toolbar, search, sidebar tree, cards/table/panels views, preview/info panel, context/action menus, upload drop area, and modals.
- `Willow`, and `WillowDark` wrap matching `@svar-ui/react-core` themes and add filemanager CSS variables.
- Theme components accept `fonts?: boolean` and optional React children.
- `Filemanager` has no `children`, `class`, `style`, or `css` passthrough prop.

### Data model

- `data` is a flat `IEntity[]`; each item must have path-like `id`, such as `"/Code/Button.js"`.
- Root `"/"` is generated internally as a folder named `"My files"`.
- `FileTree.parseId` derives `parent`, `name`, and `ext` from `id`; missing `type` defaults to `"file"`.
- Folder items are the only records rendered in the sidebar tree.
- `date` is expected as a `Date` object for built-in formatting.
- `lazy: true` on a folder triggers `request-data` when the folder path is opened.
- Duplicate create/copy names are made unique by appending `.new` before the extension, for example `"/file.new.txt"`.
- `drive` is optional and only renders storage info when both `used` and `total` are present.

### Modes and layout

- `mode` supports `"cards"`, `"table"`, `"panels"`, and `"search"`.
- Toolbar mode buttons only expose `"table"`, `"cards"`, and `"panels"`.
- Search runs `filter-files`; non-empty text switches to `"search"` mode and clearing text restores previous `mode` and `panels`.
- `preview` toggles the info pane; on containers narrower than `768px`, preview uses a narrow full-content layout.
- `panels` accepts partial panel state; common fields are `path` and `selected`.
- `activePanel` is `0` or `1` and is used in panels mode and upload drop handling.

### API and events

- Use `init(api)` for first-time API setup; it is called once after initial store setup.
- `ref={apiRef}` exposes the same public methods: `exec`, `on`, `intercept`, `detach`, `setNext`, `getState`, `getReactiveState`, `getStores`, `getFile`, and `serialize`.
- Component event props are generated from store action names by removing hyphens and prefixing `on` (camelCase in React), for example `onRequestData`, `onDownloadFile`, `onOpenFile`, `onCreateFile`.
- Event callback payloads are the same objects passed to `api.exec(action, payload)`.
- Action flow is store first, then component event props, then any next bus set by `api.setNext(...)`.
- `api.intercept(action, callback)` can cancel or replace built-in behavior by returning `false`, as shown by backend filtering demos.
- The store mutates some action payloads before downstream handlers/providers: `rename-file.newId`, `create-file.newId`, `copy-files.newIds`, `move-files.newIds`, and `skipProvider` when copy/move into self is rejected.

### Built-in actions

- Selection/navigation: `select-file`, `set-path`, `set-active-panel`, `open-tree-folder`.
- View/search/sort: `show-preview`, `filter-files`, `set-mode`, `sort-files`.
- File operations: `create-file`, `rename-file`, `delete-files`, `copy-files`, `move-files`.
- Backend/user hooks: `request-data`, `provide-data`, `download-file`, `open-file`.
- Hotkeys use the current `menuOptions` result, so removed menu items also remove their default hotkey behavior.
- Built-in hotkeys include `Ctrl/Cmd+C`, `Ctrl/Cmd+X`, `Ctrl/Cmd+V`, `Ctrl/Cmd+R`, `Ctrl/Cmd+D`, `Delete`, `Enter`, and arrow navigation with Ctrl/Cmd or Shift selection modifiers.

### Menus

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

### Icons, previews, and info

- `icons(file, size)` is used for image URLs in cards/table/info; `size` is `"big"` or `"small"`.
- `icons="simple"` is supported by source and demos and disables image icon URLs, falling back to icon font classes.
- Default icons use `https://cdn.svar.dev/icons/filemanager/vivid/${size}/${icon}.svg`.
- `previews(file, width, height)` is used for card thumbnails and info preview; return a URL string or a falsy value.
- `extraInfo(file)` runs for a single selected item in the info pane; it may return an object, a promise, or null.
- Extra info object entries are appended to the info grid as name/value rows.

### Saving

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

## Public Types

```ts
import type { ComponentType, ReactNode } from "react";
import type { IMenuOption } from "@svar-ui/react-menu";

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

export declare const Filemanager: ComponentType<
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

export declare const Willow: ComponentType<{
	fonts?: boolean;
	children?: ReactNode;
}>;

export declare const WillowDark: ComponentType<{
	fonts?: boolean;
	children?: ReactNode;
}>;

/* get component events from store actions*/
type RemoveHyphen<S extends string> = S extends `${infer Head}-${infer Tail}`
	? `${Head}${Capitalize<RemoveHyphen<Tail>>}`
	: S;

type EventName<K extends string> = `on${Capitalize<RemoveHyphen<K>>}`;

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

## Styling

Import the package CSS before using the component (`all.css` includes dependency styles, `style.css` is this component only)

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
- Menu popups come from `@svar-ui/react-menu` and use `.wx-menu`, `.wx-option`, `.wx-separator`, `.wx-subtext`, and related menu hooks; the popup is portaled outside the filemanager layout.
- Several classes are generic (`.wx-list`, `.wx-item`, `.wx-wrapper`, `.wx-name`); always scope selectors from a wrapper or a more specific filemanager section.

```jsx
import "./FmShell.css";

<div className="filemanager">
	<Filemanager data={data} drive={drive} />
</div>

/* FmShell.css
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
*/
```

## Recipes

### Basic Filemanager

```jsx
import { Filemanager, Willow } from "@svar-ui/react-filemanager";

function BasicFm() {
	const data = [
		{ id: "/Code", type: "folder", date: new Date(2023, 11, 2, 17, 25) },
		{ id: "/Code/Button.js", type: "file", size: 1177, date: new Date() },
	];

	const drive = {
		used: 15200000000,
		total: 50000000000,
	};

	return (
		<Willow>
			<Filemanager data={data} drive={drive} />
		</Willow>
	);
}
```

### Initial Mode, Path, Selection, And Preview

```jsx
import { Filemanager } from "@svar-ui/react-filemanager";

function InitialFm() {
	const panels = [
		{ path: "/Code", selected: ["/Code/Button.js"] },
		{ path: "/", selected: ["/Music"] },
	];

	return (
		<Filemanager
			data={data}
			drive={drive}
			mode="panels"
			panels={panels}
			activePanel={0}
			preview
		/>
	);
}
```

### Handle API And Component Events

```jsx
import { useRef, useState } from "react";
import { Filemanager } from "@svar-ui/react-filemanager";

function ApiFm() {
	const apiRef = useRef(null);
	const [saved, setSaved] = useState([]);

	function init(fm) {
		apiRef.current = fm;

		fm.on("download-file", ({ id }) => {
			window.open(`/download?id=${encodeURIComponent(id)}`, "_self");
		});

		fm.on("open-file", ({ id }) => {
			window.open(`/direct?id=${encodeURIComponent(id)}`, "_blank");
		});
	}

	function serializeCode() {
		setSaved(apiRef.current.serialize("/Code"));
		apiRef.current.exec("provide-data", { id: "/Code", data: [] });
	}

	function loadLazy({ id }) {
		fetch(`/files/${encodeURIComponent(id)}`)
			.then(res => res.json())
			.then(data => apiRef.current.exec("provide-data", { id, data }));
	}

	return (
		<>
			<button onClick={serializeCode}>Serialize /Code</button>

			<Filemanager
				ref={apiRef}
				init={init}
				data={data}
				drive={drive}
				onRequestData={loadLazy}
			/>
		</>
	);
}
```

### Customize Context Menus

```jsx
import { useRef } from "react";
import { Filemanager, getMenuOptions } from "@svar-ui/react-filemanager";

function CustomMenusFm() {
	const apiRef = useRef(null);

	function init(fm) {
		apiRef.current = fm;
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
						const { panels, activePanel } = apiRef.current.getState();
						apiRef.current.exec("copy-files", {
							ids: [context.id],
							target: panels[activePanel].path,
						});
					},
				},
			];
		}

		return getMenuOptions(mode);
	}

	return <Filemanager data={data} drive={drive} init={init} menuOptions={menuOptions} />;
}
```

### Use Server Data And RestDataProvider

```jsx
import { useEffect, useRef, useState } from "react";
import { Filemanager } from "@svar-ui/react-filemanager";
import { RestDataProvider } from "@svar-ui/filemanager-data-provider";

function ServerFm() {
	const server = "https://example.com/api";
	const provider = new RestDataProvider(server);

	const apiRef = useRef(null);
	const [data, setData] = useState([]);
	const [drive, setDrive] = useState({});

	function init(fm) {
		apiRef.current = fm;
		fm.setNext(provider);

		fm.on("download-file", ({ id }) => {
			window.open(`${server}/direct?id=${encodeURIComponent(id)}&download=true`, "_self");
		});

		fm.on("open-file", ({ id }) => {
			window.open(`${server}/direct?id=${encodeURIComponent(id)}`, "_blank");
		});
	}

	function loadData({ id }) {
		provider.loadFiles(id).then(files => {
			apiRef.current.exec("provide-data", { id, data: files });
		});
	}

	useEffect(() => {
		provider.on("file-renamed", ({ id, newId }) => {
			const name = newId.slice(newId.lastIndexOf("/") + 1);
			apiRef.current.exec("rename-file", { id, name, skipProvider: true });
		});

		Promise.all([provider.loadFiles(), provider.loadInfo()]).then(([files, info]) => {
			setData(files);
			setDrive(info);
		});
	}, []);

	return <Filemanager init={init} data={data} drive={drive} onRequestData={loadData} />;
}
```

### Custom Icons, Previews, And Extra Info

```jsx
import { Filemanager } from "@svar-ui/react-filemanager";
import { formatSize } from "@svar-ui/filemanager-store";

function CustomVisualsFm() {
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

	return <Filemanager data={data} drive={drive} icons={icons} previews={previews} extraInfo={extraInfo} preview />;
}
```

### Backend Search Intercept

```jsx
import { useRef } from "react";
import { Filemanager } from "@svar-ui/react-filemanager";

function SearchInterceptFm() {
	const apiRef = useRef(null);

	function init(fm) {
		apiRef.current = fm;

		fm.intercept("filter-files", ({ text }) => {
			const { panels, activePanel } = fm.getState();
			const id = panels[activePanel].path;

			fetch(`/files/${encodeURIComponent(id)}?text=${text || ""}`)
				.then(res => res.json())
				.then(data => {
					fm.exec("set-mode", { mode: text ? "search" : "cards" });
					fm.exec("provide-data", { id, data });
				});

			return false;
		});
	}

	return <Filemanager init={init} data={data} drive={drive} />;
}
```

### Localize Filemanager

```jsx
import { Locale } from "@svar-ui/react-core";
import { cn } from "@svar-ui/filemanager-locales";
import { cn as cnCore } from "@svar-ui/core-locales";
import { Filemanager } from "@svar-ui/react-filemanager";

function LocalizedFm() {
	return (
		<Locale words={{ ...cn, ...cnCore }}>
			<Filemanager data={data} drive={drive} />
		</Locale>
	);
}
```

## Implementation Notes

- `Filemanager` stores all unknown props in `restProps` for generated action callbacks; unknown props are not spread onto DOM.
- Source supports `icons="simple"`, but the declaration types `icons` only as a function.
- Source default `icons` can return `false` for folders, but the declaration says `string`.
- Source accepts falsy `previews` return values, but the declaration says `string | null`.
- `menuOptions` can suppress menus with falsy returns, but the declaration says it returns `IFileMenuOption[]`.
- Store source `IMenuOption.id` is `string | number`, while generated `store/dist/types/types.d.ts` has `id?: string`.
- `RestDataProvider.loadFiles()` and `loadInfo()` are called without arguments in demos, but generated provider declarations require `id: TID`.
- `DataStore` mutates the input file objects during parse by adding `parent`, `name`, `ext`, default `type`, and tree state fields.
- Context/action menus and tests rely on ids encoded by `setID`; use raw file ids in app code and let the library set data attributes.
- `registerMenuItem("upload", UploadButton)` runs inside `Sidebar`; a custom `"upload"` add item only works through the built-in sidebar add menu.
- `extraInfo` errors are caught and logged, then ignored.
- In readonly mode, hotkeys use readonly menu options, so edit hotkeys do not open modals.
