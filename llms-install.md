# Installing the ShortSync MCP server (for AI agents)

ShortSync is a **hosted remote MCP server**. There is nothing to clone, build or run, and no API key to ask the user for.

- Do **not** clone this repository.
- Do **not** create or edit files in the user's current project.
- Only add one entry to your own MCP client settings.

## Cline

Easiest: in Cline open **MCP Servers** (Customize → MCP) → **Add Remote Server**, name `shortsync`, URL `https://www.shortsync.app/api/mcp`, transport **Streamable HTTP**.

To edit the file instead, open it with **Edit Configuration** on that same screen so you change the file Cline actually loads. In current Cline versions it is `~/.cline/data/settings/cline_mcp_settings.json` (Windows: `%USERPROFILE%\.cline\data\settings\cline_mcp_settings.json`). Older versions used `globalStorage/saoudrizwan.claude-dev/settings/cline_mcp_settings.json` inside the VS Code user folder; newer versions ignore that file. Add:

```json
{
  "mcpServers": {
    "shortsync": {
      "type": "streamableHttp",
      "url": "https://www.shortsync.app/api/mcp",
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

If the file already has other servers, add the `shortsync` entry inside the existing `mcpServers` object instead of replacing it. Afterwards, check that `shortsync` appears under MCP Servers → Installed; if it doesn't, you edited a file Cline doesn't load.

## Sign-in

The server uses OAuth 2.1. When the first ShortSync tool is called, the client opens a browser window where the user signs in to ShortSync (or creates a free account) and clicks **Allow**. No token needs to be copied anywhere.

## Check that it works

Call `list_workspaces` (or `get_user_profile`). It returns the user's ShortSync workspaces once sign-in is done.

## Other clients

Use the same URL, `https://www.shortsync.app/api/mcp`, with the client's remote or HTTP server type. See the README for Claude, Claude Code, Gemini CLI, Cursor and VS Code.
