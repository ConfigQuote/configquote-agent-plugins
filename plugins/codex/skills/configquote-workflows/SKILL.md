---
name: configquote-workflows
description: Use ConfigQuote tenant tools to create product configurations, build quotes, assign quotes to team members, and send quotes to customers through the tenant MCP server.
---

# ConfigQuote Workflows

Use the `configquote` MCP server for tenant data. Do not scrape or automate the Filament UI when an MCP tool exists.

## Defaults

- Search products before creating a configuration unless the product ID is already known.
- Create configurations as `draft` unless the user explicitly asks to publish or activate.
- Create quotes as `draft` unless the user asks for a different status.
- Use `send_quote` only after the user clearly asks to send the quote to the customer.
- Prefer assigning quotes to an existing `admin` or `manager` returned by the team tool.

## Common Flow

1. Use `search_products` to find the configurable product.
2. Use `create_configuration` or `update_configuration` for configurator structure.
3. Use `create_quote` with visual selections or manual line items.
4. Use `assign_quote` when a team member should own follow-up.
5. Use `get_quote_preview_link` for review.
6. Use `send_quote` only as an explicit final action.

## 3D Model Tools

- `list_models` — list stored STEP/GLB/STL/implicit models in tenant storage
- `upload_model` — upload a base64-encoded STEP/GLB/STL/DXF/URDF file; returns `model_url` and `viewer_url`
- `create_implicit_model` — store an `.implicit.mjs` SDF module (browser-native parametric 3D); returns `model_url` and `viewer_url`

Bind a model to a configuration by including a `node-cad-viewer` node (for STEP/GLB) or `node-implicit-viewer` node (for implicit.mjs) in the `nodes` array of `create_configuration` or `update_configuration`, with `data.modelUrl` set to the returned `model_url`.
