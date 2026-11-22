# SmartBin Antigravity Agent Kit

This kit prepares a Google Antigravity workspace to coordinate SmartBin development from the corrected SRS.

## What's included
- `AGENTS.md`: always-on project instructions and file ownership rules.
- `.agents/rules/smartbin-always-on.md`: Antigravity workspace rule.
- `.agents/skills/smartbin-build/SKILL.md`: implementation procedure.
- `.agents/skills/smartbin-verify/SKILL.md`: independent verification procedure.
- `prompts/00-TEAMWORK-LAUNCH.md`: initial `/teamwork` prompt.
- `prompts/01` to `05`: individual specialist work orders.
- `prompts/06`: independent critic/challenger checklist.
- `docs/SmartBin_Corrected_SRS.md` and `.docx`: authoritative requirements baseline.
- `docs/agent-coordination/`: work board, integration contract template and handoff format.

## Install into your SmartBin repository
1. Extract this ZIP.
2. Copy the kit contents into the root of your SmartBin repository. Merge folders carefully; do not overwrite existing app files. If an `AGENTS.md` already exists, merge the rules instead of replacing it.
3. Confirm `docs/SmartBin_Corrected_SRS.md` is present and readable.
4. Open the repository root as the Antigravity workspace.
5. Ensure the agent sees the workspace instructions. Antigravity discovers root `AGENTS.md` and `.agents/rules/*.md`; skills are discovered under `.agents/skills/`.
6. Open `prompts/00-TEAMWORK-LAUNCH.md`, copy the prompt block, and run it after `/teamwork`.
7. During Phase 1, approve the plan only after the orchestrator presents: requirement matrix, milestones, file ownership, integration contracts and independent acceptance tests.
8. Choose `demo` integrity mode for a reproducible judged prototype. Do not choose a mode that permits fabricated test evidence.
9. After each milestone, inspect the project plan, progress artifact, Critic/Challenger/Auditor findings and actual diffs before accepting integration.

## If `/teamwork` is unavailable
The official docs currently list `/teamwork` for paid plans. If it is not available in your Antigravity account, use `/swarm` (documented for all plans) with the same launch prompt, replacing the first sentence with: "Use /swarm to split this into named workers and a verifier." The individual work orders still apply.

## Important Antigravity guidance
- Prefer the native `/teamwork` command for this multi-milestone project; it handles scoping, orchestration, project plan, parallel workers and verification gates.
- Do not build a legacy custom Workflows folder for this kit. Antigravity's current Workflows documentation says IDE workflows are deprecated and the system is moving to Skills; this kit uses workspace Rules and Skills.
- Teamwork uses a dedicated project directory by default. When prompted for the working directory, choose the existing SmartBin repo if you need the orchestrator to work on existing code; otherwise use the new dedicated directory and copy the repo/SRS there.
- Do not let two agents edit the same shared file concurrently. If your UI or account exposes isolated worktrees, use them.
- Never provide passwords, API keys, Supabase service-role secrets or personal data in prompts. Configure secrets through secure environment settings.

## Deadline strategy
Target a reliable end-to-end vertical slice first. P0/P1/P2 indicate implementation order, not a change to the SRS. If any requirement is unfinished on November 25, report it clearly in the final walkthrough and traceability matrix.
