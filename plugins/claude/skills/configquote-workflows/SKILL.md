---
name: configquote-workflows
description: Use ConfigQuote MCP tools to manage tenant product configurations and quote workflows.
---

# ConfigQuote Workflows

Use the `configquote` MCP server for all tenant reads and writes.

- Create configurations as drafts by default.
- Create quotes as drafts by default.
- Only call `send_quote` when the user explicitly asks to send the quote.
- Use `assign_quote` only with a real tenant admin or manager.
- Use `get_quote_preview_link` before sending when the user wants review.
