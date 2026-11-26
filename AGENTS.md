# AGENTS.md

 the specification as reference, the architecture, the conventions, test-first work, and what is forbidden: unbounded queues, state shared between components other than the log and the run context (clock, stop flag), libraries without approval, and risky constructs (unwrap() in Rust, a bare except: in Python, …).

## Agent skills

### Issue tracker

Issues live in this repo's GitHub Issues, managed with the `gh` CLI. See `docs/agents/issue-tracker.md`.

### Triage labels

The five default labels: needs-triage, needs-info, ready-for-agent, ready-for-human, wontfix. See `docs/agents/triage-labels.md`.

### Domain docs

Single-context: one `GLOSSARY.md` and `docs/adr/` at the repo root. See `docs/agents/domain.md`.
