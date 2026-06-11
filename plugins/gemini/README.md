# ConfigQuote for Gemini-Compatible Workflows

Gemini consumer chat does not use the same installable plugin model as Codex or ChatGPT Apps. This package provides Gemini-compatible assets for private beta workflows.

## Gemini API Function Calling

Use `function_declarations.json` with a Gemini API app or internal assistant. The app should execute calls against the tenant API:

```text
https://<tenant-domain>/api/agent/v1
```

Authenticate each employee with ConfigQuote OAuth where possible.

## Gemini Gem Instructions

Use `gem-instructions.md` for a planning/read-assist Gem. For write actions, route through a Gemini API assistant that can call ConfigQuote APIs.

Sending a quote requires explicit confirmation and `confirmed: true`.
