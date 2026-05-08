# SVAR React Core Pager

Package: `@svar-ui/react-core`

## Package

```js
import { Pager } from "@svar-ui/react-core";
```

## Supported Functionality

- Pagination control with rows-per-page input, page navigation icons, current page input, and total page count.
- `value` is the current page; default is `1`. Pair with `onChange` to keep state in sync.
- `pageSize` is controlled; default is `20`.
- `pageCount` is `Math.ceil(total / pageSize)`.
- `from` is the zero-based row offset: `(value - 1) * pageSize`.
- `to` is capped by `total`: `Math.min(value * pageSize, total)`.
- Page navigation emits `{ value, from, to }` after updating the bound page.
- Labels come from locale group `core`.

## Public Types

```ts
import type { FC } from "react";

export declare const Pager: FC<{
	total?: number;
	pageSize?: number;
	value?: number;
	onChange?: (ev: { value: number; from: number; to: number }) => void;
}>;
```

## Styling

- Wrapper: `.wx-pager`
- Sections: `.wx-left`, `.wx-center`, `.wx-right`
- Navigation icons: `.wx-icon`, icon font classes `wxi-angle-dbl-left`, `wxi-angle-left`, `wxi-angle-right`, `wxi-angle-dbl-right`
- Disabled icons: `.wx-disabled`
- Inputs use local `input` styles inside the component.

```jsx
<div className="grid-footer">
	<Pager total={100} />
</div>
```

```css
.grid-footer .wx-pager {
	justify-content: flex-end;
}
```

## Recipes

### Bound Page And Page Size

```jsx
import { useState } from "react";
import { Pager } from "@svar-ui/react-core";

function Example() {
	const [page, setPage] = useState(2);
	const [pageSize, setPageSize] = useState(10);

	return (
		<Pager
			total={100}
			value={page}
			pageSize={pageSize}
			onChange={ev => {
				setPage(ev.value);
				console.log(ev.value, ev.from, ev.to);
			}}
		/>
	);
}
```

## Implementation Notes

- Page-size input calls `onChange` with `value` equal to the entered page size, not the active page.
- Page navigation calls `onChange` with `value` equal to the active page.
- Current-page input rejects values below `1`, above `pageCount`, or `NaN`.
