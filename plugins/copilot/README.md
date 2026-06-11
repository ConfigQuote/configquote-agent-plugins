# ConfigQuote for Microsoft Copilot

Private-beta assets for Microsoft Copilot Studio.

## Preferred Path: MCP Tool

Create a Copilot Studio agent and add a Model Context Protocol tool that points at:

```text
https://<tenant-domain>/mcp
```

Use end-user authentication where available so ConfigQuote roles and scopes apply per employee.

## REST API Fallback

If MCP is unavailable in the target tenant's Microsoft environment, add a REST API tool from:

```text
https://<tenant-domain>/api/agent/v1/openapi.json
```

Use OAuth authorization code authentication and the same scopes as the OpenAPI schema.

`sendQuote` requires `confirmed: true`. Configure the agent to ask the user before sending.
