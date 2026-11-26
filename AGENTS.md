# Project rules for AI agents

Every tool reads this one file: Copilot directly, Claude Code through `CLAUDE.md`. These rules hold for any language. When an implementation exists, its folder gets its own `AGENTS.md` with its architecture and forbidden constructs, as in the airlock.

Read `GLOSSARY.md` first, then `SPEC.md`, then `TEST.md`. SPEC.md and TEST.md are the reference: if the code and the specification disagree, stop and say so, and do not change a property to make a test pass. The decisions behind them are in `docs/adr/` and `docs/grilling/`.

## The airlock is the reference

The teachers' worked example is at `reference/airlock` (a submodule pinned at `51eb571`).

- Mirror its structure, architecture, formats and skills: the root layout, the log and scenario formats, `tracecheck/` (copied unchanged), and the skills in `reference/airlock/.github/skills/`.
- Log every copy: say in the session's agent-log entry what was copied from where, and what was changed.
- The airlock has two doors and one token; the bridge has a road, a river and one span. Watch for two-door assumptions that survive the adaptation: symmetry between the sides, one token passed back and forth, a door's open and closed states standing in for the span's down and raised. When a copied part assumes two of something alike, stop and say so.

## Roles and sessions

- Three roles, each with one human owner: **oracles** (scenarios and expected logs), **controller**, and **test driver**. Owners rotate once, when the main scenario passes.
- Each agent session works for one role only, and says which in its log entry.
- Oracle sessions never see code. They write scenarios and expected logs from SPEC.md and TEST.md alone; do not open implementation folders in them.

## Architecture, in any language

- One component per active object (road controller, river controller, span controller): its own thread, and one bounded, blocking inbox, read with a timeout, that receives the messages of all its senders. A decision function only decides (no I/O, threads or clock); the thread does what was decided.
- The span controller owns the span. The road holds it at rest; the span controller takes it back with `Revoke`, and the lock messages are `Request`, `Granted`, `Release` and `Revoke` (ADR-0001, ADR-0002).
- One function starts the system, the fake hardware included: it creates the queues, starts the threads, and is given the times and the fake hardware's settings. Components get their queues there, never from each other. It knows nothing of the scenario.
- The controller uses only the real clock. Running faster than real time is the test driver's job: it gives shorter times, speeds up the environment the same way, and converts the log back.
- The environment (cars and boats, played by the test driver) talks only to the fake hardware. Neither decides for the controller.
- Only the queues and the run context (the clock, the event log and the stop flag) are shared. Every message is logged, in the exact format SPEC.md fixes for the expected logs.
- `scenarios/`: scenario files and expected logs (`*.expected.txt`), read by every implementation. One test runs every file there.
- The expected logs come from oracle sessions, approved by the oracles' owner. Other sessions propose changes, but do not edit them unless asked.

## Conventions

- One small task at a time. Run every test and the linter before reporting a task as finished, and report any failure as it is.
- Every timing value is a named constant that matches SPEC.md (required times) or TEST.md (test and implementation values).
- Test first: each task starts from a scenario that fails (its file and expected log, from the specification). Implement just enough for it to pass, then refactor with every scenario passing. Never edit an expected log to make a test pass.
- Every failure found by a test becomes a regression scenario.
- An expected log is written from the specification, never from the program's output. If a test shows they differ, stop and say so: either the code or the specification is wrong.
- Every actual log is also checked whole against the safety properties, by the shared Python checker and by each implementation's own check; the two must agree (ADR-0005).
- Tests on threads keep wide margins: no scenario may depend on the order of two events less than half a second apart; where events happen together, the expected log lists every order allowed.
- Traceability: every item in SPEC.md and TEST.md has an id (J journeys, A and E flows, P properties, T transitions, D decisions, S scenarios). Code that provides one carries `Implements: P1`, and a test that checks one carries `Verifies: P1`, in the language's comment syntax. Say which ids each change serves.
- Name domain concepts with the glossary's terms in code, logs and docs, and none of the words it says to avoid.

## Forbidden, in any language

- state shared between components other than the run context (clock, event log, stop flag): send a message instead
- unbounded queues
- sleeping or reading the clock in a decision function
- any library beyond the standard one and the test framework, without the teachers' approval
- risky constructs: `unwrap()` or `expect()` outside tests in Rust, a bare `except:` in Python, a caught and ignored exception in any language, `null` as a message

## Agent log

Every session gets one entry in `agent-log/`, written before the session's work is merged; `agent-log/README.md` has the naming and the template. Summarize the prompt; never paste a raw transcript. Do not add commit trailers that credit the agent. `AGENT_LOG.md` is the weekly overview, drafted from the entries by the prompt it holds.

## Agent skills

### Issue tracker

Issues live in this repo's GitHub Issues, managed with the `gh` CLI. See `docs/agents/issue-tracker.md`.

### Triage labels

The five default labels: needs-triage, needs-info, ready-for-agent, ready-for-human, wontfix. See `docs/agents/triage-labels.md`.

### Domain docs

Single-context: one `GLOSSARY.md` and `docs/adr/` at the repo root. See `docs/agents/domain.md`.
