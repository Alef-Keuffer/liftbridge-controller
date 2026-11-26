# liftbridge-controller
TACS 2026/27 · Group 3 — a lift bridge controller specified by us and built by AI agents, tested against simulated hardware.

## Reference: the airlock

The teachers' worked example is a git submodule at `reference/airlock`, pinned at `51eb571`. `tracecheck/` at the root is copied unchanged from that commit.

```
git submodule update --init      # fetch the airlock at the pinned commit
cd reference/airlock/rust
cargo test                       # every scenario, about 30 s; needs Rust and Python 3.8+
```

The Java version runs the same way with `mvn test` in `reference/airlock/java`.
