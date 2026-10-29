# Connect KuroKit to Grok or Grok Bot

Grok and Grok Bot both support custom remote MCP servers. KuroKit is not in a Grok connector catalog, so add it as a custom server.

Grok Bot is Cursor's cloud agent, not the same product as Grok on grok.com. The setup screens differ.

Official, always-current KuroKit guide: https://kurokit.com/docs/mcp

## Grok on grok.com

1. Open https://grok.com/connectors.
2. Select **New Connector**, then **Custom**.
3. Enter the KuroKit MCP URL:

   ```text
   https://mcp.kurokit.com/mcp
   ```

4. Complete the authentication step. Prefer OAuth if Grok opens a KuroKit sign-in page. If Grok offers only a token field, create a token at https://kurokit.com/dashboard/mcp and paste it into that field, not into the chat.
5. Ask Grok to call `listMonitors` to confirm the connection.

Grok requires a publicly reachable HTTPS server. KuroKit's hosted endpoint already meets that requirement.

Official Grok documentation: https://docs.x.ai/grok/connectors

## Grok Bot

Grok Bot supports custom remote MCP servers as plugins. The server must be reachable over public HTTPS, and OAuth sign-in is supported. The exact add flow can change between Grok Bot versions.

1. Install Grok Bot and sign in. Grok Bot requires an eligible paid Cursor plan or a linked SuperGrok subscription.
2. Open **Connect apps** in the sidebar. If Grok Bot offers a custom MCP or custom plugin option, choose it.
3. Enter `https://mcp.kurokit.com/mcp`.
4. Complete the KuroKit OAuth sign-in if prompted. If the app offers a separate credential field, use a token from https://kurokit.com/dashboard/mcp and keep it out of the chat.
5. If you are on a Cursor team, your admin may need to allow the connector in the team's plugin or MCP policy.
6. Ask the Bot to call `listMonitors` to confirm the connection.

Some Grok Bot versions add a custom MCP server by asking the Bot in chat. If your version has no form, ask it to add the KuroKit MCP server and follow the prompts. Do not use a localhost URL; Grok Bot runs in the cloud.

Official Grok Bot documentation:

- https://docs.x.ai/grok-bot
- https://docs.x.ai/grok-bot/team-bots
- https://cursor.com/help/grok-bot/connect-plugins

## Authentication notes

- OAuth is the preferred path. The MCP app must open the sign-in page; do not open `https://kurokit.com/oauth/authorize` by itself.
- If OAuth is unavailable and the app asks for a token, create one at https://kurokit.com/dashboard/mcp. Paste it into the app's settings, not into the chat.
- Grok Bot team admins can restrict connectors. If KuroKit shows as disabled by an admin, ask the admin to allow it.

## Check the connection

Open a new chat and ask:

```text
Call the KuroKit MCP tool listMonitors. Do not fetch any web pages.
Tell me how many monitors I have and their names.
```

If the assistant lists your monitors, the connection works.

## If it does not work

- No KuroKit tools or 401: reconnect with OAuth, or create a new token and update the app settings.
- "Not in the catalog": choose the custom or manual remote server option.
- Grok Bot cannot reach the URL: confirm it is public HTTPS and ends in `/mcp`.
- More help: [Troubleshooting](troubleshooting.md) and https://kurokit.com/docs/mcp.
