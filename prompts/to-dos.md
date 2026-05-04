# To-Do

> Generated from notes on 2026-05-03. Context: Zunftiq — bugs, demo script, QR-Rechnung.

| # | Task | Area | Notes |
|---|------|------|-------|
| 1 | Fix duplicate "Mitarbeiter zuweisen" dropdown on job detail page — only one `<select id="assign-worker">` should render after assigning a worker | `components/jobs/job-assignments.tsx`, `jobs/[id]/page.tsx` | Component itself renders one dropdown; likely a stale-state or `router.refresh()` race causing the assign form to re-mount while old instance is still visible |
| 2 | Diagnose and fix timer stop bug — click "Stoppen" triggers an error; add console/server logs around `handleClockOut` to pinpoint the failure | `components/time/time-tracker.tsx`, `lib/client-logger.ts` | Logs go to `/api/log` and browser console; check if `activeEntry` is null on click or if the Supabase update returns an RLS/permission error |
| 3 | Reduce Marco's Selenium demo to one start/stop cycle — remove Phase 4.3 (zweiter Einsatz) and adjust Phase 4.4 + 5 to handle a single time entry | `scripts/demo-walkthrough.mjs`, `docs/demo-walkthrough.md` | Currently creates 2 entries (4.1 + 4.3) and submits/approves both; change to 1 entry so the demo is cleaner |
| 4 | Seed QR-IBAN for the test company so the demo PDF shows a Swiss QR-Rechnung payment slip | `supabase/seed-iban-testdata.sql` | Infrastructure exists (company settings field, `swissqrbill` in PDF gen, encrypted storage via `encrypt_company_iban` RPC); just needs the seed script run with the real `PGCRYPTO_ENCRYPTION_KEY` instead of placeholder `'your-base64-encoded-key'` |
