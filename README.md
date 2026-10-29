# KuroKit MCP

KuroKit watches web pages, RSS feeds, and official APIs. It tells your AI assistant when something changes.

This repository is the setup guide and example hub for the hosted KuroKit MCP server. You do not need to download or run a server.

- Official setup guide: https://kurokit.com/docs/mcp
- Dashboard: https://kurokit.com
- Pricing: https://kurokit.com/pricing
- Chrome extension: https://chromewebstore.google.com/detail/kurokit-webpage-change-mo/fndfgkdjhbaoiadepfhgmhbgfjgfpiao
- Edge extension: https://microsoftedge.microsoft.com/addons/detail/kurokit-webpage-change-/oiohkchggekefhcdamceinpmabpfiifk
- MCP endpoint: https://mcp.kurokit.com/mcp

## Quick start

1. Create a free KuroKit account and stay signed in.
2. For webpage watches, install the browser extension (Chrome or Edge). RSS and official-API watches do not need it.
3. Add KuroKit to your AI app. If KuroKit is in the app's connector store, use that listing and sign in. Otherwise add it as a custom remote MCP server.
4. Ask your assistant to list your monitors. If it can, the connection works.
5. Create a watch for your own page, feed, or API.

The full walkthrough, including the Wikipedia test, is at https://kurokit.com/docs/mcp.

## Connect your AI app

Use the store listing first:

1. Open your AI app's connector or MCP marketplace.
2. Search for KuroKit.
3. Add it and finish the sign-in.

If KuroKit is not listed, add a custom remote MCP server:

- URL: `https://mcp.kurokit.com/mcp`
- Authentication: `Authorization: Bearer <your KuroKit token>`

Create the token at https://kurokit.com/dashboard/mcp. Paste it into the app's MCP settings, not into the chat.

Most apps need either a token or an OAuth sign-in, not both. If the app opens a sign-in page with `?client_id=` in the address bar, approve it there. Do not open `https://kurokit.com/oauth/authorize` by itself; it only works when the MCP app opens it.

Client-specific notes:

- [Claude](docs/connect-claude.md)
- [Cursor](docs/connect-cursor.md)
- [ChatGPT / Codex](docs/connect-chatgpt.md)
- [Grok / Grok Bot](docs/connect-grok-bot.md)
- [Another MCP client](docs/connect-any-client.md)

Meta Muse and OpenAI dots use their own connector or plugin directories. KuroKit is not listed there yet. See the [client support matrix](docs/client-support.md) before promising a setup path for those apps.

## Send changes to a workflow

Use a webhook when n8n, Make, Zapier, or your own service should react immediately. Edit the monitor, check **Webhook**, and paste your workflow's public HTTPS URL. KuroKit POSTs signed JSON and retries failed deliveries. See [Webhooks and workflow automation](docs/webhooks.md).

MCP `getEvents` is pull-only and needs no channel selection.

## What you can watch

- **Web page changes** using the browser extension (Chrome or Edge). This works with public pages and pages where you are already signed in.
- **RSS feeds** without the extension.
- **Official APIs** without the extension.

The free plan includes one active monitor. See https://kurokit.com/pricing for current limits.

## Examples

The [examples](examples/) folder contains fallback custom-server configs:

- [MCP JSON with a token](examples/mcp.json)
- [MCP JSON with OAuth only](examples/mcp-oauth.json)
- [Hermes YAML with a token](examples/hermes.yaml)
- [Hermes YAML with OAuth](examples/hermes-oauth.yaml)

Replace `PASTE_TOKEN_FROM_DASHBOARD_MCP` before saving. Never commit a real token.

## Common problems

**The app has no KuroKit tools, or returns 401.**
Create a new token at https://kurokit.com/dashboard/mcp, paste it into the app's settings, and reload the app.

**The app says "not in the MCP catalog".**
Choose "Add custom" or "manual remote server", then use `https://mcp.kurokit.com/mcp` in lowercase.

**The monitor's Last check stays blank.**
Open the watched page, click the KuroKit extension icon on that tab, and make sure "This site" says Allowed. The browser must stay open.

**The first check shows no events.**
That is normal. The first check saves a snapshot. The second check can find a change.

**n8n, Make, or Zapier receives nothing.**
Check **Webhook** in the monitor, use the workflow's production HTTPS URL, activate the workflow, and return a `2xx` response quickly. See [Webhooks and workflow automation](docs/webhooks.md).

More help: [Troubleshooting](docs/troubleshooting.md) and https://kurokit.com/docs/faq.

## Security

- Do not paste passwords, tokens, or card numbers into an AI chat.
- Create and revoke tokens at https://kurokit.com/dashboard/mcp.
- Approve payments only on KuroKit or Stripe pages.
- See [SECURITY.md](SECURITY.md) for vulnerability reporting.

## Documentation

- [Quick start](docs/quickstart.md)
- [Client support matrix](docs/client-support.md)
- [Connect any MCP client](docs/connect-any-client.md)
- [Webhooks and workflow automation](docs/webhooks.md)
- [Troubleshooting](docs/troubleshooting.md)
- [FAQ](docs/faq.md)
- [Screenshot checklist](assets/README.md)
- [Agent-readable summary](llms.txt)

## License

Documentation and images are licensed under [CC BY 4.0](LICENSE). JSON, YAML, and other code examples are licensed under the [MIT License](LICENSE-CODE).

## About this repository

This is a documentation-only mirror generated from the private KuroKit repository. The MCP server, web app, and extension source code are not published here. Changes made directly in this repository may be overwritten by the next sync.
