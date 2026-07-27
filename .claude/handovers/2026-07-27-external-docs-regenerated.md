# Session checkpoint — 2026-07-27 — External security docs regenerated
Archive filename: 2026-07-27-external-docs-regenerated.md
Repos touched: unconsult/no5pilot (branch claude/sync-checklist-doc-regen; PR #72 merged to main)

## Where we left off
All four externally shared Bundl documents regenerated (26 July) from docs/SECURITY.md and
saved over the 15-July originals in OneDrive (1 AI TOOLS/unconsult): the 4-page law-firm
briefing, the CTO/CISO/DPO security briefing (now 12pp: new audit-trail page, six-item
residual-risk page), the DPIA (13pp, retitled "July 2026 revision B" with a three-row version
history), and the 17-page law-firm explainer. Carried into all four: EU-inference claim
withdrawn (model leg stated as Anthropic's global API endpoint under SCCs, withdrawal recorded
with the 26 July verification date), ZDR requested-and-declined (July 2026), R2 region
confirmed Western Europe (WEUR) EU, daily in-region backups verified with the untested restore
stated plainly, MFA step-up on every sign-in path once enrolled, append-only audit trail, and
the C1–C13 self-attested register. Built as branded HTML (Syne / DM Sans / Space Mono, ink
navy + yellow) rendered via a local Playwright script; every page visually checked for
overflow. PR #72 (sync-checklist tick + changelog) merged to main with admin bypass, CI green.

## Decisions made
- The updated PDFs will go out to firms (Bontle, this session).
- Bontle handles the investor-brief re-export (#63) herself.
- In the 4pp comparison table, Bundl's own "UK / EU data plane" row moved from Yes to Partial
  ("data at rest UK + EU; model call global API") for consistency with how rivals are marked.
- DPIA transfer-exposure risk re-rated Medium/Medium mitigated to Low residual by SCCs, in
  place of the withdrawn EU-inference mitigation.

## What was tried
- beautiful-pdf skill loaded for the pipeline, but its default look (Garamond, rose/gold) and
  its bundled render script were unusable here; wrote a scratchpad Playwright render script
  and kept the Bundl brand system. pymupdf used for old-PDF text extraction and per-page
  overflow rasters. Old PDFs backed up only in the session scratchpad (ephemeral).

## Open questions
- Test restore run + date (#60); legal sign-off on IR commitments (#61); routing platform
  (#62, Vertex fallback if AWS silent past early August); pen test path (#64); Anthropic
  rate-limit tier (#67); Emma repo invite + dashboard share (#66); audit_events SQL hand-run?
- Does the Partial self-mark in the comparison table stand after Bontle reviews it?

## Start here
NEXT SESSION: return to the deferred main thread — build the ISO 27001 / SOC 2 layer
(policy-as-code: machine-checked gates with short plain-language policy docs on top), starting
from the gap list in docs/controls-mapping.md. Full brief is in the 2026-07-26 checkpoint's
"Start here". Constraint unchanged: solo founder + Emma (non-code), pre-revenue, nothing that
needs a paid GRC platform or standing meetings; anything CI can attest is in.
