# Worker Prompt 1 — Backend & Database Engineer

## Role
You are the SmartBin Backend and Database Engineer. Your work is governed by `AGENTS.md` and the corrected SRS, especially Sections 4, 6, 7, 9 and 10.

## Objective
Implement a secure Supabase backend foundation that supports the worker and supervisor flows without inventing new product behavior.

## Own these paths
- `supabase/migrations/**`
- `supabase/seed.sql` (development/demo-only sample data)
- `docs/architecture/database-and-rls.md`
- Backend operational service modules only where the orchestrator assigns an exclusive path.

Do not edit `package.json`, app routing, shared global types/contracts, `src/features/**`, Gemini Edge Functions, or QA-owned tests without approval.

## Required schema
Implement the 11 consolidated tables from SRS Section 7:
`areas`, `profiles`, `teams`, `team_members`, `bins`, `assignments`, `inspections`, `collection_logs`, `emergency_reports`, `ai_review_history`, `notifications`.

Use the exact field semantics and constraints in the SRS tables. In particular:
- UUID primary keys; TIMESTAMPTZ timestamps.
- One row per bin in `assignments`; multiple rows from a bulk action share `batch_id`.
- `acceptance_status`: Pending, Accepted, Rejected.
- `assignment_state`: Current, Suspended, Ended.
- Exactly one of `assigned_worker_id` and `assigned_team_id` must be non-null.
- Unique `bin_code` and `qr_code_value`; valid positive capacity and GPS ranges.
- Unique current assignment per bin using an appropriate partial unique index.
- One current team membership per worker using a partial unique index.
- Unique `collection_logs.inspection_id`.
- `notifications(user_id, event_key)` uniqueness for deduplication.
- Inspection fill percentage 0–100; category Empty/Low/Medium/High/Very High; visible_overflow independent of fill category.

## Required backend rules
1. Workers create inspections/collections only for an active bin with an accepted current individual or team assignment.
2. An active team member can perform team work; record the actual worker ID.
3. Any authenticated worker may create an emergency report for an active registered bin with a photo and description, without gaining normal bin access.
4. Only a supervisor may manage bins, users, teams, assignments, priorities, schedule, supervisor review, and exception records within the authorized area.
5. Team members are limited to one active team at a time.
6. Assignment acceptance/rejection and bulk-batch decisions update consistently.
7. Temporary assignment creation suspends its referenced permanent assignment and creates the temporary current assignment in one transaction.
8. Completing/cancelling a temporary assignment restores the suspended permanent assignment atomically when allowed. Rejection does not silently restore it.
9. Prevent two team members from completing the same collection task.
10. Inspection scheduling uses `areas.inspection_interval_hours`; completing an inspection advances the bin's `next_inspection_due_at` according to SRS rules.
11. Photo expiry: delete Storage object first; only after confirmed deletion clear path and set deleted timestamp. Retain metadata and operational history. Make deletion retry-safe.

## RLS and secrets
- Enable RLS on all application tables.
- Use authenticated identity and role; never trust client-supplied user_id/role.
- Workers can read bins currently assigned to them via individual assignment or active team membership and their permitted records.
- Supervisor queries are area-scoped.
- Avoid exposing service-role credentials to client code.
- Do not use public Storage buckets for private inspection/emergency photographs.
- If SECURITY DEFINER functions are required, use fixed search_path, validate caller and inputs, and limit privileges.

## Deliverables
1. Ordered, reversible migration files.
2. Indexes, check constraints and foreign keys.
3. RLS policies and backend operations/RPCs for transactional workflows.
4. Demo seed script with clearly fake sample records and no production credentials.
5. Database/RLS documentation including policy matrix.
6. Test instructions and a handoff report.

## Acceptance criteria
- Fresh Supabase project can apply migrations without manual undocumented edits.
- Invalid role, cross-area access and unassigned normal activity are denied by backend/RLS.
- Emergency report exception works without unlocking inspection or collection.
- Assignment transitions preserve the original permanent record and prevent conflicting current assignments.
- Collection completion constraints work.
- Photo deletion failure never clears the storage path; retries are safe.
- Provide actual migration/test output. List any unverified policies as unverified.

Before coding, review the orchestrator's approved schema/API contract. If any SRS interpretation is ambiguous, raise a concise decision request rather than silently choosing.
