# Setup and CLI

## Use the minimum command that satisfies scope

- Use `create` to scaffold a new app.
- Use `init` to attach assistant-ui to an existing app.
- Use `add` to install or refresh specific components.
- Use `update`, `upgrade`, and `codemod` only for dependency or API migrations.

## Bootstrap flows

### New project

```bash
npx assistant-ui@latest create my-app
cd my-app
```

Common template variants:

```bash
npx assistant-ui@latest create my-app -t cloud
npx assistant-ui@latest create my-app -t langgraph
npx assistant-ui@latest create my-app -t mcp
```

### Existing project

```bash
npx assistant-ui@latest init
npx assistant-ui@latest add thread
```

Add multi-thread UI when needed:

```bash
npx assistant-ui@latest add thread-list
```

## Component operations

- Add one or more components:

```bash
npx assistant-ui@latest add thread assistant-modal
```

- Overwrite existing generated files only when intentional:

```bash
npx assistant-ui@latest add thread --overwrite
```

## Safe upgrade workflow

1. Preview package changes.
2. Run upgrade migration.
3. Run specific codemod if needed.
4. Re-test runtime and tool rendering.

```bash
npx assistant-ui@latest update --dry
npx assistant-ui@latest update
npx assistant-ui@latest upgrade
npx assistant-ui@latest codemod v0-11/content-part-to-message-part ./src
```

## Optional MCP docs server install

```bash
npx assistant-ui@latest mcp --cursor
```

Supported flags include IDE-specific installs such as `--cursor`, `--vscode`, and `--claude-code`.

## Source pointers

- `docs/libaries/assistant-ui-docs.md`
- `https://github.com/assistant-ui/assistant-ui/blob/main/apps/docs/content/docs/(docs)/llm.mdx`
