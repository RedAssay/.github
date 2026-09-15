# Security policy

This policy covers RedAssay's own code and services: every repository in this
organisation, the marketing site, and the infrastructure we run assessments on. It is not
the channel for a finding RedAssay produced about your application. That one goes to your
run report and to the engineer on your account.

## Reporting a vulnerability

Email [hello@redassay.com](mailto:hello@redassay.com) with `SECURITY` in the
subject line. If a repository has GitHub private vulnerability reporting enabled, use its
**Security → Report a vulnerability** form instead. We prefer that route, because it keeps
the thread attached to the code.

Please do not open a public issue for a suspected vulnerability, and please do not post it
to a public channel before we have had a chance to fix it.

Include:

- What you did, in steps we can repeat: the request, the payload, the sequence.
- What you observed, and what you expected instead.
- The impact you believe it has, and why.
- The target: a URL, a commit SHA, or a version.
- Anything we need to reproduce it, such as a PoC, a script, or a capture. Redact your own
  secrets.

Reports in any language are fine. We would rather have a rough report we can reproduce
than a polished one we cannot.

## What to expect

| | |
| --- | --- |
| Acknowledgement | Within 3 business days. |
| Triage and initial assessment | Within 10 business days, with our severity view and whether we could reproduce it. |
| Fix or mitigation | Targeted at 90 days from triage, and faster for anything actively exploitable. If it will take longer, we will tell you why and when. |
| Disclosure | Coordinated. We agree a date with you, and we credit you by the name or handle you choose unless you prefer to stay anonymous. |

We are a small pre-launch team and we do not run a paid bug bounty. We do credit
reporters, we answer every report a human sent, and we publish a GitHub Security Advisory
for anything that affects users.

## Scope

In scope:

- Source in any public repository of this organisation.
- `redassay.com` and its subdomains.
- The assessment platform: the control plane, the browser sidecar, the operator console,
  and the model-serving tier. We care most about anything that would let one run's data
  reach another run, let an assessment escape its scope allowlist, or defeat the
  candidate-to-confirmed gate.
- Secrets or customer data reachable from outside their intended boundary.

Out of scope:

- Findings with no demonstrated security impact, such as missing headers on a static page,
  version banners, SPF and DMARC opinions, or weak ciphers with no exploit path.
- Automated scanner output pasted without a reproduction. We run scanners for a living,
  and an unconfirmed scanner result is not a report.
- Social engineering, phishing, and physical attacks against our team or vendors.
- Denial of service, resource exhaustion, and volumetric or brute-force testing.
- Vulnerabilities in third-party services we consume. Those go to that vendor.
- Anything requiring a compromised device, a rooted browser, or a privileged local user.

## Safe harbour

If you make a good-faith effort to follow this policy, we will not pursue or support legal
action against you for your research, and we will say so on the record if a third party
raises it. Good faith means:

- Stay within the scope above, and stop as soon as you have proven the issue.
- Use only your own accounts and test data. Do not access, modify, or retain another
  person's or customer's data. If you encounter it, stop and tell us immediately.
- Do not degrade the service for anyone else. No DoS, no mass automated scanning, no data
  destruction.
- Give us a reasonable window to fix before disclosing publicly.

This authorisation covers only us. It does not extend to a customer's application, or to
any third-party system, even if you reach it through ours.

## How we run assessments

Every assessment run is bounded by a scope allowlist, safe-mode by default, a request
budget and a per-host rate limit. We write every prompt, tool call and request to an
append-only audit log, with secrets redacted at the store boundary. Both model tiers are
open-weight and hosted by us, so no customer traffic, code or finding is routed to a
third-party model API. If you find a way around any of that, tell us.
