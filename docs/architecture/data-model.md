# Data model

```
Category 1---N Product N---1 Brand (optional)
                 |
                 +--1---N ProductImage
                 +--1---N ProductSpecification
Service        (independent)
AdminUser      (independent)
StoreSettings  (single row)
```

| Table | Main fields |
|---|---|
| `category` | name, slug, description, sort_order, is_active |
| `brand` | name, slug, is_active |
| `product` | category_id, brand_id (nullable), name, slug, model, description, price (nullable = on request), availability, stock_quantity (nullable, internal), is_featured, is_active, **is_demo**, timestamps |
| `product_image` | product_id, file_key, alt_text, position, width, height |
| `product_specification` | product_id, label, value, position |
| `service` | name, slug, summary, description, sort_order, is_active |
| `admin_user` | email, password_hash, name, is_active, last_login_at |
| `store_settings` | store_name, whatsapp_number, phone, address fields, opening_hours (JSON), social links, about text |

`availability` is an enum: `in_stock` ("Disponível na loja"),
`on_request` ("Consultar disponibilidade"), `unavailable`.

## Decisions

- One category per product (1:N), unlike Absurd Market's many-to-many: simpler
  URLs, breadcrumbs, canonical and admin. Edge cases go to "Outros equipamentos".
- `Brand` is an entity (Absurd Market stored it as text) because filters and
  the admin depend on it.
- Specifications are free label/value pairs: each category has different specs
  and a definitions table would be overkill. Trade-off: no filtering by spec.
- Interest list has no table (browser only).
- Search uses `LIKE` with an accent-insensitive `utf8mb4` collation; FULLTEXT
  only if the catalog outgrows it.
- Deliberately absent: customer, cart, order, address, role, tag, pivot tables.
