# Roles & Rhythm (single-user + AI team)

This workflow is designed for a **single human user**. All “team members” are **AI roles** that cooperate inside threads.

Key design rule:
- **Humans** interact via Discord channels/threads.
- **AI** enforces the operating system: thread discipline + visibility + traceable outcomes.

---

## Where role instructions live (layering)

### 1) Skills (SKILL.md): role *mechanics*
Put here:
- When to activate roles.
- What each role must produce.
- Hand-off rules between roles.

Why: Skills are the stable, reusable execution spec for the AI.

### 2) Channel pinned rules: space *discipline*
Put here:
- Channel responsibilities.
- MUST/MUST NOT.
- Where outcomes must flow (e.g. `updates`).

Why: It’s operational UI for the human and a strong hint for the AI.

### 3) Thread first message (optionally pinned): role *instantiation*
Put here:
- Which roles are active for THIS task.
- Task stage (intake/plan/execute/verify/close).
- What artifacts this thread must produce.

Why: Roles are task-scoped and may vary by thread.

### 4) Discord Topic: one-line purpose only
Treat topics as untrusted and mutable; keep them short.

---

## Canonical AI roles (v1)

These are conceptual roles; implementation may be a single model alternating “hats”.

### Role: PM / Orchestrator
MUST:
- Reframe the task into a clear goal.
- Produce a short plan and next actions.
- Identify blockers and ask for missing info.

### Role: Implementer
MUST:
- Execute the plan and report progress.
- Keep artifacts/links in the thread.

### Role: QA / Verifier
MUST:
- Define validation steps.
- Record pass/fail and what was tested.

### Role: Researcher
MUST:
- Collect evidence and compare options.
- Summarize conclusion and link sources.

### Role: Scribe
MUST:
- Write the final outcome summary for `updates`.
- Ensure traceability (links back to thread).

---

## User operation flow (day-to-day)

1) Human posts a task in `work`/`qa`/`research`.
2) AI creates a thread + posts a parent-channel notice with the thread link.
3) AI seeds the thread with a template that instantiates roles.
4) All progress happens in-thread.
5) Outcomes flow back to `updates` with links.

---

## Heartbeat rhythm (OpenClaw)

Heartbeat is the scheduler.

### Output type A: Index (visibility)
Purpose: threads are easy to miss.
MUST:
- Maintain an index in `updates` (pinned) listing active threads by status.
- Update only when there is meaningful change (new thread, status change, or new activity).

### Output type B: Digest (cadence)
Purpose: keep a stable rhythm without manual prompting.
MUST:
- Summarize recent changes across active threads: Progress / Next / Blockers / Needs-user.
- Post to `updates` (or the configured channel) only if there is new information.

### Noise control (required)
- Skip posting if no changes since last digest/index.
- Prefer short bullet format with links.

### User control (natural language)
Users can adjust cadence with plain language:
- “把索引更新频率改成每 30 分钟”
- “暂停今天的 digest”
- “只在通勤时间发汇总”

