# OpenSSF Scorecard — backlog insights (Nov 2026)

_From the 254 open [issues](https://github.com/ossf/scorecard/issues) of ossf/scorecard (created 2020–2026): titles, labels, comment counts, and the full bodies of the highest-traction candidates; cross-checked against a Nov 2026 community thread on conformance-mode reporting. Local working notes by Mistral Vibe — not a project document._

## At a glance

- 254 open issues; **120 (~47%) `Stale`** — the backlog is half triage debt.
- Labels: 128 `kind/enhancement`, 73 `kind/bug`, only **6 `kind/new-check`** — check proposals are heavily under-labeled (title/label search finds ~1 in 8).
- Hottest check labels: `Pinned-Dependencies` 19, `Dangerous-Workflow` 10, `Signed-Releases` 6, `Dependency-Update-Tool` 6.

## Five core problems

1. **Trust the number (accuracy & noise).** Inaccurate social-signal checks, stale heuristics, gaming → false positives on public badges; issues get filed to defend reputations.
2. **Does the right thing today count? (currency).** GitHub ships security features (attestations, OIDC publishing, private vulnerability reporting) faster than Scorecard encodes them; early adopters watch scores *drop* while being more secure.
3. **Now what? (actionability).** Consumers need work items — remediation diffs, ticket-ready checklists — not findings.
4. **My own verdict (enforcement).** *Not* "decide for me": consumers reject the tool dictating which checks matter. The ask is **per-check signal + configurable thresholds** for an appetite gate ("overall ≥ X, my critical checks not below Y") — per-consumer verdicts on shared signal. The OSPS-Baseline conformance mode is the structural answer.
5. **Am I safe from the attack of the week? (threat currency).** Security researchers use Scorecard as the distribution channel for newly disclosed CI-attack techniques.

**Two personas, not one.** The issue tracker is almost entirely *maintainers defending their badge*; largely missing is the **consumer vetting upstream dependencies** — Scorecard's original design purpose — whose asks (per-check detail, "why is this only level 1?", evidence behind a gate) surface in threads, not issues. "Trust" and "enforce" each split into a maintainer-side and a consumer-side complaint; label roadmap work by which persona it serves.

**Proposals are solutions, not wants.** People arrive frustrated and propose "add a check" — the only lever the project visibly offers, funneled there by the template's "Describe the solution you'd like":

| Proposed check | What they actually want |
| --- | --- |
| GitHub attestations [#4080][_4080] | Stop punishing me for current best practice (a Signed-Releases fairness fix) |
| Private vulnerability reporting [#2465][_2465] | Credit for security work my team already did |
| CHANGELOG [#4824][_4824] / criticality & maturity [#3821][_3821] | The score should mean something — validity complaint about existing signals |
| Tag protection [#2476][_2476] | The score should predict the supply-chain risk I actually care about |

Tell: proposed "new checks" overwhelmingly detect something the requester's *own project already does* that Scorecard fails to see. Consequence: triage by underlying goal, not title — the fix is usually "make an existing evaluation recognize a new mechanism" (smaller and faster than a new check), and answering the fairness complaint prevents regrowth: six separate attestation issues exist because the first five were answered as feature requests. **Exception: threat disclosures** ([#2733][_2733]) — for a freshly disclosed attack the check genuinely *is* the ask; adoption at scale is the goal. Rule of thumb: x-ray scoring proposals for the hidden want; take attack-disclosure checks at face value.

## Prioritized arrangement

- **Step 0 — triage harvest.** One pass over the 120 `Stale` issues (many superseded by the probes refactor and conformance work) before new planning.
- **Column 1 — trust, first.** Inaccurate scores actively generate issues in every other column.
- **Column 2 — enforcement.** Maintainers already chose the conformance direction; migrate threshold/exemption asks into that framework.
- **Column 3 — currency.** Consolidate before building: the 6 attestations issues → one "Signed-Releases v2" epic; per-GitHub-feature tracking issue so future features get a known landing place.
- **Column 4 — actionability.** Cheapest user-visible wins (remediation snippets, markdown export); localized output-layer work.
- **Column 5 — threats (despite being loudest).** Externally paced — arrange *capacity* (a `workflow-threats` probe family as the landing zone), not a schedule.
- **Sequencing:** interleave cheap correctness wins with one structural track at a time; KPI is Column-1 issue inflow — below trend a healthy backlog, above it a support channel.

## Check proposals — who and how many

**~45 genuine check/probe proposals from ~40 unique proposers** (heavy repeat proposers, including maintainers); ~65 open issues match proposal-shaped language, the rest being bugs, docs, and infra requests.

### Column 1 — accuracy & anti-gaming (~16)

- Frozen-Deps: don't require pinning for libraries [#689][_689]; enforce hash-pinning [#427][_427]; pinning enhancements [#383][_383]
- Pinned-Deps: Makefile support [#884][_884]; more unpinned Go commands [#1606][_1606]
- Code-Review: recognize zappr enforcement [#2952][_2952]; recognize prow (`/lgtm`+`/approve`) gate [#5280][_5280]
- SAST: recognize CodeQL [#3817][_3817]
- Vulnerabilities: separate "no vulns" from "no disclosure" [#4789][_4789]; ignore dev-dependencies in OSV scan [#4550][_4550]
- Security-Policy beyond SECURITY.md [#4192][_4192]
- Bus-factor: contributor absence [#5416][_5416]; account-age weighting (anti-sockpuppet) [#4000][_4000]; criticality & maturity [#3821][_3821]
- Branch-Protection: collect bypass allowances (protection overstated) [#5451][_5451]; CODEOWNERS freshness probe [#3931][_3931]

### Column 2 — policy & standards (~2)

- Align checks with S2C2F Maturity Level 2 [#4296][_4296]; (inverse) remove CII-Best-Practices [#2904][_2904]
- Mostly requests for *mechanisms* (thresholds, exemptions), not new checks.

### Column 3 — platform & ecosystem currency (~15)

- Signed-Releases via GitHub attestations [#4080][_4080]; SBOMs in CI artifacts [#4119][_4119]
- Private vulnerability reporting [#2465][_2465]; OIDC-based publishing (PyPI etc.) [#2761][_2761]; tag-protection rules [#2476][_2476]
- Allow job-level write permissions when hash-pinned [#3022][_3022]; pre-commit framework as SAST [#5333][_5333]
- Maintained: activity within the last year [#2160][_2160]; Deps-Update-Tool still active [#2165][_2165]
- Packaging recognition: goreleaser fork [#5131][_5131], cargo-dist [#5145][_5145], winget [#5168][_5168], Helm charts [#5288][_5288], docker/bake-action [#5365][_5365]
- Ecosystem: Composer (PHP) support [#4378][_4378]

### Column 4 — actionability (zero)

No check-shaped proposals — its asks are remediation steps [#1850][_1850] and markdown export [_3798]: *output*, not new detections. That itself is signal: this cohort wants pasteables, not checks.

### Column 5 — threat currency (~11)

- Imposter commits (Chainguard/clank) [#2733][_2733]; `on: workflow_run` trigger chaining [#3861][_3861]
- Dangerous-Workflows: detect refs [#2404][_2404]; declared branches [#2406][_2406]; Jenkinsfiles [#2214][_2214]; untrusted-input expansion [#3915][_3915]
- Tokens able to create/approve PRs [#2707][_2707]; secure runners (self-hosted abuse vector) [#3801][_3801]
- Unpinned repo clones in scripts/Makefiles [#608][_608]; `.whl` download → pip install execution [#613][_613]; AI / external-communication usage detection [#4565][_4565]

## Consolidation opportunities

1. **Signed-Releases v2 epic** — the attestations cluster [#4080][_4080], [#4667][_4667], [#4174][_4174], [#382][_382], [#2684][_2684], [#5308][_5308] is six issues asking one thing.
2. **`workflow-threats` probe family** — [#2733][_2733], [#3861][_3861], [#2404][_2404], [#2406][_2406], [#3915][_3915] become probes composed into one check; new disclosures get slotted, not architected per-issue.
3. **Policy/conformance migration** — threshold [#4631][_4631], exemption [#2614][_2614], and output [#1850][_1850], [#3798][_3798] asks fold into the OSPS-Baseline conformance layer rather than the classic score.
4. **Stale harvest** — the Step 0 pass over 120 stale issues (many pre-2023, superseded by the probes refactor).

## Open decision: conformance reporting granularity

Not in the issue backlog (Nov 2026 community thread): **what does conformance output report by default?**

- *Granular:* maturity levels as default, control details in evidence files or behind an explicit flag — consumers need "why is this level 1?" for risk decisions; "one analysis, two tools" is bad UX.
- *Binary:* conform or don't — granular per-control consumer reporting would recreate the dynamic that made maintainers wary of Scorecard: a vector for "please do these things," punishment for project shapes where a lower level is appropriate.

Unresolved. The "use the existing granular tool for debugging" counterpoint loses to the UX argument on the consumer side, but the punishment-cycle warning is the strongest maintainer-side argument and precisely what Scorecard lived through with per-check scores — it deserves equal weight.

## Method & caveats

- All 254 open issues fetched via GitHub API, clustered by title keywords, labels, and comment counts; ~12 high-traction bodies read in full; regex proposal detection across all bodies, then hand-curated.
- Classification ambiguities remain for [#4565][_4565] and [#4769][_4769].
- Column 2 ranked above Column 4 is a judgment call, sensitive to weighting large-org gate users vs. individual contributors.

[_382]: https://github.com/ossf/scorecard/issues/382
[_383]: https://github.com/ossf/scorecard/issues/383
[_427]: https://github.com/ossf/scorecard/issues/427
[_608]: https://github.com/ossf/scorecard/issues/608
[_613]: https://github.com/ossf/scorecard/issues/613
[_689]: https://github.com/ossf/scorecard/issues/689
[_884]: https://github.com/ossf/scorecard/issues/884
[_1606]: https://github.com/ossf/scorecard/issues/1606
[_1850]: https://github.com/ossf/scorecard/issues/1850
[_2160]: https://github.com/ossf/scorecard/issues/2160
[_2165]: https://github.com/ossf/scorecard/issues/2165
[_2214]: https://github.com/ossf/scorecard/issues/2214
[_2404]: https://github.com/ossf/scorecard/issues/2404
[_2406]: https://github.com/ossf/scorecard/issues/2406
[_2465]: https://github.com/ossf/scorecard/issues/2465
[_2476]: https://github.com/ossf/scorecard/issues/2476
[_2614]: https://github.com/ossf/scorecard/issues/2614
[_2684]: https://github.com/ossf/scorecard/issues/2684
[_2707]: https://github.com/ossf/scorecard/issues/2707
[_2733]: https://github.com/ossf/scorecard/issues/2733
[_2761]: https://github.com/ossf/scorecard/issues/2761
[_2904]: https://github.com/ossf/scorecard/issues/2904
[_2952]: https://github.com/ossf/scorecard/issues/2952
[_3022]: https://github.com/ossf/scorecard/issues/3022
[_3798]: https://github.com/ossf/scorecard/issues/3798
[_3801]: https://github.com/ossf/scorecard/issues/3801
[_3817]: https://github.com/ossf/scorecard/issues/3817
[_3821]: https://github.com/ossf/scorecard/issues/3821
[_3861]: https://github.com/ossf/scorecard/issues/3861
[_3915]: https://github.com/ossf/scorecard/issues/3915
[_3931]: https://github.com/ossf/scorecard/issues/3931
[_4000]: https://github.com/ossf/scorecard/issues/4000
[_4080]: https://github.com/ossf/scorecard/issues/4080
[_4119]: https://github.com/ossf/scorecard/issues/4119
[_4174]: https://github.com/ossf/scorecard/issues/4174
[_4192]: https://github.com/ossf/scorecard/issues/4192
[_4296]: https://github.com/ossf/scorecard/issues/4296
[_4378]: https://github.com/ossf/scorecard/issues/4378
[_4550]: https://github.com/ossf/scorecard/issues/4550
[_4565]: https://github.com/ossf/scorecard/issues/4565
[_4631]: https://github.com/ossf/scorecard/issues/4631
[_4667]: https://github.com/ossf/scorecard/issues/4667
[_4769]: https://github.com/ossf/scorecard/issues/4769
[_4789]: https://github.com/ossf/scorecard/issues/4789
[_4824]: https://github.com/ossf/scorecard/issues/4824
[_5131]: https://github.com/ossf/scorecard/issues/5131
[_5145]: https://github.com/ossf/scorecard/issues/5145
[_5168]: https://github.com/ossf/scorecard/issues/5168
[_5280]: https://github.com/ossf/scorecard/issues/5280
[_5288]: https://github.com/ossf/scorecard/issues/5288
[_5308]: https://github.com/ossf/scorecard/issues/5308
[_5333]: https://github.com/ossf/scorecard/issues/5333
[_5365]: https://github.com/ossf/scorecard/issues/5365
[_5416]: https://github.com/ossf/scorecard/issues/5416
[_5451]: https://github.com/ossf/scorecard/issues/5451
