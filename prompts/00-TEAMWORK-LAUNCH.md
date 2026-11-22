# SmartBin: Google Antigravity Teamwork launch prompt

Paste this after `/teamwork` in Antigravity.

```text
/teamwork Build the SmartBin MVP from the authoritative corrected SRS at docs/SmartBin_Corrected_SRS.md (and matching docs/SmartBin_Corrected_SRS.docx). Deliver a reliable, reproducible project demonstration for the November 25, 2026 deadline.

Use the SRS as the source of truth. Do not ask me to restate decisions already documented. During the scoping phase, inspect the repository and SRS, identify only genuinely unresolved blockers, and create a reviewable implementation prompt, project plan, requirement traceability matrix, milestone acceptance criteria, and integration contracts. Do not start parallel coding until file ownership and the shared contracts are defined and approved.

Use the native Teamwork orchestration model. Create these five non-overlapping implementation workstreams, with one worker responsible for each:
1) Backend & Database Engineer
2) Supervisor Dashboard Engineer
3) Worker Application Engineer
4) Gemini AI Integration Engineer
5) QA, Security, Deployment & Documentation Engineer
Use the matching detailed task prompt in prompts/01 through prompts/05 as each worker's brief. Use the Critic, Challenger and Auditor gates at every milestone. Use the final Success Auditor for an end-to-end check.

Integrity mode: DEMO. Use established frameworks and libraries, but do not fake working behavior, test results, AI outputs, security or deployment. Use only documented demo seed data. No external service keys in the browser or Git.

MVP scope: one locality; Supervisor and Sanitation Worker roles; bin registration/map/QR; worker/team management; permanent and temporary assignments; authorized QR/manual lookup; emergency reports; before-photo inspection; Gemini structured image analysis; worker/supervisor review history; after-photo collection and comparison; in-app notifications; overdue tracking; Hindi/English-ready UI; and a read-only role-scoped chatbot. Keep 90-day photo expiry and safe deletion behavior in the design. If a feature cannot be fully completed before the deadline, record it as incomplete—do not silently remove it from the SRS.

Critical priority order for a demo vertical slice:
P0: authenticated supervisor and worker paths; supervisor registers bins; worker sees assigned bins; assignment authorization; QR/manual lookup; before photo upload; server-side Gemini analysis; worker review; after photo upload; collection record; supervisor can inspect saved history.
P1: permanent/temporary assignment transition, emergency report, role-scoped read-only chatbot, map filters and in-app notifications.
P2: automated overdue scheduler, 90-day deletion job with retry, full localization coverage, bulk assignment edge cases and extended analytics. These remain SRS requirements; report honestly if unfinished.

Architecture: React + Vite + TypeScript + Tailwind; Supabase Auth/PostgreSQL/Storage/Edge Functions; Google Gemini API only from Edge Functions; Leaflet + OpenStreetMap; QRCode generation and html5-qrcode scanning; GitHub; Vercel. Do not introduce another backend or database without approval.

Non-negotiable data rules:
- Use the 11 consolidated SRS tables: areas, profiles, teams, team_members, bins, assignments, inspections, collection_logs, emergency_reports, ai_review_history, notifications.
- One assignment row per bin; bulk rows share batch_id. Do not add a competing assignment_bins design.
- assignments.acceptance_status = Pending/Accepted/Rejected; assignments.assignment_state = Current/Suspended/Ended.
- Exactly one assignment target: worker XOR team. A partial unique index enforces one Current assignment per bin.
- A temporary assignment suspends its permanent assignment transactionally. If temporary assignment is rejected, do not silently restore permanent assignment; supervisor chooses a replacement or explicit restoration.
- collection_logs.inspection_id is unique. Normal completion requires uploaded after photo. AI comparison failure does not block completion if photo upload succeeded.
- Emergency reporting is allowed to any authenticated worker for an active registered bin with a photo and description. It does not grant inspection/collection permission.
- Worker history access follows current bin assignments and own records; supervisor access is area-scoped.
- Photos expire 90 days after uploaded_at. Delete from Storage first; clear DB path only after confirmed deletion; retry failures and retain all operational history.
- AI results are estimates. Keep original results and each review/correction in immutable history.
- Chatbot is read-only; do not let Gemini write SQL or invoke arbitrary database actions. Use allowlisted, parameterized, role-scoped backend queries.

Collaboration/file ownership:
- Orchestrator owns shared app entry/routing, package.json/lockfile, build configs, global styles, shared types/contracts, .env.example and integration decisions.
- Backend owns supabase/migrations/**, supabase/seed.sql and backend operational services/RPCs (except Gemini-only functions).
- Supervisor UI owns src/features/supervisor/**.
- Worker UI owns src/features/worker/**.
- AI owns supabase/functions/analyze-bin-image/**, supabase/functions/smartbin-chat/** and src/lib/ai/**.
- QA owns tests/**, docs/qa/**, README and deployment/evidence docs; QA reports source defects rather than editing another worker's files.
- Adapt paths only after repository inspection; do not overwrite current user work. Use isolated worktrees/branches where available. No concurrent edits to shared files.

Every milestone must pass Critic and Challenger review plus Auditor verification using real command output. Do not claim success based on stubs, mocked external APIs or unexecuted tests. Capture screenshots, demo steps, test output, AI-tool contribution log and known limitations.

Start with repository inspection and the scoping prompt artifact. Then propose the five workstreams, their dependencies, file boundaries, API/database contracts, and exact acceptance criteria for my approval. Do not begin unrestricted code changes before approval.
```
