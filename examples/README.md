# Examples

These are fallback configs for a **custom remote MCP server**. If KuroKit appears in your AI app's connector store, use that listing instead.

| File | Use when |
| --- | --- |
| [mcp.json](mcp.json) | The app uses JSON and asks for a token |
| [mcp-oauth.json](mcp-oauth.json) | The app uses JSON and can open its own OAuth sign-in |
| [hermes.yaml](hermes.yaml) | Hermes uses YAML and asks for a token |
| [hermes-oauth.yaml](hermes-oauth.yaml) | Hermes uses YAML and can open its own OAuth sign-in |

## Before you save

1. Create a token at https://kurokit.com/dashboard/mcp.
2. Replace `PASTE_TOKEN_FROM_DASHBOARD_MCP` with that token.
3. If the file already has other servers, add only the `kurokit` block. Do not replace the whole file.
4. Reload MCP or restart the app.

Never commit a real token.

## Check the connection

Open a new chat and ask:

```text
Call the KuroKit MCP tool listMonitors. Do not fetch any web pages.
Tell me how many monitors I have and their names.
```

If the assistant lists your monitors, the connection works.

More help: [Quick start](../docs/quickstart.md) and [Troubleshooting](../docs/troubleshooting.md).
