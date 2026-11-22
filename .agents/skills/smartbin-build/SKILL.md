---
name: smartbin-build
description: Implements SmartBin features from the corrected SRS using agreed contracts, file ownership, and testable handoffs.
---
# SmartBin implementation workflow
1. Read `AGENTS.md` and the relevant sections of `docs/SmartBin_Corrected_SRS.md`.
2. Inspect the current repository and `git status`; do not overwrite existing work.
3. Read `docs/agent-coordination/INTEGRATION_CONTRACTS.md`. If it is not approved yet, do not guess API shapes; send the orchestrator a proposed contract.
4. Confirm your assigned file scope and avoid shared files.
5. Implement the smallest complete vertical slice first; use existing project conventions.
6. Add input validation, loading/error/empty states, and authorization assumptions.
7. Run the relevant test/build/type-check commands. Fix failures caused by your work.
8. Update the requirement matrix and create a handoff from `docs/agent-coordination/HANDOFF_TEMPLATE.md`.
9. Report blockers and incomplete acceptance criteria explicitly.
