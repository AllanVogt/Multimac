# ADR-007: Interest list lives in the browser

- **Status:** Accepted
- **Date:** 2026-10-05

## Context

The store wants a list that customers can send through WhatsApp. It must not behave like a shopping cart.

## Decision

The list is stored in the browser (product slugs only). When opened, it re-fetches current price and availability through `GET /products?slugs=`. The WhatsApp message includes each product link and is capped at about 15 items because of URL length. Wording avoids purchase language ("consult availability", never "checkout"). The header shows a discreet counter instead of a floating cart.

## Consequences

No backend table, no account, no personal data. The list is not shared across devices. The direct 'I am interested in this product' button stays the primary action on the product page.
