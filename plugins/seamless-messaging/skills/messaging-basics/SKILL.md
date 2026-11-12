---
name: messaging-basics
description: Rules for working with Seamless Messaging tools (WhatsApp, Telegram, SMS and Pipedrive context). Use whenever the user asks to look up, read, search, draft, edit or send a customer message, check who said what to a client, list their WhatsApp or Telegram groups, or pick which number or account to send from.
---

# Working with Seamless Messaging

Seamless Messaging connects a team's WhatsApp, Telegram and SMS (Twilio) accounts to Pipedrive. The `seamless-messaging` MCP server gives you the same Inbox the team uses, limited to the workspaces and conversations the signed-in member can see.

## Workspaces

- Call `list_workspaces` first in a session. Every result carries `workspaceId` and `workspaceName`.
- Search and list tools query every approved workspace by default. Pass `workspaceIds` only to narrow down.
- Tools that read or change one item (`get_conversation`, `get_draft`, `create_draft`, `send_draft`, and others) need `workspaceId` when more than one workspace is approved. Take it from the search result; never guess it.
- If the user wants to add or remove a workspace, call `manage_workspace_access` with a new UUID `requestId`. Reuse the same UUID after they approve. Only do this when they ask.

## Finding things

- Text in messages: `search_conversations` with a short `query` (a name, a word from the message, an order number).
- People: `find_contacts`. It pages **per workspace**; while `pagination.hasMore` is true for a workspace, repeat the same query with `cursors` keyed by `workspaceId`.
- One thread: `get_conversation` (recent messages and CRM context) or `get_contact_timeline` (longer history). Conversation keys look like `p:42`, `c:17` or `g:9`.
- Pipedrive deal, person and organisation: `get_crm_context`.
- Groups: `list_groups` (WhatsApp and Telegram). Group ids can be used as draft recipients.

## Channels

Supported channels are `whatsapp`, `telegram` and `twilio` (SMS). Do not offer other channels.

## Sending: always draft, show, confirm

Messages reach real customers, so never send on your own initiative.

1. **Pick the sender.** If several senders could apply, call `list_senders` and use the exact `from` value: an E.164 number for WhatsApp and SMS, the handle or id for Telegram. Never guess a sender.
2. **Create a draft.** Use `create_draft` with `conversationKey` (to reply in an existing thread) or `channel` + `to`. The draft also appears in the team's Inbox, where anyone with access can edit or send it.
3. **Show the user the exact text, recipient, channel and sender**, and ask whether to send.
4. **Send only after an explicit yes** to that exact text, with `send_draft` and the `confirmationToken` from the latest draft response.
5. If the text changes, call `update_draft`. Editing issues a new `confirmationToken`, so a "yes" to older text can never send the newer one.
6. If the user changes their mind, `discard_draft` deletes the draft permanently. Ask first.

Default to leaving a draft rather than sending when the user's intent is unclear. A draft is safe; a sent message cannot be recalled.

## Writing style

- Reply in the language the customer wrote in, unless the user says otherwise.
- Match the thread's tone. WhatsApp and Telegram messages are short and conversational; SMS should be shorter still.
- Bodies are limited to 4096 characters.
- Never invent prices, dates, order statuses or promises. Use only what is in the conversation, CRM context or what the user told you, and ask when something is missing.

## Privacy

Conversations contain customers' personal data. Quote only what the task needs and do not copy message content into other tools unless the user asks.
