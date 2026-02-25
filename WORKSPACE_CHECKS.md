# WORKSPACE_CHECKS.md — Source of Truth

## Rules

- Agents MUST NOT execute any command not listed here.
- If a new service is detected (package.json/Cargo.toml/etc.) but missing here:
  - Agent may propose an entry (with evidence)
  - Human must approve before adding
- Prefer pnpm for Node projects.

---

## Entries

### root-docs

- path: .
- stack: node
- install: pnpm -s install
- fmt: pnpm -s format:check
- build: N/A
- lint: N/A
- type: N/A
- test: N/A
