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
$c2c-control-room

Implement the approved task.
```

Copilot is the default.

Control Room may plan, execute, review, and repair the current Gate through the
normal C2C workflow. When that Gate is complete, it stops before starting
another one.

### Autopilot

```text
$c2c-control-room autopilot

Complete the approved sprint.
```

Autopilot may automatically continue from one completed Gate to the next inside
the approved sprint scope.

It still stops when human input is genuinely required, including:

- product or architecture decisions outside the approved scope;
- scope expansion;
- destructive or irreversible actions;
- credentials, login, consent, CAPTCHA, or 2FA;
- upstream C2C iteration limits;
- genuine external blockers.

`unattended` remains supported as an alias for `autopilot`.

## What Control Room adds

`codex-with-chatgpt` already owns the C2C infrastructure:

- ChatGPT ↔ Codex communication;
- MCP workspace review;
- TASK_ID and iterations;
- checkpoints and HANDOFF;
- connector and conversation management.

Codex Control Room does not replace those systems.

It adds only workflow policy:

- clear ChatGPT / Codex responsibility boundaries;
- bounded, reviewable Gates;
- independent review before accepting work;
- Copilot and Autopilot execution rules;
- explicit scope control.

If Control Room and `codex-with-chatgpt` conflict on operational behavior,
upstream C2C is authoritative.

## Optional two-step launch

For a long or important Autopilot run, you can initialize Control Room before
sending the actual implementation goal:

```text
$c2c-control-room autopilot

Initialize Control Room only.
Verify C2C readiness and stop after initialization.
```

After:

```text
Control Room Ready
```

send the actual goal, scope, constraints, and success criteria.

This two-step launch is optional.

## Codex Goal mode

Codex Desktop **Goal mode** and Control Room **Autopilot** are complementary
but independent.

- **Goal mode** keeps Codex working toward a target.
- **Autopilot** allows Control Room to continue across completed Gates.

Goal mode does not automatically enable Autopilot.

For long autonomous work, a useful combination is:

```text
Codex Goal mode
+
$c2c-control-room autopilot
```

## Install

`codex-with-chatgpt` must already be installed and configured.

Copy the Skill into your Codex skills directory:

```bash
mkdir -p ~/.codex/skills/c2c-control-room
cp skill/SKILL.md ~/.codex/skills/c2c-control-room/SKILL.md
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
