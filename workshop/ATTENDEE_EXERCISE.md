# Complete the shared API-client Skill

Install the same starter Skill:

```bash
npx skills add ThatCoolGuyyy/api-client-generation-skill --skill api-client-generation
```

Choose the coding agent you will use in the workshop. The CLI prints the installed location of `api-client-generation/SKILL.md`; open that file before the exercise.

The retry section is the worked example completed with the instructor. Complete the three remaining TODO sections for the same Notes API.

## Twelve-minute build

1. **Authentication:** define the credential source, refresh limit, replay behaviour, second-`401` outcome, and secret-handling rule.
2. **Error handling:** define when bodies are parsed, which fields a typed error preserves, and what fails without retry.
3. **Pagination:** define the iteration interface, cursor propagation, termination condition, and repeated-cursor protection.
4. Run the exact prompt in `demo/PROMPT.txt` once without the Skill and once with your completed Skill available.
5. Keep both outputs open. Use `demo/COMPARISON_CHECKLIST.md` to mark evidence in the generated code and tests.

Write rules that can be verified. Replace words such as “properly,” “safely,” or “handle errors” with a limit, condition, field, or expected behaviour.

## Room comparison

Compare two completions of the same starter:

- Which generated output follows the team's standards?
- Which team decision was missing?
- Which rule was too vague for the agent to apply?
- What should be merged into the canonical Skill?

The completed instructor reference is revealed after the comparison in `workshop/REFERENCE_SKILL.md`.

