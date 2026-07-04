# skyway

**The Claude Code harness builder.** skyway runs durable, multi-node AI workflows defined in `.sky` files — a format written by LLMs, for LLMs, reviewed by humans.

A workflow is a DAG of nodes (Claude sessions, bash, scripts, HTTP calls, approval gates) with triggers (GitHub webhooks, cron schedules, manual runs), budgets, retries, and fan-out. The daemon executes them, streams every step over WebSocket, and keeps the full run history queryable.

```
§scan§
bash = "gh pr list --json number --jq '[.[].number]'"
§§

§review§
depends_on = ["scan"]
foreach.items = "$scan.output"
foreach.max_concurrency = 3
§§

∆review∆
Review PR {{item}} ({{item_index}}/{{item_total}}). Post findings as a comment.
∆∆
```

## Repositories

| Repo | What it is |
|------|------------|
| [essential-workflows](https://github.com/skyway-harness-builder/essential-workflows) | The curated first-party workflow library — essentials only. Embedded in every binary and installable via `skyway library`. |
| [issues](https://github.com/skyway-harness-builder/issues) | Bug reports and feature requests for the harness builder. |

## Highlights

- **Workflows as text** — the whole automation is one reviewable `.sky` file: triggers, DAG, prompts, budgets.
- **Fail-closed by design** — judge → sentinel → deterministic gate patterns, per-node USD budgets, per-dependency circuit breakers, secret scrubbing at the log boundary.
- **A quality flywheel** — `skyway lint` (SKY-WF-* codes), `skyway eval` (outcome scoreboard), `skyway optimize` (prompt-variant search).
- **Runs anywhere** — single Go binary for Linux, macOS, and Windows; SQLite state; no external services required.

Built by [Skylence](https://skylence.be).
