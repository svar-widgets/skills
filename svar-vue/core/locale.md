# SVAR Vue Core Locale

Package: `@svar-ui/vue-core`

## Package

```js
import { Locale, locale, en } from "@svar-ui/vue-core";
```

For all bundled language packs, import from `@svar-ui/core-locales`:

```js
import { en, cn, de, es, fr, it, ja, pt, ru } from "@svar-ui/core-locales";
```

## Supported Functionality

- `Locale` reads Vue inject key `wx-i18n`.
- If no locale context exists, it creates one from English words.
- If `words` is not `null`, it extends the current locale with `words`.
- `optional` is passed to the locale `extend` call.
- Use `Locale` around the smallest subtree that needs different words or formats.
- Locale affects calendar labels, date/time formats, modal buttons, pager labels, empty-list text, notices/modal helper strings, and color board select text.
- `locale` is re-exported in JS from `@svar-ui/lib-dom`.
- `en` is re-exported in JS from `@svar-ui/core-locales`.

## Public Types

```ts
import type { Component } from "vue";

export declare const Locale: Component<{
	words?: any;
	optional?: boolean;
	children?: () => any;
}>;

export type { ILocale, Terms, TPosition } from "@svar-ui/lib-dom";
```

## Styling

- `Locale` does not render a wrapper element or public classes.
- It only changes locale context for children.
- Styling changes that depend on locale direction or content length must be handled by app CSS or theme variables.

## Recipes

### Localize A Calendar Subtree

```vue
<script setup>
import { Calendar, Locale } from "@svar-ui/vue-core";
import { de } from "@svar-ui/core-locales";
</script>

<template>
  <Locale :words="de">
    <Calendar :value="new Date(2025, 4, 1)" />
  </Locale>
</template>
```

### Override Date Formats

```vue
<script setup>
import { Calendar, Locale } from "@svar-ui/vue-core";
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

<template>
  <Locale :words="words">
    <Calendar :value="new Date(2025, 4, 1)" />
  </Locale>
</template>
```

### Use The Locale Helper Directly

```vue
<script setup>
import { en, locale } from "@svar-ui/vue-core";

const i18n = locale(en).extend(
	{
		core: {
			"Rows per page": "Rows",
		},
	},
	true
);
const _ = i18n.getGroup("core");
</script>

<template>
  <span>{{ _("Rows per page") }}</span>
</template>
```

## Implementation Notes

- `Locale` renders only `children`; it has no DOM wrapper.

## Other information

extra details about locales can be obtained from `../locales.md`
