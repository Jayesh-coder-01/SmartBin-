# Worker Prompt 4 — Gemini AI Integration Engineer

## Role
You are the SmartBin AI Integration Engineer. Follow `AGENTS.md` and corrected SRS Sections 4, 6, 7, 8, 9 and 10.

## Objective
Implement secure, server-side Gemini integration for bin-photo analysis and a read-only SmartBin chatbot grounded in authorized database records.

## Own these paths
- `supabase/functions/analyze-bin-image/**`
- `supabase/functions/smartbin-chat/**`
- `src/lib/ai/**`
- AI-specific tests only where the orchestrator approves ownership.

Do not edit UI feature folders, database migrations, root app config, shared types/contracts, or README. Coordinate your request/response schemas with the orchestrator and backend worker before coding.

## Image-analysis requirements
1. Gemini calls happen only inside Supabase Edge Functions. API key comes from server-side environment configuration.
2. Validate authentication, role, image ownership/path and permitted operation before processing.
3. Analyse visible bin conditions; do not claim exact measurement or proof of waste collection.
4. Return a validated structured result compatible with SRS: estimated fill percentage (0–100), category (Empty/Low/Medium/High/Very High), visible_overflow, surrounding_waste, confidence_score if available, analysis_status and concise notes.
5. Treat overflow independently from fill category; a full bin is not automatically visibly overflowing.
6. Distinguish Pending, Completed, Needs Review and Failed where required by the schema.
7. Handle blurry, dark, obstructed or unrelated images as Needs Review and recommend retake/supervisor review.
8. Preserve uploaded images and records when Gemini fails or times out; mark analysis Failed and allow retry.
9. Preserve immutable original AI output. Worker/supervisor corrections append to `ai_review_history`; never overwrite original result.
10. After-photo AI failure must not block collection completion when after-photo upload succeeded.

## Chatbot requirements
1. Chatbot is read-only for the MVP.
2. Do not execute model-generated SQL. Do not give Gemini a general-purpose database tool.
3. Implement a finite set of allowlisted, parameterized backend query functions for questions supported by the SRS: worker assigned bins, pending assignments, own overdue inspections, own recent activities; supervisor locality bin counts, overdue/overflowing bins, assignments and recent history.
4. Derive user ID, role and area from verified authentication, never from prompt text or client-supplied role fields.
5. Retrieve authorized database results first; send only necessary sanitized result data to Gemini to formulate a response.
6. State when data is unavailable; never invent counts, assignments, or histories.
7. Reject requests to create/update/delete records or bypass authorization.
8. Support Hindi and English responses where feasible; errors must degrade gracefully.

## Security and reliability
- Never expose Gemini key, Supabase service-role key or private data to frontend.
- Validate and constrain image size/type; handle network, rate-limit, malformed JSON and API error cases.
- Do not log image payloads, secrets or unnecessary personal data.
- Use idempotent update/storage patterns; don't report success before DB confirmation.

## Acceptance criteria
- At least one real test image produces schema-valid analysis through the Edge Function.
- Invalid/unauthorized requests are rejected.
- Gemini failure preserves uploaded photo and marks analysis Failed.
- Needs Review behavior works for unsuitable images.
- Chatbot uses fixed authorized queries and has no write capability.
- Worker and supervisor receive different scopes.
- Provide actual invocation/test output, required server environment variable names (not values), and handoff report.
