---
name: openclaw-chatops-task-thread
description: Turn a Discord channel message into a tracked task by creating a thread, posting a parent-channel notice with the thread link (visibility), and seeding the thread with a structured template. Use when a user says “create a task/thread for this”, “把这个需求/bug 开一个 thread”, “thread 化这个任务”, “start tracking this requirement/bug”, or when the workflow requires one-task-one-thread discipline in Discord.
---

# OpenClaw ChatOps — Task → Thread (Discord)

Convert an ad-hoc requirement/bug into a **threaded task** with guaranteed visibility and a stable structure.

## Procedure

0) Strict triage (AI decision)
- Classify the message intent (best-effort):
  - **Task** (requirement/bug/research to be tracked)
  - **Decision** (needs user confirmation; still trackable)
  - **Info** (material/result; may belong in an existing thread)
  - **Chat/Noise** (no action)
- In **strict mode**, treat **Task/Decision** and **task-like** messages as thread-worthy.
- Target misposts:
  - If detailed discussion appears in a main channel (especially `updates`), immediately contain it in a thread.

1) Identify the parent channel and the task intent
- Determine whether this is `work` (requirement/implementation), `qa` (bug/verification), or `research` (investigation).
- If unclear, default to using the current channel rather than moving it.
- If the message is clearly in the wrong channel, do **soft routing**:
  - create the thread in the correct channel, and
  - leave a short link notice in the original channel.
  - Do not attempt to move/delete the original message.

2) Create the thread
- Use `message.thread-create` from the parent channel.
- Prefer anchoring to the triggering message (use the message id when available) so context is preserved.
- Use a title with status prefix (default: `[WIP]`) and a short name.

3) Post the visibility notice in the parent channel (MUST)
- Immediately send a short parent-channel message:
  - “已创建任务线程：<thread链接>（请在该 thread 内继续）”

4) Seed the thread with an **intake-first** template (MUST)
- Post a short first message that makes the next step obvious.
- If information is incomplete, use an **Intake** variant first (ask only 1–3 minimal questions):
  - Goal / Done definition
  - Next action you want from the AI (research/plan/execute/verify)
  - Blocker (if any)
- Then (or once clarified) seed using the appropriate template from `docs/channel-contracts.md`:
  - Work thread template
  - Bug thread template
  - Research thread template

5) False-alarm / out-of-scope handling (MUST)
- If you later determine this was not a task:
  - change the thread title prefix to `[ARCHIVE]`, and
  - post a short note explaining it.
- Ensure `[ARCHIVE]` threads do not appear in the active index/digest (see `docs/index-and-status.md`).

6) (Optional) Pin the template inside the thread
- If thread pinning is supported and useful, pin the template message.

7) (Optional) Update index
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
- Use the skill slash command (auto-exposed by OpenClaw): `/openclaw_chatops_task_thread <title>`
- Or use the generic runner: `/skill openclaw-chatops-task-thread <title>`
- Text-command convention: `task <title>` / `bug <title>` / `thread <title>`

## Guardrails

- Do not create private threads unless explicitly asked.
- Do not split or merge tasks automatically; one thread should map to one intent.
- Keep the parent channel clean: after creating the thread, move discussion into the thread.
