# Webhooks and workflow automation

Use a webhook when you want KuroKit to push a change into n8n, Make, Zapier, or your own service.

This is different from MCP. `getEvents` is pull: your AI app asks KuroKit for events. A webhook is push: KuroKit sends an HTTP `POST` to your URL when a monitor matches.

You can use both on the same monitor.

## Pull or push?

| Option | Direction | Best for |
| --- | --- | --- |
| MCP `getEvents` | Pull | An AI assistant that checks for changes when asked, or on a schedule. No per-monitor channel is required. |
| Webhook | Push | n8n, Make, Zapier, or your own backend that should react immediately. |
| Email / Telegram | Push | A person who wants the alert in an inbox or chat. |

MCP does not have a real-time stream of monitor matches, and there is no `registerTrigger` tool. Poll `getEvents` with `since=` for incremental reads.

## Before you start

You need:

- A KuroKit account and a monitor.
- A public `https://` receiver URL.
- A receiver that returns a `2xx` response within 5 seconds.

Localhost and private network URLs are rejected. The receiver must be reachable from the public internet.

## Enable a webhook in the dashboard

1. Open the monitor and edit it.
2. Under **Notify me via**, check **Webhook**.
3. Paste the URL from your workflow's webhook node.
4. Save the monitor.
5. Copy the signing secret when it appears. It is shown once.
6. Send a test notification from the monitor and confirm the receiver gets it.

Test deliveries include `"test": true` in the JSON body. Use that field to avoid treating a test as a real change.

Changing the URL later keeps the same signing secret. Removing the webhook channel stops deliveries.

## Create a webhook monitor through MCP

When an AI agent creates or updates a monitor, add `webhook` to `notifyChannels` and provide `webhookUrl`:

```json
{
  "notifyChannels": ["webhook"],
  "webhookUrl": "https://your-receiver.example.com/kurokit"
}
```

The write response includes a one-time `webhookSecret`. Store it in your receiver's environment variables. `listMonitors` shows the last webhook error, but never the secret.

## Request format

KuroKit sends:

```text
POST /your-path HTTP/1.1
Content-Type: application/json
X-KuroKit-Event: monitor.change
X-KuroKit-Signature: t=1760000000,v1=<hex hmac>
```

Example body:

```json
{
  "schema_version": 2,
  "monitor_id": "11111111-1111-1111-1111-111111111111",
  "event_id": "22222222-2222-2222-2222-222222222222",
  "monitor_name": "Competitor pricing",
  "subject": "KuroKit: Competitor pricing",
  "body": "The watched text changed.",
  "target_url": "https://example.com/pricing",
  "diff_summary": "The watched text changed.",
  "judged_by": "rule",
  "added": ["Pro plan: $49"],
  "removed": ["Pro plan: $39"],
  "sent_at": "2026-10-21T12:00:00.000Z"
}
```

Fields such as `event_id`, `monitor_name`, `target_url`, `diff_summary`, `added`, and `removed` are omitted when they are not available. `test: true` is present only on test deliveries.

Use `event_id` as an idempotency key if your workflow can receive duplicates.

## Verify the signature

The signature is an HMAC-SHA256 over the timestamp, a literal dot, and the raw request body:

```text
signature = HMAC-SHA256(secret, "<t>.<raw body>")
```

The `X-KuroKit-Signature` header contains `t=<unix seconds>` and `v1=<hex digest>`. Verify with the raw body before parsing JSON, and reject old timestamps to limit replay.

Node.js example:

```js
import crypto from "node:crypto";

function verifyKuroKitSignature(rawBody, header, secret, maxAgeSeconds = 300) {
  const parts = Object.fromEntries(
    header.split(",").map((part) => {
      const index = part.indexOf("=");
      return [part.slice(0, index), part.slice(index + 1)];
    })
  );

  const timestamp = Number(parts.t);
  const received = parts.v1;
  if (!Number.isFinite(timestamp) || !received) return false;
  if (Math.abs(Date.now() / 1000 - timestamp) > maxAgeSeconds) return false;

  const expected = crypto
    .createHmac("sha256", secret)
    .update(`${timestamp}.${rawBody}`)
    .digest("hex");

  const expectedBuffer = Buffer.from(expected, "hex");
  const receivedBuffer = Buffer.from(received, "hex");
  return (
    expectedBuffer.length === receivedBuffer.length &&
    crypto.timingSafeEqual(expectedBuffer, receivedBuffer)
  );
}
```

Keep the secret server-side. Do not put it in a browser, a public workflow, or an AI chat.

## n8n

1. Add a **Webhook** node.
2. Set **HTTP Method** to `POST`.
3. Set **Respond** to `Immediately` with response code `200`.
4. Copy the **Production URL**. The test URL only works while the workflow is listening for a test event.
5. Paste the production URL into the KuroKit monitor's **Webhook URL** field and save.
6. Copy the signing secret into your n8n credentials or environment variables.
7. Activate the workflow.
8. Send a KuroKit test notification. Filter or branch on `test: true` if you do not want test events to run the real actions.

If your n8n version has a raw-body option, enable it when verifying the signature. Otherwise verify the signature in a small proxy or skip signature verification and protect the webhook URL as a secret.

Return a `2xx` quickly. If the workflow does long work, acknowledge first and continue asynchronously; KuroKit times out after 5 seconds.

## Make and Zapier

- **Make:** add a **Custom webhook**, copy its address, and paste it into KuroKit.
- **Zapier:** use **Webhooks by Zapier -> Catch Hook**, copy the URL, and paste it into KuroKit.

Both should return a success response immediately. If the workflow can receive retries, deduplicate with `event_id`.

## Retries and errors

- Timeout: 5 seconds per attempt.
- Retries: about 1 minute, 5 minutes, 30 minutes, and 30 minutes later.
- Maximum: 5 attempts including the first.
- After that, KuroKit stops retrying that delivery.

The monitor's edit page shows the last webhook error. MCP `listMonitors` also returns `webhook.lastError`. A failed delivery does not mean the change was lost; it is still in the event log and can be read with `getEvents`.

## Troubleshooting

**The workflow receives nothing**

- Confirm **Webhook** is checked and the URL is saved.
- Use the production URL, not the n8n test URL.
- Activate the n8n workflow.
- Confirm the receiver returns `2xx` within 5 seconds.
- Confirm the monitor has matched a change. The first check only creates a snapshot.

**KuroKit rejects the URL**

The URL must be public `https://`. Localhost, private IPs, and non-HTTPS URLs are rejected.

**The test arrived but real changes did not**

- Check that the workflow is active.
- Check that the monitor actually matched.
- Make sure you are not filtering out every real event by requiring `test: true`.

**The receiver gets duplicates**

Retries and at-least-once delivery can produce duplicates. Deduplicate with `event_id`.

**I only need an AI agent to read changes**

Do not use a webhook. Keep the monitor pull-only and call MCP `getEvents` with `since=`.

## Related

- [Quick start](quickstart.md)
- [Troubleshooting](troubleshooting.md)
- [FAQ](faq.md)
- [Agent-readable summary](../llms.txt)
