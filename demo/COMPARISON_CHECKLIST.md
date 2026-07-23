# Compare observable behaviour

## Within each attendee's A/B run

Keep the model, repository, API contract, installed libraries, and prompt fixed. The only variable is whether the completed `api-client-generation` Skill is available.

Mark evidence in the generated code and tests:

- **Authentication:** credential source, bearer header, bounded refresh/replay, concurrent refresh handling, and no secret logging
- **Retries:** correct retryable failures, `Retry-After`, bounded backoff with jitter, and an idempotency gate for unsafe requests
- **Errors:** status checked before success parsing, typed error fields, safe malformed-body fallback, and no retry for `422`
- **Pagination:** async iteration, cursor propagation, explicit termination, and repeated-cursor protection
- **Verification:** focused tests cover the important success and failure paths

Do not score line count, confidence, or how polished the explanation sounds.

## Across attendee versions

Everyone began with the same starter, API contract, and prompt. The main variable is how the three TODO sections were written.

Ask:

1. Which rule produced an observable difference?
2. Which team decision was assumed but never written?
3. Which wording was too vague to apply?
4. Which rules should become the shared canonical version?

Clearer rules make compliant output more likely; they do not make probabilistic outputs identical or remove the need for review and tests.

