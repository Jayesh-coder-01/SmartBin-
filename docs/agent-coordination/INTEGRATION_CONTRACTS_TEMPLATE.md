# SmartBin integration contracts — template

The Orchestrator must complete and approve this file before parallel coding. Do not implement guessed payloads.

## Environment variable names
- `VITE_SUPABASE_URL` (public project URL only)
- `VITE_SUPABASE_ANON_KEY` (public anon key; RLS must protect data)
- `SUPABASE_URL` (server/Edge Function)
- `SUPABASE_SERVICE_ROLE_KEY` (server-side only; never in Vite/browser)
- `GEMINI_API_KEY` (server-side only)

Do not store actual values in this file or commit secrets.

## Frontend auth contract
- Session/profile lookup:
- Role enum:
- Area/locality resolution:
- Inactive-user behavior:
- Route guard behavior:

## Backend service contracts
- Bin list/detail/create/update/deactivate/reactivate:
- Worker/team management:
- Bulk assignment create/accept/reject:
- Temporary assignment creation/end/rejection/restoration:
- Inspection create + before photo:
- AI analysis invoke/retry:
- Worker/supervisor review append:
- Collection create/complete/exception:
- Emergency report create/review:
- Notification list/read:
- Overdue detection:
- Photo deletion job:

## AI image response schema
Document exact JSON schema and validation behavior here.

## Chatbot allowlisted query contract
List each approved query, required parameters, role scope and response schema. No general SQL execution.

## Error model
Define stable error codes, user-facing messages and retry rules.

## Shared type ownership
The Orchestrator owns canonical shared types and changes after consulting all consumers.
