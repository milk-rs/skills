---
name: write-agents-md
description: Create or update a concise AGENTS.md for a repository. Use when asked to write, simplify, audit, or refresh AGENTS.md or coding-agent instructions. Produces a small, high-signal file without unverified technology examples, attribution policy, generated markers, or exhaustive file inventories.
---

# Write AGENTS.md

Create or update `AGENTS.md` as compact, durable operating notes for future coding-agent sessions.

Every line must pass this test: **Would an agent likely make a wrong guess without this?** If not, omit it.

## Core Principles

- Keep the file small: target 20-50 lines; exceed that only for genuinely unusual repositories.
- Prefer stable facts over detailed inventories that drift.
- Record what changes agent behavior: exact commands, non-obvious setup, important boundaries, and hard-earned gotchas.
- Do not include AI attribution, `Co-Authored-By`, commit authorship rules, generated timestamps, managed-section markers, or symlink instructions.
- Infer technologies and tools only from the target repository; never carry over technologies from prompts, templates, prior examples, or user anecdotes unless repository evidence verifies them.
- The generated `AGENTS.md` may name the repository's verified technologies and tools when they change how agents should work, such as exact commands, required versions, generated artifacts, migrations, or unusual setup.
- Do not explain common software practices, generic safety rules, or agent behavior defaults.
- Do not create nested instruction files unless the user explicitly asks for them.

## Investigation

Read the highest-signal sources first:

1. Existing instruction files: `AGENTS.md`, tool-specific instruction files, repo-local agent config.
2. Human docs: readme, contributing, security, architecture, release, or policy docs.
3. Executable truth: manifests, task runners, build/test/lint/format/codegen config, CI, hooks.
4. Representative code only when docs and config do not reveal the system shape.

Trust executable config over prose when they conflict. Ask the user only when an important team convention cannot be inferred from the repository.

## What To Include

Use only sections that add value. Prefer this order:

```markdown
# AGENTS.md

## Project
- One sentence describing what this repository does.

## Commands
| Task | Command |
|------|---------|
| ... | `...` |

## Structure
- `path/`: short, stable responsibility.

## Rules
- Repo-specific constraint or gotcha.
```

### Project

- One sentence only.
- State purpose, not a broad inventory of tools; mention verified technologies elsewhere only when they change agent behavior.

### Commands

- Include exact commands found in executable sources.
- Prefer focused verification commands when available.
- Include full-repo checks only when they are the only reliable command or are used by CI.
- Do not invent single-test or local-development commands.
- If command order matters, state the order in one bullet.

### Structure

- List only top-level or architecturally important paths.
- Describe directory responsibility, not every file.
- Omit paths whose names already say everything.
- Do not include generated, cache, vendor, build-output, or dependency directories unless agents must avoid or regenerate them.

### Rules

Include only repository-specific rules, such as:

- Config or secret handling that differs from ordinary expectations.
- Generated files, migrations, schemas, fixtures, or assets that require a special workflow.
- Expensive, flaky, external-service, or stateful checks.
- Public interface, persistence, protocol, or deployment boundaries that require extra care.
- Existing docs that should be treated as source of truth.

## What To Exclude

Remove these even if previous files contain them:

- Welcome text, explanations of what `AGENTS.md` is, or conclusions.
- Generic advice: write clean code, add tests, follow best practices, do not introduce bugs.
- Exhaustive file trees or per-file descriptions.
- Language, runtime, framework, package manager, or tool claims that are not verified in this repository.
- Duplicated linter, formatter, typechecker, or style config.
- Contributor, branch, PR, release, or commit rules unless they are explicitly documented in the repository or requested by the user.
- Agent identity, disclosure, or authorship policy.
- Temporary observations, speculation, or TODOs.

## Update Existing Files

When `AGENTS.md` exists:

1. Preserve concise, verified, repo-specific guidance.
2. Delete stale, generic, speculative, or over-detailed content.
3. Reconcile commands and paths against current executable sources.
4. Keep user-owned custom sections only if they still meet this skill's signal bar.
5. Prefer surgical edits over a full rewrite unless the file is mostly noise.

## Verification Before Writing

Before creating or updating the file, check:

- Every command and path exists or is documented in a verified source.
- No unverified technology claims or example-driven assumptions remain.
- Structure stops at stable directory responsibilities, not file-level descriptions.
- The file has no attribution policy, generated markers, timestamps, or symlink instructions.
- The final file is short enough that future agents will read it instead of skimming it.
