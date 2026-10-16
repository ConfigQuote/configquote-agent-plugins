---
name: edit-quote
description: Edit an existing ConfigQuote quote — update customer details, notes, addresses, or line items. Also covers adding products to a quote or managing tenant quotations.
---

# Edit Quote

Use `update_quote` to modify an existing quote. Always call `list_quotes` or `get_quote` first to confirm the quote exists and show the user its current state.

## What can be edited

- **Customer details** — name, email, phone, company
- **Notes** — customer-facing `notes`, internal `internal_notes`
- **Addresses** — `billing_address`, `shipping_address`
- **Line items** — add products, change quantities/prices, or replace the full item list
- **Currency** — `currency` (ISO 4217)
- **Expiry** — `valid_until` date

## Adding products to a quote

To add one or more products to an existing quote without losing current items, use `items_mode: append`:

```json
{
  "quote_id": 42,
  "items_mode": "append",
  "items": [
    { "name": "Steel Bracket", "sku": "SKU-001", "quantity": 2, "unit_price": 49.99 }
  ]
}
```

To replace all items (e.g. rebuild from a new selection), omit `items_mode` or set it to `replace`.

## Editing customer details only

```json
{
  "quote_id": 42,
  "customer": {
    "name": "Jane Smith",
    "email": "jane@acme.com",
    "phone": "+1 555 0100"
  }
}
```

Only the fields you include are changed; everything else stays as-is.

## Rules

- Always confirm the quote number with the user before making changes.
- Do not change `status` via `update_quote` — use `update_quote_status` for status transitions.
- Do not send the quote unless the user explicitly asks; use `send_quote` with `confirmed: true` for that.
- After updating, return the updated quote number, total, and a summary of what changed.
