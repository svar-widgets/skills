# SVAR Skills

Skills and LLM context packs for [SVAR](https://svar.dev) UI widgets — Vue, Svelte, and React.

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

| Framework | Skill folder    | Bundled guide              |
| --------- | --------------- | -------------------------- |
| Vue 3     | `svar-vue/`     | `guides/svar-vue-all.md`    |
| Svelte 5  | `svar-svelte/`  | `guides/svar-svelte-all.md` |
| React     | `svar-react/`   | `guides/svar-react-all.md`  |

## Links

- [SVAR widget docs](https://docs.svar.dev/)
- [SVAR on GitHub](https://github.com/svar-widgets)

## License

MIT
