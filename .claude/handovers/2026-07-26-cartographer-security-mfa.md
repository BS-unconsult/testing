# Session checkpoint — 2026-07-26 — Cartographer security gaps and required MFA

Archived as: 2026-07-26-cartographer-security-mfa.md
Repos touched: BS-unconsult/cartographer (branch claude/cartographer-security-gaps-4y7851; PRs #1, #2, #3 all merged to main); BS-unconsult/testing (main, this checkpoint).

## Where we left off

Three PRs shipped and merged today, all prompted by CISO-style feedback Dan Brown forwarded. PR #1: client-facing docs/SECURITY.md, vendored supabase-js (2.110.7) and fonts so the app touches no third-party origin, security headers plus CSP, machine-checked eu-west-1 region pin, invariants 12 and 13. PR #2: security contact corrected to me@bontlesenne.com, daily Pro-plan backups verified and recorded. PR #3: MFA required for every account — restrictive aal2 policies on all seven entity tables (migration 009, applied to the live project after deploy and verified live), CartoAuth adapter fence in index.html (machine-checked), enrolment and challenge screens, suite grown 31 to 36 checks, invariant 14. Live state: app deployed, 009 applied, seven require_aal2 policies confirmed in pg_policies.

## Decisions made

Bontle decided: paperwork plus cheap pins first, written for Origina; MFA required for everyone, not optional; build MFA now with SSO as a parallel conversation with Origina's IT (adapter interface ready for a second provider); reveal log lands before the customer-facing audit trail (DPIA's own gate, and reads become loggable through it); lost-phone recovery is admin-reset only; session-lifetime tightening deferred; enforcement package (invariant 14, fence rule, CSP img-src data:) signed off. From the bundl email comparison: claims 2 (audit trail shipped) and 6 (controls mapping) are NOT true for Cartographer and must not be reused; tenancy and region claims are stronger here. AI layer: someday, stays gated, not a concern now.

## What was tried

Deny-covered label race: CI reads labels from the frozen event payload, so a label applied seconds after PR creation is invisible; fix is close-and-reopen, not re-run. Region probe: no documented Supabase region header, so check:invariants falls back to resolving db.<ref>.supabase.co (IPv6 in practice) into Amazon's published eu-west-1 ranges — answers even from the sandbox. Pinned client fact: removing a user's factor does not evict a live aal2 session, so the lost-phone runbook requires deleting the factor AND revoking sessions, with a roughly one-hour residual token window stated honestly. Checker's first MFA verdict was SHIP WITH NITS after an earlier DO NOT SHIP on PR #1 was fixed by building the missing checks (migration scans for USING (true) and publication additions) rather than softening the document's claims.

## Open questions

Bontle's live verification is pending: one real enrolment, a wrong-code refusal, and the lost-phone rehearsal (delete factor, revoke sessions), results to be recorded in SECURITY.md. Backup retention and point-in-time recovery still unverified; restore test not yet scheduled. SSO waits on Origina's identity provider. Optional next docs: ISO 27001 Annex A / SOC 2 controls mapping and explicit incident-response SLAs. DPIA (now 0.4) stays unsubmittable until the reveal log exists.

## Start here

Next phase is the reveal log with name pseudonymisation (DPIA section 3's adopted measure): plan through the feasibility gate, Opus subagents for schema and app, suite coverage in the same PR. Fold in the one-line migrations README fix (it still says 009 is not yet applied). Branch restarts from main per the merged-PR rule. Gates: check:invariants (11 checks), format:check, npm test (36), loop:privacy.
