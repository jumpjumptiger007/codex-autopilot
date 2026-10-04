# Codex Autopilot

Codex Autopilot is a thin autonomous multi-Gate sprint orchestration layer
built on top of [`codex-with-chatgpt`](https://github.com/XiaoDuoYa/codex-with-chatgpt).

> C2C = inner bounded-task loop. Codex Autopilot = outer autonomous sprint loop.

## Normal C2C

```text
$codex-with-chatgpt

Implement the requested bounded task.
```

Use this for ordinary ChatGPT-planned and independently reviewed Codex work.
The upstream Skill owns setup, browser and connector behavior, and the task
workflow.

## Multi-Gate autonomous sprint

```text
$codex-autopilot autopilot

Complete this sprint: <goal, scope, constraints, and success criteria>
```

Use this only when you explicitly want autonomous execution across multiple
bounded C2C tasks. Autopilot chooses meaningful Gates inside the approved
sprint scope. Each Gate is one complete upstream C2C task; after it reaches
`DONE`, Autopilot checks the sprint criteria and starts the next in-scope task
or finishes. It stops when the sprint is complete or material human input is
required.

## Initialize first, provide the sprint next

You can initialize Autopilot before sharing the sprint goal:

```text
$codex-autopilot autopilot

Initialize Codex Autopilot only.

Use the authoritative codex-with-chatgpt workflow to establish readiness.

Do not begin implementation, modify project files, or invent a goal.

Stop when the upstream C2C workflow is ready and reply exactly:

Codex Autopilot Ready
```

Then send the sprint goal, scope, constraints, and success criteria in your
next message.

## Install

Install [`codex-with-chatgpt`](https://github.com/XiaoDuoYa/codex-with-chatgpt)
first, then copy the Skill into your Codex skills directory:

```bash
mkdir -p ~/.codex/skills/codex-autopilot
cp skill/SKILL.md ~/.codex/skills/codex-autopilot/SKILL.md
```

Start a new Codex conversation to refresh Skill discovery. Follow the upstream
Skill for all C2C setup, browser, connector, task, review, and recovery details.

## License

MIT
