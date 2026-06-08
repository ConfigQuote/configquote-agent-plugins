# ConfigQuote Agent Plugins

Private-beta plugin bundles for connecting Codex, Claude, and Antigravity to a tenant ConfigQuote MCP server.

## Tenant Setup

1. Sign in to the ConfigQuote tenant app as an `admin` or `manager`.
2. Open Integrations -> Agent Plugins.
3. Copy `CONFIGQUOTE_MCP_URL`.
4. Click Generate token and copy `CONFIGQUOTE_ACCESS_TOKEN`.
5. Configure your agent host with those two values.

Do not commit tenant URLs, generated access tokens, OAuth secrets, or customer data to this repo.

## Codex

In Codex's custom plugin platform dialog:

- Source: `ConfigQuote/configquote-agent-plugins`
- Git reference: `main`
- Sparse checkout: `plugins/codex`

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

This repo also includes Codex marketplace catalog files at:

```text
marketplace.json
.agents/plugins/marketplace.json
```

For catalog-based installation, use the repo root as the platform source. If sparse checkout is required, include both the marketplace file path and `plugins/codex`.

## Public vs Private

Public is fine if this repo contains only plugin manifests, skills, MCP config templates, and generic docs. Keep it private while the beta contract is changing or if you include internal support notes. Never commit tenant tokens or tenant-specific configuration.

## Assets

Each bundle includes the ConfigQuote icon at `assets/icon.svg`. The Codex manifest references it as both the composer icon and plugin logo.
