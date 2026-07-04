# Contributing to skyway

Thanks for wanting to help. A few things to know before you open a PR — they keep review fast for everyone.

## Where things go

| I want to… | Go to |
|---|---|
| Report a bug or request a feature | [skyway-harness-builder/issues](https://github.com/skyway-harness-builder/issues) — one central tracker for the whole product |
| Contribute a workflow | [essential-workflows](https://github.com/skyway-harness-builder/essential-workflows) — read its README first; the bar is *essentials only* |
| Improve the linter | [workflow-lint](https://github.com/skyway-harness-builder/workflow-lint) (Apache-2.0, Go) |
| Improve the CI action | [lint-action](https://github.com/skyway-harness-builder/lint-action) |
| Build your own workflow collection | Fork [workflow-collection-skeleton](https://github.com/skyway-harness-builder/workflow-collection-skeleton) — no PR needed, it's yours |

The `skyway` binary itself is proprietary and not open to code contributions; bug reports and feature requests about it are very welcome on the tracker.

## Ground rules for PRs

- **Lint must pass.** `.sky` files are gated by [lint-action](https://github.com/skyway-harness-builder/lint-action) in CI (`skyway lint` locally); Go repos gate on `go vet` + golangci-lint + `go test -race`. A red check will not be reviewed.
- **Small and single-purpose.** One workflow, one fix, one concern per PR. Every changed line should trace to the PR's stated purpose.
- **Conventional commits.** `feat:`, `fix:`, `docs:`, `chore:` — look at `git log` in the target repo and match it.
- **Workflows are reviewed as prompts, not just code.** For `.sky` contributions: terse machine-oriented prompt bodies, human-oriented `※※` doc blocks, budgets set (`max_budget_usd`), propose-don't-apply for anything destructive. The `sky-workflow-authoring` skill in essential-workflows is the authoritative reference.
- **Curation beats volume.** The public library deliberately stays small. A well-built workflow may still be declined for scope; forking the skeleton is always an option and encouraged.

## Developer certificate

By submitting a PR you certify you wrote the change or have the right to submit it under the repository's license (Apache-2.0 unless the repo states otherwise).
