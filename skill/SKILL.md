---
name: codex-autopilot
description: >
  Explicitly requested autonomous execution of a multi-Gate sprint, with each
  Gate handled as one complete codex-with-chatgpt task. Do not activate for
  ordinary bounded tasks or infer authorization from requests to continue,
  finish, automate, or from Goal mode.
---

# Codex Autopilot

This Skill coordinates an approved sprint across ordinary
[`codex-with-chatgpt`](https://github.com/XiaoDuoYa/codex-with-chatgpt) tasks.
It does not replace that Skill. C2C owns its setup, task workflow, review,
recovery, and protocol. Its current instructions are authoritative.

## Activation

Activate only when the user explicitly requests Autopilot for autonomous,
multi-Gate execution, for example:

- `$codex-autopilot autopilot`
- “Run this sprint autonomously with Codex Autopilot.”

Do not infer that authorization from “continue,” “finish this,” “do it,”
“automatic,” Goal mode, or task size. For one bounded task, use
`codex-with-chatgpt` directly.

## Initialization

The user may initialize Autopilot before giving the sprint goal. In that case,
follow the current `codex-with-chatgpt` readiness workflow and let it establish
whatever readiness it requires. Do not modify project files, invent a goal,
or begin implementation. Stop once C2C is ready. If the user requested the
standard acknowledgement, reply exactly:

`Codex Autopilot Ready`

The user provides the sprint goal and its scope, constraints, and success
criteria in the next message. Surface any human action required by C2C.

## Sprint loop

Treat the user's explicit Autopilot request and sufficiently specified goal as
the sprint authorization. Establish a concise envelope from available context:
goal, in-scope work, exclusions, constraints, and success criteria. Do not
invent requirements or ask for information already available. If the goal is
clear enough, proceed.

Choose meaningful, bounded, independently reviewable Gates within that
envelope. Refine the remaining Gates as repository facts emerge, but do not
expand scope or create work merely to continue. The invariant is:

**One Gate is exactly one complete upstream C2C task.**

Run each Gate through the normal `codex-with-chatgpt` workflow. Let that Skill
handle its own iterations and review. Do not start the next Gate until the
current upstream task reaches `DONE`; then check the sprint criteria and
either finish, stop for a material decision, or start a fresh C2C task for the
next in-scope Gate. A `PLAN` within a Gate remains part of that same upstream
task.

Do not create another protocol, task identifier, iteration counter,
checkpoint, session, or recovery mechanism. The Gate is only an orchestration
unit above C2C.

## Responsibility and stopping

`codex-with-chatgpt` owns planning and review for each task, execution
mechanics, setup, browser and connector behavior, conversation management,
protocol, and recovery. Codex performs repository work and local validation
under the approved scope. This Skill owns only the sprint envelope, Gate
selection, continuation between completed tasks, overall completion, and
scope enforcement.

Continue through ordinary engineering failures and scope-local repairs using
the upstream workflow. Stop and return control when the sprint criteria are
met, or when progress requires a material decision, scope expansion,
destructive or irreversible action, security/privacy judgment, human-only
action, or external dependency. Also stop when upstream C2C reaches its own
limit or reports a genuine blocker; never bypass or extend its limits.

When useful, report Autopilot status, the sprint goal, current and completed
Gates, the relevant upstream state, the next action, and any blocker. Keep this
as a brief status update, not a persisted workflow format.
