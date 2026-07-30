# Prototype Notes — pdp-render-fixes
_Date: 2026-07-30 | Page: PDP (enriched render, Fairweather Johnson Gilmore Lightweight Tee)_

## Task
Corrected-PDP prototype implementing all fixes from the verified UX review
(`research/reports/2026-07-30-pdp-enriched-render-ux-review.md`) while reusing the site's
ORIGINAL styles and components — zero invented design tokens.

## Source
Live page `https://admin.promotionpros.com/fair-weather-johnson-gilmore-lightweight-tee-...-2`,
captured 2026-07-30 (`_temporary/pdp-ux-review/2026-07-30/wu1` + `wu6`).

## Design Library
Base kit: `_temporary/pdp-proto/2026-07-30/base/` (theme.styles.css excerpts, font-face rules,
fonts, logo). All component CSS below is copied from `theme.styles.css` verbatim or with only
the review-prescribed value changes.

---

## A. Consistency matrix — same role → same style (ONE style per role)

| Role | The one style (source) | Replaces on live |
|---|---|---|
| Page title (H1) | `h1.product-name`: latobold 24px/1.2 #1f1f1f | unchanged (content re-bound per P-04) |
| Section title | `span.pdp-section__title`: latosemibold 20px/30 #1f1f1f, Title Case, inside `<h2>` | 3 idioms → 1: also applied to Q&A headings (P-28), semantic h2 (P-15) |
| Kicker (small uppercase) | Key Facts treatment: latobold 13px, uppercase, ls .08em, #1f1f1f | the ONLY uppercase on the page; also the When-to-choose title (P-36). 11px gray caps labels + 12px orange caps eliminated |
| Step-bar header | charcoal #525252 bar; `.step-number` latobold 20px white + `.step-label` latomedium 16px white; static `<h2>` | do-nothing buttons + phantom checkboxes removed (P-22) |
| Pane sub-heading | latosemibold 16px #1f1f1f, **Title Case** ("Imprint Method: Full Color", "Imprint Location", "Imprint Colors", "How Many Would You Like of Each Size?") | casing disagreement resolved (P-36) |
| Row label (spec + method facts + charges th) | `table.pdp-spec-table th`: latosemibold 16px/24 #525252, col 38%, padding 8px 12px 8px 0 | 11px caps labels (P-11), nested charge-labels (P-12), charges th/td weight inversion (P-36), column misalignment (P-33) |
| Body text | latoregular 16px/24 #525252 (16px/26 in Description) | 13px method description promoted (P-35); decision slab demoted from all-semibold (P-35) |
| Secondary/meta (13px floor) | latoregular 13px #525252 — collapsed-header summaries only | nothing renders below 13px anywhere (was 11px) |
| Price (subtotal value) | `span.pdp-section__title` metrics: latosemibold 20px/30 #1f1f1f | price = label 16px parity (P-13) |
| Inline emphasis | `font-family: latobold; font-weight: normal` (the H1's own pattern) | faux-bold `latoregular`+700 synthesis (P-05) |
| Positive/success | `.text-success` green (the IN STOCK green); ✓ inline + aria-hidden | orphaned block-level ::before tick (P-10) |
| Text action/link | `.view-price-breakdown-link`: latoregular 14px #fe5000, real `<button>` | span-with-cursor mouse-only triggers (P-08) |
| CTA | `.btn-secondary.add-to-cart-lg`: orange #fe5000, latobold 20px + `, sans-serif` fallback | missing font fallback on money elements (P-05) |

Casing rule (from review §3c): uppercase exists at exactly ONE level — the 13px latobold dark
kicker. Everything else Title Case (titles/labels) or sentence case (body). Every font-family
declaration terminates in `, sans-serif` (P-05).

## B. Hierarchy map — element → user importance → visual weight/position

| Element | Importance | Weight / position |
|---|---|---|
| Product name (pdpTitle) | orient first | 24px latobold, 1 line, first screen right col; on mobile above buy flow (P-01) |
| Subtotal price | decision | 20px latosemibold dark — only price-level text at 20px in the band; sticky right col (P-16) |
| CTA | action | 54px orange full-width bar, directly under price, sticky |
| Tier table + size grid | decision input | 14–16px latomedium, active tier highlighted (`attr-active`), non-mutating (P-06) |
| Subtitle + audience-fit line | qualify | 16px/24 gray, directly under H1 (P-37) |
| Key Facts | scan | bordered peach card, latobold lead-ins; top of content col; mobile: before buy flow (P-14) |
| Section titles | navigate | 20px latosemibold h2 — one step under H1 |
| Body copy / method description | read | 16px latoregular gray — nothing readable is smaller than 13px |
| Row labels | support values | 16px latosemibold gray — label never outweighs its value |
| Meta (SKU, collapsed summaries) | ambient | 13–16px gray/latolight |
| Decision aid (When to choose) | on-demand | collapsed by default; 16px regular body when opened — no longer outweighs the always-visible summary (P-35) |

Weight follows decision value: price > CTA label > titles > values > labels > meta. The only
persuasion-colored element is the CTA + link orange; green appears only as "included/free/stock"
semantics.

---

## Key Design Decisions
- One DOM stack, reordered responsively via `display:contents` + `order` (P-21's "render one
  stack and reorder via CSS" option). No duplicate desktop/mobile trees.
- Method-facts grid re-rendered as a literal `table.pdp-spec-table` — same component as
  Specifications, which closes P-11/P-12/P-26/P-33 with zero new CSS.
- Sticky right column = plain `position:sticky; top:16px` (P-16); corrected pane is short
  enough to fit a 900px viewport, so no internal scroll region.
- Configurator is a static corrected state swapped into the right pane by the Customize CTA
  (per brief: faithful corrected rendering, not a working configurator). Location listbox is a
  real absolute overlay (P-39) with basic keyboard support.
- Fixed | Annotated toggle: annotation chips + register drawer only exist in Annotated view;
  Fixed view is chip-free.
- Spec-table dedup (P-31) rendered as one row "Fabric — 4.3 oz lightweight (146 GSM)" (146 GSM
  = the review's own conversion); the Weight row is dropped rather than inventing a
  composition value the feed does not supply (zero-fabrication).

## Baymard Compliance (register-cited rules, post-fix)
| Rule | Where | Status |
|---|---|---|
| B-PDP038/043/045 (title/orientation) | pdpTitle H1 + mobile hero/Key Facts order | Pass (P-01/P-04/P-14) |
| B-PDP013/F-PDP004 (tier pricing reachable) | tier table `overflow-x:auto`, non-mutating | Pass (P-02/P-06) |
| B-PDP014 (price emphasis) | 20px subtotal | Pass (P-13) |
| B-PDP019 (color selection) | button swatches, aria-label + title, 8px gap | Pass (P-03/P-23) |
| B-PDP016 (delivery estimate) | collapsed Production header keeps estimate | Pass (P-38) |
| B-PDP001/003 (buy-box visibility) | sticky column; overlay listbox stops CTA push | Pass (P-16/P-39) |
| B-PDP024/029 (labels/headings) | one label style, one heading system | Pass (P-11/P-15/P-28/P-36) |
| B-PDP015/017/025 (shipping cost, sample, rating) | NOT built — platform-template gap flagged to Boris | Exception, annotated-only (P-25) |
| B-PDP027/F-PDP008 (overlays) | no interstitial/ribbon in prototype; Klaviyo config change | Annotated-only (P-20), removal shown (P-09/P-34) |

## Competitor Summary
Not re-run this session — the review (and its v5.2 spec lineage) carries the 4imprint
benchmarking; no new competitor claims introduced.

## Known Deviations from Live Site
- Header simplified to logo + breadcrumb (fix scope is the PDP region; site chrome omitted).
- Footer / newsletter / Wisconsin band omitted (out of fix scope; P-24's footer `.px-5`
  contributor noted in DISPOSITION.md).
- Q&A module rendered as empty-state stub (Answerbase is third-party).
- Klaviyo popup/ribbon/cookie banner intentionally absent (P-20/P-34 are config/removal fixes).
- Product photos hotlink the live CDN (house rule).

## Change Log
- 2026-07-30 Initial corrected prototype: all 40 register problems dispositioned
  (see DISPOSITION.md), Fixed + Annotated views, corrected configurator state, mobile 390 path.
- 2026-07-30 Tier cells at theme-scale padding so all 7 tiers fit the 522px pane (P-02 desktop parity).
- 2026-07-30 Mobile: thumbnail rail min-width:0; reordered flex items capped at viewport width —
  the 620px natural image width was re-creating P-24's horizontal scroll via flex min-content floors.
- 2026-07-30 Contact affordance reduced to a 48px icon positioned clear of the buy pane
  (P-09 desktop facet: live bubble covered "Price each").
