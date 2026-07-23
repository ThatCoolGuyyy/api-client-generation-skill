---
name: api-client-generation
description: Generate or review HTTP API clients that must follow the team's authentication, retry, error-handling, and cursor-pagination standards. Use when implementing an API client from an OpenAPI document, endpoint documentation, HTTP examples, or an existing integration.
---

# Generate an API client

Inspect the API contract and existing project patterns before writing code. Use the project's installed HTTP library and public API style. Do not invent endpoints, fields, credentials, or dependencies.

## Retries

- Retry `429`, `502`, `503`, `504`, connection resets, and transient network timeouts.
- Do not retry other `4xx` responses.
- Retry safe or idempotent requests by default. Retry an unsafe request only when the caller supplies an idempotency key.
- Honour `Retry-After` when present. Otherwise use exponential backoff with full jitter.
- Allow at most five total attempts, including the original request.
- Respect cancellation and a finite request timeout.

Examples:

- A `429` with `Retry-After: 2` waits for the server-directed delay before retrying.
- A `POST` without an idempotency key fails without an automatic retry.

## Authentication

<!-- TODO: Replace this comment with explicit rules for:
- where credentials come from
- how many times a 401 may trigger refresh and replay
- what happens after the replay also returns 401
- what must never be logged
-->

## Error handling

<!-- TODO: Replace this comment with explicit rules for:
- when the response body may be parsed
- the fields exposed by a typed client error
- how malformed or non-JSON error bodies are preserved safely
- which errors must fail without retry
-->

## Pagination

<!-- TODO: Replace this comment with explicit rules for:
- the public iteration interface
- when cursor parameters are sent
- what counts as a valid next cursor
- how iteration terminates and avoids repeated-cursor loops
-->

## Finish with evidence

Add focused tests for the rules above. Run the narrowest relevant tests and type checks. Report which standards appear in the generated code, which are missing, and any API-contract gaps that still require confirmation.

