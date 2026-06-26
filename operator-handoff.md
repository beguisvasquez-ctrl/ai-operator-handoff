# Operator Handoff — Claude x Codex Collaboration Protocol

> Drop this file into the root of any repository.
> Both agents read it on startup to align on roles, ownership, and workflow.

---

## 1. Who Does What

| Dimension | Claude (Cowork / claude.ai) | Codex (VS Code) |
|---|---|---|
| **Primary role** | Source of truth, strategy, memory | Logic, debugging, speed |
| **Strengths** | Long-horizon reasoning, architecture decisions, human-quality prose, context retention across sessions | Fast iteration, precise code edits, catching edge-case bugs, refactoring |
| **Writing** | PRDs, specs, ADRs, commit messages, PR descriptions, comments that read like a human wrote them | Inline code comments, type annotations, test names |
| **Code** | High-level scaffolding, naming conventions, patterns to follow | Implementation, bug fixes, unit tests, performance optimization |
| **Review** | Audits Codex output for correctness against spec and intent | Audits Claude output for logic errors, edge cases, and regressions |
| **Memory** | Owns CLAUDE.md, AGENTS.md, and this file | Reads memory files before starting; never overwrites without Claude sign-off |

**One-sentence rule:** Claude thinks and writes; Codex builds and fixes; both audit each other.

---

## 2. Shared Memory Files

These files are the single source of truth. Both agents read them at the start of every session.

- CLAUDE.md - Claude persistent memory: decisions, context, open questions
- AGENTS.md - Shared agent manifest: who owns what, current sprint goals
- operator-handoff.md - This file: roles, conventions, protocol
- .agent-log/ - Append-only audit log of significant changes (optional)

### Update rules

- **Claude** updates CLAUDE.md after any architectural decision, scope change, or new constraint.
- **Codex** appends a one-line summary to .agent-log/YYYY-MM-DD.md after each completed task.
- Neither agent deletes content from memory files. Use [SUPERSEDED] tag so history is preserved.

---

## 3. File Ownership

| Path pattern | Owner | Notes |
|---|---|---|
| *.md, docs/** | Claude | All prose, specs, and documentation |
| CLAUDE.md, AGENTS.md | Claude | Never overwritten by Codex unilaterally |
| src/**/*.ts, src/**/*.tsx | Codex | Implementation files |
| **/*.test.ts, **/*.spec.ts | Codex | Tests; Claude reviews for coverage intent |
| scripts/**, Makefile | Codex | Automation; Claude approves naming |
| .github/workflows/** | Shared | Claude authors steps; Codex authors runner config |
| *.config.js, *.config.ts | Shared | Discuss before changing |

---

## 4. Git Conventions

Branch naming: type/short-description
Examples: feat/add-search, fix/null-cart, docs/add-adr, refactor/auth-hook

Commit format (Conventional Commits):
  type(scope): short imperative summary
  [optional body - Claude writes for non-trivial commits]
  [optional footer: BREAKING CHANGE / closes #issue]

Types: feat, fix, docs, style, refactor, test, chore, perf

PR descriptions: Claude always authors using What / Why / How / Test plan / Checklist.

---

## 5. Code Style & Linting

- TypeScript strict mode, no any, explicit return types on exports
- Prettier defaults (2-space indent, single quotes, trailing commas)
- ESLint with @typescript-eslint/recommended
- Absolute imports preferred; no circular imports
- camelCase vars/functions, PascalCase components/classes, SCREAMING_SNAKE constants

Codex runs lint + typecheck before marking any task done.
Claude flags style issues in review but does not auto-fix - that is Codex's job.

---

## 6. Mutual Audit Protocol

Every significant change goes through a two-pass review:

  Codex implements -> Claude reviews for intent alignment + prose quality
  Claude drafts spec/doc -> Codex reviews for logical gaps + implementability

Claude auditing Codex code: spec alignment, edge cases, naming clarity, human-readable errors
Codex auditing Claude writing: implementability, missing error states, data model under load, implicit assumptions

---

## 7. Conflict Resolution

1. Codex defers to Claude on: naming, intent, UX copy, architectural direction, PR descriptions
2. Claude defers to Codex on: runtime behavior, edge cases, performance trade-offs, test coverage
3. Genuinely ambiguous: both write reasoning into a Decision needed block in CLAUDE.md and flag for the human

---

## 8. Session Start Checklist

- [ ] Read CLAUDE.md - open questions or blockers from last session?
- [ ] Read AGENTS.md - current sprint goal?
- [ ] Read .agent-log/ for last 2 days - what changed recently?
- [ ] Confirm file ownership before writing to a new area
- [ ] No pending review requests sitting in PRs

---

## 9. Session End / PR Ready Checklist

- [ ] .agent-log entry appended
- [ ] CLAUDE.md updated if any decision was made or reversed
- [ ] Lint + typecheck passing
- [ ] PR description authored by Claude
- [ ] Mutual audit complete (both agents reviewed)
- [ ] No TODO or FIXME left without a linked issue

---

## 10. Quick Reference

- Arch decision needed? Ask Claude first, log in CLAUDE.md
- Found a bug? Codex fixes, Claude reviews the fix
- Writing a spec or doc? Claude drafts, Codex audits for gaps
- Refactoring? Codex leads, Claude approves naming
- Unclear who owns something? Check this file, then ask the human
- Agent wrote something wrong? Other agent flags it - never silently overwrites

---

Last updated by: Claude | Template v1.0
Works with: Claude (Cowork / claude.ai) + OpenAI Codex (VS Code)
