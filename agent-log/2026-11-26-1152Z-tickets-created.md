# Slice the decisions into tickets

- **Who:** Alef Keuffer, before roles were assigned
- **Tools:** Claude Code (Claude Opus 5.5), skill `mattpocock-skills:to-tickets`
- **Goal:** Turn the grilling record into GitHub issues that agents can pick up one at a time.
- **Context given:** the grilling record, the glossary, ADRs 0001–0005, the assignment brief.
- **Prompt (summary):** `/to-tickets` on the grilling record.
- **Outcome:** corrected. Issues #3 to #12: the airlock reference, this agent-log convention, the SPEC and TEST frame, four spec slices (one opening; boat give-up and the race scenario; contention, road priority and clearance; faults), the S1 oracle, the shared safety checker, and the language choice.
- **Where it was wrong:** the first draft sliced the spec work by document section, not by behaviour; it kept the S1 expected log inside the one-opening slice; and it had a ticket to give the teachers access to the repository, which was already done.
- **Caught by:** the human's review of the draft tickets before they were created.
- **Harness fix:** none yet. The draft was corrected: spec work sliced vertically, S1 split into its own oracle ticket (#7, so an oracle session writes it without seeing code, Q3), and the repo-access ticket dropped.
