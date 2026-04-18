# Reconstruct — GitHub Copilot plugin (releases)

This repository hosts the **`reconstruct`** [Agent plugin](https://code.visualstudio.com/docs/copilot/customization/agent-plugins) for VS Code ([`plugins/reconstruct/`](./plugins/reconstruct/)) and a small [`.github/plugin/marketplace.json`](./.github/plugin/marketplace.json) catalog for optional **GitHub Copilot CLI** use.

## Users — VS Code (recommended)

Use **this** repository for VS Code Agent plugins — not [reconstruct-claude-plugin](https://github.com/blkinnovate/reconstruct-claude-plugin) (that layout is for Claude Code’s marketplace only).

**Prerequisites:** Agent plugins are [in preview](https://code.visualstudio.com/docs/copilot/customization/agent-plugins); ensure **`chat.plugins.enabled`** is on (your org may manage this).

1. **`reconstruct install --assistant copilot`** (after [`reconstruct auth login`](https://github.com/blkinnovate/reconstruct/blob/main/docs/cli-auth-install.md)) — copies the bundled plugin to `~/.reconstruct/vscode-copilot-plugin`, writes **`.mcp.json`**, and registers **`chat.pluginLocations`**. Reload VS Code.

2. **Marketplace:** Add **`blkinnovate/reconstruct-copilot-plugin`** to VS Code **`chat.plugins.marketplaces`**, open **Extensions** → search **`@agentPlugins`**, install **reconstruct**, then add **`.mcp.json`** at the **plugin root** for that install (copy from **[`plugins/reconstruct/.mcp.json.example`](./plugins/reconstruct/.mcp.json.example)**) with your Reconstruct **`mcp_…`** key.

3. **Install from Git:** Run **Chat: Install Plugin From Source** and enter the repo URL, e.g. **`https://github.com/blkinnovate/reconstruct-copilot-plugin.git`**. VS Code clones the repository and loads the root **`plugin.json`**, which points at **`plugins/reconstruct/`** for skills and MCP. Copy **`plugins/reconstruct/.mcp.json.example`** to **`plugins/reconstruct/.mcp.json`** and add your key.

4. **Local checkout:** Register the folder in **`chat.pluginLocations`**. You can use the repo root (uses root **`plugin.json`**) or only **`plugins/reconstruct/`** (uses the nested **`plugin.json`**). Add **`.mcp.json`** next to the **`plugin.json`** you are using (`plugins/reconstruct/.mcp.json` in both cases).

After install, reload VS Code. Mint an MCP API key from the Reconstruct app (**Settings → MCP keys**) if you do not already have one.

See also: [docs/cli-auth-install.md](https://github.com/blkinnovate/reconstruct/blob/main/docs/cli-auth-install.md) for **`reconstruct auth login`** and MCP overview (Copilot-specific automation may be added in a future CLI release).

## Users — Copilot CLI (optional)

If you use the terminal **Copilot CLI** (`copilot` on PATH):

1. **`copilot plugin marketplace add blkinnovate/reconstruct-copilot-plugin`**
2. **`copilot plugin install reconstruct@reconstruct-plugins`**

Docs: [Finding and installing plugins for GitHub Copilot CLI](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/plugins-finding-installing).

## Maintainers — sync from the main repo

The canonical bundled copy used by **`reconstruct-cli`** lives in the monorepo at **`reconstruct-cli/bundled/reconstruct-copilot-plugin/`**. Before tagging a release here, sync that tree into **`plugins/reconstruct/`** (replace contents) so the marketplace and the CLI bundle stay aligned.

**VS Code “Install from Git”** resolves **`plugin.json`** at the [repository root](https://code.visualstudio.com/docs/copilot/customization/agent-plugins#_cross-tool-compatibility) first. This repo keeps **root `plugin.json`** (paths into **`plugins/reconstruct/`**) so a full clone works; do not delete it when syncing the nested folder.

```bash
# From the reconstruct monorepo root
rm -rf reconstruct-copilot-plugin/plugins/reconstruct
cp -R reconstruct-cli/bundled/reconstruct-copilot-plugin reconstruct-copilot-plugin/plugins/reconstruct
# Keep version/description in root plugin.json aligned with plugins/reconstruct/plugin.json when you bump releases
```

Then commit, tag, and push this repository.

## Marketplace id

- **Marketplace name:** `reconstruct-plugins`
- **Plugin install spec:** `reconstruct@reconstruct-plugins`
