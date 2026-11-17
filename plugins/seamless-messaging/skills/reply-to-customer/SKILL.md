---
name: reply-to-customer
description: Draft a reply to a customer's WhatsApp, Telegram or SMS message using the conversation history and Pipedrive context, then send it only after the user approves. Use when the user says things like "reply to Anna", "answer the last message from Acme", "what should I tell this client", "draft a follow-up to the WhatsApp from yesterday".
argument-hint: "[customer name, company or phone number] [what the reply should say]"
---

# Reply to a customer

Follow the rules in the `messaging-basics` skill, especially the draft-confirm-send flow.

1. **Find the conversation.** Search for the customer the user named:
   - `find_contacts` for a name, company or phone number;
   - `search_conversations` for words from the message.

   If several conversations match, show a short list (name, channel, workspace, last message date) and ask which one. Do not pick for the user.
2. **Read the context.**
   - `get_conversation` for the recent messages.
   - `get_crm_context` for the Pipedrive deal, stage, owner and notes.
   - If the thread is long or refers to earlier messages, use `get_contact_timeline` (page back with `nextBefore`).
   - If the customer sent a file, photo or voice note you need to answer, open it with `get_attachment`.
3. **Work out what needs answering.** Summarise the customer's last message(s) in one or two lines, plus anything still open (questions not answered, promised follow-ups).
4. **Write the reply.**
   - Use the customer's language and the tone of the thread.
   - Use what the user asked you to say. Fill in facts only from the conversation or CRM.
   - Ask the user rather than inventing a missing fact: a price, a date, an availability, a status.
5. **Create a draft** with `create_draft` and the `conversationKey`, so it goes back on the same channel and thread. If more than one sender could apply, check `list_senders` first. If the user wants a file sent with it, add it with `attach_file_to_draft`.
6. **Show the draft**: recipient, channel, sending number or account, the full text and any attached file. Ask whether to send, change it, or leave it as a draft in the Inbox.
7. **On an explicit yes**, call `send_draft` with the latest `confirmationToken` and report the result. On changes, `update_draft` and show it again.
