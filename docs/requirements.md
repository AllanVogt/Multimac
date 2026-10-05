# Requirements

## 1. Product principle

A professional digital catalog for a physical store specialized in two-stroke
equipment, connected to the workshop and to WhatsApp. It is **not** a
simplified e-commerce.

Out of scope (never add without explicit approval): marketplace, delivery,
shipping, online payment, checkout, online orders, subscriptions, loyalty
points, complex reviews, built-in chat, microservices, Redis without a real
need, Kubernetes, mandatory customer registration.

## 2. Functional requirements

### Public site

- **Home**: hero, company presentation, catalog call-to-action, categories,
  featured products, workshop and main services, WhatsApp call-to-action,
  in-store purchase notice, location, opening hours, footer.
- **Catalog**: search; filters (category, brand, price range, availability);
  sorting; pagination.
- **Product card**: image, name, brand, model, price, availability, category.
- **Product page**: image gallery, name, brand, model, price, availability,
  description, technical specifications, category, WhatsApp call-to-action with
  a dynamically generated message, notice that purchase is in-store only.
- **Interest list**: add products, review the list, send it through WhatsApp
  (not a cart; no quantities, checkout or order).
- **Workshop**: services page and one page per service; "Bring your equipment"
  section with WhatsApp call-to-action.
- **About us** and **Visit our store** (address, phone, WhatsApp, hours, map,
  route button), all configurable.
- **WhatsApp**: contextual messages (product, workshop, general); number
  defined in a single place; floating button on mobile.

### Admin panel (Sprint 6; architecture ready from the start)

- Products: create, edit, deactivate; price, availability, stock, description,
  brand, model, category, images, specifications.
- Categories, brands and services: create, edit, deactivate.
- Store settings: name, WhatsApp, phone, address, hours, social links, general
  information.
- Secure login (no customer accounts).

## 3. Non-functional requirements

| Area | Requirement |
|---|---|
| Performance | Fast on mobile 4G; WebP responsive images; lazy loading (except the main image); admin code not shipped to public visitors; pagination; HTTP caching only where useful. |
| SEO | Per-page title, description, Open Graph and canonical in the initial HTML; sitemap; robots.txt; JSON-LD; clean URLs; semantic headings; image alt text; no keyword stuffing. |
| Accessibility | WCAG 2.1 AA: contrast, keyboard navigation, focus states, labels, alt text, understandable errors, reduced motion. |
| Security | argon2id password hashing; protected admin endpoints; input validation; upload validation; restrictive CORS; security headers; secrets only in environment variables; no registration endpoint. |
| Responsiveness | Mobile-first; touch targets of at least 44px; filters usable on phones. |
| Maintainability | Small commits, ADRs, tests for critical flows, simple CI. |
| Privacy | No accounts or personal data; interest list stays in the browser. |

## 4. Content rules

- Do not invent addresses, phone numbers, company history, certifications,
  services or product specifications. Use clearly marked placeholders.
- Mock products are flagged `is_demo` and removed before go-live.
- Real brands and models used in demo data have specifications treated as
  unconfirmed until validated by the store.
- No random internet images presented as official product photos.

## 5. Assumptions (to be confirmed with the store owner)

| # | Topic | Working assumption |
|---|---|---|
| 1 | Stock | Availability is set manually; stock quantity is internal and never public. |
| 2 | Price freshness | Show a notice that price and availability are subject to confirmation in store. |
| 3 | Catalog size | Unknown. Decides whether spreadsheet import is worth building. |
| 4 | Compatible parts | Stored as a text specification in the MVP; structured relation later. |
| 5 | Service pricing | Services are quote-based; no price field is shown. |
| 6 | Hosting and domain | Neither exists yet; decision deferred to Sprint 8 (ADR-009). |
| 7 | Admin users | A single administrator is enough; no roles. |
| 8 | Original brief | The text received ended in the middle of item I (visual identity). Anything after it is unknown. |
