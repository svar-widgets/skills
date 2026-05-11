# SVAR Skills

Skills and LLM context packs for [SVAR UI components](https://svar.dev) — Vue, Svelte, and React.

This repo gives an AI agent (Claude Code, Cursor, or any LLM that can read local files) the knowledge gists that it needs to write correct SVAR widget code on the first try.

## What's inside

- `svar-vue/` — skill for `@svar-ui/vue-*` packages
- `svar-svelte/` — skill for `@svar-ui/svelte-*` packages
- `svar-react/` — skill for `@svar-ui/react-*` packages
- `guides/` — flat per-package context files for any LLM or agent

## Use skill

### SVAR for React

```bash
npx skills add svar-widgets/skills --skill svar-react
```

### SVAR for Svelte


```bash
npx skills add svar-widgets/skills --skill svar-svelte
```

### SVAR for Vue


```bash
npx skills add svar-widgets/skills --skill svar-vue
```
### Manual installation

You can clone the repo copy the framework folder that you need into your skills directory:

```sh
cp -r svar-vue ~/.claude/skills/
```

## Use as raw context (`guides/`)

The `guides/` folder holds pre-bundled markdown files for agents that don't support skills, or for one-shot prompts:

- `svar-<framework>-<package>.md` — single package (e.g. `svar-vue-grid.md`)
- `svar-<framework>-all.md` — every package for the framework, in one file

Drop the file into your prompt, attach it to a Cursor rule, paste it into a ChatGPT conversation, or feed it to any tool that accepts file context.

## Frameworks

| React | Svelte | Vue |
| --- | --- | --- |
| [all components](guides/svar-react-all.md) (279kb; ~77k tokens) | [all components](guides/svar-svelte-all.md) (263kb; ~73k tokens) | [all components](guides/svar-vue-all.md) (275kb; ~76k tokens) |
| [comments](guides/svar-react-comments.md) (20kb; ~5.6k tokens) | [comments](guides/svar-svelte-comments.md) (19kb; ~5.4k tokens) | [comments](guides/svar-vue-comments.md) (20kb; ~5.6k tokens) |
| [core](guides/svar-react-core.md) (107kb; ~30k tokens) | [core](guides/svar-svelte-core.md) (101kb; ~28k tokens) | [core](guides/svar-vue-core.md) (105kb; ~29k tokens) |
| [editor](guides/svar-react-editor.md) (28kb; ~7.6k tokens) | [editor](guides/svar-svelte-editor.md) (26kb; ~7.3k tokens) | [editor](guides/svar-vue-editor.md) (27kb; ~7.5k tokens) |
| [filemanager](guides/svar-react-filemanager.md) (33kb; ~9k tokens) | [filemanager](guides/svar-svelte-filemanager.md) (32kb; ~8.7k tokens) | [filemanager](guides/svar-vue-filemanager.md) (32kb; ~8.9k tokens) |
| [filter](guides/svar-react-filter.md) (49kb; ~13k tokens) | [filter](guides/svar-svelte-filter.md) (47kb; ~13k tokens) | [filter](guides/svar-vue-filter.md) (49kb; ~13k tokens) |
| [gantt](guides/svar-react-gantt.md) (38kb; ~10k tokens) | [gantt](guides/svar-svelte-gantt.md) (36kb; ~9.9k tokens) | [gantt](guides/svar-vue-gantt.md) (37kb; ~10k tokens) |
| [grid](guides/svar-react-grid.md) (37kb; ~10k tokens) | [grid](guides/svar-svelte-grid.md) (35kb; ~9.8k tokens) | [grid](guides/svar-vue-grid.md) (37kb; ~10k tokens) |
| [layout](guides/svar-react-layout.md) (19kb; ~5.3k tokens) | [layout](guides/svar-svelte-layout.md) (18kb; ~5k tokens) | [layout](guides/svar-vue-layout.md) (19kb; ~5.2k tokens) |
| [menu](guides/svar-react-menu.md) (21kb; ~5.9k tokens) | [menu](guides/svar-svelte-menu.md) (20kb; ~5.6k tokens) | [menu](guides/svar-vue-menu.md) (21kb; ~5.8k tokens) |
| [tasklist](guides/svar-react-tasklist.md) (16kb; ~4.4k tokens) | [tasklist](guides/svar-svelte-tasklist.md) (15kb; ~4.2k tokens) | [tasklist](guides/svar-vue-tasklist.md) (16kb; ~4.3k tokens) |
| [toolbar](guides/svar-react-toolbar.md) (21kb; ~5.8k tokens) | [toolbar](guides/svar-svelte-toolbar.md) (20kb; ~5.6k tokens) | [toolbar](guides/svar-vue-toolbar.md) (21kb; ~5.8k tokens) |

## Links

- [SVAR widget docs](https://docs.svar.dev/)
- [SVAR on GitHub](https://github.com/svar-widgets)

## License

MIT
