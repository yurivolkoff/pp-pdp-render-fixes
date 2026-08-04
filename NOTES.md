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

State: **Variant C "Accent Spine" applied (2026-08-04)** — the client-chosen direction from
`variants.html` §vC, extended to the left column per client amendment B.

| Role | The one style (source) | Notes |
|---|---|---|
| Page title (H1) | `h1.product-name`: latobold 24px/30 #1f1f1f | content = v5.2 pdpTitle (P-04) |
| **Spine waypoint** | 3px `#fe5000` left bar + 12px inset | EXCLUSIVE set: audience line, step headers 1–4, both subtotal blocks — see §C |
| Step header (buy path) | `.step-header`: 18px/24 latosemibold #1f1f1f + latobold #fe5000 numeral, 32/12 rhythm, static `<h2>` | charcoal 522×40 bands retired (noise cause N-1); P-22 semantics unchanged |
| Section title (left col + Q&A) | `span.pdp-section__title` / `.qa-title`: 18px/24 latosemibold #1f1f1f, barless, inside `<h2>` | ONE h2 voice page-wide — steps add the bar, off-path never does |
| Kicker | Key Facts title ONLY: latobold 13px #1f1f1f, Title Case | When-To-Choose left the kicker system for the disclosure-title voice |
| Disclosure panel | quiet gray panel: `#fafafa`, radius 6, 12×16 toggle inset, hover `#f5f5f5`, gray chevron | ONE disclosure idiom: When-To-Choose + method block (filled-band header retired) |
| Disclosure title | 14px latosemibold #1f1f1f (WTC); method name 16px latosemibold #1f1f1f | navy method name retired — navy is for text links only |
| Pane sub-heading | latosemibold 16px #1f1f1f, Title Case | unchanged (P-36) |
| Table voice (spec + method facts + charges) | label: latoregular #757575 col 38% / value: #1f1f1f, hairline #eee rows | 16px in the left column, 14px in the buy pane; label never outweighs its value |
| Body text | latoregular 16px/24 #525252 (16px/26 in Description); WTC body 14px/21 | |
| Meta (13px floor) | latoregular 13px #757575 — SKU, wishlist, after-CTA line, secure line, badges, collapsed summaries | nothing renders below 13px |
| Price (subtotal value) | latobold 24px/30 #1f1f1f in the spine price zone | strongest buy-box text; label + per-unit = 14px #757575 quiet meta (P-13) |
| Inline emphasis + positive semantics | `font-family: latobold; font-weight: normal` dark ink | the bright `.text-success` green is retired — "Included", "first location free", "In Stock" are latobold dark (C monochrome off-path) |
| Text action/link | underlined gray #525252, hover #1f1f1f (breakdown, add-location); navy #001542 for nav/support links | AA everywhere (orange smalls were 3.0–3.3:1) |
| Secondary action | hairline outline: 1px #b3b3b3, radius 4, latomedium 14px #1f1f1f, hover border #1f1f1f | Edit button leaves the accent system |
| Selection / active state | `#fe5000` border + `#fff6f2` tint | ONE selection orange — #ff6b00 retired |
| CTA | `.btn-secondary.add-to-cart-lg`: #fe5000 fill, latobold 20px, radius 4 | disabled = solid #909090 (3.19:1 — was 1.41) |

Casing rule: NO uppercase anywhere (0 rendered instances). Title Case for titles, labels, and
the kicker; sentence case for body. Every font-family declaration terminates in `, sans-serif`
(P-05). Structural guards: `html{font-synthesis-weight:none}` + `h1,h2,h3,h4{font-weight:normal}`
— bold exists only by family switch.

## B. Hierarchy map — element → user importance → visual weight/position

Attention path (the C thesis): **orange audience bar → 1 → 2 → price bar → orange CTA** — the
spine literally draws the buy path down the pane; everything off it is monochrome and quiet.

| Element | Importance | Weight / position |
|---|---|---|
| Product name (pdpTitle) | orient first | 24px latobold dark, first screen right col; mobile above buy flow (P-01) |
| Audience-fit line | qualify | spine waypoint 1: 3px orange bar, dark 16px text, directly under the H1 and ABOVE the description (client amendment A) |
| Step headers 1–4 | way-find | spine waypoints: 18px latosemibold dark + orange latobold numeral — chroma, not area-mass, does the guiding (N-1 resolved) |
| Subtotal price | decision | spine waypoint: 24px latobold dark — the largest dark type in the pane, on the same bar as the steps |
| CTA | action | 54px orange fill — the page's only filled color block, directly under the price |
| Tier table + size grid | decision input | 14–16px, selection = orange border + #fff6f2 tint (`attr-active`), non-mutating (P-06) |
| Subtitle | read | 16px/24 gray under the audience line |
| Key Facts | scan | monochrome hairline card, dark latobold lead-ins + ✓; top of content col; mobile before buy flow (P-14) |
| Section titles | navigate | 18px latosemibold dark h2, barless — same voice as steps, minus the spine |
| Body copy / method description | read | 16px latoregular gray; WTC body 14px/21 |
| Row labels | support values | latoregular #757575 — value (#1f1f1f) always outweighs its label |
| Meta (SKU, wishlist, secure, badges) | ambient | 13px #757575 |
| Decision aid (When To Choose) | on-demand aside | quiet #fafafa panel, deliberately OFF the spine — an aside, not a waypoint |

Weight follows decision value: price > CTA label > step/section titles > values > labels > meta.
Accent = meaning: spine bars + numerals (buy path), CTA (action), selection states, focus.
Positive semantics are latobold dark ink — no green on the page.

## C. The spine rule (exclusivity — keep or C degrades)

**The 3px #fe5000 left bar marks buy-path waypoints ONLY (audience qualifier, step headers,
subtotal). Nothing else on the page may carry it. Off-path accent is limited to: CTA,
active/selection states, focus outlines.** The left content column carries NO spine bars — the
spine is exclusively the buy path. If future elements adopt the bar decoratively, C degrades
back toward the noise the redesign removed (review §5, Variant C trade-off). Current spine
census: 7 sites (audience line, steps 1–4, buy + configurator subtotals).

---

## Key Design Decisions
- One DOM stack, reordered responsively via `display:contents` + `order` (P-21's "render one
  stack and reorder via CSS" option). No duplicate desktop/mobile trees.
- Method-facts grid re-rendered as a literal `table.pdp-spec-table` — same component as
  Specifications, which closes P-11/P-12/P-26/P-33 with zero new CSS.
- Sticky right column = plain `position:sticky; top:16px` (P-16). Buy state fits a 900px
  viewport (859px measured post-C); the configurator state measures ~1203px — it exceeded one
  viewport before C as well (~+40px of that is the C spacing scale), tail reachable at page
  end. Candidate for a follow-up if the client wants the config CTA always in view.
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
- 2026-08-04 Variant C "Accent Spine" applied page-wide with two client amendments — see R3
  below; all 40 dispositions re-verified intact, floors re-swept (0 uppercase, 0 computed 700,
  min 13px, price 24px latobold).

## R2 (2026-07-31, client review)
- R2-1 Kickers lose uppercase: `.pdp-key-facts__title` + `.imprint-method-decision__title` drop `text-transform:uppercase`/`letter-spacing:.08em` — Title Case is now the kicker's own casing (P-36).
- R2-2 Decision box subordinated: `.imprint-method-decision` loses the orange tint/border, reused as a plain `border-top:1px solid #eee` disclosure (the `.pdp-section` quiet-separator idiom); chevron stays orange (P-35). [Superseded by R3 — quiet gray panel.]
- R2-3 Decoration & Imprint header summary restored, recomposed: `.pdp-section__hsummary` "Full-color imprint · first location included" added, matching Production's collapsed-only visibility (P-27/P-40).
- R2-4 Audience-fit line split to its own `.product-subtitle` line below the 2-sentence subtitle paragraph, chip intact (P-37). [Superseded by R3 — moved above the description, carries the spine bar.]
- R2-5 Charges table recomposed action-oriented: "First location → Included" / "Additional location → $30.00 setup + $5.95/item"; the redundant anchor sentence and a third "?"-tooltip repetition removed, leaving one statement of the fact (P-12/P-39).

## R3 (2026-08-04) — Variant C "Accent Spine" applied

Client chose Variant C from `variants.html` (review §5 recommendation). Applied to the
canonical `index.html` with two client amendments; `variants.html` untouched (exploration
archive). Sections A–C above describe the applied state.

- **Amendment A — audience line placement.** The line moves ABOVE the description, directly
  under the H1 (hero order: SKU meta → H1 → barred audience line → subtitle → steps).
  Rationale: directly adjacent to the step spine it reads as a false first step; under the H1
  it reads as the product qualifier. (The C variant board had it below the subtitle.)
- **Amendment B — left-column extension.** The left column adopts the same system: §1e spacing
  steps at its boundaries, hairline separators + quiet gray panel as the only container idioms
  (peach Key Facts tint, filled method-block band, dashed imprint border all retired), the
  consolidated type voices (one 18px h2, gray-label/dark-value tables), monochrome off-path.
  NO spine bars in the left column — see §C.
- Right pane per the C spec: spine system (7 sites), barred 18px step headers with orange
  numerals, 24px latobold price in the spine price zone (gray band retired), quiet-panel
  When-To-Choose with hover/focus, monochrome links/chevrons/badges, 4/8/12/16/24/32 scale
  (inline 20px margins killed), support link relocated below the CTA.
- Contrast resolutions (review §2a): breadcrumb #757575; links underlined-gray AA; disabled
  CTA solid #909090 (3.19:1, was 1.41); dim subtotal #909090 on white (3.19:1 large, was 2.93
  on gray); bright green (1.70:1) retired — positive semantics latobold dark ink; #ff6b00,
  #f05323, #0d6efd, #2e7d32, #e54800 all leave the page. Structural font guards added at html
  level + grouped heading reset; the SVG "?" glyph swapped from font-weight="bold" to latobold.
- Deviations from the vC board, both integration-driven: (1) the configurator Edit button gets
  the 32px hero-gap the buy state inherits from its step header; (2) the modal keeps its
  orange Close (primary action in its own surface) with the standard CTA hover pair.
