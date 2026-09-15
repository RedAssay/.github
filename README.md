# `.github` — RedAssay organisation defaults

This repository holds the files GitHub reads on behalf of every repository in the
[RedAssay](https://github.com/RedAssay) organisation, plus the org profile page. It
contains no product code.

| Path | What GitHub does with it |
| --- | --- |
| `profile/README.md` | Rendered as the org landing page at [github.com/RedAssay](https://github.com/RedAssay). |
| `SECURITY.md` | The "Report a vulnerability" policy shown on any org repo without its own. |
| `CONTRIBUTING.md` | Linked from the issue and pull-request forms of any org repo without its own. |
| `CODE_OF_CONDUCT.md` | Shown in the community profile of any org repo without its own. |
| `.github/ISSUE_TEMPLATE/` | Default issue forms, inherited by org repos that define none. |
| `.github/PULL_REQUEST_TEMPLATE.md` | Default PR body, inherited the same way. |
| `LICENSE` | Covers this repository only. Each product repo carries its own. |

A repository that defines any of these itself wins. Inheritance is per-file, and it only
applies to public repositories.

## Editing the profile

`profile/README.md` is buyer-facing copy, bound by the same claims discipline as the
marketing site. Before changing a word of it, read `PRODUCT.md` in the website repository.
The rules that bite most often:

Capability facts only. No scan counts, endpoint counts, confirmation rates, or named
customer targets. Published third-party benchmark results are the one exception, and every
figure ships with the sample it came from.

Precision is never quoted without recall beside it. A projection is labelled a projection,
and a benchmark we could not run is listed as not run rather than dropped.

Containment is about the data, not the machines. The words *self-hosted*, *sovereign*,
*your own hardware*, *inside your perimeter* and *never leaves your network* must not
appear. We run the assessment on infrastructure we control, and the load-bearing claim is
that nothing we collect crosses that boundary.

Never claim we do your SOC 2. We prove the technical controls by attacking them.

Benchmark figures in `profile/README.md` are transcribed from `benchmark.md` in the
product repository and keyed to its version and revision. When that file changes, this one
changes with it, and we do not author a figure here independently of it.

## Brand assets

`profile/assets/` carries the two wordmark lockups the profile header uses, copied from the
website's brand kit (`public/brand/`). A script generates them, so regenerate at the source
rather than editing them here. The profile references them by absolute
`raw.githubusercontent.com` URL, because relative image paths do not reliably resolve on an
organisation profile page.

The square mark (`mark-1024.png` in the same brand kit) is the org avatar. Avatars cannot
be set through the API, so upload it under **Organisation settings → Profile**.

## Contact details

Two values appear in several files here, and they have to match `site.contact` and
`site.cal` in the website repository:

| Value | Where it appears |
| --- | --- |
| `hello@redassay.com` | `profile/README.md`, `SECURITY.md`, `CODE_OF_CONDUCT.md`, `.github/ISSUE_TEMPLATE/config.yml` |
| `https://cal.com/redassay/demo` | `profile/README.md`, `.github/ISSUE_TEMPLATE/config.yml` |

`hello@redassay.com` currently receives vulnerability reports, conduct reports and general
mail. If you split those later, `SECURITY.md` and `CODE_OF_CONDUCT.md` are the two files to
change, and a forwarding alias is enough. Whatever address ends up in `SECURITY.md` has to
be read by someone: an address that silently drops a vulnerability report is worse than no
policy at all.

The org description, website URL, public email and avatar are already set under
**Organisation settings → Profile**. Everything except the avatar can also be changed with
`gh api -X PATCH /orgs/RedAssay`, which needs the `admin:org` scope. The Location field is
a fixed country picker with no remote option, and it is deliberately left blank.
