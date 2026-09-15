<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)"
            srcset="https://raw.githubusercontent.com/RedAssay/.github/main/profile/assets/logo-dark-512.png">
    <img alt="RedAssay"
         src="https://raw.githubusercontent.com/RedAssay/.github/main/profile/assets/logo-light-512.png"
         width="420">
  </picture>
</p>

<p align="center">
  <strong>An AI pentest agent that proves what it finds.</strong>
</p>

<p align="center">
  <a href="https://redassay.com">redassay.com</a> ·
  <a href="https://cal.com/redassay/demo">Book a call</a> ·
  Pre-launch · 2026
</p>

---

You nominate an authorized target. We run the assessment on infrastructure we control: an
LLM orchestrator drives a real Chromium session through the app the way a person uses it,
captures every backend call it provokes, exercises what it finds, and replays every
candidate before it becomes a finding. What the replay cannot reproduce never reaches your
report.

Teams today pick between two bad options. A manual pentest goes deep but runs once a year
and is stale on the next commit. A legacy DAST runs continuously but buries the team in
unconfirmed findings nobody trusts. RedAssay runs on every deploy and proves what it
reports.

## What we claim

|  |  |
| --- | --- |
| **Continuous** | Runs on every deploy instead of once a year. Exposure shrinks from months to hours. |
| **Proven** | Every finding passes a candidate-to-confirmed gate. A finding that cannot be replayed does not ship, and we never report a probability score in place of proof. |
| **Contained** | The assessment runs on infrastructure we control, on open-weight models we host ourselves, and on dedicated infrastructure where an enterprise customer needs it. No traffic, no code and no finding reaches a third-party service. We keep run data for re-runs and for diffing across deploys, and delete it on request. |

## How a run works

**1. Map.** Real Chromium exercises the app the way a person does: form login, Google, or
a saved session, then clicking, submitting, paginating. Every backend call it provokes is
captured, including XHR, GraphQL, WebSocket frames and form posts. It works the rendered
app rather than a list of raw endpoints.

**2. Fingerprint.** The same traffic identifies the stack. We infer it passively and map
versions to OSV and NVD advisories.

**3. Probe.** A differential engine and 44 deterministic checks exercise the captured
surface. Blind bugs are proven out-of-band through an HTTP or DNS callback.

**4. Confirm.** Replay verification gates every finding before it exists. Reports emit
JSON, SARIF 2.1.0 and PDF, and headless CI mode exits non-zero on confirmed findings.

All four stages run inside a scope allowlist, safe-mode, a request budget (default 2000),
a per-host rate limit (default 5 rps), and an append-only audit log of every prompt, tool
call and request. The agent cannot leave the scope you set, and you can read exactly where
it went.

## Depth

- 44 deterministic, replay-confirmed vulnerability checks.
- ~90 catalogued security tools the agent orchestrates, rules-of-engagement gated and
  deduped into a single report.
- CVSS 3.1 on every finding, CWE and OWASP tagged, with request and response proof
  attached.

<details>
<summary><strong>Classes covered</strong></summary>

SQLi · stored XSS · SSTI · command injection · XXE · SSRF · IDOR and BFLA · request
smuggling · mass assignment · JWT forgery · CORS · security headers · secrets and
source-map exposure · GraphQL · NoSQLi · path traversal and LFI · open redirect ·
host-header injection · CRLF · cache poisoning · verb tampering · prompt injection ·
subdomain takeover · clickjacking · weak TLS · race conditions and rate limits.

</details>

## Measured on public testbeds

Public benchmarks, served locally, scored against the same detectors that ship. Every
figure states the sample it came from, and we list anything we could not measure as not
measured. Transcribed from `benchmark.md` v0.1.0, rev 5, 2026-09-11.

| Benchmark | Result | State |
| --- | --- | --- |
| **OWASP Benchmark v1.2** | 97.5% precision · 46.4% recall · 1.3% false positives (163 form-parameter cases across 6 categories) | measured |
| **WAVSEP** | 66.7% recall. The gate cuts false positives from 37.5% to 12.5%, holding 2 of 3 raw FPs at needs-review | measured |
| **VAmPI** | 3 of 7 documented vulns · 0 confirmed false positives, including a JWT weak key cracked, re-signed and replayed | measured |
| **OWASP Juice Shop** | 18 findings · 14 confirmed, 4 held as candidates. The agent claimed an SQLi and the gate held it until replay | measured |
| **CVE-Bench** | 36 of 40 CVEs fall in a class we have a detector for | projection: a coverage ceiling rather than an exploitation score, since the targets were not run |
| **Meta CyberSecEval** | 88% prompt-injection resistance · 12% attack-success rate (25-case sample, deterministic substring judge, seed 11) | measured |
| **AutoPenBench** | Not run, so not claimed | not run: its agent and its grader both need a capable model, and a 9B model grading itself is not a score |

We never quote precision without recall beside it. The 1.3% false-positive figure is
compared against the ~82% OWASP cites for a typical DAST tool, not against a tool we ran
ourselves.

### Not claimed

The same run measured what we cannot do yet. These gaps are open, and closing them is the
next work.

- Header and cookie injection vectors, roughly a third of the OWASP Benchmark, are outside
  the fuzzer's reach today.
- Blind path traversal and XPath injection produce no black-box signal our oracles can
  read. There is no detection path yet, and we will not guess.
- API access control and auth logic need multi-identity, stateful context the black-box
  checks do not carry. Across WAVSEP and VAmPI this is the clearest coverage gap.
- The figures are sampled rather than exhaustive: 163 cases of 2,740, to bound wall-clock.

## Compliance mapping

Every finding carries the control IDs it maps to, covering SOC 2 Trust Services Criteria
and ISO 27001 Annex A, with per-framework rollups. We cover the technical-control slice
and produce attack-proven evidence for it. We complement a GRC platform like Vanta or
Drata rather than replacing one. We never claim to do your SOC 2. We prove the technical
controls by attacking them.

## Who it's for

Regulated, code-sensitive engineering and security teams in fintech, health, EU and NATO
defence, and AI labs. Organisations that need an application tested without handing its
attack surface to a cloud AI provider.

## This organisation

RedAssay is pre-launch. The product repositories (the Go control plane, the Node and
Playwright browser sidecar, and the Next.js operator console) are private while we run
design-partner pilots. Anything we open-source appears here, and the org-wide
[security policy](https://github.com/RedAssay/.github/blob/main/SECURITY.md) applies to
every repository under it.

## Talk to us

To request a scoped assessment or join the design-partner pilot, book a call at
[cal.com/redassay/demo](https://cal.com/redassay/demo). For anything else,
email [hello@redassay.com](mailto:hello@redassay.com). To report a
vulnerability in RedAssay itself, read
[SECURITY.md](https://github.com/RedAssay/.github/blob/main/SECURITY.md) first.

---

<sub>Scoped, authorized targets only. Safe-mode is on by default, every run is
rate-limited, budgeted and logged, and secrets are redacted at the store boundary. We
never run against a host you are not authorized to assess.</sub>
