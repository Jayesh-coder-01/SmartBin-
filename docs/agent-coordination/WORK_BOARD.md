# SmartBin Agent Work Board

The Project Orchestrator owns this board. Keep statuses current and record blockers. Do not mark a task complete without a handoff and test evidence.

| ID | Track | Owner | Depends on | Status | Evidence / blocker |
|---|---|---|---|---|---|
| M0-01 | Inspect repo + SRS, identify existing work | Orchestrator / Explorer | None | Not started | |
| M0-02 | Agree architecture, API/DB contracts and file ownership | Orchestrator + Backend + UI + AI | M0-01 | Not started | |
| M1-01 | Supabase schema, RLS, seed, core transactional operations | Backend | M0-02 | Not started | |
| M1-02 | Shared app shell, auth and route composition | Orchestrator | M0-02 | Not started | |
| M1-03 | Supervisor feature screens | Supervisor UI | M0-02 | Not started | |
| M1-04 | Worker feature screens | Worker UI | M0-02 | Not started | |
| M1-05 | Gemini image/chat Edge Functions | AI | M0-02 | Not started | |
| M2-01 | Connect supervisor flows to real backend | Supervisor UI + Backend | M1 | Not started | |
| M2-02 | Connect worker flows to real backend | Worker UI + Backend | M1 | Not started | |
| M2-03 | Connect AI analysis and chatbot to UI/backend | AI + UI + Backend | M1 | Not started | |
| M2-04 | Critical path, RLS and failure-path tests | QA + Critic + Challenger | M2 | Not started | |
| M3-01 | Fix critical/high defects and regressions | Relevant owner | M2-04 | Not started | |
| M3-02 | Deploy and smoke-test if approved | QA/Release + Orchestrator | M3-01 | Not started | |
| M3-03 | README, demo evidence, prompt/tool contribution log | QA/Release | M3-02 | Not started | |

## Priority policy
- P0: end-to-end core demo path and secure role separation.
- P1: temporary assignment/emergency reporting/chatbot/notifications that are required for a compelling demo.
- P2: full scheduled automation, photo-expiry job, full language polish and rare edge cases.

P2 means lower delivery order, not removed from the SRS. Every non-delivered requirement must be listed as incomplete before final handoff.
