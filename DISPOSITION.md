# Disposition — all 40 register problems

**Variant C applied (2026-08-04).** The client-chosen design direction "Accent Spine"
(`variants.html` §vC + `research/reports/2026-08-01-pdp-proto-ui-design-review.md` §5) is now
the canonical `index.html` render, with two client amendments: the audience-fit line sits above
the description under the H1, and the left content column adopts the same system (no spine bars
off the buy path). All 40 dispositions below remain in force — the restyle changed how several
fixes LOOK (charcoal step bands → barred headings, green semantics → dark latobold ink, 20px →
24px price, quiet-panel disclosures); rows updated inline with "C:" notes where the described
visual changed. Functional behavior (one DOM stack, mobile order, tier scroll, overlay listbox,
toggle/chips) is unchanged and was re-verified live.

Source of truth: `research/reports/2026-07-30-pdp-enriched-render-ux-review.md` (§2 P-01…P-34,
§2b P-35…P-40). Counts: **36 implemented · 4 annotated-only · 0 excluded**.

Annotated-only = the fix lives outside page markup/CSS (third-party config, platform template,
or content-pipeline change) — the prototype shows the corrected end state where visible and the
Annotated view explains the real-site lever.

| ID | Sev | Disposition | How it lands in the prototype |
|---|---|---|---|
| P-01 | Critical | Implemented | One DOM stack; at ≤768px the hero (`.product-summary-section`: SKU, H1, subtitle) orders between gallery and Colors — the product is named on the first mobile screen |
| P-02 | Critical | Implemented | Tier-table wrapper `overflow-x:auto` at mobile; all 7 tiers reachable by swipe |
| P-03 | Critical | Implemented | Swatches are real `<button aria-label="…" title="…">` reusing `.color-circle` visuals; fully tabbable, Enter/Space selects |
| P-04 | Critical | Implemented | H1 = v5.2 `pdpTitle` "Fairweather Johnson Gilmore Lightweight Tee"; SEO compound string only in `<title>`/meta; `h1.product-name` styling unchanged |
| P-05 | High | Implemented | `strong` → `font-family:latobold; font-weight:normal` (H1's own pattern); every family chain ends `, sans-serif` incl. subtotal/price/CTA; subtitle = `latoregular, sans-serif`; @font-face mirrors theme (all faces weight-normal aliases) |
| P-06 | High | Implemented | Tier cells highlight-only (`attr-active`), never write quantities; click moves focus to the size-grid heading |
| P-07 | High | Implemented | All sizes load at 0; MOQ helper line is the neutral initial hint; price element shows "From $11.95/unit at 1008+" until quantity entered |
| P-08 | High | Implemented | "View Price Breakdown" is a real `<button>` (link class); production "?" is a 24px-hit-area `<button>` with focus-visible tooltip (`aria-describedby`) |
| P-09 | High | **Annotated-only** (config note) | No Klaviyo ribbon in prototype; single Contact affordance desktop-only, hidden ≤768px so no input occlusion. Real-site lever: Klaviyo display settings |
| P-10 | High | Implemented | INCLUDED row: inline `aria-hidden` ✓ + hanging indent per the Key Facts reference; sentence demoted to standard value style. **C:** ✓ and all positive semantics = latobold dark ink; the 1.70:1 bright green retired |
| P-11 | High | Implemented | Method-facts labels re-rendered with `table.pdp-spec-table th` style + geometry (38% col); uppercase dropped. **C:** shared table voice = latoregular #757575 label / #1f1f1f value — label never outweighs its value |
| P-12 | High | Implemented | Charges flattened to standard rows in the informational Decoration & Imprint spec table: "Setup fee — $30.00 per add'l location — first location free" / "Add'l location — $5.95/item". **R2 (2026-07-31):** configurator charges table separately recomposed to user-action rows — "First location → Included" / "Additional location → $30.00 setup + $5.95/item". **C:** "Included" = `<strong>` dark ink, no green; gray-label/dark-value rows on hairlines |
| P-13 | High | Implemented | **C:** `$183.00` = 24px/30 latobold dark in the accent-spine price zone (3px orange bar; gray band retired) — the strongest buy-box text; label + "Price each" = deliberate 14px quiet meta |
| P-14 | Medium | Implemented | Key Facts card orders between hero and Colors at mobile widths |
| P-15 | Medium | Implemented | Section titles wrapped in `<h2>` (class carries the look); Key Facts title = `<h2>`; `$183.00` demoted to styled `<span>`; outline: H1 → H2s |
| P-16 | Medium | Implemented | Right column `position:sticky; top:16px` — price/CTA visible while reading content |
| P-17 | Medium | Implemented | Below MOQ: tier-1 unit price stays in "Price each"; subtotal grayed, MOQ message carries the explanation; CTA disabled |
| P-18 | Medium | Implemented | Label renders "Subtotal:" when computed setup = $0 |
| P-19 | Medium | Implemented | Breakdown modal captioned "Includes: full-color imprint, one location (configured next step)"; "1Right Chest" run-on fixed |
| P-20 | Medium | **Annotated-only** | Klaviyo popup delay/suppression + cookie-banner co-occurrence are Klaviyo/consent config, not page code; prototype shows the clean first paint |
| P-21 | Medium | Implemented | Single DOM stack; mobile order via `display:contents` + CSS `order` — no duplicate trees, no state desync |
| P-22 | Medium | Implemented | Step bars are static `<h2>` headers; checkboxes/buttons removed from DOM and tab order; no false mobile checkmarks. **C:** charcoal 522×40 bands retired — barred text headings (3px #fe5000 spine bar + orange latobold numeral, 18px latosemibold dark) |
| P-23 | Medium | Implemented | Each swatch: `aria-label` + `title` (name data), 8px flex gap, 48px wrapper target |
| P-24 | Medium | Implemented (scope note) | Prototype has no horizontal scroll at 390 (tier strip scrolls inside its own wrapper). Footer `.px-5` contributor is site chrome outside prototype scope — flagged for Boris |
| P-25 | Medium | **Annotated-only** | Rating, Request Free Sample, shipping cost, returns link are platform-template blocks (v5.2 rollout, Boris) — not invented here; chip marks the buy-box slot |
| P-26 | Medium | Implemented | Locations render as comma-separated 16px latoregular text in the spec-row pattern (Specifications "Sizes" precedent) |
| P-27 | Medium | Implemented | Method summary suppressed (single-method product). **R2 (2026-07-31):** the section header carries a recomposed summary ("Full-color imprint · first location included") via `.pdp-section__hsummary`. **C:** the filled-band header idiom is retired — the method block is the page's ONE quiet gray disclosure panel (shared with When-To-Choose), dark name, gray chevron |
| P-28 | Medium | Implemented | Q&A headings get `pdp-section__title`. **C:** ONE 18px latosemibold h2 voice page-wide — left section titles, Q&A, and spine step headers share it (steps add the bar; left stays barless) |
| P-29 | Medium | Implemented | Closed by the sticky right column (P-16 option); no dead half-page while reading |
| P-30 | Low | Implemented | Gallery arrows have `aria-label`s; no clone slides exist; rail padded so no thumb clips |
| P-31 | Low | Implemented | Spec table deduped: single "Fabric — 4.3 oz lightweight (146 GSM)" row (contentV5 pipeline owns the permanent rule) |
| P-32 | Low | Implemented | The one-off italic callout removed from Description. **C:** the accent bar deliberately RETURNS on this line — not ad-hoc but as the named "buy-path waypoint" role of the spine system; the line is the hero qualifier under the H1 (P-37) |
| P-33 | Low | Implemented | Method facts reuse the literal `pdp-spec-table` component — label columns align by construction |
| P-34 | Low | **Annotated-only** (removal) | No "GO!" scrap, no detached ribbon close in the corrected render; real-site fix is suppression/re-attachment |
| P-35 | High | Implemented | Configurator: method description promoted to the pane's body style; decision body demoted, semibold reserved for "Best for:" lead-in. **R2 (2026-07-31):** orange tint/border stripped. **C:** When-To-Choose = quiet #fafafa panel with radius, standard 16px inset, hover + focus states, gray chevron, 14px/21 body — a defined aside, deliberately off-spine (closes the review's N-5 "white, no defined paddings" percept) |
| P-36 | Medium | Implemented | ONE kicker style, 13px latobold Title Case (uppercase dropped in R2) — **C:** carried by Key Facts alone; "When To Choose This?" moves to the 14px latosemibold disclosure-title voice; labels stay Title Case; charges rows use the C table voice (gray label / dark value) |
| P-37 | Medium | Implemented (spec note) | Audience-fit line lives in the hero; removed from Description. Requires v5.2 spec §2.5 amendment (content-template change) — flagged. **C (client amendment A):** the line moves ABOVE the description, directly under the H1, and carries the 3px orange spine bar as the buy path's first waypoint — adjacent to the steps it would read as a false first step |
| P-38 | Medium | Implemented | Collapsed Production & Shipping header shows "Est. delivery Aug 13 – Aug 20 · 5–10 business days production" via the method-block summary pattern (collapse the section to see it) |
| P-39 | Medium | Implemented | Location listbox = `position:absolute` overlay (Subtotal/CTA no longer pushed); included-fact triplet deduped to anchor sentence + charges table (note dropped). **R2 (2026-07-31):** deduped further to ONE statement — the recomposed charges table row ("First location — Included"); the anchor sentence and a third, previously-undocumented "?" tooltip repetition on Imprint #1 cost are both removed. **R2 live-verification fix:** a fourth repetition, the "Imprint #1 cost: Free" line itself, was also removed; its label cells ("First location"/"Additional location") corrected from `<td>` to `<th scope="row">` so the existing 16px/24 latosemibold th pattern applies |
| P-40 | Low | Implemented (via P-27) | Summary suppressed on this single-method product; recomposed multi-method string documented: "1 full-color location included · extra location $30.00 setup + $5.95/item". **R2 (2026-07-31):** now rendered live at the section-header level ("Full-color imprint · first location included", single-method wording) |

## Annotated-only rationale (2 + 2 borderline)
- **P-20** — Klaviyo targeting + consent-banner sequencing: third-party config, no site code.
- **P-25** — platform-template blocks; adding them here would fake scope that belongs to Boris's
  template half of the v5.2 rollout.
- P-09 / P-34 are implemented-as-removal in the prototype but their real-site levers are also
  config-side (Klaviyo display settings; widget artifact suppression) — chips say so.
