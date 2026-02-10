# Channel Contracts (Topic + Pinned Rules)

This project is **Discord-only (v1)** and is designed to be executed by **OpenClaw skills + heartbeat**.

A *Channel Contract* is the shared operating agreement for humans **and** the AI:
- **Topic**: one-line purpose of the channel.
- **Pinned Rules**: strict “MUST / MUST NOT / SHOULD” rules plus lightweight templates.

> Note (OpenClaw): Discord channel topics are injected as **untrusted context**. If you need hard guarantees, encode them in (1) pinned messages and (2) the agent/system prompts and skills.

---

## Global rules (apply everywhere)

### Task unit = Thread
- Every task/requirement/bug is a **thread**.
- Main channel messages are for: **creating the task**, **linking to the thread**, and **announcing outcomes**.
- All task discussion happens **inside the thread**.

### Visibility guarantee (threads are easy to miss)
- When a thread is created, the bot/human **MUST** post a short notice in the parent channel with a **link to the thread**.
- Avoid private/hidden threads unless explicitly required.

### Misposts / off-topic handling (strict mode)
- If someone posts task-like content in the wrong place (or posts detailed discussion in a main channel), the AI **MUST**:
  - create a thread to contain it, and
  - leave a short parent-channel notice linking to that thread.
- This is a safety mechanism to keep channels readable and keep work traceable.

### Traceability
- Any conclusion/decision MUST include a link to the source thread.
- “Done” means: outcome announced + links + next steps (or explicit “no next steps”).

---

## `updates` — announcements & outcomes

**Topic (1-liner)**
- Final outcomes, key decisions, and periodic digests. Everything important becomes visible here.

**Pinned Rules**
- MUST:
  - Post final outcomes/decisions here (with links to the originating threads).
  - Use the update template below.
- MUST NOT:
  - Run long implementation debates here (move to `work` threads).

**Update template**
- TL;DR:
- Progress:
- Decisions:
- Next:
- Links (threads):

---

## `research` — investigation & evidence

**Topic (1-liner)**
- Research *process* and evidence. Conclusions must be summarized into `updates`.

**Pinned Rules**
- MUST:
  - One research question = one thread.
  - When a conclusion is reached, post a short outcome to `updates` with links.
- SHOULD:
  - Keep raw links/snippets inside the research thread.
- MUST NOT:
  - Turn research channel into general task execution (move execution to `work`).

**Research thread template (first message)**
- Question:
- Context:
- What we already know:
- Sources:
- Candidate answers:
- Decision / Recommendation (when ready):

---

## `work` — requirements & implementation

**Topic (1-liner)**
- Where requirements turn into work. Every requirement is managed as a thread.

**Pinned Rules**
- MUST:
  - Every new requirement/task becomes a thread immediately.
  - Keep the parent channel clean: create task + link thread + announce outcomes.
- SHOULD:
  - Keep a running “Next actions” list in the thread.
- MUST NOT:
  - Discuss multiple tasks in the same thread.

**Work thread template (first message)**
- Background:
- Goal:
- Acceptance criteria:
- Plan / Tasks:
- Blockers:
- Links:

---

## `qa` — bugs & verification

**Topic (1-liner)**
- Bugs, regressions, verification. Every bug is a thread with a reproducible report.

**Pinned Rules**
- MUST:
  - Every bug becomes a thread.
  - Include repro steps + expected vs actual.
  - When verified, post outcome to `updates` with links.
- MUST NOT:
  - “Drive-by bug reports” without a thread.

**Bug thread template (first message)**
- Summary:
- Environment:
- Steps to reproduce:
- Expected:
- Actual:
- Logs/Screenshots:
- Fix notes (when available):
- Verification result:

---

## Threads (task execution space)

**Thread Rules (pinned as the first message in each thread)**
- Keep all task discussion in-thread.
- Keep a visible “Next actions” list.
- When status changes (blocked/done), update the thread title prefix and post a short note.
- When done, post a final summary + link in `updates`.
