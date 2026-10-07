# Project Guidelines

<!--
This is a minimal stub. Replace the sections below with your project's real
rules. The sub-agents in `.opencode/agents/` treat this file (together with
`.specify/memory/constitution.md`) as the source of truth they verify work
against, so keep it accurate and specific.
-->

## Overview
Describe the project: purpose, stack, and the directories that matter.

## Architecture & Layering
- Describe the layers (e.g. endpoints -> services -> repositories) and what each
  layer may and may not do.

## Code Style
- Language/style rules, import conventions, validation approach, naming.

## Testing & Verification
- The exact commands an agent should run before declaring work done
  (e.g. `npm run typecheck`, `npm test`).

## Boundaries
- Files or directories agents must not touch.
- Any secrets/credentials handling rules.