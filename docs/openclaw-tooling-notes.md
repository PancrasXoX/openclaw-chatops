# OpenClaw + Discord tooling notes (capabilities, permissions, failure modes)

This doc is a practical reference for implementing ChatOps skills on top of OpenClaw’s Discord channel.

## Core facts (from OpenClaw docs)
- **Threads inherit parent channel config** (allowlists, `requireMention`, skills filters, prompts) unless you add per-thread overrides.
- Guild channels are often **mention-gated by default** (`requireMention`). If the bot appears “silent”, check per-guild/per-channel `requireMention` and mentionPatterns.
- Pins and threads are supported by the `message` tool, but require:
  - Discord permissions in that channel, and
  - OpenClaw Discord action gates enabled (e.g. `channels.discord.actions.pins`, `threads`).

## Required Discord capabilities (typical)
- Create thread / send messages in parent channel
- Send messages in thread
- Manage pins (if the workflow requires pinning)

## Recommended skill fallbacks
- **Pin failed** (permission or action gate): post a “Canonical link” message instead, and ask a human to pin if needed.
- **Thread create failed**: fall back to posting a structured template in-channel (and clearly mark that thread creation is unavailable).

## Token/format limits
- Discord outbound messages are chunked (character and line limits). Prefer short bullet outputs.

## Reference
- OpenClaw docs: `channels/discord` and `tools/slash-commands`.
