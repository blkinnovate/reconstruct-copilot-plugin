# Reconstruct — GitHub Copilot plugin (releases)

This repository hosts the **`reconstruct`** [Agent plugin](https://code.visualstudio.com/docs/copilot/customization/agent-plugins) for VS Code ([`plugins/reconstruct/`](./plugins/reconstruct/)) and a small [`.github/plugin/marketplace.json`](./.github/plugin/marketplace.json) catalog for optional **GitHub Copilot CLI** use.

## Users — VS Code (recommended)

From [reconstruct-cli](https://github.com/blkinnovate/reconstruct/tree/main/reconstruct-cli), after **`reconstruct auth login`**:

```bash
reconstruct install --assistant copilot
```

That copies the bundled plugin to **`~/.reconstruct/vscode-copilot-plugin`**, writes **`.mcp.json`**, and registers the folder in VS Code **`chat.pluginLocations`**. Reload VS Code.

Alternatively: add **`blkinnovate/reconstruct-copilot-plugin`** to **`chat.plugins.marketplaces`**, or **Chat: Install Plugin From Source** with this repo — then add **`.mcp.json`** from **`.mcp.json.example`** with your **`mcp_…`** key.

## Users — Copilot CLI (optional)

If you use the terminal **Copilot CLI** (`copilot` on PATH):

1. **`copilot plugin marketplace add blkinnovate/reconstruct-copilot-plugin`**
2. **`copilot plugin install reconstruct@reconstruct-plugins`**

Docs: [Finding and installing plugins for GitHub Copilot CLI](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/plugins-finding-installing).

## Maintainers — sync from the main repo

The canonical bundled copy used by **`reconstruct-cli`** lives in the monorepo at **`reconstruct-cli/bundled/reconstruct-copilot-plugin/`**. Before tagging a release here, sync that tree into **`plugins/reconstruct/`** (replace contents) so the marketplace and the CLI bundle stay aligned.

```bash
# From the reconstruct monorepo root
rm -rf reconstruct-copilot-plugin/plugins/reconstruct
cp -R reconstruct-cli/bundled/reconstruct-copilot-plugin reconstruct-copilot-plugin/plugins/reconstruct
```

Then commit, tag, and push this repository.

## Marketplace id

- **Marketplace name:** `reconstruct-plugins`
- **Plugin install spec:** `reconstruct@reconstruct-plugins`
