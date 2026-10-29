# Connect KuroKit to ChatGPT or Codex

Remote MCP support in ChatGPT and Codex depends on your plan, region, and app version. If your app does not offer custom connectors, use another MCP-capable client or the KuroKit dashboard.

Official, always-current guide: https://kurokit.com/docs/mcp

## If KuroKit is in the app's connector store

1. Open the app's connector or MCP marketplace.
2. Search for KuroKit.
3. Add it and complete the sign-in.

Use this path when it is available. You do not need to paste a token.

## If the app supports custom connectors

Add a remote MCP server:

- URL: `https://mcp.kurokit.com/mcp`
- Header: `Authorization: Bearer <your token>`

Create the token at https://kurokit.com/dashboard/mcp. Paste it into the app's MCP settings, not into the chat.

If the app asks for a JSON config, use [examples/mcp.json](../examples/mcp.json) and replace the placeholder.

## Check the connection

Open a new chat and ask:

```text
Call the KuroKit MCP tool listMonitors. Do not fetch any web pages.
Tell me how many monitors I have and their names.
```

If the assistant lists your monitors, the connection works.

## If custom connectors are not available

You can still use KuroKit from the dashboard at https://kurokit.com, or connect another MCP client such as Claude, Cursor, or Grok/Grok Bot.

OpenAI dots is separate from ChatGPT's custom MCP setup. Dots uses installed plugins, and KuroKit is not a published plugin yet. See the [client support matrix](client-support.md).

## Troubleshooting

- No KuroKit tools or 401: create a new token and paste it into the MCP settings.
- "Not in the MCP catalog": choose the custom or manual remote server option.
- Do not open `https://kurokit.com/oauth/authorize` by itself. It only works when the app opens it with `?client_id=` in the address bar.
- More help: [Troubleshooting](troubleshooting.md).
