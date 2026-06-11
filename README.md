# ConfigQuote Agent Plugins

Private-beta plugin bundles for connecting employee chat assistants to a tenant ConfigQuote MCP/API server.

## Tenant Setup

1. Sign in to the ConfigQuote tenant app as an `admin` or `manager`.
2. Open Integrations -> Employee Chat Integrations.
3. Copy `CONFIGQUOTE_MCP_URL`.
4. Click Generate token and copy `CONFIGQUOTE_ACCESS_TOKEN`.
5. Configure your agent host with those two values, or use the tenant OpenAPI schema for REST-action hosts.

Do not commit tenant URLs, generated access tokens, OAuth secrets, or customer data to this repo.

## ChatGPT

Use the ChatGPT bundle at:

```text
plugins/chatgpt
```

For a Custom GPT Action, import:

```text
https://<tenant-domain>/api/agent/v1/openapi.json
```

For a ChatGPT App/custom MCP connector, use the MCP server URL:

```text
https://<tenant-domain>/mcp
```

ChatGPT should discover OAuth from the tenant well-known endpoints. Do not enter `/oauth` or `/oauth/authorize` as the MCP server URL.

After connecting, start a new ChatGPT conversation and select the ConfigQuote app/connector. Ask a direct action prompt such as "Use ConfigQuote to list my recent quotes." Generic "what tools are available?" prompts may not show connected MCP app tools.

## Microsoft Copilot

Use the Copilot bundle at:

```text
plugins/copilot
```

Prefer MCP in Copilot Studio. Use the OpenAPI schema as a REST API fallback.

## Gemini-Compatible Workflows

Use the Gemini bundle at:

```text
plugins/gemini
```

This includes function declarations and Gem instructions rather than a consumer Gemini plugin.

## Codex

In Codex's custom plugin platform dialog:

- Source: `ConfigQuote/configquote-agent-plugins`
- Git reference: `main`
- Sparse checkout: leave blank

If you do use sparse checkout, include both `.agents/plugins` and `plugins/codex` on separate lines.

The Codex bundle reads:

- `CONFIGQUOTE_MCP_URL`
- `CONFIGQUOTE_ACCESS_TOKEN`

## Claude

Use the Claude bundle at:

```text
plugins/claude
```

It uses the same tenant MCP URL and access token.

## Antigravity

Use the Antigravity bundle at:

```text
plugins/antigravity
```

It uses the same tenant MCP URL and access token.

## Marketplace Catalog

This repo includes the Codex marketplace catalog at:

```text
.agents/plugins/marketplace.json
```

For catalog-based installation, use the repo root as the platform source. Leave sparse checkout blank unless you specifically need a partial checkout.

## Public vs Private

Public is fine if this repo contains only plugin manifests, skills, MCP config templates, and generic docs. Keep it private while the beta contract is changing or if you include internal support notes. Never commit tenant tokens or tenant-specific configuration.

## Assets

The installable Codex, Claude, and Antigravity bundles include the ConfigQuote icon at `assets/icon.svg`. The Codex manifest references it as both the composer icon and plugin logo.

## Safety

All hosts must ask for explicit confirmation before sending a quote. REST tools pass `confirmed: true`; MCP tools pass `confirmed: true` to `send_quote`.
