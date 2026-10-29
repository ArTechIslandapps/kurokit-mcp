# Client support

Last checked: 2026-10-21.

KuroKit exposes one hosted remote MCP endpoint. Several AI apps can add it directly. Some apps only expose MCP through their own reviewed connector or plugin directory.

| Client | How it uses MCP | KuroKit status | Guide |
| --- | --- | --- | --- |
| Claude | Connector directory or custom remote MCP | Use the direct setup | [Claude](connect-claude.md) |
| Cursor | MCP marketplace or custom remote MCP | Use the direct setup | [Cursor](connect-cursor.md) |
| ChatGPT / Codex | Connectors or custom remote MCP, where available | Use the direct setup | [ChatGPT / Codex](connect-chatgpt.md) |
| Grok / Grok Bot | Custom remote MCP connector | Supported by Grok and Grok Bot; KuroKit is not in a Grok catalog, so add it as a custom server | [Grok / Grok Bot](connect-grok-bot.md) |
| Meta Muse | MCP connectors through the Muse Connector Platform; approved connectors appear in Settings > Connectors | KuroKit is not a reviewed Muse connector and has no documented self-serve MCP URL | See the Muse note below |
| OpenAI dots | Plugins installed for the ChatGPT account; a plugin can include an MCP server | KuroKit is not a published plugin and dots has no documented custom MCP URL | See the dots note below |
| Another MCP client | Custom remote MCP | Use the endpoint and OAuth or a token | [Any MCP client](connect-any-client.md) |

## Meta Muse

Meta documents MCP connectors for Muse, but public connectors go through the Muse Connector Platform review process. Approved connectors are discoverable in Muse under **Settings > Connectors**.

Muse can also create a Custom Connector when a service is not in its list. Meta says it does not review custom connectors, and that flow can ask for API information rather than a plain MCP URL. Do not assume that pasting a URL is enough, and do not paste a KuroKit token into a Muse chat.

KuroKit is not a reviewed Muse connector today. Use another client until KuroKit is available there or Meta documents a self-serve custom MCP flow.

Sources:

- https://platform.muse.ai/docs
- https://www.meta.com/help/artificial-intelligence/1687253048996149/

## OpenAI dots

OpenAI dots uses supported plugins installed and enabled for your ChatGPT account. OpenAI's plugin documentation allows a plugin to include an MCP server, but the dots documentation does not expose a direct custom MCP URL setting.

KuroKit is not a published ChatGPT plugin today, so there is no direct dots setup to document. Use ChatGPT/Codex with a custom MCP connector, or another client in the table above. If KuroKit becomes available as a plugin, enable it for the account and dot that should use it.

Sources:

- https://learn.chatgpt.com/docs/dots
- https://developers.openai.com/plugins/concepts/mcp-server

## Verification notes

"Supports MCP" does not mean KuroKit is listed in that app's directory. Directory availability requires a separate submission and review. The statuses above describe documented support, not a tested KuroKit listing.
