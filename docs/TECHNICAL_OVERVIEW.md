# Technical Overview

## Architecture
- **One static file, `index.html`** (~130 KB). It contains embedded CSS, vanilla JavaScript and a JSON data block
  (`<script id="app-data" type="application/json">`).
- **No dependencies, no network calls at runtime, no backend, no API key.** It works from `file://` and from GitHub Pages.
- **Hash-based routing** gives every screen its own link:
  `#/dashboard`, `#/prospects`, `#/p/<id>/<stage>` (stage = `find|research|fit|contact|email`), `#/map`,
  `#/scoring`, `#/about`.
- **Persistence:** `localStorage` key `goBooster.v1` stores stage changes, an activity log, edited drafts and
  custom weights. Every access is wrapped in try/catch, so the app still works if storage is blocked.
  *How it works → Clear my local edits* resets it.

## Data model
Each prospect has: `name, address, postcode, category, price_tier, ownership, current_delivery, has_online_store,
description, website, contact_email, contact_phone, contact_page, evidence_url`, plus coordinates
(`lat, lon, geo_precision`).

Real prospects also carry a research dossier:
- **Verified facts:** `facts[] {text, source}`.
- **Context:** `source_urls[]`, `contact_routes[]`, `other_locations[]`.
- **Hypotheses:** `positioning, target_customer, distinctive, why_local, angle, fit_notes[], objections[]`.
- **Gaps:** `unknowns[]`.
- **Research's own rating:** `research_rank, research_score (/25), evidence_confidence`.
- **Email personalisation:** `email {greeting, subject, hook, value, question, visit, followup_topic, area}`.

## Data provenance
| Data | Source | Notes |
|---|---|---|
| 10 real prospects | Independent research file (21 Nov 2026) from official brand websites | Names, addresses, postcodes, URLs, emails and phones copied verbatim. Missing fields left empty (shown as *Unknown*). |
| Price tier, category, ownership, delivery class | Classification of the research for scoring | Shown as classifications, not brand claims. |
| 27 demo records | Fictional | Labelled DEMO everywhere; never used for outreach. |
| Coordinates | postcodes.io, looked up at build time | Real prospects: full-postcode centroids. Demo: district centroids. |

## Scoring
Six criteria, each returning a fraction of its weight, a reason, a confidence level and its missing fields:
Product suitability (25), Customer demand (20), Geographic suitability (20), Brand/product value (15),
Digital readiness (10), Feasibility (10).
- **Total:** the sum of `fraction × weight`.
- **Confidence %:** `Σ(weight × {High 1, Medium 0.6, Low 0.25}) / Σ weight`.
- **Priority:** High ≥ 80, Medium ≥ 60, otherwise Low.

The weights can be changed live on the Scoring page; they must total 100. The model is a proposal, not
Booster's official model.

## Email generation
- **Real prospects:** greeting, fact-based opening, a one-sentence Booster description, a value hypothesis, a
  discovery question and a low-commitment ask. The follow-up references the pilot outline.
- **Demo prospects:** a generic template, marked "DEMO DRAFT".
- **Recipients:** only the published route is shown. If none exists (Crockett & Jones), the app points to the
  enquiry form and phone number.
- **Actions:** Copy, Download .txt, *Open draft in my email app* (`mailto:`, which the user sends), Save/Reset edits,
  and *Mark as contacted* (asks for confirmation that the user sent it).

## Quality assurance performed
- Rendered all 37 prospects × 5 stages plus every page (190 views): 0 JavaScript errors.
- Checked that no real email draft contains any email address in its body, or the text "undefined" or "null".
- Tested filters, search, sorting, row navigation, CSV/JSON/TXT downloads, stage update, draft save/reset,
  mark-as-contacted, weight sliders (blocked unless the total is 100), the demo toggle and map navigation.
- Opened from `file://` in headless Microsoft Edge (screenshots) and Google Chrome (DOM check): rendered correctly.
- Mobile emulation at 375 px: page width equals viewport, with no horizontal scrolling.
- Scanned for API keys, tokens and personal data: none in the package.

## Rebuilding (optional)
The app was generated from a source template and a JSON data file in the original working folder. The published
`index.html` is the complete artefact, and editing it directly is fine.
