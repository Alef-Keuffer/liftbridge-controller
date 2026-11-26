# Install the airlock reference

- **Who:** Alef Keuffer
- **Tools:** Claude Code (Claude Opus 5.5), skill `mattpocock-skills:implement`
- **Goal:** Issue #3: add the airlock as a submodule, copy `tracecheck/`, run the worked example.
- **Context given:** the issue, the grilling record (Q10, Q24, Q16/Q25), the assignment brief.
- **Prompt (summary):** `/implement 3`.
- **Outcome:** accepted. `reference/airlock` is a submodule pinned at `51eb571`. `tracecheck/` was copied unchanged from that commit (`diff -r` shows no difference). `cargo test` in `reference/airlock/rust` passed (`every_scenario_file`, 26 s). The Java version was not run: Maven is not installed here.
