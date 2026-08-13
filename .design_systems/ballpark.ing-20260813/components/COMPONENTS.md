# Component Contracts

Reference source: https://www.ballpark.ing/ · sampled 2026-08-13 · theme: single (no
light/dark toggle) · regime: Tailwind (density 0.85) + Radix primitives.

Atoms first, then section patterns. Every Composition line is verifiable in the referenced
snippet's markup; content-dependent parts (names, prices, quotes) are marked conditional.

## button
**File:** button--primary.html / button--secondary.html / button--row-action.html · **Confidence:** high · **Evidence:** 33 button instances / 3 pages

**Anatomy**
1. root — `<button>`; flex row, centered; radius 16px (primary/secondary) or 6px (row-action)
2. label — single `<span>`, Antartica 16–17px

**Variants × states**
| Variant | Base | Hover | Focus |
|---|---|---|---|
| primary | bg `#0a0a0a`, text `#f1f1f1`, radius 16px | opacity → ~0.83 (authored `hover:opacity-80`; measured diff was smaller, trust the class) | browser-default 1px blue outline |
| secondary | transparent, 1px border `rgba(0,0,0,.2)`, text `#0a0a0a`, radius 16px | opacity → 0.8 (same pattern) | same outline |
| row-action | bg `rgba(241,241,241,.05)`, text `#f1f1f1`, radius 6px, fixed ~78×37px | no visual change | same outline |

**Transition:** opacity 300ms cubic-bezier(0.4,0,0.2,1) (primary/secondary only)
**Usage:** primary = filled marketing CTA ("Add to your site", "Get started"); secondary =
outline CTA paired next to a primary ("See a demo"); row-action = small ghost button inside
dense UI rows (dashboard "Details"). No custom focus style is authored anywhere — all three
fall back to the browser's default outline.
**Screenshots:** ../screenshots/states/button--primary-hover.png, button--secondary-hover.png

## status-badge
**File:** status-badge.html · **Confidence:** medium — colors of non-"New" states are
screenshot-observed, not independently extracted · **Evidence:** 9 instances, dashboard-preview screenshot

**Anatomy**
1. root — `<button>` (non-interactive display use); pill, 1px border `rgba(255,255,255,.1)`, radius full
2. dot/icon — 16×16 SVG, leading
3. label — Antartica 14px

**Variants × states**
| Variant | Base |
|---|---|
| New | empty ring dot, text `#fafafa` |
| Contacted | orange dot (screenshot-observed) |
| To Follow Up | amber half-dot (screenshot-observed) |
| Project Won | green dot (screenshot-observed) |
| Project Lost | red dot (screenshot-observed) |

**Transition:** opacity 150ms
**Usage:** CRM/dashboard lead-status indicator; appears inside the dashboard-preview
section's decorative product screenshot, not on the marketing chrome itself.
**Screenshots:** ../screenshots/states/status-badge-hover.png, ../screenshots/sections/dashboard-preview.png

## filter-tab
**File:** filter-tab.html · **Confidence:** high · **Evidence:** 10 instances / directory page

**Anatomy**
1. root — `<button>`; pill, radius 13px, 1px border `rgba(0,0,0,.05)`
2. icon (optional) — 16×16, leading
3. label — Antartica 14px/520 weight, tracking -0.28px

**Variants × states**
| Variant | Base | Hover |
|---|---|---|
| default | bg `rgba(255,255,255,.3)`, text `rgba(0,0,0,.5)` | bg → `rgba(255,255,255,.7)` |

**Usage:** category filter chips above the directory grid ("All", "Agencies", "Freelancers",
"Workflow"...). Active/selected-state styling was not captured — no selected tab was
present in the sampled DOM state; verify against the live site before relying on it.

## input-field
**File:** input-field.html · **Confidence:** high · **Evidence:** 5 instances / home page

**Anatomy**
1. root — `<input>` or `<textarea>`; radius 6px, 1px border `#262626`

**Variants × states**
| Variant | Base | Focus |
|---|---|---|
| text/textarea | bg `rgba(241,241,241,.03)`, text `#fafafa`, Geist 14px | 0px solid blue outline (near-invisible; site relies on border, not outline, for focus) |

**Usage:** embedded product-mockup form fields (widget builder demo), not the real
marketing-page lead capture (this site has none — its whole pitch is no contact forms).

## accordion-item
**File:** accordion-item.html · **Confidence:** high · **Evidence:** 18 instances / FAQ section

**Anatomy**
1. root — list container, max-width 900px, centered
2. item — bordered row (`border-b`, 10% opacity), collapsed by default
3. trigger — `<h3><button>` flex row, question text + rotating chevron
4. panel — answer text, `#0a0a0a` on paper surface, revealed on expand

**Variants × states**
| Variant | Base | Expanded |
|---|---|---|
| default | collapsed, chevron down | panel visible, chevron rotated (Radix `aria-expanded`) |

**Usage:** FAQ section, one accordion per page. Radix-driven (`aria-expanded` present) —
reproduce with any accessible accordion primitive, not custom JS.

## feature-check-row
**File:** feature-check-row.html · **Confidence:** high · **Evidence:** 9+ instances / pricing cards + comparison table (visually, not componentized there — see comparison-table)

**Anatomy**
1. root — flex row, 8px gap
2. icon — 16×16 checkmark SVG (`stroke-width:1`), 70%-opacity
3. label — Geist, inherits card text color

**Usage:** pricing-card feature list item. The comparison-table section shows the same
visual pattern (check/✕ + label) but as CSS-grid cells, not this componentized row — treat
them as the same design language, not the same DOM component.

## directory-card
**File:** directory-card.html · **Confidence:** high · **Evidence:** ~20 cards / directory grid

**Anatomy**
1. root — `<a>` wrapping a `<div>` panel; bg `#f7f7f7`, radius 24px, padding 80px/56px
2. thumbnail — 4:3 image, radius 10px, 1px border `rgba(0,0,0,.05)` (conditional: falls
   back to a blank/skeleton fill for listings without a screenshot — seen in "UNSCRIPTED" card)
3. name — heading text
4. tagline — muted single-line description
5. tag row (optional) — category pills, provenance: seen on some cards, not this snippet

**Variants × states**
| Variant | Base | Hover |
|---|---|---|
| default | bg `#f7f7f7` | bg → `#faf9f9` (name: `group-hover:bg-[#FAF9F9]`) |

**Usage:** one per listing in the directory grid (`directory-grid-section`).

## auth-form
**File:** auth-form.html · **Confidence:** high · **Evidence:** sign-in + sign-up (identical layout, copy swapped)

**Anatomy**
1. logo mark — 67×67 rounded-12px tile, gradient icon
2. heading — "Welcome to Ballpark"
3. sub-link — "Don't have an account? Sign up" (conditional: text swaps per page)
4. OAuth button — "Sign in/up with Google", full-width, outline, radius ~13px

**Usage:** Google OAuth is the only auth method — no email/password fields exist on this
site. Don't invent a password input for a clone.

---

## hero
**File:** hero-section.html · **Confidence:** high · **Evidence:** home, order 0, confidence 0.9

**Composition:** h1 + body + button--primary + button--secondary, a client-logo strip
(conditional — logo marks are the sampled brand's own client names, replace, don't reuse),
and an embedded product-screenshot graphic (decorative, app-token styling, not reproducible
from this catalog).
**Skeleton:** flex column, centered, 240px top padding, full viewport width.

## nav-header
**File:** nav-header-section.html · **Confidence:** high · **Evidence:** all 5 pages, confidence 0.95

**Composition:** logo mark + 2 nav links (Directory, Pricing) + button--row-action-style
"Sign in" (ghost) + button--primary "Get started".
**Skeleton:** fixed, centered pill, `backdrop-filter: blur`, flex row, space-between, 24px gap.

## dashboard-preview
**File:** dashboard-preview-section.html · **Confidence:** high · **Evidence:** home, order 2 (auto-classifier mislabeled this "pricing-table" — corrected)

**Composition:** h2 + body, two side-by-side panels — a light "client email" card (decorative,
app content) and a dark CRM panel with 3 stat-tile numbers (13 / 57% / 17%, conditional —
sample data) and a lead table using status-badge rows.
**Skeleton:** two-column flex, each panel radius 20px, dark canvas background.

## comparison-table
**File:** comparison-table-section.html · **Confidence:** medium — grid is CSS-grid, not a
componentized row, see feature-check-row note · **Evidence:** home, order 5 (auto-classifier
mislabeled this "logo-wall" — corrected)

**Composition:** h2 + 7 label rows × 2 columns (Ballpark ✓ / Contact form ✕), closing
testimonial quote (conditional — content-specific).
**Skeleton:** CSS grid, alternating row background tint, check/✕ icon per cell.

## pricing-cards
**File:** pricing-cards-section.html · **Confidence:** high (manually located — the section
classifier's DOM walk didn't traverse this page's double `<main>` wrapper) · **Evidence:** /pricing, only route section

**Composition:** h1 + body + 2 cards (Free Trial, Ballpark Pro), each: heading, feature-check-row
list (conditional count — plan-specific), price line, button--primary.
**Skeleton:** centered flex column → 2-up card row, dark canvas (`#0f0f0f`), radius-20 cards.

## faq
**File:** faq-section.html · **Confidence:** high · **Evidence:** home, order 6, confidence 0.85

**Composition:** h2 + accordion-item (list).
**Skeleton:** centered column, max-width 900px.

## directory-grid
**File:** directory-grid-section.html · **Confidence:** high (manually located, same
double-wrapper gap as pricing-cards) · **Evidence:** /directory, ~20 cards

**Composition:** filter-tab row (conditional — not in this snippet's crop, see filter-tab.html)
+ CSS grid of directory-card.
**Skeleton:** `grid-cols-1 md:grid-cols-2 xl:grid-cols-3`, 16px gap, max-width 1920px.

## footer
**File:** footer-section.html · **Confidence:** high · **Evidence:** all 5 pages, confidence 0.95

**Composition:** brand blurb + copyright + 2 nav-link columns + contact email. Matches
whichever tone its route committed to (dark on /pricing, /sign-in; light on /, /directory —
see DESIGN.md Colors) rather than being a fixed dark exception; a decorative radial glow
accent bleeds in from the bottom-right on every route regardless of tone.
**Skeleton:** block layout, 240px top padding, multi-column link groups.
