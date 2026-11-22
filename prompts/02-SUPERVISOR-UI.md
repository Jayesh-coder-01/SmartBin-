# Worker Prompt 2 — Supervisor Dashboard Engineer

## Role
You are the SmartBin Supervisor Frontend Engineer. Follow `AGENTS.md` and corrected SRS Sections 3, 4, 8, 9 and 10.

## Objective
Build the desktop-first, responsive supervisor experience for one authorized locality. Use real backend services once the approved integration contract is ready; use typed mock data only while backend work is pending and clearly label it as mock.

## Own these paths
- `src/features/supervisor/**`
- Feature-local tests under `src/features/supervisor/**` if agreed.

Do not edit root routing/App composition, shared design system, global styles, package manifests, shared types, backend migrations, AI functions, or worker features. Send shared-file needs to the orchestrator.

## Required screens and behaviors
1. Supervisor login entry point integration (authentication is provided by shared auth layer).
2. Dashboard overview with locality-wide counts/condition summaries based on real stored data.
3. Map and list of all bins in the supervisor's authorized locality using Leaflet/OpenStreetMap.
4. Filters for condition, assignment status, overdue, manual priority, and active/inactive state where applicable.
5. Bin registration/editing with bin type, capacity, GPS from map selection or device location, validation and QR generation.
6. Worker management and team management, including current membership and historical membership display.
7. Permanent and temporary assignment creation, individual or bulk; show assignment status and history. Respect accepted/rejected vs current/suspended/ended as two distinct dimensions.
8. Bin detail side panel with latest condition, assignment, inspection/collection history and emergency reports.
9. Supervisor AI review screen: original image/AI result, worker review/correction, separate supervisor correction and audit timestamps.
10. Overdue/priority views and in-app notification centre.
11. Emergency report review, dismiss, mark reviewed, or create a supervisor-approved temporary assignment through existing backend operations.
12. Deactivate/reactivate bin actions, guarded by supervisor permissions and confirmation.

## UI requirements
- Professional, clean, judge-ready visual design; avoid a generic admin-template look.
- Desktop layout should use map/list together where space permits; mobile should provide clear switching or stacked layout.
- Hindi/English-ready labels from the shared localization approach; do not hardcode repeated text across components.
- Accessible labels, keyboard focus, validation, loading/empty/error states and clear confirmations.
- Do not invent condition data or fabricate success messages.

## Priority
P0: supervisor login integration, bin registration, bin list/detail, map/list, assignments and saved inspection/collection history.
P1: team management, temporary assignment lifecycle, AI review/correction, emergency review, notifications.
P2: advanced filters, localization polish and rare edge-case screens.

## Acceptance criteria
- All screens use agreed typed service/API contracts.
- Supervisor can only see/manage records returned for their authorized area; server/RLS is authoritative.
- A supervisor can register a bin and it appears in list/map after confirmed save.
- Assignment controls show correct lifecycle and acceptance statuses.
- Review history is append-only in display; original AI result is never replaced by a correction.
- Screens render correctly on desktop and mobile widths.
- Run feature tests/build/type-check and provide real results plus handoff report.
