## What

<!-- One sentence: what does this PR do? -->

## Why

<!-- The problem it solves, or link the issue: skyway-harness-builder/issues#NNN -->

## Checklist

- [ ] Lint passes locally (`skyway lint` for .sky files, `make lint` / `golangci-lint` for Go)
- [ ] Tests pass (`go test -race ./...` where applicable)
- [ ] For .sky workflows: budgets set, destructive steps gated, prompt bodies terse, `※※` docs current
- [ ] Single concern — every changed line traces to the What above
