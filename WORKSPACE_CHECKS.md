# WORKSPACE_CHECKS.md — Source of Truth

## Rules
- Agents MUST NOT execute any command not listed here.
- If a new service is detected (package.json/Cargo.toml/etc.) but missing here:
  - Agent may propose an entry (with evidence)
  - Human must approve before adding
- Prefer pnpm for Node projects.

---

## Entries

### example-node
- path: ./example-node
- stack: node
- install: pnpm -s install
- fmt:     pnpm -s format:check
- lint:    pnpm -s lint
- type:    pnpm -s typecheck
- test:    pnpm -s test
- build:   pnpm -s build

### example-rust
- path: ./example-rust
- stack: rust
- fmt:     cargo fmt --check
- lint:    cargo clippy -- -D warnings
- test:    cargo test
- build:   cargo build
