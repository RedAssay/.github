# Contributing to RedAssay

Thanks for taking the time. RedAssay is pre-launch, so how you can help depends on which
repository you are looking at.

Most of our code is private today. The Go control plane, the Node and Playwright browser
sidecar and the Next.js operator console live in private repositories while we run
design-partner pilots. Anything we open-source appears in
[this organisation](https://github.com/RedAssay), and this guide covers it.

Security vulnerabilities do not go in issues. Follow [SECURITY.md](SECURITY.md) instead.

## Before you write code

Open an issue first for anything beyond a typo or an obvious one-line fix. A short thread
about the approach costs both of us less than a pull request we have to decline. If an
issue already exists, say you are picking it up so nobody duplicates the work.

## Pull requests

1. Branch off `main`. We do not commit directly to `main`.
2. Keep one pull request to one logical change. Unrelated cleanups belong in their own.
3. Build and run the tests locally before pushing. Not every repository has CI.
4. Fill in the pull-request template. The section that matters most is how you verified
   it: say what you ran, and paste what it printed.
5. Update the docs in the same PR as the behaviour they describe.

### Commit messages

Imperative summaries, scoped by subsystem, in the style already in the log:

```
agent: dependency-aware plan ordering
vuln: gate generic-base64 on nearby keyword context
docs: agent-subsystem map and upgrade plan
```

Group related changes into one logically-scoped commit rather than a trail of `update`.

## Code style

Each repository states its own rules, so read its `CLAUDE.md` or `README.md` first. Across
all of them: Go is `gofmt` clean, one package per concern, errors wrapped with `%w`, and
tests run with `-race`. The codebase runs bounded worker pools, so that flag is not
optional. TypeScript and React changes typecheck and build before they are pushed.

Match the surrounding code, so a reviewer can read the diff without switching styles.

## The invariants

These are not style rules. A pull request that breaks one will not merge, whatever else it
improves.

A finding is real only when it has been independently replayed. The model files
*candidates*, and a deterministic verify pass promotes them to *confirmed*. Nothing is ever
marked confirmed from a model's claim.

Rules of engagement are enforced in code, not in a prompt. Scope, safe-mode, budgets and
rate limits gate every active behaviour. Do not move a safety decision into a model's
hands.

Every meaningful step is an audit event, appended to the log and published to the live
stream in the same shape. The persisted log and the stream do not diverge.

Redaction happens at the store boundary, before anything is persisted or published.

Reports are deterministic. Findings are ordered by content, not by insertion.

## Testing against live targets

Never run any part of RedAssay against a host you are not authorised to assess. For
development, use the bundled targets: OWASP Juice Shop, VAmPI, WAVSEP, and the local OWASP
Benchmark harness. A contribution that ships a default pointing anywhere else will be
rejected on sight.

If you touch a detector, say what it does to the benchmark numbers. Give precision and
recall together, with the sample the figures came from. We may take a recall gain that
costs precision, but only if the PR says so.

## Conduct

By participating you agree to the [Code of Conduct](CODE_OF_CONDUCT.md).
