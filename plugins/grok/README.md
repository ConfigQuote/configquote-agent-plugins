# ConfigQuote for Grok

Grok Build plugin (xAI plugin marketplace format) that connects Grok to a tenant's ConfigQuote MCP server for product configuration and quote workflows.

## Contents

- `.grok-plugin/plugin.json`: manifest
- `.mcp.json`: remote HTTP MCP server
- `skills/`: workflows, create-quote, edit-quote, generate-3d-model

## Network endpoints and credentials

- `CONFIGQUOTE_MCP_URL`: the tenant's own MCP endpoint, `https://<tenant-domain>/mcp`
- `CONFIGQUOTE_ACCESS_TOKEN`: bearer token generated in the tenant app under Integrations -> Employee Chat Integrations

The plugin contacts only that endpoint. It runs no code, has no hooks and sends no telemetry. Never commit tokens.

## Publishing to xai-org/plugin-marketplace

1. Publish this folder at the root of a public repo under the official org (e.g. `ConfigQuote/configquote-agent-plugins`); the marketplace rejects personal-account sources for branded plugins.
2. Copy `marketplace-entry.example.json` into `.grok-plugin/marketplace.json` in a fork and set `sha` to the full 40-char commit (`git ls-remote <repo> HEAD`).
3. Run `python3 scripts/generate-plugin-index.py` and `python3 scripts/validate-catalog.py`, then open a PR.


## License

MIT, see `LICENSE` in the repository root.
