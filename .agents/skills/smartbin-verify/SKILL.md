---
name: smartbin-verify
description: Independently verifies SmartBin code, security boundaries, end-to-end flows, and evidence before milestone approval.
---
# SmartBin verification workflow
1. Read the corrected SRS and the implementation handoff.
2. Verify acceptance criteria from the actual repository and running application, not from descriptions alone.
3. Run the exact relevant test commands and preserve actual output.
4. Probe negative and failure cases: unauthorized role access, inactive bin, missing photo, Gemini failure, duplicate submissions, temporary-assignment rejection, and Storage deletion failure.
5. Check that secrets are absent from frontend bundles, Git history, logs, and committed environment files.
6. Verify read-only chatbot behavior using authorized queries; confirm no arbitrary SQL or write path is exposed.
7. Report each finding with severity, reproduction steps, expected result, actual result, and owner.
8. Do not modify implementation files unless the orchestrator explicitly assigns a fix.
9. Approve only criteria supported by reproducible evidence; list unverified items as unverified.
