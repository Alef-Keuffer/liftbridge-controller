# Agent log

The weekly overview of the agent work. The entries themselves, one per session, are in [`agent-log/`](agent-log/). Each week, run the prompt below, then edit its draft: it is a draft, and a person answers for what stays.

## Coalescing prompt

> Read every file in `agent-log/` dated in week N of the assignment (week 1 is 2026-11-12 to 11-18, Thursday to Wednesday, UTC; week 4 ends 2026-12-09) and draft that week's section of `AGENT_LOG.md`. Write one table row per entry: date, who, tool and model, skill, goal, outcome (accepted, corrected or rejected), and a link to the entry. Under the table, in at most five sentences, say what the agents got wrong that week, how it was caught, and what changed in the harness. Then add every corrected or rejected entry of the week to its student's list under "Corrected and rejected, by student", one line each with a link. Copy facts from the entries only; do not add any, and do not quote transcripts.

## Weeks 1 and 2 (2026-11-12 → 11-25)

No entries: the grilling session ran through both weeks and ended in week 3, where its entry is.

## Week 3 (2026-11-26 → 12-02)

| Date | Who | Tool and model | Skill | Goal | Outcome | Entry |
| :- | :- | :- | :- | :- | :- | :- |
| 11-12 → 11-26 | Alef Keuffer | Claude Code, Opus 5.5 | `grill-with-docs` | Initial decisions: glossary, ADRs 0001–0005, grilling record | accepted | [entry](agent-log/2026-11-26-1138Z-initial-decisions-recorded.md) |
| 11-26 | Alef Keuffer | Claude Code, Opus 5.5 | `to-tickets` | Tickets #3–#12 from the grilling record | corrected | [entry](agent-log/2026-11-26-1152Z-tickets-created.md) |
| 11-26 | Alef Keuffer | Claude Code, Opus 5.5 | `implement` | #3: install the airlock reference | accepted | [entry](agent-log/2026-11-26-1158Z-airlock-installed.md) |
| 11-26 | Alef Keuffer | Claude Code, Opus 5.5 | `implement` | #4: AGENTS.md and this log | accepted | [entry](agent-log/2026-11-26-1230Z-agents-md-and-log.md) |

The ticket draft sliced the spec by document section, kept the S1 expected log inside a spec slice, and had a ticket for work already done; the human's review caught all three before the tickets were created.

## Corrected and rejected, by student

The brief asks for at least two per student. Add one heading per member.

### Alef Keuffer

- 2026-11-26, corrected: [ticket slicing](agent-log/2026-11-26-1152Z-tickets-created.md)
