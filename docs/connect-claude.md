# Connect KuroKit to Claude

The exact menu names can change between Claude apps and plans. The official, always-current guide is https://kurokit.com/docs/mcp.

## If KuroKit is in Claude's connector directory

1. Open Claude's connectors or MCP settings.
2. Search for KuroKit.
3. Add it and complete the sign-in.

Use this path when it is available. You do not need to paste a token.

## If KuroKit is not listed

Add KuroKit as a custom remote MCP server:

- URL: `https://mcp.kurokit.com/mcp`
- Header: `Authorization: Bearer <your token>`

Create the token at https://kurokit.com/dashboard/mcp. Paste it into Claude's MCP settings, not into the chat.

If Claude asks for a JSON config file, use [examples/mcp.json](../examples/mcp.json) and replace the placeholder.

## Check the connection

Open a new chat and ask:

```text
Call the KuroKit MCP tool listMonitors. Do not fetch any web pages.
Tell me how many monitors I have and their names.
```

If Claude lists your monitors, the connection works.

## Troubleshooting

- No KuroKit tools or 401: create a new token and paste it into the MCP settings.
- "Not in the MCP catalog": choose the custom or manual remote server option.
- Do not open `https://kurokit.com/oauth/authorize` by itself. It only works when Claude opens it with `?client_id=` in the address bar.
- More help: [Troubleshooting](troubleshooting.md).
