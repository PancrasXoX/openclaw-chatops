---
name: openclaw-chatops-task-thread
description: Turn a Discord channel message into a tracked task by creating a thread, posting a parent-channel notice with the thread link (visibility), and seeding the thread with a structured template. Use when a user says “create a task/thread for this”, “把这个需求/bug 开一个 thread”, “thread 化这个任务”, “start tracking this requirement/bug”, or when the workflow requires one-task-one-thread discipline in Discord.
---

# OpenClaw ChatOps — Task → Thread (Discord)

Convert an ad-hoc requirement/bug into a **threaded task** with guaranteed visibility and a stable structure.

## Procedure

1) Identify the parent channel and the task intent
- Determine whether this is `work` (requirement/implementation), `qa` (bug/verification), or `research` (investigation).
- If unclear, default to using the current channel rather than moving it.

2) Create the thread
- Use `message.thread-create` from the parent channel.
- Use a title that includes a status prefix (default: `[WIP]`) and a short name.

3) Post the visibility notice in the parent channel (MUST)
- Immediately send a short parent-channel message:
  - “已创建任务线程：<thread链接>（请在该 thread 内继续）”
- This is mandatory because threads are easy to miss.

4) Seed the thread with a template message (MUST)
- First message in thread includes:
  - Background
  - Goal
  - Acceptance criteria
  - Next actions
  - Blockers
  - Links

5) (Optional) Pin the template inside the thread
- If thread pinning is supported and useful, pin the template message.

6) (Optional) Update index
- If there is a known index message (typically pinned in `updates`), append or update it with the new thread link.
- If no index exists yet, do not invent one; suggest running workspace init.

## Output (what success looks like)

- A thread exists for the task.
- The parent channel contains a notice linking to the thread.
- The thread contains a structured first message that makes next steps obvious.

## Trigger phrases (examples)

Natural language:
- “给这个开个 thread 继续”
- “把这个 bug 线程化跟踪一下”
- “把需求收口到一个 thread”

Command-style (convention; not required):
- `/task <title>`
- `/bug <title>`
- `/thread <title>`

## Guardrails

- Do not create private threads unless explicitly asked.
- Do not split or merge tasks automatically; one thread should map to one intent.
- Keep the parent channel clean: after creating the thread, move discussion into the thread.
