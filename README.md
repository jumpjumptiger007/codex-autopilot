# Codex Control Room

A lightweight **Copilot / Autopilot workflow layer** for
[`codex-with-chatgpt`](https://github.com/XiaoDuoYa/codex-with-chatgpt).

> ChatGPT plans and reviews. Codex executes.

## Two modes

| Mode | Behavior |
| --- | --- |
| **Copilot** | Default. Completes the current bounded Gate, then returns control to you. |
| **Autopilot** | Explicit opt-in. Continues automatically across Gates inside the approved scope. |

### Copilot

```text
$codex-control-room

Implement the approved task.
```

Copilot is the default. Control Room may plan, execute, review, and repair the
current Gate through the normal C2C workflow. When that Gate is complete, it
stops before starting another one.

### Autopilot

```text
$codex-control-room autopilot

Complete the approved sprint.
```

Autopilot may continue automatically from one completed Gate to the next inside
the approved sprint scope.

It still stops when human input is genuinely required, including:

- product or architecture decisions outside the approved scope;
- scope expansion;
- destructive or irreversible actions;
- credentials, login, consent, CAPTCHA, or 2FA;
- upstream C2C iteration limits;
- genuine external blockers.

`unattended` remains supported as an alias for `autopilot`.

## Recommended Autopilot launch

For a long or important autonomous run, use a two-step launch.

**Step 1 — Initialize Control Room**

```text
$codex-control-room autopilot

Initialize Control Room in Autopilot mode only.

Verify C2C readiness, connector availability, conversation state, and MCP review access.

Do not begin implementation, modify project files, invent a goal, or perform unrelated cleanup.

Prepare Control Room for autonomous multi-Gate execution within the goal and scope I will provide next.

Stop after readiness is established and reply exactly:

Control Room Ready
```

**Step 2 — Send the actual goal**

After `Control Room Ready`, send the actual goal, scope, constraints, and
success criteria.

The two-step launch is optional. For long autonomous work, Codex Desktop
**Goal mode + Control Room Autopilot** is a useful combination.

Goal mode and Autopilot are complementary but independent:

- **Goal mode** keeps Codex working toward a target.
- **Autopilot** allows Control Room to continue across completed Gates.

Goal mode does not automatically enable Autopilot.

## What Control Room adds

`codex-with-chatgpt` already owns C2C communication, MCP review, TASK_ID /
iterations, checkpoints, HANDOFF, connector behavior, and conversation
management.

Codex Control Room adds workflow policy only:

- clear ChatGPT / Codex responsibility boundaries;
- bounded, reviewable Gates;
- independent review before accepting work;
- Copilot and Autopilot execution rules;
- explicit scope control.

If Control Room and `codex-with-chatgpt` conflict on operational behavior,
upstream C2C is authoritative.

## Install

`codex-with-chatgpt` must already be installed and configured.

Copy the Skill into your Codex skills directory:

```bash
mkdir -p ~/.codex/skills/codex-control-room
cp skill/SKILL.md ~/.codex/skills/codex-control-room/SKILL.md
```

Start a new Codex conversation so the Skill catalog refreshes.

## Principles

- Copilot by default.
- Autopilot only by explicit authorization.
- No automatic scope expansion.
- One meaningful reviewable Gate at a time.
- ChatGPT owns high-level WHAT / WHY.
- Codex owns implementation HOW.
- No duplicate C2C state machine, session system, or HANDOFF format.

## Status

Early release.

Codex Control Room intentionally stays small and delegates C2C mechanics to
`codex-with-chatgpt`.

## License

MIT
