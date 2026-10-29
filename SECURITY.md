# Security

## Reporting a vulnerability

Do not open a public issue for a security problem. Email support@kurokit.com with:

- a short description
- steps to reproduce
- the affected URL or client
- any relevant logs, with tokens and personal data removed

We will reply as soon as possible.

## Tokens and secrets

KuroKit MCP uses a Bearer token. Treat it like a password.

- Never commit a real token to this repository.
- Never paste a token into an AI chat.
- Create and revoke tokens at https://kurokit.com/dashboard/mcp.
- Use the placeholder `PASTE_TOKEN_FROM_DASHBOARD_MCP` in examples.

## Payments

Approve payments only on KuroKit or Stripe pages. Do not send card numbers in an AI chat.
