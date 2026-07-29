# Session checkpoint — 2026-07-29 — Ops-dashboard round: 13 PRs, #75/#76 closed

Archived as: 2026-07-29-ops-dashboard-round.md
Repos touched: unconsult/no5pilot (PRs #104-#116, all merged to main)

## Where we left off

Thirteen PRs merged. Richard's worst bug (#75, ET1 race-discrimination box misread) and the whole Assessment of Claim complaint (#76, five points) are closed. Also closed: #71 edited badge, #69 wider isolation tests, #53 eval regression, and three stale Healthchecks alerts (#49/#73/#74) from the July spend-cap outage. The ops dashboard is regenerated at its usual URL with each open feedback item now naming what it waits on. Feedback log corrected twice (#109, #116) and now matches reality.

Open user feedback is down to 4: #68 (decided and dated, being built), #77 module redesign, #83 highlighting, #82 chronology page-refs verification.

## Decisions made

- **#68 ask-a-question: BUILD IT.** Bundle-navigation half first, targeted w/c 10 Aug; case-law half held for the Richard + Emma conversation because of the no-invented-citations rule. Recorded on the issue. **Draft note to Richard written but NOT sent** (scratchpad, this session) — Bontle sends it.
- **Em dash rule enforced deterministically** (Bontle chose "auto-correct after the model writes"). Dashes normalised to a hyphen after generation, before storage. The eval applies the same normalisation, so `test/editorial.test.js` is now what the eval check used to be for that rule.
- **CI gained `workflow_dispatch`** after GitHub stopped delivering pull_request events for hours; nothing removed or relaxed.
- Constraints register corrected: worst case is 4,000 pages not 2,000 (2,000 was Azure's per-request cap), and the 160,000-token input guard is now a named limit.

## What was tried

- #53 was NOT a quality regression. The judge was never told which side counsel acts for, so it marked correct cross-examination as targeting the wrong witnesses, and read the brief's required evidential-gap questions as fabrication. Fixed in #107; verified by a full judged eval, all green.
- #76's authority half had a structural cause, not just wording: on bundles over ~320 pages the reduce path dropped AUTHORITIES entirely while still sending the prompt clause forbidding case law when none exist.
- Live RLS deny tests dispatched against production: **24 checks, all passed**, covering matters, documents, module_outputs, usage_log and audit_events. The six RLS_TEST_* secrets have existed since 28 Jul — an earlier claim in this session that they were missing was wrong.
- Concurrent-session collision: another window was working in the same checkout all day. #115 (theirs) added a worktree convention. Verified my #111 commit did NOT sweep their prompt edit (zero crossExamination lines).

## Open questions

- **Emma still has no GitHub access.** Verified: not in the org (Team plan, 1 of 2 seats used, so a seat is free), not on any repo, no pending invite. Path is the **People** tab, not Settings. Needs her username.
- **#108** (auto-filed eval regression) is partly stale: em dash now fixed; one failure is a **false positive in the new `checkboxStateNotAsserted` criterion**, which wrongly failed correct hedged output ("If counsel's inspection of the ET1 reveals that further boxes were ticked..."). Task chip spawned. Third failure (preliminaryIssuesFocus) is pre-existing.
- #70 deliberately part-open: unknown Azure error shapes still finalise, needs a live repro.

## Start here

**#68 build, bundle-navigation half.** The feasibility gate is done and merged (#114) and the design is on the issue: the naive design fails by 6.25x to 12.5x, so it must retrieve pages and never send the bundle. Binding constraints are the 160,000-token input guard and the 10 s synchronous function timeout.

WIP already pushed on branch `claude/68-retrieval-wip`: `netlify/functions/_retrieval.mjs`, the pure page-scoring core, committed but not PR'd and imported by nothing. Still to build: the synchronous function with token verification and RLS-scoped document reads, the answer prompt carrying SOURCE_GUARD, citation rendering, the panel, and the eval fixture. One trap found: the citation click handler is bound to the centre column only, so a Q&A panel inside the source pane would not get citation clicks.

Work in a git worktree, not the shared checkout (CLAUDE.md, added today).
