# Platforms capability matrix (draft)

This doc is used to decide what we can support beyond Discord.

## Capabilities we care about
- Threads
- Pin / unpin
- Reactions
- Rich text / formatting
- Mentions
- File upload
- Search / history fetch
- Webhook / events / bot permissions model

## Platforms (initial hypotheses)
- Discord: strong across threads/pins/reactions.
- Slack: likely strong (threads, reactions), but API/permissions differ.
- Telegram: has threads (topics in groups) and reactions, but feature parity varies; bot APIs can be limiting.
- WhatsApp/Signal: typically more limited and/or more constrained APIs.

