# Seamless Messaging

Work with your [Seamless Messaging](https://seamless-messaging.eu) team inbox from Claude. Search WhatsApp, Telegram and SMS conversations, open the photos, documents and voice notes customers send, read the Pipedrive context of a customer, and prepare replies that you review before anything is sent.

## Install in Claude Code

```
/plugin marketplace add seamless-messaging/claude-plugin
/plugin install seamless-messaging@seamless-messaging
```

Then run `/mcp`, choose `seamless-messaging`, select **Authenticate** and sign in.

## What it includes

- **Seamless Messaging MCP server** (`https://seamless-messaging.eu/mcp`). You sign in with your Seamless Messaging account (OAuth with PKCE) and choose which workspaces Claude may use. Claude sees only those workspaces and only the conversations your role allows in the Inbox.
- **`messaging-basics` skill**: how Claude picks the workspace and the sending number, and the draft, review, confirm, send flow.
- **`reply-to-customer` skill**: finds the conversation, reads the history and CRM context, and drafts a reply in the customer's language.
- **`customer-brief` skill**: a read-only summary of a customer before a call, with the deal, recent messages, open items and a suggested next step.

## How sending works

Claude never sends on its own. It creates a draft, which also appears in your team's Inbox, shows you the recipient, channel, sending number and text, and sends only after you approve that exact text. Editing a draft invalidates earlier approvals.

## Data

The plugin contains only instructions and the server address. It runs no local code and sends data to no service other than the Seamless Messaging server above. Message content is read from and written to your Seamless Messaging workspaces through that server. Privacy policy: https://seamless-messaging.eu/en/legal/privacy

## Requirements

A Seamless Messaging account with access to at least one workspace. Supported channels: WhatsApp, Telegram and SMS (Twilio).

## Documentation and support

- Setup guide: https://seamless-messaging.eu/docs/en/claude
- Support: https://seamless-messaging.eu
