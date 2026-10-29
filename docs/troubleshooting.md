# Troubleshooting

Start with the official guide if this page does not solve the problem: https://kurokit.com/docs/mcp

## The app has no KuroKit tools, or returns 401

1. Open https://kurokit.com/dashboard/mcp
2. Create a new token.
3. Paste it into the app's MCP settings.
4. Reload MCP or restart the app.
5. Ask again: `Call the KuroKit MCP tool listMonitors.`

Do not paste the token into the chat.

If you added KuroKit from a marketplace, remove it and add it again, then sign in.

## My app is Meta Muse or OpenAI dots

Those apps do not document a generic custom MCP URL flow. Muse connectors go through the Muse Connector Platform, and dots uses installed plugins. KuroKit is not listed in either directory yet. Use Claude, Cursor, ChatGPT/Codex, Grok/Grok Bot, or the KuroKit dashboard instead. See the [client support matrix](client-support.md).

## The app says "not in the MCP catalog"

Choose **Add custom** or **manual remote server**, then use:

```text
https://mcp.kurokit.com/mcp
```

Use lowercase. Do not add a trailing slash or a path after `/mcp`.

## The app asks for a token or OAuth

- If the app opens a sign-in page with `?client_id=` in the address bar, approve it there. You may not need a token.
- If the app asks for a token, create one at https://kurokit.com/dashboard/mcp and paste it into the app's MCP settings.
- Do not open `https://kurokit.com/oauth/authorize` by itself. It does nothing without the `?client_id=` value added by the MCP app.

## A webpage monitor's Last check stays blank

The browser extension (Chrome or Edge) is what opens the page. Check it on the watched page:

1. Keep the watched page open.
2. Click the KuroKit icon on that tab, not on the dashboard tab.
3. Check that **This site** says **Allowed** for the watched site.
4. If you see an **Allow** button, click it and approve the browser prompt.
5. Keep the browser open. Closing the browser or sleeping the computer stops checks.

**Connected** only means the extension is signed in. It does not mean the site is allowed.

## The first check shows 0 events

That is normal. The first check saves a snapshot. The second check can find a change. Wait 5–10 minutes, then ask for events again.

## The monitor limit is full

The free plan includes one active monitor. Delete an old monitor or move it to the Saved shelf, then try again. See https://kurokit.com/pricing for current limits.

## A page needs a login

KuroKit can watch a page where you are already signed in when the browser extension (Chrome or Edge) is installed and the site is allowed. The AI app does not receive your password or session cookies.

## A page is built with JavaScript

Ask your assistant to use the browser-tab render mode and keep the page open in your browser. The browser must stay running.

## The assistant cannot find the right part of the page

Use the click-to-select tool on the KuroKit dashboard. If a monitor stays empty, set the watched area there.

## n8n, Make, Zapier, or my webhook receives nothing

1. Edit the monitor and confirm **Webhook** is checked and the URL is saved.
2. Use the workflow's production URL, not a test URL that only listens briefly.
3. Activate the workflow.
4. Return a `2xx` response within 5 seconds. A workflow that does long work should acknowledge first.
5. Confirm the monitor actually matched. The first check only creates a snapshot.

KuroKit retries failed deliveries, but a receiver that never returns `2xx` will eventually stop receiving retries. Check the monitor's last webhook error. See [Webhooks and workflow automation](webhooks.md).

## My webhook URL is rejected

The URL must be public `https://`. Localhost and private network addresses are rejected. The receiver must be reachable from the public internet.

## My webhook test arrives but real changes do not

- Check that the workflow is active.
- Check that the monitor has matched a change.
- Make sure your filter is not requiring `test: true`; real deliveries omit it.
- Use `event_id` to deduplicate retries.

## I only need an AI agent to read changes

Do not use a webhook. Keep the monitor pull-only and call MCP `getEvents` with `since=`. No channel selection is needed.

## Still stuck

- FAQ: https://kurokit.com/docs/faq
- Contact: support@kurokit.com
- Include the monitor name, the page URL, and the error text. Do not send your token.
