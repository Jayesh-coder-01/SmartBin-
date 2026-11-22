# SmartBin workspace instructions

You are working in the SmartBin project. The authoritative requirements baseline is `docs/SmartBin_Corrected_SRS.md`; the matching Word copy is `docs/SmartBin_Corrected_SRS.docx`. Read the Markdown SRS before planning or changing code. Do not use the older draft or conversation summaries as a substitute for the corrected SRS.

## Project objective
Build a reliable, demonstrable SmartBin MVP for one designated locality with two roles: Supervisor and Sanitation Worker. The stack defined by the SRS is React + Vite, Tailwind CSS, Supabase Auth/PostgreSQL/Storage/Edge Functions, Google Gemini API, Leaflet + OpenStreetMap, QR generation/scanning, GitHub and Vercel.

## Non-negotiable product rules
1. Preserve the SRS scope. Do not add product features or silently remove requirements.
2. Maintain a requirement-to-implementation-to-test matrix. Any item not implemented must be listed as incomplete, not represented as done.
3. All sensitive authorization is enforced on the backend and through Supabase RLS. UI hiding is not security.
4. Gemini API keys and service-role secrets stay server-side. Never put them in `VITE_*`, browser code, committed files, screenshots, or logs.
5. AI estimates visible conditions. They are not exact sensor measurements and do not prove that waste was collected.
6. Successfully uploaded photos must remain preserved if Gemini fails. Normal collection completion requires a successfully uploaded after-photo; AI comparison failure alone does not block completion.
7. Emergency reports are the explicit permission exception: any authenticated worker may report an active registered bin with photo and description, but this does not authorize normal inspection/collection or assignment changes.
8. One assignment row represents one bin. Bulk assignment rows share `batch_id`; do not introduce a second assignment_bins design alongside `assignments.bin_id`.
9. Assignment concepts stay separate: `acceptance_status` = Pending/Accepted/Rejected; `assignment_state` = Current/Suspended/Ended. Do not collapse them into one status field.
10. A temporary assignment suspends, but does not delete, the permanent assignment it replaces. Rejection of a temporary assignment does not silently restore the permanent one; a supervisor chooses a replacement or explicitly restores it.
11. One worker can have only one active team membership. Team tasks must record the actual worker. Prevent duplicate task completion transactionally or with constraints.
12. Collection records have one unique `inspection_id` and are separate from inspections.
13. Photo deletion at 90 days occurs only after confirmed Storage deletion. Clear the database path only after successful object deletion; preserve reports, review history, identity and timestamps.
14. The chatbot is read-only. Gemini must not generate unrestricted SQL or directly modify records. Use fixed, parameterized, role-scoped backend queries.
15. Do not claim tests, integrations, deployments, permissions, or tool usage succeeded unless you have real evidence from command output or a live check.

## Collaboration rules
- The Project Orchestrator owns milestone planning, shared contracts, file ownership, integration and merges.
- Give each implementation worker a non-overlapping file scope. Never let two workers edit the same file concurrently.
- The orchestrator owns shared files: `package.json`, lockfile, Vite/TypeScript/Tailwind config, root routing/App composition, global styles, shared design tokens, `.env.example`, and the canonical API/type contracts. Workers must request changes to those files rather than edit them.
- Backend worker owns `supabase/migrations/**`, `supabase/seed.sql`, database/RLS documentation, and backend domain operations other than Gemini-specific functions.
- Supervisor UI worker owns `src/features/supervisor/**` and its own feature-local tests.
- Worker UI worker owns `src/features/worker/**` and its own feature-local tests.
- AI worker owns `supabase/functions/analyze-bin-image/**`, `supabase/functions/smartbin-chat/**`, and `src/lib/ai/**`. UI components for the worker/supervisor screens remain with the corresponding UI worker.
- QA/release worker owns `tests/**`, `docs/qa/**`, README and release/evidence documentation. It must not edit product source files; send defects to the orchestrator.
- If the repository already has a structure, inspect it first and adapt these paths without destructive restructuring.
- Do not overwrite existing user work. Inspect `git status` and current files before making changes.
- Use separate branches or Antigravity-isolated worktrees when available. Do not assume parallel agents share the same filesystem unless Antigravity confirms it.
- Never force-push, reset, delete user files, run destructive database operations, or deploy without explicit approval.

## Engineering standards
- TypeScript strict mode; avoid `any` unless justified and isolated.
- Validate all untrusted input at the backend boundary.
- Use typed service modules; keep UI components free of direct privileged logic.
- Use accessible forms, loading states, empty states and actionable error messages.
- Use reusable components, but avoid overengineering.
- Add idempotency/duplicate protection to submissions and assignment transitions.
- Do not place secrets in source code; provide `.env.example` with names only.
- Use realistic demo seed records only in a clearly identified development/demo seed script.
- Keep Hindi/English labels centralized so localization can be finished without rewriting screens.

## Definition of done for every task
1. Changed files and responsibility boundaries are listed.
2. The requirement IDs/sections addressed are listed.
3. Relevant tests/build/lint/type-check commands were run and actual results recorded.
4. Known gaps, assumptions and blockers are disclosed.
5. A handoff note is created using `docs/agent-coordination/HANDOFF_TEMPLATE.md`.
6. The change integrates with agreed contracts and does not break another worker's ownership.
