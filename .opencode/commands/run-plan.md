---
description: Start the spec-kit phase loop — implement phase-by-phase, verify each phase against AGENTS.md + the constitution, and converge/re-implement on failure. Run after you are happy with plan.md and tasks.md.
agent: orchestrator
subtask: false
---

Start the phased spec-kit orchestration loop now.

Feature directory: `$ARGUMENTS` (if empty, use the `feature_directory` in
`.specify/feature.json`).

Follow your Orchestration Procedure exactly:
- Parse the `## Phase N` sections from that feature's `tasks.md`.
- For each phase in order: delegate to `spec-implementer` (which runs
  `/speckit.implement` scoped to that phase), then to `phase-verifier`
  (AGENTS.md + `.specify/memory/constitution.md`), and only advance on
  `VERDICT: PASS`.
- On `VERDICT: FAIL`: delegate to `spec-converger` (which runs
  `/speckit.converge` to append remediation tasks), re-implement the appended
  tasks, and re-verify — up to 3 iterations, then hand off to me.
- Finish with a final `/speckit.converge` confirmation and a summary.

Report each phase's verdict as you go. Do not edit files yourself.