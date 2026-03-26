# AGENTS.md

## Project Overview

This repository contains the source definitions for **The Agency**: specialist AI agents authored as Markdown files and grouped by category directories such as `engineering/`, `sales/`, `support/`, `product/`, and `trader/`.

The authoritative agent definitions live in those category directories. Files under `integrations/` are **generated artifacts** derived from the source agents by the conversion scripts.

If you are editing agents, edit the source `.md` files in the category folders first.

## Repository Structure

Source agents are organized by top-level category folders:

- `academic/`
- `design/`
- `engineering/`
- `game-development/`
- `marketing/`
- `paid-media/`
- `product/`
- `project-management/`
- `sales/`
- `spatial-computing/`
- `specialized/`
- `support/`
- `testing/`
- `trader/`

Supporting files:

- `README.md` — human-facing project overview and agent roster
- `CONTRIBUTING.md` — agent authoring conventions and contribution rules
- `scripts/convert.sh` — converts source agents into tool-specific integration formats
- `scripts/lint-agents.sh` — validates source agent markdown files
- `integrations/` — generated or integration-specific outputs and docs

## Source of Truth and Generated Files

- **Source of truth**: category directories like `support/`, `sales/`, `product/`, `trader/`
- **Generated**: integration outputs under `integrations/<tool>/...`
- Do **not** manually hand-edit generated integration files unless you are intentionally changing the conversion logic itself.
- When an agent changes, regenerate the affected integration outputs from source.

## Authoring Expectations

Match the repository house style documented in `CONTRIBUTING.md` and existing source agents.

At minimum, each source agent should include frontmatter with:

- `name`
- `description`
- `color`
- `emoji`
- `vibe`

Recommended body structure mirrors the repo examples:

- identity / role definition
- core mission or capabilities
- critical rules / constraints
- concrete deliverables or templates
- workflow/process
- communication style
- success metrics

Agents should be narrow, opinionated specialists with concrete outputs, not generic assistants.

## Setup and Validation Commands

Run commands from the repository root.

Lint all source agents:

```bash
./scripts/lint-agents.sh
```

Lint specific source agents while iterating:

```bash
./scripts/lint-agents.sh trader/trader-quant-strategy-engineer.md trader/trader-market-regime-analyst.md trader/trader-strategy-validator.md trader/trader-risk-execution-architect.md
```

Regenerate all integration outputs:

```bash
./scripts/convert.sh
```

Regenerate one tool only:

```bash
./scripts/convert.sh --tool opencode
```

Parallel regeneration is also supported:

```bash
./scripts/convert.sh --parallel
```

## Conversion Workflow

Typical workflow for agent changes:

1. Edit the source agent Markdown in the appropriate category directory.
2. Run `./scripts/lint-agents.sh` on the changed files.
3. Regenerate affected integrations with `./scripts/convert.sh` (or `./scripts/convert.sh --tool <tool>`).
4. Verify generated outputs only reflect the intended source changes.
5. Update `README.md` and `CONTRIBUTING.md` if you added a new category, notable agent, or contribution rule.

## Category Wiring Rule

When adding a **new category directory**, you must also update the `AGENT_DIRS` arrays in:

- `scripts/convert.sh`
- `scripts/lint-agents.sh`

If the new category is not added there, linting and conversion will silently miss its agents.

## Editing Guidance for Coding Agents

- Prefer minimal, targeted edits that preserve existing house style.
- Keep Markdown ASCII unless an existing file already uses Unicode or emoji; emoji in headings/frontmatter is normal in this repo.
- Do not convert source-agent files into another tool's subagent style.
- Preserve the distinction between source content and generated integration content.
- If changing script behavior, keep the logic aligned between `scripts/convert.sh` and `scripts/lint-agents.sh`.

## Contribution Notes

- New agents should be first-class additions: distinctive personality, concrete deliverables, measurable success metrics.
- New categories require doc updates plus script wiring.
- Keep generated-file churn limited to what is justified by the source changes.
- Before considering work complete, verify linting and any needed conversions from the repo root.

## Quick Reference

Common commands:

```bash
./scripts/lint-agents.sh
./scripts/convert.sh
./scripts/convert.sh --tool opencode
```

Use this file together with `README.md` and `CONTRIBUTING.md`; when in doubt, the category source files are the canonical agent definitions.
