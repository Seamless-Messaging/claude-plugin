# Seamless Messaging for Claude

Use your [Seamless Messaging](https://seamless-messaging.eu) Inbox from Claude: list and search WhatsApp, Telegram and SMS conversations with the Inbox filters and your saved views, open the photos, documents and voice notes customers send, read the Pipedrive context, reports and logs, see where you were mentioned or what was assigned to you, block senders who should not reach your team, keep notes, labels and templates tidy, and draft replies that you approve before they are sent.

## What's inside

| Part | What it does |
|---|---|
| MCP server | Connects Claude to `https://seamless-messaging.eu/mcp` with OAuth. You sign in with your Seamless account and choose which workspaces Claude may use. |
| `messaging-basics` skill | Rules Claude follows: workspace and sender selection, and draft → show → confirm → send. |
| `reply-to-customer` skill | Finds the conversation, reads history and CRM context, and drafts a reply in the customer's language. |
| `customer-brief` skill | Read-only summary of a customer before a call: deal, recent messages, open items, next step. |

Supported channels: WhatsApp, Telegram and SMS (Twilio).

## Install

Full step-by-step guide: [Connect Claude](https://seamless-messaging.eu/docs/en/claude) ([en español](https://seamless-messaging.eu/docs/es/claude)).

### Claude Code

Run these in Claude Code:

```
/plugin marketplace add seamless-messaging/claude-plugin
/plugin install seamless-messaging@seamless-messaging
```

Then run `/mcp`, choose `seamless-messaging` and select **Authenticate**. A browser window opens. Sign in to Seamless Messaging and select the workspaces Claude may use.

### Claude apps (web, desktop, mobile)

Add a custom connector in **Settings → Connectors** with this URL:

```
https://seamless-messaging.eu/mcp
```

Custom connectors require a paid Claude plan. On Team and Enterprise plans, an owner may need to add the connector first.

## How sending works

Claude never sends on its own. It creates a **draft**, which also appears in your team's Seamless Inbox, shows you the recipient, channel, sending number and text, and sends only after you say yes to that exact text. Editing a draft invalidates earlier approvals.

## Security and privacy

- Sign-in uses OAuth 2.1 with PKCE. Claude never sees your password, API keys or channel credentials.
- Claude sees only the workspaces you select and the conversations your role allows in the Inbox.
- Read access (`mcp:read`) and draft/send access (`mcp:write`) are separate scopes.
- You can remove access at any time by disconnecting the connector in Claude.

Privacy policy: https://seamless-messaging.eu/en/legal/privacy

## Requirements

- A Seamless Messaging account with access to at least one workspace.
- Claude Code, or a Claude plan that supports custom connectors.

## Support

- Documentation: https://seamless-messaging.eu/docs/en/claude
- Website: https://seamless-messaging.eu
