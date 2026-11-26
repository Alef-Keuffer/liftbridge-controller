# Grilling record: initial decisions

Started 2026-11-12 and closed 2026-11-26 with `/grill-with-docs` in Claude Code (Opus 5.5). This is the input for `/to-spec` and `/to-tickets`. The vocabulary is in [GLOSSARY.md](../../GLOSSARY.md), and the decisions that are hard to reverse are in [docs/adr/](../adr/).

**Sources:**
- the brief: [TACS_202627_Assignment2.docx.md](../assignment/TACS_202627_Assignment2.docx.md);
- the kickoff slides;
- the airlock worked example, studied at commit `51eb571`;
- research on agent-log practice: the course book, Böckeler and Morris on martinfowler.com, and the AI policies of open-source projects.

**Scope (Q18):** this record settles only the decisions that shape SPEC.md, TEST.md and the process. The spec tickets will write the wording of the journeys, the full message table, the state machines and their transition numbers, the time values, and the scenario list.

## Domain model

| # | Decision | Notes |
| :- | :- | :- |
| Q4 | The **span controller** drives the span: it owns the span motor and the span's position sensors. | [ADR-0001](../adr/0001-span-controller-drives-the-span.md) |
| Q5, Q20 | The road holds the span by default. The lock vocabulary is `Request`, `Granted`, `Release`, plus `Revoke`. | [ADR-0002](../adr/0002-road-holds-the-span-by-default.md) |
| Q19 | The coordinator is named **span controller**. | glossary |
| Q6 | Boats come from one direction only. | [ADR-0004](../adr/0004-boats-from-one-direction.md) |
| Q7 | The barriers are one logical pair, with one command and one confirmation. The road light is green or red only, with no amber. One sensor says whether the span is clear. | goes in the exclusions |
| Q13 | The river side has an approach sensor, the boat signal and a channel sensor. The span never lowers while a boat is in the channel; this is a new safety property. If no boat enters the channel within a named time after green, the signal turns red and the span lowers once the channel is clear. That boat loses its turn and must be detected again. | |
| Q14 | A car that stays on the span makes the road wait indefinitely. The boat's bounded-response property says "unless a car stays on the span". | no new timer |
| Q21 | One boat per **opening**. A boat that arrives during an opening waits for the next one. A new opening starts only after the road has been open for a named minimum time. | follows the brief's "road reopens within T" as written |
| Q22 | After the road light turns red, a named **clearance time** passes before the span is trusted to be clear. | removes the hazard of a car that just passed the light |
| Q8 | A faulted component latches the fault, raises the alarm and keeps the span. There is no reset. | [ADR-0003](../adr/0003-faults-latch-and-keep-the-span.md) |
| Q9 | Exclusions: an operator or manual mode, emergency vehicles, pedestrians and cyclists, boat-height detection, weather, partial raises, cars breaking through the barriers. Assumptions: cars obey the road light, boats obey the boat signal, and the system starts at rest (span down, road open, boat signal red). | |

**Safety properties so far:**
- the span moves only while the road is closed and the span is clear;
- the span never lowers while a boat is in the channel.

**Bounded responses still to name and give values:**
- a boat's wait;
- the road reopening after the boat;
- the barrier and span movement timeouts;
- the boat's give-up time;
- the minimum time the road stays open;
- the clearance time.

## Tests

| # | Decision |
| :- | :- |
| Q23 | Every actual log is checked whole against the safety properties twice: by a shared Python checker next to tracecheck, and in each implementation's own language. The two must agree ([ADR-0005](../adr/0005-shared-safety-checker.md)). |
| Q26 | The required race scenario is a boat entering the channel just as its give-up time ends. It runs 10 times. Its two outcomes are that the boat passes, or that the boat signal turns red and the span lowers only once the channel is clear. |
| Q3 | Write the scenarios and expected logs during the docs phase: before any code exists, they are independent oracles by construction. |

## Process

| # | Decision |
| :- | :- |
| Q1 | The language is **deferred**: documentation first. The brief made the choice a week-1 deliverable. Ada/SPARK is not on the brief's language list, so ask the teachers before using it. |
| Q10 | Use the airlock's layout: SPEC.md, TEST.md, AGENTS.md, README.md, `scenarios/` and `tracecheck/` (copied unchanged) at the root, with one folder per implementation (Rust, Java, maybe Ada/SPARK). Since every implementation shares the expected logs, SPEC.md fixes the exact text of every log line. |
| Q24 | The airlock becomes a git submodule at `reference/airlock`, pinned at `51eb571`. AGENTS.md tells agents to mirror its structure, architecture, formats and skills, to log every copy, and to watch for two-door assumptions that survive the adaptation. |
| Q2 | Tools are mixed (Copilot, Claude Code). One AGENTS.md is read by every tool. |
| Q3 | Each role (oracles, controller, test driver) has one human owner. The agent work runs in role-scoped sessions, and oracle sessions never see code. Owners rotate once, when the main scenario passes (about the start of week 4). |
| Q16, Q25 | The agent log follows the LES two-layer convention. Raw entries go in `agent-log/YYYY-MM-DD-HHMMZ-<outcome-slug>.md`, one per session. The fields are Who, Tools, Goal, Context given, Prompt (summary), Outcome (accepted, corrected or rejected, with links and spec ids), and optionally Where it was wrong, Caught by, and Harness fix. The root `AGENT_LOG.md` is a weekly overview that a coalescing prompt drafts and a person edits; it includes each student's corrected and rejected entries. No commit trailers, and no raw transcripts. |
| Q15 | ADRs keep the history of decisions, and SPEC.md always shows the current state. Its D table summarizes the decisions and links the ADRs. |
| Q12, Q17 | `main` requires a PR. CI (tests, linter, Python for tracecheck) arrives with the first implementation and becomes a required check; no approval is required. PRs are still reviewed by another member, as the brief requires, but a review doesn't block a merge. |

## Open outside this record

- Choose the language or languages, and get the teachers' approval for Ada/SPARK.
- Check that the teachers and every member are collaborators on the repository, and that the link is in the Groups sheet; neither was the case on 2026-11-12.
