# Workflow layer: hybrid (Matt Pocock for requirements, Superpowers for execution)

Skill packs: [mattpocock/skills](https://github.com/mattpocock/skills) (`mattpocock-skills@mattpocock`) and [obra/superpowers](https://github.com/obra/superpowers) (`superpowers@superpowers-marketplace`). Both are installed; this table decides which one runs at each step, so they never compete.

| Factory step (docs/dsf/workflows.md) | Mode | Skill (pack) | Output goes to |
| --- | --- | --- | --- |
| PRD interview | design | `/grill-with-docs` (Matt), then `/to-spec` (Matt) | `specs/prd.md`, `GLOSSARY.md` |
| UAT interview | design | `dsf-uat-interview` (factory) | `uat/features/` |
| Architecture | design | `dsf-architect` (factory), using `/codebase-design` and `/domain-modeling` (Matt) | `docs/architecture/` |
| Plan into tasks | design | `/to-tickets` (Matt) for tracer-bullet tickets; `writing-plans` (Superpowers) for the step-by-step plan of one ticket | task backend; `plans/` |
| Build | build | `subagent-driven-development` with `test-driven-development` (Superpowers), in a worktree from `using-git-worktrees` | `src/`, tests, `uat/steps/` |
| Bugfix | build | `/diagnosing-bugs` (Matt) to find the cause, then `test-driven-development` (Superpowers) | failing test first, then the fix |
| Review | build | `dsf-code-reviewer` (factory) through `requesting-code-review`; `/code-review` (Matt) as a second pass | PR comments |
| Finish | build | `verification-before-completion` (run `make check`), `finishing-a-development-branch` choosing "open a pull request" (Superpowers), `/pr` (Matt) for the description | PR |
| Exploration | design | `/research` and `/prototype` (Matt) on a `spike/` branch | `docs/architecture/proposals/` |
| Architecture maintenance | design | `dsf-arch-maintenance` (factory), with `/improve-codebase-architecture` (Matt) | `docs/architecture/proposals/` |
| Factory | factory | `dsf-factory-improve` (factory); `/retro` (Matt) to collect lessons; `writing-skills` (Superpowers) for new skills | `.claude/skills/` |

Rules for the overlap:

- Superpowers' `brainstorming` would also run before design work. In this factory the requirements interview is `/grill-with-docs`; use `brainstorming` only to compare solution options inside a step.
- For test-first work use Superpowers' `test-driven-development`, not Matt's `/tdd`.
- The Matt pack's configuration is in `docs/agents/` (task backend, ADRs in `docs/architecture/adr/`); do not run `/setup-matt-pocock-skills` unless the human asks.
- Specs go to `specs/` (not `docs/superpowers/specs/` or the issue tracker), plans to `plans/`, ADRs to `docs/architecture/adr/`.
- Never merge into `main` locally; always open a PR.
