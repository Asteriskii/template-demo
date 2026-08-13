---
version: alpha
name: Ballpark
description: Instant-estimate widget for agencies and freelancers — dark-canvas marketing site with a bright "paper" content layer and a Geist-based product UI embedded inside it.
colors:
  primary: "#0a0a0a"
  accent: "#0a0a0a"
  canvas: "#111111"
  surface: "#f1f1f1"
  surfaceDark: "#0f0f0f"
  onSurfaceLight: "#0a0a0a"
  onSurfaceDark: "#fafafa"
  onSurfaceDarkMuted: "#f1f1f1"
  border: "#262626"
  buttonSurfaceDark: "#303030"
  focusRing: "#005fcc"
typography:
  h1:
    fontFamily: "Antartica, sans-serif"
    fontSize: 56px
    fontWeight: 400
    lineHeight: 61.6px
    letterSpacing: -1.12px
  h2:
    fontFamily: "Antartica, sans-serif"
    fontSize: 36px
    fontWeight: 400
    lineHeight: 41.4px
    letterSpacing: -1.296px
  body:
    fontFamily: "Antartica, sans-serif"
    fontSize: 16px
    fontWeight: 400
    lineHeight: 24px
  ui-dense:
    fontFamily: "Geist, \"Geist Fallback\""
    fontSize: 14px
    fontWeight: 400
    lineHeight: 20px
rounded:
  sm: 6px
  filterTab: 13px
  button: 16px
  card: 20px
  directoryCard: 24px
  full: 9999px
spacing:
  gutter: 24px
  sectionPad: 240px
  cardGap: 80px
components:
  button-primary:
    backgroundColor: "{colors.primary}"
    textColor: "{colors.onSurfaceDarkMuted}"
    typography: "{typography.body}"
    rounded: "{rounded.button}"
    padding: "0px 24px"
  button-secondary:
    backgroundColor: "transparent"
    textColor: "{colors.onSurfaceLight}"
    typography: "{typography.body}"
    rounded: "{rounded.button}"
  input-field:
    backgroundColor: "rgba(241,241,241,0.03)"
    textColor: "{colors.onSurfaceDark}"
    typography: "{typography.ui-dense}"
    rounded: "{rounded.sm}"
    padding: "8px 12px"
  filter-tab:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.onSurfaceLight}"
    typography: "{typography.ui-dense}"
    rounded: "{rounded.filterTab}"
    padding: "10px 12px"
  directory-card:
    backgroundColor: "#f7f7f7"
    textColor: "{colors.onSurfaceLight}"
    typography: "{typography.body}"
    rounded: "{rounded.directoryCard}"
  button-row-action:
    backgroundColor: "rgba(241,241,241,0.05)"
    textColor: "{colors.onSurfaceDarkMuted}"
    typography: "{typography.ui-dense}"
    rounded: "{rounded.sm}"
    padding: "8px 16px"
---

## Overview

Ballpark sells one promise — turn a site visitor into a priced estimate without a contact
form — and the marketing site performs that promise visually before it says a word: a
huge, tight-tracked headline over a live product screenshot, an instantly-legible before/after
(inbox → dashboard), and a comparison table that out-argues "Get in Touch" buttons row by
row. The tone is confident, engineering-literate, a little deadpan (footer: "Ballpark is
designed, built, and backed by Over-Stimulated... based at the bottom of the world";
"We hope you enjoyed your time."). It reads as a solo/small-studio SaaS product, not an
enterprise vendor — no logos-as-social-proof grid beyond a thin client strip, testimonials
are short and specific, pricing is one paragraph.

Two design systems share the same Next.js bundle. The pages sampled here (home, pricing,
directory, sign-in/up) all run the **bespoke marketing/"landing" language** documented
below — `--color-landing*` / `--color-content*` tokens, the Antartica display face, arbitrary
one-off Tailwind radii. A second, separate **shadcn/ui-style app token set** (`--color-sidebar`,
`--color-popover`, `--radius-*`, Geist) also ships in the bundle for the logged-in dashboard
product, visible only as the embedded screenshot inside the hero and "So they submitted"
sections — it was not sampled directly and is out of scope for this catalog.

## Colors

The site has no light/dark toggle (`prefers-color-scheme` unused, no theme switch in the
DOM) — instead every **route** (not section) commits wholesale to one of two fixed tones,
via a single wrapper `<div>` around that route's entire content:

- **Canvas** `#111111` — the true `<body>` background on every route, always near-black.
  It's fully covered by whichever tone the route commits to and only becomes visible as a
  soft radial glow bleeding in from the bottom-right corner past the footer — a constant
  decorative accent present on every page, not a sign of "dark mode."
- **Dark-committed routes** (`/pricing`, `/sign-in`, `/sign-up`): the page wrapper paints
  `#0a0a0a`/`#0f0f0f` (`--color-landingDark`), and the footer — a direct child of that same
  wrapper — inherits the dark tone too. Text on this tone: `#fafafa` body / `#f1f1f1` secondary.
- **Light-committed routes** (`/`, `/directory`): the page wrapper paints `#f1f1f1`
  (`--color-landingLight` / `--color-contentLight`), and its footer matches — light, not a
  fixed dark exception. Text on this tone: `#0a0a0a` headings, `oklab(...,0.5)` (~50%-opacity
  near-black) body. Cards floating on this surface (hero product screenshot, testimonial
  cards, directory cards) get a 20px radius, a 1px near-black hairline border at 5–10%
  opacity, and a soft ambient shadow (`0 12px 24px rgba(0,0,0,.2)`) — a floating-panel look,
  not a flat fill.
- **Buttons invert with their route's tone**: on a light-committed route, the primary CTA is
  filled `#0a0a0a` on `#f1f1f1` text; on a dark-committed route (and inside the
  dashboard-preview product-screenshot chrome), the equivalent filled button flips to
  `#303030` fill with near-white `#fefefe` text. Borders throughout are a single `#262626`
  hairline at low opacity, not a scale.
- **Status colors** (observed only in the dashboard-preview product screenshot, not
  independently extracted as CSS — confidence: low, verify before reuse): amber/half-filled
  dot = "To Follow Up" or "Contacted", empty ring = "New", red = "Project Lost", green =
  "Project Won".

## Typography

One display face carries the entire marketing surface: **Antartica** (with a system
sans-serif fallback), used for everything from the 56px hero h1 down to 16px body copy —
there's no separate serif or mono voice on this layer. Weight stays at 400 throughout what
was sampled; hierarchy comes from size and tracking, not boldness.

| Role | Size / Line-height | Letter-spacing | Evidence |
|---|---|---|---|
| h1 (hero) | 56px / 61.6px | -1.12px | measured, home hero |
| h2 (section) | 36px / 41.4px | -1.296px | measured, section headings |
| body | 16px / 24px | normal | measured, hero subhead |

Tighter negative tracking scales with size (h2's -1.296px is proportionally tighter than
h1's -1.12px) — a deliberate "big type pulls in" display convention. The embedded product
screenshots (dashboard, email mockup) run on **Geist** at small sizes (12–14px) — that's the
separate app system bleeding through as pixel content, not a second brand voice; don't pull
Geist into new marketing copy.

## Layout

Every route wraps its whole content stack in a single tone-committed container (see
Colors), inside which sections are full-bleed `<section>` blocks, vertically stacked, each
padded up to 240px top before its heading — a slow, generous rhythm that reads as one idea
per screen rather than a dense scroll. Content itself clamps to a centered column (hero
copy, FAQ, pricing cards) or runs edge-to-edge in a responsive grid (directory card grid,
comparison-table rows). The nav header is a small pill, fixed and centered at the top
(`position: fixed`, `border-radius: full`, `backdrop-blur`), independent of the section
flow — it stays pinned over every section, including in this bundle's section screenshots.
Card grids and multi-column bands use consistent 80px gaps; page gutter is 24px.

## Elevation & Depth

Depth is built from soft ambient shadow + hairline border, never a hard drop shadow or
`z`-scale of shadow tokens. The paper cards (widget-demo screenshot, testimonial cards) carry
`0 12px 24px rgba(0,0,0,.2)` at 20px radius with a near-black 1px border at 5–10% opacity;
smaller inline elements (badges, inputs) carry no shadow at all. The canvas itself has no
elevation — it's the resting plane everything else floats above.

## Shapes

Two radius vocabularies coexist. The **app-token scale** (`--radius-sm/md/lg/xl`, 4–12px,
shadcn-style) exists in the bundle but wasn't observed driving any sampled marketing
element. The **marketing surface uses bespoke arbitrary values** instead: 6px on small
in-card actions (row-action buttons, inputs), 13px on filter tabs, 16px on primary/secondary
CTAs, 20px on floating panel cards (testimonial/product-screenshot cards), 24px on directory
cards (with a smaller 10px radius on their inner thumbnail — two radii on one component, not
one), and full/9999px pill radius on anything status- or filter-chip-like (status badges,
the nav pill). Corners read soft and consistent, but are not tied to the app's own scale —
treat the two as separate systems and don't mix them in new work.

## Components

See `components/COMPONENTS.md` for full per-component contracts (anatomy, variants, states,
screenshots). Summary:

## Component Catalog

Reference implementations live in `components/`. Consult `AGENTS.md` before building.

| Component | Variants | States | Reference | Contract |
|---|---|---|---|---|
| button | primary, secondary, row-action | hover, focus (browser default) | components/button--primary.html (+ --secondary, --row-action) | components/COMPONENTS.md#button |
| status-badge | New, Contacted, To Follow Up, Project Won, Project Lost | — | components/status-badge.html | components/COMPONENTS.md#status-badge |
| filter-tab | active, inactive | hover | components/filter-tab.html | components/COMPONENTS.md#filter-tab |
| input-field | text, textarea | focus | components/input-field.html | components/COMPONENTS.md#input-field |
| accordion-item | collapsed, expanded | — | components/accordion-item.html | components/COMPONENTS.md#accordion-item |
| feature-check-row | included | — | components/feature-check-row.html | components/COMPONENTS.md#feature-check-row |
| directory-card | — | — | components/directory-card.html | components/COMPONENTS.md#directory-card |
| auth-form | sign-in, sign-up | — | components/auth-form.html | components/COMPONENTS.md#auth-form |
| nav-header (section) | — | — | components/nav-header-section.html | components/COMPONENTS.md#nav-header |
| hero (section) | — | — | components/hero-section.html | components/COMPONENTS.md#hero |
| dashboard-preview (section) | — | — | components/dashboard-preview-section.html | components/COMPONENTS.md#dashboard-preview |
| comparison-table (section) | — | — | components/comparison-table-section.html | components/COMPONENTS.md#comparison-table |
| pricing-cards (section) | — | — | components/pricing-cards-section.html | components/COMPONENTS.md#pricing-cards |
| faq (section) | — | — | components/faq-section.html | components/COMPONENTS.md#faq |
| directory-grid (section) | — | — | components/directory-grid-section.html | components/COMPONENTS.md#directory-grid |
| footer (section) | — | — | components/footer-section.html | components/COMPONENTS.md#footer |

## Do's and Don'ts

- **Do** keep the canvas/paper split binary — a section is either fully dark or fully light;
  don't blend a light card onto a light page for "contrast," the system doesn't do tinted
  neutrals.
- **Do** invert button fill with its surface (dark-on-paper, `#303030`-on-canvas) rather than
  using one fixed brand color everywhere.
- **Do** keep tracking tight and negative at display sizes; don't set the hero h1 at default
  letter-spacing.
- **Don't** pull the embedded product screenshot's Geist/app-token styling into new marketing
  components — it's a different system that happens to render inside this one as pixel
  content.
- **Don't** invent a shadow scale; this system only has "none" and the one soft ambient
  panel shadow.
