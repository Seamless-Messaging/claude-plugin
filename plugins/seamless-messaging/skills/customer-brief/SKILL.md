---
name: customer-brief
description: Build a short brief about a customer from their WhatsApp, Telegram and SMS history plus Pipedrive context. Use before a call or meeting, or when the user asks "what's going on with this client", "catch me up on Acme", "what did we promise Anna", "summarise my conversation with this customer".
argument-hint: "[customer name, company or phone number]"
---

# Customer brief

This skill only reads. It never creates drafts or sends messages unless the user asks for that afterwards. Follow the `messaging-basics` skill for workspaces and lookups.

1. **Find the customer** with `find_contacts` (follow pagination until every workspace has `hasMore: false`) or `search_conversations`. If several people match, ask which one.
2. **Collect the history.** For each of the customer's conversations (they may have more than one channel or be in a group), use `get_contact_timeline`, and page back with `nextBefore` when the period the user cares about is older. Add `get_crm_context` for the Pipedrive deal. When a recent message carries a document or image that matters (an offer, an invoice, a photo of a problem), read it with `get_attachment`.
3. **Write the brief** in the user's language, compact:
   - **Who**: name, company, channels and numbers used, workspace.
   - **Deal**: Pipedrive deal, stage, value and owner, if available.
   - **Recent conversation**: three to six bullets, newest first, with dates.
   - **Open items**: questions the customer asked that nobody answered, and anything the team promised (with the date it was promised).
   - **Mood and risks**: complaints, urgency, or long silences.
   - **Suggested next step**: one line.
4. Quote messages only when the exact wording matters. Mark anything you inferred as inferred.
5. If the user then wants to reply, continue with the `reply-to-customer` skill.
