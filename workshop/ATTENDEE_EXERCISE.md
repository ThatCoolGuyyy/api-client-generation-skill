# Complete and verify the starter Skill

The Skill is already in this repository. Do not install it globally and do not
copy it into the baseline repository.

## 1. Complete the Skill

Open `skills/api-client-generation/SKILL.md`.

Retries are complete as the worked example. Replace the TODO comments under:

- Authentication
- Error handling
- Pagination

Write observable rules. Prefer “replay once, then throw a typed authentication
error” over “handle authentication properly.”

## 2. Generate the client

In your coding agent, say:

> Read and follow `skills/api-client-generation/SKILL.md`. Then complete the
> task in `PROMPT.txt` using `openapi.yaml`.

Keep the generated client and tests in this attendee workspace.

## 3. Verify your own output

Open `VERIFICATION_CHECKLIST.md`. For each rule, find evidence in the generated
code or tests and mark it `PASS`, `PARTIAL`, or `MISSING`.

The question is not “is this generally good code?” It is “does this output
conform to the exact standard I wrote?”

## 4. Improve one rule

Choose one partial or missing behaviour. If your rule was vague, make it
specific and testable, regenerate that part, and verify it again. If the rule
was already explicit, record the failure as agent non-conformance rather than
silently changing the standard.
