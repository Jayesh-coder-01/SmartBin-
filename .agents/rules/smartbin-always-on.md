---
trigger: always_on
---
# SmartBin invariants
Treat `docs/SmartBin_Corrected_SRS.md` as the authoritative specification. Before implementation, read the relevant SRS sections. Never expose Gemini or Supabase service-role secrets in frontend code. Enforce authorization in backend/RLS. Keep assignment acceptance status separate from assignment lifecycle state. Preserve photos and reports correctly on AI failure and 90-day expiry. Chatbot is read-only and must use fixed role-scoped queries. Do not report unrun tests as passing. Respect file ownership in `AGENTS.md`.
