# Codex Autopilot

Codex Autopilot is autonomous multi-Gate orchestration for Codex, built on top
of [`codex-with-chatgpt`](https://github.com/XiaoDuoYa/codex-with-chatgpt).
Upstream C2C handles each individual Gate; Codex Autopilot decides when to
advance to the next Gate and when the overall sprint is complete.

## Choose a workflow

For an ordinary bounded task that needs ChatGPT planning and review, use
upstream:

```text
$codex-with-chatgpt

Implement the requested bounded task.
```

For an autonomous multi-Gate sprint, invoke Codex Autopilot:

```text
$codex-autopilot

Complete this sprint: <goal, scope, constraints, and success criteria>
```

Autopilot establishes upstream C2C readiness before Gate 1. Existing
workspace configuration and session state are reused under upstream rules;
a first-time workspace may require a human authorization step. Follow upstream
C2C for workspace setup.

For important or long runs, use a recommended two-step launch. First send
`$codex-autopilot` and ask it to initialize only. It establishes readiness,
confirms the execution boundary, and stops before implementation with:

```text
Codex Autopilot Ready
```

Then send the Sprint Goal / Sprint Envelope. That message begins Gate
execution. For a simple, clear sprint, the invocation and goal may be sent
together.

## Sprint boundary

Keep the Sprint Envelope concise: the goal, allowed scope, important
constraints, success criteria, and relevant exclusions or stop conditions.
Autopilot can derive bounded Gates as the work progresses.

**One Gate is exactly one complete upstream C2C task.** Review-requested
repairs stay inside that Gate and task. A later Gate starts only after the
current task reaches upstream `DONE`; Autopilot then evaluates the sprint
criteria and continues or stops.

Upstream C2C owns readiness and individual-task workflow, including browser
and connector handling, task protocol, iterations, review, and recovery.
Autopilot owns the outer sprint loop and stops for completed criteria or when
human input, a material decision, a genuine blocker, or work outside the
approved envelope is required.

## Install

Install [`codex-with-chatgpt`](https://github.com/XiaoDuoYa/codex-with-chatgpt)
and copy this Skill into your Codex skills directory:

```bash
mkdir -p ~/.codex/skills/codex-autopilot
cp skill/SKILL.md ~/.codex/skills/codex-autopilot/SKILL.md
```

Start a new Codex conversation to refresh Skill discovery.

## License

MIT
