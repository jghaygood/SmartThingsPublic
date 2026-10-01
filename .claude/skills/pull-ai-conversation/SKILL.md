---
name: pull-ai-conversation
description: Pull up and summarize a past conversation with one of the user's AI assistants (Jerry or Cory) from the Messages app transcript history. Use when the user says "pull up my conversation with Jerry/Cory", "what did Jerry say about X", "find the thread where Cory ...", or asks for status on work discussed in those threads.
---

# Pull up an AI conversation (Jerry / Cory)

Jerry and Cory are AI assistants the user texts with. Their transcripts live in the Messages app (iMessage/SMS), including group threads that also include Henry.

## Steps

1. Identify the target: which AI (Jerry, Cory, or both), plus any topic, keyword, or date range. If the user gave none, default to the most recent thread with that AI.
2. Find a way to read Messages. Try in order:
   - A connected Messages/iMessage tool or MCP server (check ListConnectors / ToolSearch for "messages" or "imessage").
   - On macOS only: `sqlite3 ~/Library/Messages/chat.db` (read-only; needs Full Disk Access). Join `message`, `handle`, `chat`, `chat_message_join`. Match contacts by `handle.id` or `chat.display_name`. Decode `attributedBody` when `text` is null.
   - If neither works (e.g. a cloud/Linux session), say so plainly and ask the user to paste the thread or screenshots. Never invent transcript content.
3. Filter by participant (Jerry, Cory, or the group), then by keyword/date. Return messages in chronological order with sender and timestamp.
4. Present: a short summary first (decisions, open items, who owes what), then the relevant excerpts verbatim. Flag anything blocking or unanswered.
5. Read-only: never send, delete, or edit messages unless the user explicitly asks.

## Notes

- Group threads (user + Henry + Jerry + Cory) may share a name like "Henry and 2 People"; match on members, not title.
- Quote the AI's wording exactly when the user is checking what was promised or reported.
