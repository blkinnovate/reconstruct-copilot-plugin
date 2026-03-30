# Reconstruct — GitHub Copilot plugin (releases)

This repository is the **GitHub Copilot CLI plugin marketplace** for Reconstruct: a small catalog ([`.github/plugin/marketplace.json`](./.github/plugin/marketplace.json)) plus the **`reconstruct`** plugin under [`plugins/reconstruct/`](./plugins/reconstruct/).

## Users — Copilot CLI

1. **`copilot plugin marketplace add blkinnovate/reconstruct-copilot-plugin`**
2. **`copilot plugin install reconstruct@reconstruct-plugins`**

Or use **`reconstruct install --assistant copilot`** from [reconstruct-cli](https://github.com/blkinnovate/reconstruct/tree/main/reconstruct-cli), which runs the same flow and writes your **`.mcp.json`** credentials into the plugin install path.

Docs: [Finding and installing plugins for GitHub Copilot CLI](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/plugins-finding-installing).

## Users — VS Code Agent plugins (Preview)

The same **`plugins/reconstruct/`** tree includes a root **`plugin.json`** for [Agent plugins in VS Code](https://code.visualstudio.com/docs/copilot/customization/agent-plugins). Add **`blkinnovate/reconstruct-copilot-plugin`** to **`chat.plugins.marketplaces`**, or use **Chat: Install Plugin From Source** with this repo URL. Copy **`.mcp.json.example`** to **`.mcp.json`** in the installed plugin directory and add your **`mcp_…`** key.

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
