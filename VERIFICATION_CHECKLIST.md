# Personal verification

Verify conformance, not general code quality: **does the generated client follow
the exact rules written in your `SKILL.md`?**

For every item, mark `PASS`, `PARTIAL`, or `MISSING` and record the line or test
that proves your answer. Do not award a pass because the code merely looks
reasonable.

## Authentication

- Credentials come from the source named in your rule; none are hardcoded.
- The request sends the required authorization scheme.
- A `401` triggers exactly the refresh-and-replay behaviour you specified.
- A failed refresh or failed replay produces the result your rule specifies.
- Secrets are absent from logs and thrown messages.

## Retries

- Only the statuses and transport failures listed in the Skill are retried.
- Other `4xx` responses, including `422`, fail without retry.
- `Retry-After` is honoured when present.
- The fallback uses exponential backoff with full jitter.
- The maximum is five total attempts, including the original request.
- Cancellation and a finite request timeout are supported.

## Error handling

- HTTP status is checked before a success body is parsed.
- Documented API errors become the typed error described in the Skill.
- The typed error exposes the fields named in the Skill.
- Malformed or non-JSON bodies use the safe fallback described in the Skill.
- Non-retryable errors fail immediately.

## Pagination

- The public interface can consume every page, not only the first one.
- `cursor` is sent only when it is defined.
- Iteration stops for every terminal cursor value named in the Skill.
- A repeated cursor cannot create an infinite loop.
- Page size remains configurable within the documented limits.

## Improve one rule

Choose one `PARTIAL` or `MISSING` result.

1. If the Skill was vague or incomplete, rewrite the rule so it is observable
   and testable.
2. If the rule was already explicit, keep it and note that the generated code
   failed to conform.
3. Ask the agent to regenerate the affected part.
4. Verify the same item again and record the new evidence.
