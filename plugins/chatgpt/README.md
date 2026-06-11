# ConfigQuote for ChatGPT

Private-beta assets for connecting ChatGPT to a tenant ConfigQuote workspace.

## Custom GPT Action

Use this for the first employee beta.

1. Create or edit a Custom GPT.
2. Add an Action.
3. Import the tenant OpenAPI schema:

```text
https://<tenant-domain>/api/agent/v1/openapi.json
```

4. Configure OAuth with the tenant endpoints:

```text
Authorization URL: https://<tenant-domain>/oauth/authorize
Token URL: https://<tenant-domain>/oauth/token
OAuth metadata URL: https://<tenant-domain>/.well-known/oauth-authorization-server
Scopes: configurations:read configurations:write quotes:read quotes:write quotes:send team:read
```

5. Paste `instructions.md` into the GPT instructions.

`sendQuote` requires `confirmed: true`. The GPT must ask the user before sending a quote.

## ChatGPT App / Apps SDK

Use the existing remote MCP endpoint for the richer app path:

```text
https://<tenant-domain>/mcp
```

In ChatGPT's custom app/connector screen, put this value in the server URL field. Do not use `/oauth`, `/oauth/authorize`, or the OpenAPI URL as the MCP server URL.

OAuth should be discovered from:

```text
https://<tenant-domain>/.well-known/oauth-protected-resource/mcp
https://<tenant-domain>/.well-known/oauth-authorization-server
```

Dynamic client registration is exposed at:

```text
https://<tenant-domain>/api/agent/v1/oauth/clients
```

The Apps SDK package should reuse the same tenant MCP tools and OAuth scopes.

## Verifying In ChatGPT

The connector can show as connected in ChatGPT settings without being available to every existing conversation. Start a new chat and select the ConfigQuote app/connector when ChatGPT offers app selection.

Use a direct action prompt, for example:

```text
Use ConfigQuote to list my recent quotes.
```

or:

```text
Use ConfigQuote to search configurable products for "desk".
```

Asking "what tools do you have?" can be misleading because the model may only list built-in ChatGPT tools, not every connected MCP app. The MCP server exposes these tool names through `tools/list`:

```text
search_products
list_configurations
create_configuration
update_configuration
archive_configuration
activate_configuration
list_quotes
create_quote
assign_quote
send_quote
get_quote_preview_link
```
