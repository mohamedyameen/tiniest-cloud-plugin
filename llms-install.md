# Installing the Tiniest Cloud MCP server

Tiniest Cloud is a **hosted** MCP server. There is nothing to clone, build or run locally —
add its URL to your MCP settings and sign in.

- Server URL: `https://app.tiniest.cloud/mcp`
- Transport: Streamable HTTP
- Authentication: OAuth 2.1 in the browser (dynamic client registration). No API key.

## Cline

Add this to `cline_mcp_settings.json`:

```json
{
  "mcpServers": {
    "tiniest-cloud": {
      "type": "streamableHttp",
      "url": "https://app.tiniest.cloud/mcp"
    }
  }
}
```

The first time a tool is used, Cline opens the browser to sign in to Tiniest Cloud (or create a
free account) and approve the connection.

**If your Cline version does not open a sign-in page**, use a token instead: sign in at
https://app.tiniest.cloud, open **Settings → Coding agents → Other → Connect**, copy the token,
and add it as a header:

```json
{
  "mcpServers": {
    "tiniest-cloud": {
      "type": "streamableHttp",
      "url": "https://app.tiniest.cloud/mcp",
      "headers": { "Authorization": "Bearer <your token>" }
    }
  }
}
```

## Check it works

Ask: "What apps do I have on Tiniest Cloud?" — the `list_apps` tool answers.

Before building an app, call the `tiny_guide` tool: it returns the current SDK reference
(sign-in, per-user storage, realtime, AI) that apps on Tiniest Cloud are written against.
