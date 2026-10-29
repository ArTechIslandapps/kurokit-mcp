# FAQ

## What is KuroKit?

KuroKit watches a web page, RSS feed, or official API and tells your AI assistant when something matching your rule changes. You can also get email or Telegram notifications from the dashboard.

## Do I need to write code?

No. Describe what you want to watch in plain language. The assistant can create the monitor, or you can use the dashboard.

## Do I need to download the MCP server?

No. KuroKit hosts it at `https://mcp.kurokit.com/mcp`.

## Which AI apps can connect?

Claude, Cursor, ChatGPT/Codex, and Grok/Grok Bot can use the direct MCP setup. Meta Muse and OpenAI dots use their own connector or plugin directories, and KuroKit is not listed there yet. See the [client support matrix](client-support.md).

## Do I need the browser extension?

Only for webpage watches. RSS and official-API watches do not need it.

The extension is what opens web pages for KuroKit. It also lets KuroKit use the browser session where you are already signed in.

## Does the free plan expire?

No. The free plan includes one active monitor. See https://kurokit.com/pricing for current limits.

## Can I watch pages that require a login?

Yes, if the browser extension (Chrome or Edge) is installed, the site is allowed, and you are already signed in. KuroKit uses your browser session; your AI app does not receive your password or cookies.

## Can I watch JavaScript-heavy pages?

Yes, when the page is open in your browser. Keep the browser running.

## Where do I get a token?

Open https://kurokit.com/dashboard/mcp and click **Create token**. Paste the token into your AI app's MCP settings, not into the chat.

## Why does `https://kurokit.com/oauth/authorize` not work by itself?

That page needs a `?client_id=` value added by the MCP app. If you open it manually, it cannot connect. Use the app's connector store or add a custom remote server instead.

## Can I send changes to n8n, Make, or Zapier?

Yes. Edit the monitor, check **Webhook**, and paste your workflow's public HTTPS URL. Save the monitor, then copy the signing secret into your workflow. KuroKit POSTs signed JSON and retries failed deliveries. See [Webhooks and workflow automation](webhooks.md).

MCP `getEvents` is pull-only and needs no channel selection.

## Where can I see my monitors?

Open https://kurokit.com/dashboard. You can also ask your assistant to call `listMonitors`.

## Where can I get help?

- Setup guide: https://kurokit.com/docs/mcp
- Troubleshooting: [Troubleshooting](troubleshooting.md)
- FAQ: https://kurokit.com/docs/faq
- Email: support@kurokit.com
