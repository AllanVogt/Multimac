# ADR-010: Visual identity (Multimac)

Status: Accepted

## Context

The store name and logo were provided. The project's working name
("Two-Stroke Catalog") is replaced by **Multimac**. The visual direction is
inspired by stihl.com.br: dark surfaces, a strong orange accent, heavy
condensed headings and large, clear product-category entry points.

## Decision

- **Name:** Multimac. Tagline: "Potência e confiança para o campo e jardim".
- **Palette** (sampled from the logo and business card; confirm exact values
  with the original vector files):

  | Token | Value | Use |
  |---|---|---|
  | `--color-accent` | `#F15A22` | Buttons, highlights, icons |
  | `--color-accent-strong` | `#FF4B0F` | Hover, logo ring |
  | `--color-surface` | `#3A3A3C` | Sections, cards |
  | `--color-bg` | `#0B0B0C` | Page background |
  | `--color-text` | `#FFFFFF` | Main text |
  | `--color-text-muted` | `#B8B8BC` | Secondary text |

- **Typography:** heavy sans-serif for headings (uppercase), a neutral
  sans-serif for body text.
- **Icons:** outline icons inside orange circles, matching the business card
  (Loja, Oficina, Motosserra, Roçadeira, Sopradores).
- **Top-level navigation:** Loja, Oficina, Motosserra, Roçadeira, Sopradores.
- **Contact data** (used in header, footer and WhatsApp links):
  - WhatsApp: (41) 98854-3611
  - Phone: (41) 3010-4610
  - Address: Av. Anita Garibaldi, 5711, Loja 5, Barreirinha, Curitiba/PR

- **Layout (Stihl-inspired, hybrid):** light base with an orange promo bar
  on top (WhatsApp call to action), a white header, a dark hero, light cards,
  a dark workshop section and a dark footer.
- **Catalog data entry:** manual, through the admin. Initial product fields:
  name, category, brand, description, optional price, photos, featured flag.
  Specs per category and compatible parts are deferred.

## Consequences

- Design tokens become the single source of truth for Tailwind's theme.
- Orange on dark must keep sufficient contrast; text on orange buttons is
  checked against WCAG AA.
- Stihl is only a stylistic reference. Its logos, images and copy are not used.
