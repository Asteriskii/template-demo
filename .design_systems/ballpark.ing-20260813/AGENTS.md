# Consuming this bundle

Extracted from https://www.ballpark.ing/ on 2026-08-13. Read this before building any UI
that should feel native to Ballpark's marketing site.

1. Read `DESIGN.md` fully before writing any UI — the canvas/paper duality and per-surface
   button inversion rule are load-bearing; skimming the color table alone will miss them.
2. Before building any component or section, check the Component Catalog table in
   `DESIGN.md`; if a reference file exists in `components/`, open it and match its anatomy —
   **never invent anatomy that has a reference file**.
3. Use token variables (`tokens/design-tokens.json`, or the YAML front matter in
   `DESIGN.md`), never literal values that have a token.
4. Snippets in `components/*.html` are stack-agnostic references, not clone sources —
   reproduce structure and token bindings in the target stack's idiom.
5. States: implement every hover/focus documented in `components/COMPONENTS.md`. Most
   components have no custom focus style — don't invent a focus ring the source doesn't have.
6. When creating something with no reference file, compose from existing atoms and the
   nearest section skeleton; don't reach for a generic pattern the catalog already covers
   differently (e.g. this system's "card" is always radius-20 + soft shadow, never a flat
   bordered box).

## Known gaps (read before trusting a claim)

- Filter-tab's **active/selected** visual state was not captured (no tab was selected in
  the sampled DOM) — verify on the live site before shipping a toggle state.
- status-badge's non-"New" color values are screenshot-observed, not CSS-extracted —
  treat as directional, confirm exact hex if pixel-fidelity matters.
- The comparison-table's check/✕ rows are a CSS-grid layout, not the same DOM component as
  `feature-check-row` — visually identical language, don't assume a shared component.
- `pricing-cards` and `directory-grid` selectors were hand-located (the automatic section
  classifier missed both pages' content due to a double `<main>` / non-`<section>` DOM
  structure) — re-verify selectors if the site's markup changes.
- Two token systems ship in the same bundle: this catalog documents only the bespoke
  "landing" marketing system. A second shadcn/ui-style app token set exists for the
  logged-in dashboard product and was not sampled.
