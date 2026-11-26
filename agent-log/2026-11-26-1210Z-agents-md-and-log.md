# Write AGENTS.md and the agent-log convention

- **Who:** Alef Keuffer, before roles were assigned
- **Tools:** Claude Code (Claude Opus 5.5), skill `implement`
- **Goal:** Issue #4: one complete AGENTS.md for every tool, and the agent log in the LES two-layer convention.
- **Context given:** the issue, the grilling record (Q2, Q3, Q16, Q24, Q25), the glossary, ADRs 0001–0005, the brief, and the airlock's `AGENTS.md`, `java/AGENTS.md` and `java/AGENT_LOG.md`.
- **Prompt (summary):** `/implement 4`.
- **Outcome:** accepted. [AGENTS.md](../AGENTS.md) adapted from the airlock's root `AGENTS.md` (architecture, conventions and forbidden list copied and reworded for the three controllers and the span; new sections on the airlock as reference, roles and the agent log); `CLAUDE.md` imports it so Claude Code reads the same file; [the entry template](README.md); [AGENT_LOG.md](../AGENT_LOG.md) with its coalescing prompt; entries for the grilling and `/to-tickets` sessions.
