# Worklog

---
Task ID: 1
Agent: Main agent (Z.ai)
Task: Build Teacher's Data Copilot — complete frontend prototype (Next.js 16 + TypeScript + Tailwind 4 + shadcn/ui), synthetic data only, no backend.

Work Log:
- Initialized fullstack environment via init script; inspected scaffold (package.json, layout, globals.css, ui components).
- Created `src/lib/types.ts` — domain types (Center, Batch, Student, ScoreValue with null=blank, Intervention, FlagRule, metrics).
- Created `src/lib/data.ts` — deterministic (seeded mulberry32) synthetic engine: 6 centers, 51 batches, 1,551 students, 8 tests × 3 subjects; blanks (null) distinct from recorded 0; negative scores allowed; duplicate student names by design; 10 engineered review cases bound to real student indices; 5 transparent flag rules (R1–R5) with metric computation; scope filtering/aggregation helpers; static reference KPIs (6 / 51 / 24,742 / 12,236); DQ catalog; sample workbook (12 rows) with injected issues; 7 import issues.
- Created `src/lib/store.ts` (zustand): view switching, student/batch selection, one-shot center filter preset, intervention statuses, session notes, simulated-import records.
- Created shared UI (`src/components/shared.tsx`), charts (`src/components/charts.tsx`, recharts), navy sidebar + mobile drawer (`src/components/sidebar.tsx`), app shell with sticky footer (`src/components/app-shell.tsx`).
- Built 5 views: overview-view, centers-view (+ batch detail), students-view (+ full profile: test history, subject bars, trend, scoped ranks, notes + status), interventions-view (rule cards, status chips, status selects + toasts), import-view (6-step simulated wizard with mapping validation, issue decisions, blank-vs-zero policy, honest non-import confirmation).
- Fixed bugs found during verification: (a) engineered cases referenced non-existent reg numbers → bound to real indices; (b) rule windows/patterns corrected so all 10 interventions' claimed rules actually fire (verified via `scripts/verify-rules.ts`: 10/10 OK); (c) import issues table overlapped → table-fixed + whitespace-normal override of shadcn TableCell nowrap; (d) "setState during render" React warning from zustand consume at mount → read preset in useState initializer, clear via post-commit effect; (e) removed unused useEffect imports; (f) truncated status pills in Recent Imports → shortened labels.
- Verification: `bun run lint` clean; browser (agent-browser) end-to-end: all 5 pages navigate, search/filters/sort affect content, batch + student detail open, intervention status change + toast works, full import walkthrough completes, simulated entry appears in Recent Imports, mobile 390px layout + drawer OK, zero console errors, no page errors.

Stage Summary:
- Deliverable: runnable Next.js 16 frontend prototype at `/` (single-route SPA with in-app navigation).
- Key files: src/lib/{types,data,store}.ts, src/components/{shared,charts,sidebar,app-shell}.tsx, src/components/views/{overview,centers,students,interventions,import}-view.tsx, src/app/{page,layout}.tsx.
- All data synthetic & deterministic; demo labeling everywhere; no backend/DB/AI/network calls.
- Verified 10/10 rule triggers; screenshots in /home/z/my-project/download/prototype-screenshots/.
