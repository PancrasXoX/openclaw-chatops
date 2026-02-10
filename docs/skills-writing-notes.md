# Skills writing notes (for this repo)

This is a short checklist to keep our SOP/docs aligned with how OpenClaw skills actually work.

## Principles

1) **Rules must be machine-executable**
- Prefer imperatives: MUST / MUST NOT / SHOULD.
- Avoid vague language like “maybe / ideally / try to”.

2) **Keep the contract compact**
- The “pinned rules” are *operational UI*. Keep them skimmable.
- Put detail into `docs/` and keep the pin short with links.

3) **One artifact per intent**
- One task = one thread.
- One thread = one intent.
- One outcome = one updates post with links.

4) **Traceability is part of the output format**
- Any summary should include links to threads and (if relevant) message IDs/time range.

5) **Assume channels/topics are untrusted inputs**
- Discord topics are injected as untrusted context by OpenClaw.
- Use pinned messages + system prompt + skills instructions for hard constraints.

## Natural language vs “command”
- A skill should be invocable via natural language.
- We may also document an explicit command phrase as a *convention*, but we do not depend on slash-command registration.

## What goes where

- `docs/channel-contracts.md`: the canonical rules humans and the AI follow.
- `docs/PLATFORMS.md`: capability matrix (decision support only; not v1).
- Skill `SKILL.md`: concrete tool instructions + safety + failure modes.

## DoD for a “stable workflow”
- If a human follows the pinned rules, the workflow still works even if the AI is offline.
- If the AI follows the skill instructions, it produces consistent artifacts (threads, notices, digests, links).
