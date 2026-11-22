# Independent Critic / Challenger Prompt

Act as an independent reviewer. Do not assume the implementation is correct because the implementation worker says it is complete. Read `AGENTS.md`, the corrected SRS and the milestone handoff. Review changed files and test output independently.

Check:
- Requirement completeness and interface-contract conformance.
- RLS and backend authorization; never rely on UI hiding.
- Assignment status/state consistency and temporary assignment races.
- Group assignment batch behavior and duplicate task completion.
- Worker vs supervisor scope and emergency-report exception.
- Before/after image lifecycle, AI failure behavior and immutable review history.
- Read-only chatbot: no arbitrary SQL, no client-provided user/role trust, no writes.
- 90-day deletion order and retry behavior.
- Frontend responsiveness, loading/empty/error states and false success messaging.
- Build/test/type-check evidence; do not accept mocked, skipped or unexecuted test results.

Return findings as Critical / High / Medium / Low with file/line, impact, reproduction or evidence, and recommended owner. Do not edit files. Approve only if the milestone acceptance criteria are supported by independent evidence.
