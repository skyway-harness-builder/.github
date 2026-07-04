<div align="center">

<img src="https://raw.githubusercontent.com/skyway-harness-builder/.github/main/profile/assets/skyway-wordmark.svg" alt="skyway — the Claude Code harness builder" width="520"/>

<br/>

**Give AI real work. Keep real control.**

<br/>

![One program](https://img.shields.io/badge/one_program-no_servers_needed-00ADD8?logo=go&logoColor=white)
![Platforms](https://img.shields.io/badge/macOS_·_Linux_·_Windows-supported-6366f1)
![Powered by Claude](https://img.shields.io/badge/powered_by-Claude-a855f7)
![Every run recorded](https://img.shields.io/badge/every_run-recorded-38bdf8)

</div>

---

## What is skyway?

skyway is a program you run on your own computer that turns [Claude](https://claude.com/claude-code) into a dependable worker. You describe a job once — *when a bug report comes in, investigate it and propose a fix* — and skyway handles the rest: it wakes up at the right moment, does the work step by step, stays inside its budget, asks a human before doing anything risky, and writes down everything it did.

Each job lives in a single text file. Not settings scattered across a dashboard, not a black box — one file that answers, at a glance, the three questions you should ask of any AI acting on your behalf:

> **What will it do? What did it do? What did it cost?**

## The rules it never breaks

skyway is built around a short list of principles, and two of them tell you most of what you need to know:

- 💸 *"Cost is a parse-time input, not a bill you discover at month end."* — every job carries a spending cap, and skyway refuses to start a step that would blow it. Not warns. Refuses.
- 🧾 *"'Unknown error' is a bug, not an outcome."* — when something fails, you get a precise, coded reason. Every step of every run is kept: what ran, what it said, what it cost.

And the quieter ones do the rest: risky steps wait for a human decision (and keep waiting, even across restarts). Secrets are masked before they can reach a log. Dangerous patterns are rejected when the file is checked — before anything runs — with no override switch to talk skyway out of it.

## See one

A job that reviews every open pull request, three at a time, with a quality check before anything is posted:

```mermaid
flowchart LR
    T([something happens:<br/>a schedule, a click, a GitHub event]) --> S["gather the list of PRs"]
    S --> R["Claude reviews each one — 3 at a time"]
    R --> J{"quality check"}
    J -->|pass| D([results posted])
    J -->|fail| F["tell a human"]

    style T fill:#38bdf8,color:#fff,stroke:none
    style D fill:#22c55e,color:#fff,stroke:none
    style F fill:#f43f5e,color:#fff,stroke:none
    style J fill:#6366f1,color:#fff,stroke:none
```

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

That's the entire automation. The strange brackets are deliberate: these files are *written by AI and reviewed by humans* — skyway will even draft one for you from a plain-English sentence (`skyway compose`) and check it against 90+ safety and correctness rules before it can run.

## What people run on it

Jobs from the [essential-workflows](https://github.com/skyway-harness-builder/essential-workflows) library, ready to install:

- 🩺 **Health check** — probe your whole setup (logins, connections, missing secrets) and report red/green before anything breaks at 2am.
- 📝 **Release notes** — when you publish a release, draft human-readable notes from everything that changed, for you to approve.
- 🔍 **Failure triage** — when a job fails, a second job reads the logs, names the failing step, and proposes the fix.
- 📚 **Library upkeep** — audit, document, and diagram your whole collection of jobs, on a schedule.

## 🧭 Explore

| | |
|---|---|
| 📚 **[essential-workflows](https://github.com/skyway-harness-builder/essential-workflows)** | The curated first-party job library — essentials only, nothing padded. |
| 🐛 **[issues](https://github.com/skyway-harness-builder/issues)** | Something broken or missing? Tell us here. |
| ✅ **[sky-lint-action](https://github.com/skylence-be/sky-lint-action)** | Check workflow files automatically on every change, right in GitHub. |

<details>
<summary><strong>⚙️ For the engineers</strong></summary>
<br/>

A `.sky` file is a DAG over **15 node primitives** — Claude sessions, bash, bun/uv scripts, HTTP, approval gates, locks, `foreach` fan-out with concurrency caps, and multi-agent `spawn`/`council` with three-layer boundary enforcement (system prompt, PreToolUse hook denial, post-hoc `git status` audit). Triggers: GitHub, GitLab, Sentry, Linear, and Jira webhooks, cron schedules, workflow-to-workflow events, or `skyway run`.

The Go daemon (REST + WebSocket, SQLite state) enforces per-node/per-workflow/monthly USD budgets *before* invoking Claude, scrubs secrets at the log-emission boundary, trips per-dependency circuit breakers, and survives restarts mid-approval. Around it: `skyway lint` (90+ SKY-WF-\* codes, parse-time safety over runtime defense), `skyway eval` → `skyway optimize` (outcome scoreboard → prompt-variant search with a train/holdout split; report-only, never auto-applied), `skyway replay` / `replay-diff` / `playback` for deterministic time-travel debugging, a three-tier compound-knowledge store injected into every session, an AES-256-GCM secret vault, and ~50 CLI commands total. Workflows run in per-node git worktrees when asked; multi-user mode adds OAuth bearer tokens and tool-deny ACLs.

Claude-only, on purpose. No provider abstraction.

</details>

<br/>

<div align="center">

Built by **[Skylence](https://skylence.be)**

</div>
