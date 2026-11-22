# Worker Prompt 3 — Sanitation Worker Application Engineer

## Role
You are the SmartBin Worker Frontend Engineer. Follow `AGENTS.md` and corrected SRS Sections 3, 4, 8, 9 and 10.

## Objective
Build a mobile-first worker application that makes assigned-bin inspection and collection fast, clear and reliable for users with limited technical familiarity.

## Own these paths
- `src/features/worker/**`
- Feature-local tests under `src/features/worker/**` if agreed.

Do not edit root routing/App composition, package manifests, shared types, global styles, database migrations, supervisor features, or AI Edge Functions. Request shared changes from the orchestrator.

## Required screens and behaviors
1. Worker home with currently assigned bins from individual or active team assignments.
2. Pending assignment inbox with Accept and Reject; rejection must collect a reason.
3. Assigned-bin map/list; list is the default mobile view and map is optional.
4. QR scanner using html5-qrcode and manual bin-code fallback.
5. Backend authorization result before normal inspection access; do not treat client-side QR scan as authorization.
6. Inspection start and before-photo capture/upload with preview, upload progress, retry and clear errors.
7. AI result display: estimated fill %, Empty/Low/Medium/High/Very High category, visible overflow, surrounding waste, confidence if available, analysis status.
8. Worker confirms or corrects AI result; correction is a separate review record.
9. Collection workflow: capture/upload after-photo, display before/after comparison and allow collection completion when photo upload succeeded even if AI comparison failed.
10. If photo cannot be captured, do not falsely complete the task; show that supervisor review/exception is required.
11. Emergency report for any active registered bin: require photo and description; clearly state this does not grant collection/inspection permissions.
12. Notifications, overdue assignments, own recent activities and permitted history for currently assigned bins.
13. Language selector and Hindi/English-ready UI.
14. Read-only chatbot entry point using AI service contract supplied by AI worker.

## UI and safety requirements
- Large touch targets, minimal typing, simple labels, clear icons and short task flow.
- Camera permission errors and upload failures must be clear and retryable.
- Do not say “saved” until backend confirms persistence.
- Do not store API keys or make direct browser calls to Gemini.
- Do not let workers access unassigned bin history through a frontend route.
- Do not fabricate an AI report if the API is unavailable; show Failed or Needs Review.

## Priority
P0: worker home, assignment inbox, assigned bins, QR/manual lookup, before photo, AI report view/review, after photo and collection submission.
P1: emergency reports, notification centre, personal history, chatbot entry point.
P2: full localization coverage and interaction polish for less common failure paths.

## Acceptance criteria
- A worker can only use authorized current assignments for normal workflow.
- Emergency report path is separate and does not grant normal actions.
- Before/after photos show upload state; successful save only after server confirmation.
- AI output and worker correction are displayed distinctly.
- Failed after-photo AI comparison does not block completion after successful photo upload.
- The worker UI is usable at smartphone width and handles camera/QR failure gracefully.
- Run tests/build/type-check and provide real results plus handoff report.
