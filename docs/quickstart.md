# Quick start

This guide connects KuroKit to Claude, Cursor, ChatGPT/Codex, Grok/Grok Bot, or another MCP-capable app. It takes about 10 minutes.

You do not need to download the MCP server. KuroKit runs it for you at `https://mcp.kurokit.com/mcp`.

## What you need

- A KuroKit account: https://kurokit.com/login
- An AI app that supports MCP
- The KuroKit browser extension (Chrome or Edge), only if you want to watch web pages

RSS and official-API watches do not need the extension.

## 1. Create an account

Sign up at https://kurokit.com/login and stay signed in.

The free plan includes one active monitor and does not expire. See https://kurokit.com/pricing for current plan limits.

## 2. Prepare the extension and a token

### Browser extension (Chrome or Edge)

Skip this if you only want RSS or official-API watches.

1. Install the KuroKit browser extension:
   - Chrome: https://chromewebstore.google.com/detail/kurokit-webpage-change-mo/fndfgkdjhbaoiadepfhgmhbgfjgfpiao
   - Edge: https://microsoftedge.microsoft.com/addons/detail/kurokit-webpage-change-/oiohkchggekefhcdamceinpmabpfiifk
2. Open the extension and click Connect.
3. Sign in to KuroKit and approve the extension.
4. The extension popup should say Connected.

The extension opens web pages for KuroKit. MCP itself cannot use your browser session.

### Token

1. Open https://kurokit.com/dashboard/mcp
2. Click **Create token**.
3. Copy the token.

Paste the token into your AI app's MCP settings, not into the chat. If your app uses OAuth and opens a sign-in page, you may not need a token.

## 3. Add KuroKit to your AI app

### If KuroKit is in the app's connector store

1. Open the app's connector or MCP marketplace.
2. Search for KuroKit.
3. Add it and finish the sign-in.

This is the preferred path when available.

### If KuroKit is not listed

Add a custom remote MCP server:

- URL: `https://mcp.kurokit.com/mcp`
- Header: `Authorization: Bearer <your token>`

Some apps call this "Add custom", "Add remote server", or "Manual configuration". Use the JSON or YAML examples in [examples](../examples/) if the app asks for a config file.

Grok and Grok Bot accept a custom remote MCP server; see [Grok / Grok Bot](connect-grok-bot.md). Meta Muse and OpenAI dots use their own connector or plugin directories, and KuroKit is not listed there yet. Check the [client support matrix](client-support.md).

Do not open `https://kurokit.com/oauth/authorize` by itself. It only works when the MCP app opens it with `?client_id=` in the address bar.

## 4. Check the connection

Reload the app's MCP connection or restart the app. Open a new chat and paste:

```text
Call the KuroKit MCP tool listMonitors. Do not fetch any web pages.
Tell me how many monitors I have and their names.
```

If the assistant lists your monitors, the connection works. It is fine if the list is empty.

If you see an authentication error, create a new token and paste it into the app's settings. Do not paste it into the chat.

## 5. Run the Wikipedia test

This checks the full path: AI app → KuroKit → browser extension → web page.

1. Ask your assistant to create a monitor for `https://en.wikipedia.org/wiki/Special:RecentChanges`.
2. Open the returned `targetUrl` in your browser.
3. Click the KuroKit icon on that Wikipedia tab.
4. If the panel shows **Allow en.wikipedia.org**, click it. "This site" must say **Allowed**.
5. Keep the browser open and wait 5–10 minutes.
6. Ask your assistant to check for changes again.

The first check saves a snapshot. The second check can find a change.

## 6. Watch your own page

Ask your assistant to create a monitor for your page, feed, or API. Be clear about what should count as a change.

For example:

```text
Watch this page: https://example.com/pricing
Tell me when the monthly price changes.
Create a KuroKit webpage monitor.
I will allow this site in the browser extension and keep the browser open.
```

If the assistant cannot pick the right part of the page, use the click-to-select tool on the KuroKit dashboard.

## 7. Send changes to a workflow (optional)

If you use n8n, Make, Zapier, or your own service, edit the monitor, check **Webhook**, and paste your workflow's public HTTPS URL. KuroKit POSTs signed JSON and retries failed deliveries. See [Webhooks and workflow automation](webhooks.md).

MCP `getEvents` is pull-only and needs no channel selection.

## Next

- [Connect any MCP client](connect-any-client.md)
- [Webhooks and workflow automation](webhooks.md)
- [Client support matrix](client-support.md)
- [Troubleshooting](troubleshooting.md)
- [FAQ](faq.md)
- Official guide: https://kurokit.com/docs/mcp
