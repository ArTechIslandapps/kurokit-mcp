# Connect KuroKit to Cursor

The exact settings screen can change between Cursor versions. The official, always-current guide is https://kurokit.com/docs/mcp.

## If KuroKit is in Cursor's MCP marketplace

1. Open Cursor's MCP settings or marketplace.
2. Search for KuroKit.
3. Add it and complete the sign-in.

Use this path when it is available. You do not need to paste a token.

## If KuroKit is not listed

Add a custom remote MCP server in Cursor's MCP settings:

- URL: `https://mcp.kurokit.com/mcp`
- Header: `Authorization: Bearer <your token>`

Or paste this into the MCP config file:

```json
{
  "mcpServers": {
    "kurokit": {
      "url": "https://mcp.kurokit.com/mcp",
      "headers": {
        "Authorization": "Bearer PASTE_TOKEN_FROM_DASHBOARD_MCP"
      }
    }
  }
}
```

Create the token at https://kurokit.com/dashboard/mcp. Replace `PASTE_TOKEN_FROM_DASHBOARD_MCP` before saving. Do not paste the token into the chat.

The same example is available at [examples/mcp.json](../examples/mcp.json).

## Check the connection

Open a new chat and ask:

```text
Call the KuroKit MCP tool listMonitors. Do not fetch any web pages.
Tell me how many monitors I have and their names.
```

If Cursor lists your monitors, the connection works.

## Troubleshooting

- No KuroKit tools or 401: create a new token and paste it into the MCP config.
- If the config already has other servers, add only the `kurokit` block. Do not replace the whole file.
- Do not open `https://kurokit.com/oauth/authorize` by itself. It only works when Cursor opens it with `?client_id=` in the address bar.
- More help: [Troubleshooting](troubleshooting.md).
