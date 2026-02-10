---
name: openclaw-chatops-init
description: Initialize a Discord “OpenClaw ChatOps workspace” category and channels (updates/research/work/qa), set channel topics, and pin channel rules/index messages. Use when a user asks to “init/setup/bootstrap a workspace/category”, “create the channel group/structure”, “pin rules to the top”, or “set up the standard ChatOps workflow” for OpenClaw in Discord.
---

# OpenClaw ChatOps — Workspace Init (Discord)

Create a usable workspace in a Discord guild by creating a category + channels and publishing the **Channel Contracts** as pinned operational UI.

## Inputs to confirm (ask only if missing)

- Target guild (if ambiguous).
- Category name (default: `openclaw-chatops`).
- Channel set (default: `updates`, `research`, `work`, `qa`).
- Whether to reuse an existing category/channels or create new.

Do NOT bikeshed naming. If the user did not specify, use defaults.

## Procedure

1) Resolve target guild/channel ids
- Use `message.channel-info` / `message.channel-list` if you need ids.

2) Create (or reuse) the workspace category
- Use `message.category-create` when category does not exist.

3) Create (or reuse) the channels under the category
- Use `message.channel-create` with `parentId=<categoryId>`.
- Keep channels minimal; do not create extra channels unless requested.

4) Set each channel Topic (one-line responsibility)
- Use `message.channel-edit` with `topic=...`.
- Keep topics short; channel topics are not hard rules.

5) Pin operational rules to each channel
- Post a single “Rules” message in each channel, then `message.pin` it.
- The pinned text MUST be skimmable: responsibilities + MUST/MUST NOT.
- Link back to the canonical doc in the repo: `docs/channel-contracts.md`.

6) Create and pin an index message
- In `updates`, post an “Index / How to use this workspace” message and pin it.
- Include:
  - Where to post tasks (work/qa/research)
  - The rule: “every task is a thread”
  - How outcomes flow back to `updates`

7) Verify permissions / visibility (best-effort)
- Confirm the bot can: create threads, send messages, pin messages.
- If you detect missing permissions, report the exact missing capability and the minimal Discord permission fix.

## Output (what success looks like)

- A category with the standard channels exists.
- Each channel has a topic and a pinned “Rules” message.
- `updates` has a pinned “Index” message.

## Trigger phrases (examples)

Natural language:
- “把这个服务器初始化成 OpenClaw 的工作区”
- “帮我创建一个标准的 updates/research/work/qa 频道结构并置顶规则”

Command-style (convention; not required):
- Use the skill slash command (auto-exposed by OpenClaw): `/openclaw_chatops_init`
- Or use the generic runner: `/skill openclaw-chatops-init <your request>`
- Text-command convention (if you do not want native slash): `init workspace` / `chatops init`

## Guardrails

- Never delete or rename existing channels/categories unless explicitly asked.
- If a channel already has important pins, add a new pin but do not unpin existing content.
