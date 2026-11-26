# Safety is checked over whole logs twice: one shared checker and one per language

A `...` gap in an expected log can hide a violation, so every actual log is also checked whole against the safety properties:
- the span moves only while the road is closed and the span is clear;
- the span never lowers while a boat is in the channel.

One small Python checker next to tracecheck is the shared baseline, and every implementation's tests run it. Each implementation also checks the same properties in its own language, as the airlock does. The two must agree. This is duplication on purpose: there may be several implementations (Rust, Java, maybe Ada/SPARK), Python is already required for tracecheck, and a disagreement between the two checkers is itself a finding.
