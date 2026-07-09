---
description: Capture what was learned this session into the project's persistent file-based memory so future sessions inherit it — non-obvious decisions, current build state, directives, and gotchas. Use after meaningful work, at the end of a session, or when the user says "remember this". Keeps the MEMORY.md index and one-fact-per-file discipline.
---

Sync durable knowledge into project memory. The memory directory is the file-based memory path for THIS project (the one referenced in your system prompt / where existing `MEMORY.md` lives).

1. **Review** what happened since the last sync: decisions made, state changed, directives given, gotchas hit. Ignore anything the repo already records (code structure, git history, things in `CLAUDE.md`).
2. **Filter to what's durable and non-obvious.** A memory earns its place only if a future session would be worse off without it. Convert relative dates to absolute.
3. **Check for an existing file** that already covers each fact — update it in place rather than duplicating. Delete memories that turned out to be wrong.
4. **Write one fact per file** with the standard frontmatter (`name`, `description`, `metadata.type` of user|feedback|project|reference). For `feedback`/`project` facts, add **Why:** and **How to apply:** lines. Link related memories with `[[slug]]`.
5. **Update `MEMORY.md`** — one line per memory (`- [Title](file.md) — hook`). Never put memory content in the index itself.
6. Report a one-line summary of what you added/updated/removed.

This is the mechanism that lets separate sessions and projects share hard-won context. Use it liberally — memory is cheap; re-learning is not.
