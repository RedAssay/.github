## What this changes

<!-- One paragraph. What does the code do differently after this PR than before it? -->

Closes #

## Why

<!-- The problem this solves. Link the issue or the discussion where the approach was agreed. -->

## How it was verified

<!-- Say what you ran, and paste what it printed.
     e.g. `make backend-test` (go test -race ./...), `pnpm build`, a benchmark run. -->

```
```

## Benchmark impact

<!-- Only if this touches a detector, the fuzzer, or the confirm gate.
     Give precision and recall together, with the sample the figures came from.
     We may take a recall gain that costs precision, as long as the PR says so. -->

N/A

## Checklist

- [ ] Branched off `main`, and this PR is one logical change.
- [ ] Tests and a build pass locally, and the output is pasted above.
- [ ] Docs updated in this PR if behaviour changed.
- [ ] No secrets, customer data, or non-public benchmark artefacts in the diff.
- [ ] Nothing here promotes a finding to `confirmed` without an independent deterministic replay.
- [ ] Rules of engagement (scope, safe-mode, budgets, rate limits) are still enforced in code, not in a prompt.
- [ ] Every new meaningful step is an audit event, appended and published in the same shape.
