# c2c-control-room

A small optional workflow-policy companion for
[`codex-with-chatgpt`](https://github.com/XiaoDuoYa/codex-with-chatgpt).

It adds a stricter development workflow on top of C2C without replacing,
forking, or reimplementing C2C itself.

> ChatGPT plans and reviews. Codex executes.

## Why

`codex-with-chatgpt` already provides the C2C infrastructure and protocol:

- ChatGPT planning and review
- Codex execution
- read-only MCP workspace access
- independent diff/test review
- TASK_ID / iterations
- checkpoints and HANDOFF
- Project / long-chat management
- connector, doctor and repair workflows

`c2c-control-room` intentionally does **not** duplicate any of that.

It adds only a small workflow-policy layer for users who want:

- clearer responsibility boundaries between ChatGPT and Codex;
- smaller, reviewable implementation Gates;
- explicit scope control;
- a compact human-readable progress view;
- Copilot execution by default;
- explicitly authorized Autopilot multi-Gate sprints.

## Modes

Control Room has two user-facing modes:

- **Copilot** — the default. This is the existing `controlled` behavior.
- **Autopilot** — explicit opt-in. This is the existing `unattended` behavior.

The legacy names `controlled` and `unattended` remain valid aliases.

If no mode is specified, Control Room does **not** ask which mode to use. It
starts in Copilot mode.

### Copilot

Copilot is the default whenever Control Room is explicitly requested.

ChatGPT investigates, plans and reviews. Codex executes the current bounded
Gate.

The Gate may go through multiple normal C2C PLAN / execution / review
iterations.

When the Gate reaches `DONE`, execution stops and returns control to the user
before another Gate begins.

### Autopilot

Autopilot must be explicitly requested.

Within a pre-approved sprint scope, Control Room may automatically continue
from one completed Gate to the next.

It stops when:

- the approved success criteria are satisfied;
- a new product or architecture decision is required;
- scope expansion is required;
- human credentials, permissions, consent, CAPTCHA or 2FA are required;
- a destructive or irreversible action needs approval;
- upstream C2C reaches its iteration limit;
- a genuine external blocker prevents progress.

It never invents additional work simply to keep running.

## What this Skill does not do

This project does not create or replace:

- the C2C protocol;
- connectors or tunnels;
- MCP tools;
- TASK_IDs or iteration counters;
- checkpoints or sessions;
- HANDOFF;
- conversation management;
- browser automation;
- doctor / repair behavior;
- execution records;
- C2C security boundaries.

Those remain fully owned by `codex-with-chatgpt`.

If the two Skills ever conflict on operational behavior,
`codex-with-chatgpt` is authoritative.

## Requirements

Install and configure
[`codex-with-chatgpt`](https://github.com/XiaoDuoYa/codex-with-chatgpt)
first.

This Skill is only a companion workflow layer.

## Install

Copy the Skill into your global Codex skills directory:

```bash
mkdir -p ~/.codex/skills/c2c-control-room
cp skill/SKILL.md ~/.codex/skills/c2c-control-room/SKILL.md
```

Start a new Codex conversation after installation so the Skill catalog is refreshed.

## Usage

Explicitly invoke the Skill:

```text
$c2c-control-room
```

or ask for Control Room behavior naturally.

### Copilot — default

```text
$c2c-control-room

Implement the approved task.
```

or:

```text
Use Control Room for this task.
```

No mode argument means **Copilot**. Control Room completes the current bounded
Gate, then stops and returns control to the user.

### Autopilot — explicit opt-in

```text
$c2c-control-room autopilot

Complete the approved sprint.
```

Equivalent wording such as `unattended` remains supported.

Autopilot authorizes Control Room to continue automatically from one completed
Gate to the next inside the approved sprint envelope. It still stops for
material decisions, scope expansion, destructive actions, human-only
authentication, upstream iteration limits, or genuine external blockers.

### Optional two-step initialization

For a long or high-value run, Control Room can be initialized before the
implementation goal is sent:

```text
$c2c-control-room autopilot

Initialize Control Room only. Verify C2C readiness and stop after initialization.
```

After:

```text
Control Room Ready
```

send the actual goal, scope and success criteria.

This two-step launch is optional. It is a readiness workflow, not a requirement
of the Skill.

### Relationship to Codex Goal mode

Codex Desktop Goal mode and Control Room Autopilot are complementary but
independent:

- **Goal mode** controls Codex's persistence toward a target.
- **Autopilot** authorizes Control Room to continue across completed Gates.

Goal mode does **not** imply Autopilot. If Autopilot was not explicitly
authorized, Control Room remains in Copilot mode even when Codex is running in
Goal mode.

For a long fully autonomous sprint, a useful combination is Codex Goal mode
plus `$c2c-control-room autopilot`.

Ordinary codex-with-chatgpt tasks should not activate Control Room.

## Workflow

```text
User
  ↓
c2c-control-room
  │   workflow policy only
  ↓
codex-with-chatgpt
  │   authoritative C2C mechanics
  ↓
C2C protocol / connector / MCP / session / HANDOFF
```

## Design principles

- Policy above infrastructure.
- No duplicated C2C state machine.
- No second session or checkpoint system.
- No automatic scope expansion.
- One meaningful reviewable Gate at a time.
- ChatGPT owns high-level WHAT / WHY.
- Codex owns implementation HOW inside the approved boundary.
- Agent-to-agent communication can stay concise and machine-oriented.
- Human-facing progress uses the user's language.

## Validation

The initial workflow was smoke-tested against a real C2C-enabled workspace for:

- explicit Skill discovery;
- Copilot mode (controlled behavior);
- independent C2C review;
- stopping after a Copilot Gate;
- explicit Autopilot mode (unattended behavior);
- automatic Gate-to-Gate continuation;
- stopping after the approved Autopilot sprint;
- scope containment;
- ordinary codex-with-chatgpt usage not triggering Control Room.

## Status

Early release.
The Skill intentionally remains small so changes in upstream C2C behavior can
be inherited rather than duplicated.

## License

MIT
