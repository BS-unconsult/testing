# Session checkpoint — 2026-07-27 — Bundl outage + v27Jul26 feedback round

Archived as: 2026-07-27-bundl-outage-feedback-round.md
Repos touched: unconsult/no5pilot (seven claude/* branches, all merged to main and deleted: PRs #80, #84–#89)

## Where we left off

Everything shipped and verified. The morning outage (Anthropic org monthly spend cap tripped at $50.19 against a $50 cap, blocking all of Richard's runs) is resolved: cap raised to $100, first successful run confirmed 07:05 BST, Healthchecks green. Seven PRs merged to main and deployed; production smoke test green on no5pilot.netlify.app with today's bundle confirmed live (form toggle + extraction warning present in served JS). Reply email to Richard drafted in Bontle's voice (final version asks which highlighting he means); she pastes and sends it herself. Memory (bundl-operational-state) updated with all of this.

## Decisions made

- Spend cap: raised $50 → $100 by Bontle; resets 1 Aug; standing policy question open.
- Batch approved and merged (all seven): #80 honest billing-gate error, #84 chronology Full/Short, #85 participants Full/Short, #86 still-extracting run warning, #87 search expired-request re-sign gap, #88 assessment engagement rework + preliminary-hearing eval fixture, #89 feedback-log docs round.
- BUILD NEXT (Bontle, end of session): Case Summary as a proper first-class module (currently dashboard-only widget), and Ask a Question (bundle-grounded lookup first).
- HELD for a Richard + Emma + Bontle conversation: case law and legal principles module, opening note, written closing submissions, First Notes removal, Inconsistencies' place — the risky remainder of his nine-module redesign.
- Highlighting: scoping waits on Richard's answer to the email question (mark-up-while-reading vs highlights feeding prep).

## What was tried

- Outage diagnosed via the Anthropic Console (limits page, request log) and Healthchecks, not guesswork; the $50.19-vs-$50 arithmetic identified the tripped cap.
- One branch per feedback item; stacked PRs (#85/#86/#88 on #84/#85) merged bottom-up. Every 2026-07-27 changelog line touches the same region, so each remaining PR needed main merged in and the conflict resolved before merging — expect this on any multi-PR day.
- CI live eval passed on #88 with one stochastic retry (by design, per #52). Local qa loop runs dry-run tier only (no local ANTHROPIC_API_KEY).

## Open questions

- Spend-cap policy and notify thresholds ($50/$75 partly fired; ~$50 headroom to 1 Aug).
- Richard's highlighting answer; the three-way redesign conversation.
- Upload-and-extract smoke needs a dedicated test account (owner decision parked). WIF conversion for CI reviewer still pending. ModuleNav hasBundle/hasSource prop-bug chip spawned, unactioned.

## Start here

Build Case Summary via the /new-module (B2) loop: module-graph parity across src/lib/modules.js and netlify/functions/_modules.mjs, prompt in _prompts.mjs (UK English, no em dashes or ampersands), judge brief + eval wiring; decide its dependency (the dashboard summary currently builds from First Notes). Then Ask a Question: feasibility gate against docs/CONSTRAINTS.md FIRST (name the binding constraint; worst case ~331 MB, 2,000-page bundle), bundle-grounded scope, RLS + injection guard + its own eval; likely a /ralph slice. Update docs/feedback-log.md rows when each ships.
