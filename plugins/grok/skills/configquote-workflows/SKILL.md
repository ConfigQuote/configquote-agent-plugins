---
name: configquote-workflows
description: Use ConfigQuote MCP tools to manage tenant product configurations and quote workflows.
---

# ConfigQuote Workflows

Use the `configquote` MCP server for all tenant reads and writes.

- Create configurations as drafts by default.
- Create quotes as drafts by default.
- Use `update_quote` to edit customer details, notes, addresses, or line items on an existing quote (pass `items_mode: append` to add products without removing existing items).
- Only call `send_quote` when the user explicitly asks to send the quote.
- Use `assign_quote` only with a real tenant admin or manager.
- Use `get_quote_preview_link` before sending when the user wants review.

## 3D Model Tools

- `list_models` — list stored models in tenant model storage
- `upload_model` — upload base64-encoded STEP/GLB/STL/DXF/URDF; returns `model_url` and `viewer_url`
- `create_implicit_model` — store a `.implicit.mjs` SDF module for browser-native parametric 3D rendering; returns `model_url` and `viewer_url`

To generate a parametric model: write `.implicit.mjs` code (SDF + bounds + parameters), call `create_implicit_model`, then use the `model_url` in a `node-implicit-viewer` configurator node via `update_configuration`. See the `generate-3d-model` skill for the full workflow.
