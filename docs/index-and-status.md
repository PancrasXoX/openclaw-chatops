# Index & Status (workflow state)

This doc defines the minimal shared state for the three core skills:
- init workspace
- task → thread
- heartbeat (index/digest)

## Status prefixes
- `[WIP]` — active work
- `[BLOCKED]` — waiting on missing info/decision/external dependency
- `[DONE]` — completed (should have an `updates` outcome link)

## What counts as “active”
- Any thread with prefix `[WIP]` or `[BLOCKED]`.
- `[DONE]` threads are only listed in “recent done” for a short window.

## Canonical index location
- The canonical index lives as a **single pinned message** in `updates`.
- If pinning is not available, the canonical index is the latest “Index” message in `updates`.

## Update rules
- `task-thread` skill MAY append/update the index when it creates a new thread.
- `heartbeat` skill SHOULD refresh the index when it detects changes.

## Traceability requirement
- Any status change should be accompanied by a short note in the thread.
- Any final outcome should be posted to `updates` with a link back to the thread.
