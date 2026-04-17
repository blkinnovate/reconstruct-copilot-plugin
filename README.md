# Reconstruct — GitHub Copilot plugin (releases)

This repository hosts the **`reconstruct`** [Agent plugin](https://code.visualstudio.com/docs/copilot/customization/agent-plugins) for VS Code ([`plugins/reconstruct/`](./plugins/reconstruct/)) and a small [`.github/plugin/marketplace.json`](./.github/plugin/marketplace.json) catalog for optional **GitHub Copilot CLI** use.

## Users — VS Code (recommended)

**`reconstruct install` does not register GitHub Copilot yet** (the CLI currently wires **Cursor** and **Claude Code** only). Use one of the following:

1. Add **`blkinnovate/reconstruct-copilot-plugin`** to VS Code **`chat.plugins.marketplaces`**, install the **reconstruct** plugin from the marketplace, then add **`.mcp.json`** at the plugin root (start from **`.mcp.json.example`**) with your Reconstruct **`mcp_…`** key.
2. Or run **Chat: Install Plugin From Source** and select the **`plugins/reconstruct/`** folder from this repo — then add **`.mcp.json`** as above.

After install, reload VS Code. Mint an MCP API key from the Reconstruct app (**Settings → MCP keys**) if you do not already have one.

See also: [docs/cli-auth-install.md](https://github.com/blkinnovate/reconstruct/blob/main/docs/cli-auth-install.md) for **`reconstruct auth login`** and MCP overview (Copilot-specific automation may be added in a future CLI release).

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
