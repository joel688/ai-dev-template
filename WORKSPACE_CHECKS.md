# WORKSPACE_CHECKS.md — Source of Truth

## Rules

- Agents MUST NOT execute any command not listed here.
- If a new service is detected (package.json/Cargo.toml/etc.) but missing here:
  - Agent proposes a new entry (with evidence).
  - Human approves.
  - Agent adds the approved entry.
- If a required command is missing from an existing entry:
  - Agent proposes a command update (with evidence).
  - Human approves.
  - Agent updates the approved entry.
- Commands may be executed only when:
  - Gate 3 is approved.
  - The exact command appears in this file.
- Prefer pnpm for Node projects.

---

## Entry Template

Use this exact shape for each entry:

### <entry-id>

- path: <repo-relative service root, e.g. . or services/api>
- stack: <node|python|go|rust|other>
- install: <exact command or N/A>
- fmt: <exact command or N/A>
- build: <exact command or N/A>
- lint: <exact command or N/A>
- type: <exact command or N/A>
- test: <exact command or N/A>

## Field Rules

- `path` must be repo-relative and point to the service/workspace root.
- `stack` identifies the primary runtime/toolchain.
- Command fields must be exact, copy/paste-runnable commands.
- Use `N/A` only when a check is truly not applicable.
- Do not leave required fields blank.
- Keep one entry per service/workspace.

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
