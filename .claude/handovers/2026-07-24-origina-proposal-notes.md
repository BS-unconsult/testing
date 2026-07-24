# Session checkpoint — 2026-07-24 — Origina proposal and call notes

Also saved as: 2026-07-24-origina-proposal-notes.md
Repos touched: bs-unconsult/cartographer, branch claude/cartographer-proposal-notes-lz17db (pushed)

## Where we left off

The 23 July Origina call note is final: docx sent to Bontle, markdown committed at docs/notes/2026-07-23-origina-call.md. Section 7 (Dan's candid context) is internal to Bontle and Dan only. The proposal is at v2: a fifteen-slide deck in the Origina-aligned brand (navy #051435 ink, cyan #32C5F4, purple #6732F2, Instrument Sans, #0E121D dark bookends, no Origina logo) at docs/proposals/Cartographer_Origina_Proposal.pptx, with why-cartographer.svg alongside, committed and pushed; PDF render sent to Bontle. A Gmail draft to Dan (reply on his "Origina Proposal" thread, dan@dowelldogood.co.uk) describes v2; Bontle still needs to attach the pptx manually and delete her earlier draft on the same thread, which describes v1 and names Jon. A buyer stress test (clean-instance second opinion plus contextual interrogation) was delivered in chat on 24 July and has not been turned into any artefact.

## Decisions made

Exact pricing in the deck: £8k validation, £25k fixed fee plus £500 to £1,500 a month licence, Phase Three priced only after production usage; investment slide carries "All fees are fixed and exclusive of VAT". Outlook is consented one-click touchpoint capture, never message bodies or counterparty addresses. Works council framed as co-determination for German employees in scope; regulator cited as the Irish DPC. Deck restructured to Bontle's own proposal pattern (exec summary upfront, product screenshots, feature grid, no client names or call quotes, credibility slide, "P&L ownership" phrasing). The retained value question stays in as a purple pull-card. The v1 violet styling was rejected on brand grounds and replaced.

## What was tried

v1 was a twelve-slide violet deck, built, committed, then rejected; v2 replaced it in a full rebuild. The Playwright suite went 31/31 green only after running cartographer-team/tests/setup.sh, which regenerates the gitignored supabase-bundle fixture every fresh clone needs. Instrument Sans was installed locally for true renders; slide QA is soffice to PDF then pdftoppm.

## Open questions

Whether Bontle carries professional indemnity or cyber insurance (asked, unanswered). Success and kill criteria plus a contribution-rate metric for the £8k phase: nowhere defined, highest-leverage fix. Article 14 transparency for people in the register and exec voluntariness: flagged independently twice, belongs in the DPIA conversation with Origina. A Neon Noir generic version of the deck is parked until this one is final.

## Start here

If Dan replies with edits, the deck source is docs/proposals/ on the branch; re-render with soffice and pdftoppm after any change and check the editorial rules (no em or en dashes, no ampersands, UK spelling). The 24 July stress-test output in the session chat is the raw material if Bontle asks for an FAQ annex, a contract schedule, or DPIA additions.
