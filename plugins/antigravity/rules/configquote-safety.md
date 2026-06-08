# ConfigQuote Safety

- Do not send quotes unless the user explicitly asks to send.
- Do not store OAuth tokens in repo files.
- Treat quote totals, VAT, customer email, and recipient assignment as values that must be read back from ConfigQuote after mutation.
- Prefer existing tenant team users for assignments.
