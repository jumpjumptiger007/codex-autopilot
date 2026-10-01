---
name: c2c-control-room
description: >
  Optional workflow policy on top of codex-with-chatgpt for explicitly
  requested Control Room, controlled C2C, or unattended C2C workflows.
  Do not use for ordinary codex-with-chatgpt tasks or when the user chooses
  to relay/control the C2C workflow manually.
---

# C2C Control Room

This skill adds workflow policy above `codex-with-chatgpt`.

It does not replace or fork C2C.

Use the installed `codex-with-chatgpt` skill for all C2C mechanics.
Its current instructions and protocol are authoritative whenever the two
skills overlap.

## Activation and modes

Activate only when the user explicitly requests Control Room behavior.

Do not activate for ordinary `codex-with-chatgpt` usage.

If the user explicitly says they will manually relay, mediate, or control the
C2C exchange, do not activate Control Room unless they explicitly request it
again.

Modes:

- `controlled` — default whenever Control Room is requested.
- `unattended` — only after explicit authorization for unattended,
  autonomous, or fully automatic C2C execution.

Never infer unattended mode merely from words such as "automatic", "fix it",
or "continue".

## Initiation and readiness

Control Room may be initialized before the actual implementation goal is
provided.

When the user requests Control Room initiation, preparation, arming, or a
readiness check:

1. Use the authoritative `codex-with-chatgpt` workflow to verify C2C readiness,
   connector availability, conversation state, and MCP review access.
2. Prepare the requested Control Room mode, including `unattended` only when
   the user has explicitly authorized unattended execution.
3. Treat any already-open ChatGPT Project or browser pane supplied by the user
   as a navigation hint, not as proof that C2C is ready.
4. Do not begin project implementation, modify project files, invent a goal, or
   perform unrelated cleanup during initiation.
5. Stop after readiness has been established and wait for the user's actual
   goal.
6. When the user requests the standard readiness acknowledgement, reply
   exactly:

   `Control Room Ready`

If readiness cannot be established, do not claim success. Use normal upstream
setup or repair behavior when permitted, and surface a blocker only when
`codex-with-chatgpt` genuinely requires human action.

All connector, browser, repair, conversation-management, MCP, and protocol
mechanics remain owned by `codex-with-chatgpt`.

## Responsibility boundary

ChatGPT owns the high-level WHAT and WHY:

- investigation and external research when needed;
- product and architecture reasoning;
- alternatives and material tradeoffs;
- scope and acceptance criteria;
- decomposition into bounded work;
- independent review.

Codex owns implementation HOW inside the approved boundary:

- repository inspection needed for implementation;
- editing and shell commands;
- local code organization;
- tests and validation;
- ordinary debugging;
- lint/type/build fixes;
- small implementation-local refactors.

Codex must not become the primary product architect.

ChatGPT should not micro-manage Codex's individual tool calls.

Return to the user for a new material decision involving product behavior,
architecture/public contracts, data-model direction, meaningful dependency
tradeoffs, security/privacy policy, scope expansion, or destructive /
irreversible actions.

## Gates

A Gate is only a human-facing name for one bounded, independently reviewable
unit of work. It is not a C2C protocol state.

Prefer one bounded Gate per C2C task.

A Gate may require multiple upstream PLAN/review iterations.

If the user's request is too broad for one reviewable Gate, have ChatGPT first
reduce it to the next meaningful bounded Gate before implementation.

Do not split coherent work merely to create more Gates.

Do not create a second task ID system, iteration counter, checkpoint, session,
state machine, or HANDOFF format.

## Controlled mode

Controlled mode is the default.

For the current Gate:

1. Use ChatGPT as the investigation/planning layer.
2. Resolve or surface material design decisions before implementation.
3. Execute the bounded work through the normal `codex-with-chatgpt` workflow.
4. Let Codex handle ordinary implementation failures locally.
5. Use the normal upstream independent-review loop after meaningful execution.
6. Continue scope-local PLAN / execution / review repairs until the Gate is
   DONE or genuinely BLOCKED.

When the current Gate reaches DONE, stop before beginning a new Gate.

Report the result, current project status, and proposed next Gate to the user.

## Unattended mode

Enter unattended mode only after explicit user authorization.

Before implementation, establish an approved sprint envelope from the user's
request and available project context:

- overall goal;
- in-scope work;
- known exclusions;
- success criteria;
- established constraints.

ChatGPT may decompose that envelope into bounded Gates.

Within the approved envelope, complete Gates through the normal upstream C2C
workflow and continue automatically after a Gate reaches DONE.

Do not wake the user for ordinary engineering failures or scope-local review
repairs.

Do not invent features, architecture changes, cleanup projects, or other work
merely to continue execution.

Stop unattended execution when:

- the approved sprint success criteria are satisfied;
- a material decision outside the approved envelope is required;
- scope expansion is required;
- a destructive or irreversible action requires approval;
- C2C requires human login, consent, CAPTCHA, 2FA, credentials, or permission;
- upstream reaches its iteration limit;
- a genuine external or human-only blocker prevents progress.

Do not change, bypass, or silently extend upstream `maxIterations`.

## Review

After meaningful execution, use the existing upstream independent C2C review.

Do not trust an execution summary as proof of success.

Let ChatGPT inspect the actual repository, git state/diff, and available
execution/test evidence through the existing MCP data plane.

Never paste source files, diffs, or logs into ChatGPT when upstream MCP can
provide them.

Use only upstream C2C states and message formats.

Human-facing labels such as Gate, accepted, repair needed, or PASS must never
become new protocol states.

## Continuity

Delegate conversation mode, Project/long-chat behavior, conversation reuse,
checkpoint recovery, HANDOFF, repair, and replacement-chat behavior entirely
to `codex-with-chatgpt`.

Do not add custom context scoring, context compression, automatic conversation
rotation, or replacement-session logic.

If a ChatGPT conversation is visibly degraded, lost, or otherwise needs
replacement, use the current upstream conversation-management behavior.

Do not modify the upstream `codex-with-chatgpt` skill or global/project
`AGENTS.md` as part of running Control Room.

## Language and human status

Prefer concise English for agent-to-agent C2C instructions and protocol
content unless the task requires another language.

Use the user's language for human-facing progress and decisions.

When progress visibility is useful, show a compact status projection containing:

- mode;
- overall goal;
- current Gate;
- upstream TASK_ID and iteration;
- current C2C/checkpoint status;
- completed work;
- latest review result;
- what Codex is doing now;
- next expected step;
- blocker, if any.

This status is presentation only. Do not persist it as a second workflow state.

## Authority

Control Room governs workflow policy.

`codex-with-chatgpt` governs setup, repair, connector/browser behavior,
conversation management, protocol states/messages, TASK_ID and iteration
mechanics, sessions/checkpoints, HANDOFF, execution recording, MCP access,
evidence retrieval, security boundaries, and iteration-limit enforcement.

If operational behavior conflicts, `codex-with-chatgpt` wins.

