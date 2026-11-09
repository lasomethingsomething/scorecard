# OpenSSF Scorecard — open-issue backlog insights

_Analysis generated November 2026 by Mistral Vibe, from the 254 open issues in
[ossf/scorecard](https://github.com/ossf/scorecard/issues) (titles, labels, comment counts,
and full bodies of the highest-traction candidates). Local working notes — not a project document._

## Backlog at a glance

- **254 open issues**, created 2020–2026
- **120 (~47%) marked `Stale`** — the backlog is half triage debt
- Labels: 128 `kind/enhancement`, 73 `kind/bug`, but only **6** labeled `kind/new-check` —
  check proposals are widely under-labeled; title/label search alone finds ~1 in 8 of them
- Hottest check-specific labels: `check/Pinned-Dependencies` (19), `check/Dangerous-Workflow` (10),
  `check/Signed-Releases` (6), `check/Dependency-Update-Tool` (6)

## The five core problems people want solved

Beneath the issue titles, almost every request is one of five core problems:

1. **"Can I trust the number?" (accuracy & noise).** Inaccurate social-signal checks, stale
   heuristics, and gaming produce false positives on public badges, and people file issues to
   defend their reputation.
2. **"Does doing the right thing today count?" (currency).** GitHub ships security features faster
   than Scorecard encodes them; early adopters of attestations, OIDC publishing, private
   vulnerability reporting watch their score *drop* while being more secure.
3. **"Now what?" (actionability).** Consumers want work items — remediation diffs, ticket-ready
   checklists — not findings.
4. **"Can I enforce this?" (my own policy verdict).** Thresholds, exemptions, gates — but
   crucially *not* "decide for me": consumers consistently reject the tool dictating which
   checks matter. The real ask is **per-check signal plus configurable thresholds** so each
   consumer sets an appetite gate ("overall ≥ X, my critical checks not below Y"). The new
   OSPS Baseline conformance mode is the maintainers' structural answer here.
5. **"Am I safe from the attack of the week?" (threat currency).** Security researchers use
   Scorecard as the distribution channel for newly disclosed CI-attack techniques.

**Two personas, not one.** Almost everything filed in this backlog comes from *maintainers
defending their badge*. A second persona is largely absent from the issue tracker but real —
**consumers vetting upstream dependencies**, Scorecard's original design purpose. Their asks
(per-check detail, "why is this project only level 1?", evidence behind a gate) overlap with but
differ from maintainer asks (stop punishing me, tell me what to fix). "Trust" and "enforce" each
split into a maintainer-side and a consumer-side complaint; roadmap work should be labeled with
which persona it serves.

**Meta-observation:** people propose checks, but what they want is a signal that is
accurate, current, actionable, and enforceable. Most backlog growth comes from Scorecard being
a *measurement* tool used for *judgment*. See the next section for what this means for triage.

## Read the hidden want, not the proposed check

A "new check" request is almost never the underlying want. People arrive with a
frustration and propose "add a check" because it's the only lever the project visibly
offers — and the issue template's "Describe the solution you'd like" funnels them
straight to implementation. Reading the request as the goal mis-triages it:

| Proposed check (issue) | What they actually want |
| --- | --- |
| GitHub attestations check ([#4080](https://github.com/ossf/scorecard/issues/4080)) | Stop punishing me for adopting current best practice (a Signed-Releases fairness fix) |
| Private vulnerability reporting ([#2465](https://github.com/ossf/scorecard/issues/2465)) | Credit for security work my team already did |
| CHANGELOG check ([#4824](https://github.com/ossf/scorecard/issues/4824)) / criticality & maturity ([#3821](https://github.com/ossf/scorecard/issues/3821)) | The score should mean something — a validity complaint about existing signals |
| Tag-protection check ([#2476](https://github.com/ossf/scorecard/issues/2476)) | The score should predict the supply-chain risk I actually care about |

The giveaway: most proposed "new checks" detect something the *requester's project already
does* that Scorecard fails to see. Proposals for coverage someone doesn't personally need are
rare. Even the `kind/new-check` label confirms it — only 6 issues carry it, because most of
these are fairness complaints wearing a feature-request costume.

**Practical consequence:** triage these by underlying goal, not by title. The right fix is
usually "make an existing evaluation recognize a new mechanism" — smaller and faster than a
new check — and answering the fairness complaint prevents the backlog from regrowing: six
separate attestation issues exist because the first five were answered as feature requests
instead of a fairness problem.

**The exception is threat currency (Column 5).** When a researcher proposes detection for a
freshly disclosed attack technique ([#2733](https://github.com/ossf/scorecard/issues/2733),
imposter commits, from the disclosure itself), the check genuinely *is* the ask — adoption at
scale is their goal, and Scorecard is the distribution channel. Rule of thumb: for scoring
logic, x-ray the proposal for the hidden want; for new attack disclosures, take the check at
face value.

## Prioritized arrangement

- **Step 0 — triage harvest.** One pass over the 120 `Stale` issues (many superseded by the
  probes refactor and conformance work) before any new planning.
- **Column 1 first: trust.** Inaccurate scores actively generate issues in every other column.
- **Column 2: enforceability.** Maintainers already chose the conformance direction; migrate
  threshold/exemption asks into that framework.
- **Column 3: platform currency.** Consolidate before building: 6 attestations issues → one
  "Signed-Releases v2" epic; batch GitHub security-feature requests into one tracking issue.
- **Column 4: actionability.** Cheapest user-visible wins (remediation snippets, markdown export);
  localized output-layer work.
- **Column 5 (despite being loudest): threat currency.** Externally paced — arrange *capacity*
  (a `workflow-threats` probe family as the landing zone), not a schedule.

## Check requests — who and how many

An approximate **~45 genuine check/probe proposals** across ~40 unique proposers
(several heavy repeat proposers, including maintainers). ~65 open issues match proposal-shaped
language, of which the rest are bugs, docs, and infra requests.

### Column 1 — accuracy & anti-gaming (~16 proposals)

| Proposed check | Issue |
| --- | --- |
| Frozen-Deps: don't require pinning for libraries | [#689](https://github.com/ossf/scorecard/issues/689) |
| Frozen-Deps: enforce hash-pinning | [#427](https://github.com/ossf/scorecard/issues/427) |
| Frozen-Deps: pinning enhancements | [#383](https://github.com/ossf/scorecard/issues/383) |
| Pinned-Deps: Makefile support | [#884](https://github.com/ossf/scorecard/issues/884) |
| Pinned-Deps: more unpinned Go commands | [#1606](https://github.com/ossf/scorecard/issues/1606) |
| Code-Review: recognize zappr enforcement | [#2952](https://github.com/ossf/scorecard/issues/2952) |
| Code-Review: recognize prow (`/lgtm` + `/approve`) gate | [#5280](https://github.com/ossf/scorecard/issues/5280) |
| SAST: recognize CodeQL usage | [#3817](https://github.com/ossf/scorecard/issues/3817) |
| Vulnerabilities: separate "no vulns" from "no disclosure" | [#4789](https://github.com/ossf/scorecard/issues/4789) |
| Vulnerabilities: ignore dev-dependencies in OSV scan | [#4550](https://github.com/ossf/scorecard/issues/4550) |
| Security-Policy: look beyond SECURITY.md | [#4192](https://github.com/ossf/scorecard/issues/4192) |
| Bus-factor: contributor absence factor | [#5416](https://github.com/ossf/scorecard/issues/5416) |
| Bus-factor: contributor account-age weighting | [#4000](https://github.com/ossf/scorecard/issues/4000) |
| Bus-factor: criticality & maturity | [#3821](https://github.com/ossf/scorecard/issues/3821) |
| Branch-Protection: collect bypass allowances | [#5451](https://github.com/ossf/scorecard/issues/5451) |
| CODEOWNERS: freshness probe | [#3931](https://github.com/ossf/scorecard/issues/3931) |

### Column 2 — policy & standards (~2 proposals)

The enforcement column mostly requests *mechanisms* (thresholds, exemptions), not new checks.

| Proposed check | Issue |
| --- | --- |
| Align checks with S2C2F Maturity Level 2 | [#4296](https://github.com/ossf/scorecard/issues/4296) |
| (inverse) Remove the CII-Best-Practices check | [#2904](https://github.com/ossf/scorecard/issues/2904) |

### Column 3 — platform & ecosystem currency (~15 proposals)

| Proposed check | Issue |
| --- | --- |
| GitHub artifact attestations for Signed-Releases | [#4080](https://github.com/ossf/scorecard/issues/4080) |
| SBOMs in CI artifacts | [#4119](https://github.com/ossf/scorecard/issues/4119) |
| Private vulnerability reporting enabled | [#2465](https://github.com/ossf/scorecard/issues/2465) |
| OIDC-based publishing (PyPI etc.) | [#2761](https://github.com/ossf/scorecard/issues/2761) |
| Tag-protection rules enabled | [#2476](https://github.com/ossf/scorecard/issues/2476) |
| Allow job-level write permissions when hash-pinned | [#3022](https://github.com/ossf/scorecard/issues/3022) |
| pre-commit framework as SAST | [#5333](https://github.com/ossf/scorecard/issues/5333) |
| Maintained: activity within the last year | [#2160](https://github.com/ossf/scorecard/issues/2160) |
| Deps-Update-Tool: tool is still active | [#2165](https://github.com/ossf/scorecard/issues/2165) |
| Packaging: recognize step-security goreleaser fork | [#5131](https://github.com/ossf/scorecard/issues/5131) |
| Packaging: recognize cargo-dist workflows | [#5145](https://github.com/ossf/scorecard/issues/5145) |
| Packaging: recognize winget publishing workflows | [#5168](https://github.com/ossf/scorecard/issues/5168) |
| Packaging: recognize Helm chart publishing | [#5288](https://github.com/ossf/scorecard/issues/5288) |
| Packaging: recognize docker/bake-action | [#5365](https://github.com/ossf/scorecard/issues/5365) |
| Ecosystem: Composer (PHP) package manager | [#4378](https://github.com/ossf/scorecard/issues/4378) |

### Column 4 — actionability (zero)

No check-shaped proposals land here — its asks
([#1850](https://github.com/ossf/scorecard/issues/1850) remediation steps,
[#3798](https://github.com/ossf/scorecard/issues/3798) markdown export) want *output*, not
new detections. That itself is signal.

### Column 5 — threat currency (~11 proposals)

| Proposed check | Issue |
| --- | --- |
| Imposter commits (Chainguard/clank detection) | [#2733](https://github.com/ossf/scorecard/issues/2733) |
| `on: workflow_run` trigger chaining | [#3861](https://github.com/ossf/scorecard/issues/3861) |
| Dangerous-Workflows: detect refs | [#2404](https://github.com/ossf/scorecard/issues/2404) |
| Dangerous-Workflows: declared branches | [#2406](https://github.com/ossf/scorecard/issues/2406) |
| Dangerous-Workflows: Jenkinsfile analysis | [#2214](https://github.com/ossf/scorecard/issues/2214) |
| Dangerous-Workflows: untrusted-input expansion | [#3915](https://github.com/ossf/scorecard/issues/3915) |
| Tokens able to create/approve PRs | [#2707](https://github.com/ossf/scorecard/issues/2707) |
| Secure runners (self-hosted abuse vector) | [#3801](https://github.com/ossf/scorecard/issues/3801) |
| Unpinned repo clones in scripts/Makefiles | [#608](https://github.com/ossf/scorecard/issues/608) |
| `.whl` download → pip install execution | [#613](https://github.com/ossf/scorecard/issues/613) |
| AI / external-communication usage detection | [#4565](https://github.com/ossf/scorecard/issues/4565) |

## Consolidation opportunities

1. **Signed-Releases v2 epic** — the attestations cluster
   ([#4080](https://github.com/ossf/scorecard/issues/4080), [#4667](https://github.com/ossf/scorecard/issues/4667),
   [#4174](https://github.com/ossf/scorecard/issues/4174), [#382](https://github.com/ossf/scorecard/issues/382),
   [#2684](https://github.com/ossf/scorecard/issues/2684), [#5308](https://github.com/ossf/scorecard/issues/5308))
   is six issues asking one thing: recognize GitHub artifact attestations.
2. **`workflow-threats` probe family** — the Dangerous-Workflow additions
   ([#2733](https://github.com/ossf/scorecard/issues/2733), [#3861](https://github.com/ossf/scorecard/issues/3861),
   [#2404](https://github.com/ossf/scorecard/issues/2404), [#2406](https://github.com/ossf/scorecard/issues/2406),
   [#3915](https://github.com/ossf/scorecard/issues/3915)) become probes composed into one check; new
   disclosures get slotted, not architected per-issue.
3. **Policy/conformance migration** — threshold ([#4631](https://github.com/ossf/scorecard/issues/4631)),
   exemption ([#2614](https://github.com/ossf/scorecard/issues/2614)), and output
   ([#1850](https://github.com/ossf/scorecard/issues/1850), [#3798](https://github.com/ossf/scorecard/issues/3798))
   asks fold into the new OSPS-Baseline conformance layer rather than the classic score.
4. **Stale harvest** — 120 stale issues, many pre-2023, likely superseded by the probes refactor.

## Open decision: conformance reporting granularity

Not in the issue backlog, but the most consequential live discussion (Nov 2026 community
thread, conformance mode): **what does conformance output report by default?**

- *Granular:* maturity levels as the default, with control details in evidence files or via an
  explicit flag — consumers need "why is this level 1?" for risk decisions; splitting detail
  into a second tool is bad UX for what is conceptually one analysis.
- *Binary:* either you conform to a level or you don't — granular per-control reporting to
  consumers would recreate the exact dynamic that made maintainers wary of Scorecard in the
  first place: a vector for "please do these things" and punishment for project shapes where a
  lower level is appropriate.

The tension is unresolved: the "use the existing granular tool for debugging" counterpoint
loses to the "one analysis, two tools is bad UX" argument on the consumer side, but the
punishment-cycle warning deserves equal weight — it is the strongest maintainer-side argument
in the thread, and it is precisely what Scorecard lived through with per-check scores.

## Method & caveats

- All 254 open issues fetched via the GitHub API (state :open) and clustered by theme using
  title keywords, labels, and comment counts; ~12 high-traction bodies read in full, plus
  regex-based proposal detection across all bodies.
- Curated by hand from the machine-generated candidate list; classification ambiguities
  remain for [#4565](https://github.com/ossf/scorecard/issues/4565) and
  [#4769](https://github.com/ossf/scorecard/issues/4769).
- Priority ordering (Column 2 above Column 4) is a judgment call sensitive to weighting
  large-org gate users vs. individual contributors.
