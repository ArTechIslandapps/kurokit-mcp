# Connect any MCP client

Use this page if your app is not Claude, Cursor, ChatGPT/Codex, or Grok/Grok Bot, or if KuroKit is not in the app's connector store. For Meta Muse and OpenAI dots, check the [client support matrix](client-support.md) first; those apps use their own connector or plugin directories.

## 1. Check the app's store first

Open the app's connector or MCP marketplace and search for KuroKit. If it appears, add it there and finish the sign-in. This is usually the easiest path.

## 2. Add a custom remote server

If KuroKit is not listed, add a remote MCP server:

| Field | Value |
| --- | --- |
| Name | KuroKit |
| URL | `https://mcp.kurokit.com/mcp` |
| Header | `Authorization: Bearer <your token>` |

Create the token at https://kurokit.com/dashboard/mcp.

Some apps use a JSON or YAML config file instead of a form. See [examples](../examples/).

## 3. Test it

Reload the app's MCP connection or restart the app. Open a new chat and ask:

```text
Call the KuroKit MCP tool listMonitors. Do not fetch any web pages.
Tell me how many monitors I have and their names.
```

If the assistant lists monitors, the connection works.

## Authentication notes

- If the app supports OAuth and opens a sign-in page with `?client_id=` in the address bar, approve it there. You may not need a token.
- If the app asks for a token, paste it into the app's MCP settings. Do not paste it into the chat.
- Do not open `https://kurokit.com/oauth/authorize` by itself. It does nothing without the `?client_id=` value added by the MCP app.
- If the app says "not in the MCP catalog", choose "Add custom" or "manual remote server".

## Next

- [Quick start](quickstart.md)
- [Client support matrix](client-support.md)
- [Grok / Grok Bot](connect-grok-bot.md)
- [Troubleshooting](troubleshooting.md)
- [Example configs](../examples/)
