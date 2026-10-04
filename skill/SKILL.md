---
name: codex-autopilot
description: >
  Autonomous multi-Gate sprint orchestration for Codex, built on
  codex-with-chatgpt. Activate when the user explicitly invokes this Skill or
  clearly asks to use Codex Autopilot for a sprint. Do not infer authorization
  from requests to continue, finish, automate, or from Goal mode.
---

# Codex Autopilot

Codex Autopilot coordinates an approved sprint across ordinary
[`codex-with-chatgpt`](https://github.com/XiaoDuoYa/codex-with-chatgpt) tasks.
It owns only the outer sprint loop. Upstream C2C owns readiness and all
individual-task mechanics; its current instructions are authoritative.

## Activation and readiness

Explicit invocation of this Skill authorizes autonomous multi-Gate execution
within the user's approved Sprint Envelope. A clear natural-language request
to use Codex Autopilot for a sprint may also activate this Skill when normal
Skill discovery supports it. Do not infer authorization from “continue,”
“finish this,” “do it,” “automatic,” Goal mode, or task size. For one bounded
task that needs ChatGPT planning and review, use `codex-with-chatgpt` directly.

Before Gate 1, invoke the normal upstream `codex-with-chatgpt` readiness
workflow and proceed only when readiness is green. Reuse existing connector,
Project, conversation/session state, and endpoint according to upstream rules.
Follow upstream for workspace setup. A first-time workspace may require a
human authorization step or supported guided fallback; surface and wait for
any required human action. Do not bypass it.

For important or long runs, recommend a two-step launch. On the first
`$codex-autopilot` message, the user may ask to initialize only. Establish
upstream readiness, define or confirm the execution boundary, make no project
changes, and stop before implementation. When ready, reply exactly:

`Codex Autopilot Ready`

The user's next message supplies the Sprint Goal / Sprint Envelope and begins
Gate execution. This is a launch workflow, not a separate mode or argument. A
user may also invoke `$codex-autopilot` with the Sprint Envelope in one message
when the goal is clear and readiness can be completed cleanly.

## Sprint Envelope and loop

Keep the Sprint Envelope concise and operational: goal, allowed scope,
important constraints, success criteria, and relevant exclusions or stop
conditions. Derive bounded Gates dynamically from it; do not require a rigid
template, invent requirements, or expand scope.

Codex Autopilot owns only this outer loop:

**Sprint Envelope → select bounded Gate → one complete upstream C2C task →
wait for upstream `DONE` → evaluate sprint → next Gate or stop.**

Hard invariant: **one Gate is exactly one complete upstream C2C task.** Never
split a Gate across C2C task IDs. Never start a later Gate until the current
Gate reaches upstream `DONE`. Review-requested repair iterations remain within
the same Gate and upstream task. Then check the sprint criteria and either
finish, stop, or start one fresh C2C task for the next in-scope Gate.

Do not duplicate upstream `codex-with-chatgpt` mechanics. Upstream owns
readiness and doctor workflow, browser/IAB handling, connector setup and
repair, Project and conversation management, workspace identity, TASK_ID
lifecycle, protocol states, iteration handling, execution recording, review,
checkpoint/session state, HANDOFF, and reconnect/recovery behavior.

## Stop conditions

Continue through ordinary implementation bugs, lint failures, test or build
failures, and review-requested repairs that remain within the approved Gate.
Stop when sprint success criteria are met, or when progress requires a
material product or architecture decision outside the envelope, meaningful
scope expansion, approval for a destructive or irreversible action,
security/privacy judgment, credentials/login/CAPTCHA/2FA/consent or another
human action, an upstream C2C iteration or blocking limit, or a genuine
external dependency. Never bypass upstream limits or human authorization.
