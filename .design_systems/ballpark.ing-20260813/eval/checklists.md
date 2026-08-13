# Judge checklists

Per-component rubrics for scoring a consumer's reproduction against this catalog. Score each
axis independently (1–5) — never average axes into one number; a component that nails color
but botches radius is a radius failure, not a "3.5."

## button (primary / secondary / row-action)
- **Shape:** correct radius per variant (13 / 16 / 6px) — not the app scale (4–12px)?
- **Fill/inversion:** primary flips `#0a0a0a`↔`#303030` with its surface, never a fixed color?
- **Type:** Antartica, 16–17px, no bold weight?
- **Motion:** opacity-only hover transition (300ms), no scale/shadow hover added?

## status-badge
- **Shape:** full pill radius, 1px near-white hairline border?
- **Content:** dot + label, dot leading, never trailing?
- **Color:** matches documented status mapping (or flagged as unverified if a new status)?

## filter-tab
- **Shape:** pill, radius 13px (not 9999px — this one is deliberately smaller than status-badge)?
- **State:** hover only lightens background opacity, no color/border change?
- **Honesty:** does the implementation claim a "selected" style not in this catalog? Flag it.

## input-field
- **Fill:** near-transparent surface tint (~3% white), not a solid gray?
- **Border:** 1px `#262626`, not a colored focus border — the outline (not border) carries focus?

## accordion-item
- **A11y:** real `aria-expanded` toggle, not a CSS-only `:checked` hack?
- **Type:** trigger and panel both inherit Antartica, panel text at reduced opacity on paper?

## feature-check-row
- **Icon:** stroke checkmark (not filled), ~70% opacity, 16px?
- **Distinction:** not conflated with the comparison-table's grid-based check cells?

## directory-card
- **Shape:** radius 24px card, radius 10px inner thumbnail — two different radii, don't
  collapse to one?
- **Hover:** subtle bg tint shift only (`#f7f7f7`→`#faf9f9`), no lift/shadow-grow?
- **Conditional content:** tag row and thumbnail both handled as optional, not hard-required?

## auth-form
- **Method:** Google OAuth button only — flag any implementation that adds email/password?
- **Copy:** sign-in/sign-up differ only in heading sub-link and button label?

## Sections (hero, dashboard-preview, comparison-table, pricing-cards, faq, directory-grid, nav-header, footer)
- **Surface commitment:** is the section fully on canvas or fully on paper — never mixed?
- **Rhythm:** ~240px top padding before the section heading preserved?
- **Composition:** every atom the section claims to contain is present and matches its own
  contract (not a re-invented variant)?
- **Decorative content:** product-screenshot / testimonial-quote / lead-table content marked
  and treated as conditional, not reproduced verbatim as if it were real copy?
