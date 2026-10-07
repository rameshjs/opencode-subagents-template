# opencode-subagents-template

An [OpenCode](https://opencode.ai) sub-agent setup for **spec-driven development**
with [GitHub Spec Kit](https://github.com/github/spec-kit). Drop `.opencode/` +
`opencode.json` into any project and get a phased `implement -> verify -> converge`
loop driven by an orchestrator agent.

## What's inside

```
.opencode/
  agents/
    orchestrator.md      # primary agent: drives the phase loop, never edits code
    spec-implementer.md  # executes /speckit.implement for one phase only
    phase-verifier.md    # read-only tester: reports PASS/FAIL, fixes nothing
    spec-converger.md    # runs /speckit.converge (append-only remediation tasks)
  commands/
    run-plan.md          # /run-plan - kick off the orchestration loop
    speckit.*.md         # the Spec Kit slash commands the agents read & follow
opencode.json            # OpenCode config (plugin: @dietrichgebert/ponytail)
AGENTS.md                # minimal stub - replace with your project's rules
```

## How it works

`/run-plan <feature-dir>` starts the `orchestrator`, which reads `tasks.md` and
walks it phase by phase:

1. **spec-implementer** runs the spec-kit implement step for exactly one phase.
2. **phase-verifier** audits that phase against `AGENTS.md` and the project
   constitution (read-only) and returns `VERDICT: PASS` / `VERDICT: FAIL`.
3. On **FAIL**, **spec-converger** appends remediation tasks via the converge
   step, the implementer runs them, and the verifier re-checks (max 3 rounds).

The orchestrator never edits files itself — it only delegates and gates on
verdicts.

## Requirements

- [OpenCode](https://opencode.ai) installed.
- [GitHub Spec Kit](https://github.com/github/spec-kit) initialised in the target
  project (`.specify/`), so the `speckit.*` command files can find their scripts
  and templates.
- An `AGENTS.md` describing your project (a stub is included) and
  `.specify/memory/constitution.md` for the principles the verifier enforces.

> This template ships the **OpenCode sub-agent setup only**. Spec Kit itself
> (`.specify/`) is installed separately per project via the `specify` CLI.

## Install

Copy the following into the root of your project:

- `.opencode/` (agents + commands)
- `opencode.json`
- `AGENTS.md` (then edit it for your project)

OpenCode will install the plugin dependency on first run.

## Models

Each agent pins a model in its frontmatter; change them to whatever you have
available:

| Agent | Model |
| --- | --- |
| `orchestrator` | `openrouter/deepseek/deepseek-v4.1-flash` |
| `spec-implementer` | `openrouter/deepseek/deepseek-v4.1-flash` |
| `spec-converger` | `openrouter/deepseek/deepseek-v4.1-flash` |
| `phase-verifier` | `openrouter/z-ai/glm-5.3` |

Using a different model for the verifier than the implementer is intentional —
it gives an independent check.