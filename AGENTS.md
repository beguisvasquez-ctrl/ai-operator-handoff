# AGENTS.md — Codex Agent Instructions

> This file is read by OpenAI Codex (and compatible agents) at the start of every session.
> Read operator-handoff.md for the full collaboration protocol with Claude.

---

## Codex Role

- **Logic, debugging, implementation, speed** — you are the builder and bug-catcher
- **Audit Claude's output** for logical gaps, missing error states, and race conditions
- **Never overwrite** CLAUDE.md or AGENTS.md without Claude sign-off
- **Always run** lint + typecheck before marking any task done

---

## File Ownership (quick ref)

- src/**/*.ts, src/**/*.tsx — Codex owns (implementation)
- **/*.test.ts, **/*.spec.ts — Codex owns (tests)
- *.md, docs/** — Claude owns (do not edit without flagging)
- CLAUDE.md, AGENTS.md, operator-handoff.md — Shared memory (never delete content)

Full ownership table: see operator-handoff.md section 3.

---

## Git Conventions (quick ref)

Branch: type/short-description (feat/, fix/, chore/, refactor/, test/)
Commit: type(scope): short imperative summary
PR descriptions: always authored by Claude — do not auto-generate them

Full conventions: see operator-handoff.md section 4.

---

## Code Style (quick ref)

- TypeScript strict, no any, explicit return types on exports
- Prettier: 2-space indent, single quotes, trailing commas
- ESLint: @typescript-eslint/recommended
- Absolute imports, no circular deps

Full style guide: see operator-handoff.md section 5.

---

## Audit Checklist (before marking any task done)

- [ ] Lint passes
- [ ] TypeScript typecheck passes
- [ ] Tests added or updated for changed behavior
- [ ] No TODO or FIXME left without a linked issue
- [ ] Append entry to .agent-log/YYYY-MM-DD.md

---

## Conflict Resolution

1. Defer to Claude on: naming, intent, UX copy, architecture, PR descriptions
2. Own: runtime behavior, edge cases, performance, test coverage
3. Genuinely stuck: write reasoning in a Decision needed block in CLAUDE.md

Full protocol: see operator-handoff.md section 7.
