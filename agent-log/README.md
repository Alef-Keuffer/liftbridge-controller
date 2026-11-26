# Agent log entries

One file per agent session, named `YYYY-MM-DD-HHMMZ-<outcome-slug>.md`: when the session ended, in UTC, then a few words for what came out of it. Summarize; never paste a raw transcript. `AGENT_LOG.md` at the root is the weekly overview drafted from these files.

Copy this template. The last three fields are optional: fill them when the agent was wrong.

```markdown
# <What came out of the session>

- **Who:** the student who ran the session, and the role (oracles, controller, test driver)
- **Tools:** tool and model, and the skill used, if any
- **Goal:** the task, with its issue number
- **Context given:** the files, issues and decisions the agent was given
- **Prompt (summary):** what was asked, in a sentence or two
- **Outcome:** accepted, corrected or rejected; what came out, with links and spec ids (P1, S1, …)
- **Where it was wrong:** what the agent got wrong
- **Caught by:** how it was noticed: a test, a review, a reread
- **Harness fix:** what changed in AGENTS.md, a skill or a test so that it does not happen again
```
