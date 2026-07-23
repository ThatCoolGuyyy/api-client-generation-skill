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

- Read access and refresh credentials through the project's configuration or token-provider abstraction. Never hardcode credentials.
- Send the access token as `Authorization: Bearer <token>`.
- On the first `401`, refresh once when refresh credentials exist, then replay the original request once.
- Coalesce concurrent refresh attempts so one expired token does not create a refresh stampede.
- If refresh fails or the replay also returns `401`, throw a typed authentication error immediately.
- Never log access tokens, refresh tokens, API keys, or authorization headers.

## Error handling

- Check the HTTP status before parsing a success body.
- Parse the documented JSON error envelope into a typed client error.
- Preserve `status`, `code`, `message`, `details`, `requestId`, and retry metadata when available.
- When error parsing fails, preserve only a bounded raw-body excerpt and never include secrets.
- Fail validation, authentication, authorization, and other non-retryable `4xx` responses without retrying.

## Pagination

- Expose paginated collections as an iterator or async iterator rather than returning only the first page.
- Send `cursor` only when it is defined.
- Yield the current page's items before requesting the next page.
- Continue only when `next_cursor` is a non-empty string.
- Stop when `next_cursor` is absent, empty, or `null`.
- Detect a repeated cursor and fail rather than looping forever.
- Keep page size configurable within the API's documented limits.

## Finish with evidence

Add focused tests for:

- successful requests
- one controlled refresh and replay
- concurrent refresh coalescing
- `429` with `Retry-After`
- bounded jittered retry for transient failures
- non-retryable `422`
- typed error parsing
- pagination termination and repeated-cursor detection
- absence of secrets in logs and thrown messages

Run the narrowest relevant tests and type checks. Report which standards appear in the generated code, which are missing, and any API-contract gaps that still require confirmation.

