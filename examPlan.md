# Qoder Exam Plan — Finish Early Edition

**Session:** 08:00–17:00 (30 min planning, no coding · 7.5 h programming · 1 h lunch). Arrive 07:45.
**Your target: features frozen 14:15, audit done and leaving by ~15:00.** You can leave early; you can't get time back.
**Marked:** last commit pushed before 17:00. Repo public, `git clone` over HTTPS must work. README + `start.sh` required.
**Stack (in AGENTS.md):** React + Vite · Express · SQLite (better-sqlite3) · plain CSS "Clay & Ink" design. One command: `npm run dev`.

**Credits:** Lite free · Efficient 0.3× (maybe 0.0× — check) · Auto 1.0× (avoid) · Performance 1.1× · Ultimate 1.6× (maybe 0.8×).
Rule: **Performance for thinking** (spec analysis, app design, core features, debugging). **Efficient for typing** (scaffold, simple batches, styling, audit).

---

## Timeline

| Time | What | Model |
|---|---|---|
| 07:45 | Log in, Qoder signed in, files from Moodle | — |
| 08:00 | 2 min doing nothing. Read the spec yourself. | — |
| 08:05 | **P1 Analyse spec** → REQUIREMENTS.md (ask tutor first if allowed in planning) | Performance |
| 08:15 | **P2 Design the app** → PLAN.md | Performance |
| 08:30 | Git setup (5 min), **P3 Scaffold** | Efficient |
| 09:00 | **P4 Base features** | Performance |
| ~10:30 | Base pushed ✅ — click through whole app | — |
| 10:30–14:15 | **P5 Batches** in order; fresh chat every 1–2 batches | Efficient / Performance |
| ~12:00 | 20–30 min lunch (push first; you can eat while a batch runs) | — |
| ~13:30 | **P6 Design pass** | Efficient |
| 14:15 | Feature freeze. **P7 Final audit** | Efficient |
| ~15:00 | Last push verified → leave | — |

If you're behind at 10:30 (no working base), skip everything else and only fix the base.

---

## Tonight

1. **Read AGENTS.md once** so you know what Qoder will build.
2. **GitHub token:** Settings → Developer settings → Fine-grained tokens → expiry 7 days, All repositories, Repository permissions → **Contents: Read and write**. Save on your phone.
3. **Optional:** create the exam repo now — **Public**, tick "Add a README". Check it opens in an incognito window.
4. **Qoder:** sign in, note your credits and the Efficient/Ultimate rates.
5. **Upload to Moodle:** `exam_plan.md` and `AGENTS.md`. Also commit both to your lab3 repo as backup.
6. **Sleep.**

---

## 08:30 — Git (first 5 min of programming)

```
git clone https://github.com/<you>/<exam-repo>.git
cd <exam-repo>
git config user.name "Your Name"
git config user.email "you@students.wits.ac.za"
git config credential.helper store
```
Put `AGENTS.md` in the repo root and the spec in `spec.md` (paste the text). Then:
```
git add -A && git commit -m "docs: init" && git push
```
Username = GitHub username, password = **token**. Open the folder in Qoder. Delete `~/.git-credentials` before you go home.

(If tutors let you do P1/P2 during planning time, do git at 07:45 or right at 08:30 — P1/P2 only write .md files, no code.)

---

## P1 — Analyse the spec · Performance

```
Follow AGENTS.md. Read spec.md fully. Write no code.

Create REQUIREMENTS.md:
- Table: ID | requirement | marks | mandatory/optional | exact names that must match the spec (routes, fields, files, ports, labels) | status TODO
- List EVERY requirement, including README/submission rules and anything likely auto-marked.

Then reply briefly:
1. Anything in the spec that conflicts with the stack in AGENTS.md (e.g. required Postgres/Docker/specific framework).
2. Ambiguities, one line each, with the safest interpretation.
3. Total marks: mandatory vs optional.
Stop.
```

**You:** check REQUIREMENTS.md against the spec (2 min). Missing or misread rows = lost marks.

## P2 — Design the whole app · Performance

```
Follow AGENTS.md. Using REQUIREMENTS.md, design the complete app (mandatory + all optional features worth doing) in PLAN.md. No code.

PLAN.md sections:
1. User flows: the main workflow a marker will try, step by step.
2. Data model: every table, columns, types, constraints, relations. Design it so optional features need no schema rewrite later.
3. API: method | path | request body | response | which requirement IDs.
4. Pages: route | purpose | main components | actions | empty state. Include sidebar nav items.
5. Seed data: realistic demo records so every page looks alive on first run.
6. Batches: group optional features (same tables/pages, shared work). Table: batch | requirement IDs | marks | effort L/M/H | risk L/M/H. Ranked by marks per effort and risk. Mark any not worth doing.
7. Risks: top 3 things most likely to go wrong and how to avoid them.

Also add a "batch" column value to every row in REQUIREMENTS.md (Base, B1, B2...).
Keep it tight. Stop.
```

**You:** sanity-check the flows and the batch order. Change anything in one line, e.g. "Swap B2 and B3."

## P3 — Scaffold · Efficient

```
Follow AGENTS.md. Scaffold the project exactly as in the Stack section: workspaces, client (Vite React), server (Express, /api/health, db.js with schema from PLAN.md + seed data), concurrently, tokens.css with the full design system, app shell with sidebar + empty placeholder page for every route in PLAN.md, toast component, README.md, start.sh, .gitignore.
No feature logic yet. Install, start npm run dev, curl /api/health, confirm the client loads. Commit "chore: scaffold", push. Reply per AGENTS.md.
```

**You:** open the URL — sidebar, colours and fonts should already look right, and the dark-mode toggle should work. If not, fix it now (cheap) rather than later.

## P4 — Base features · Performance

```
Follow AGENTS.md. Implement every requirement in REQUIREMENTS.md marked Base, following PLAN.md (API, pages, flows). Real data end-to-end: UI → API → SQLite, persists after restart. Include empty/loading/error states and toasts.
Update REQUIREMENTS.md statuses. Verify (curl each endpoint, build client), commit "feat: working base", push. Reply per AGENTS.md.
```

**You:** do the main user flow from PLAN.md yourself, start to finish. Broken → **Error** prompt. The push already protects you.

## P5 — Batches · Efficient (Performance if risk is M/H or schema/auth changes)

Same chat:
```
Implement the next TODO batch in REQUIREMENTS.md per PLAN.md. Follow AGENTS.md. If something is much harder than planned, stop and tell me whether to skip it.
```

**Fresh chat** after the base and then every 1–2 batches (long chats get slow and expensive):
```
Exam in progress, now [time], I'm stopping features at 14:15. Follow AGENTS.md. Read REQUIREMENTS.md and PLAN.md (not the whole spec unless needed). App may be running; curl /api/health before starting anything. Implement the next TODO batch.
```

## P6 — Design pass · Efficient

```
Design pass only, no functional changes. Follow the AGENTS.md design system exactly on every page: spacing, typography, page headers, tables, forms, buttons, empty/loading/error states, toasts, active nav. Remove anything forbidden and any hard-coded colours. Check every page in light AND dark mode, at 1366×768 and mobile width. Commit "style: polish UI", push. Reply per AGENTS.md.
```

## P7 — Final audit · Efficient (start 14:15)

```
Feature freeze. Follow AGENTS.md. Re-read spec.md and REQUIREMENTS.md. One line per requirement: PASS / FAIL / MISSING / NOT VERIFIED. Check names match the spec exactly.
Fresh-clone check: clone the https remote into /tmp/check, run ./start.sh exactly as README says, confirm client + API work with a fresh DB (seed runs). Check package-lock.json committed, nothing required gitignored, no secrets, README URLs/ports correct.
Fix ONLY things that lose marks or break startup. Commit "fix: final", push, confirm git status clean and up to date with origin. Reply: summary table, fresh-clone result, anything unverified.
```

**You:** open the GitHub repo page in the browser and check the latest commit is there. Then go home.

---

## Every hour (phone timer)

- `git status` — anything uncommitted? Commit + push.
- Use the app like a marker: main flow start to finish, then the newest feature.
- Check the clock against the timeline. Behind by 30+ min → drop the lowest-value remaining batch.

## While Qoder is working (it's slow — use the wait)

- Click through what's already built; write down bugs to fix in one prompt later.
- Read the spec section for the next batch.
- Don't stack up new requests while it's mid-task.
- If Gemini chat works, use it for general questions to save Qoder credits.

---

## Emergency prompts

**Performance (debugging):**

Error:
```
Use the actual error output. Find root cause, smallest fix, no unrelated changes.
```

Regression:
```
This worked before the last batch. Check git diff, find the regression, restore working behaviour, no redesign.
```

Going in circles:
```
Stop editing. List what works, what fails, and the smallest path back to stable. If needed, git restore to the last good commit.
```

Several bugs at once (saves round trips):
```
Fix these bugs, smallest changes, then verify each: 1) ... 2) ... 3) ...
```

**Lite or Efficient (nudges and decisions):**

Package blocked:
```
This package can't be downloaded here. Use the fallback in AGENTS.md or the closest no-dependency alternative. Smallest change.
```

Overengineering:
```
No refactor or redesign. Minimum change to meet the requirement.
```

Servers / sleeps / stuck:
```
Stop restarting servers and sleeping. npm run dev is already running with watch mode; curl /api/health. If a command hangs, kill it and use a non-blocking alternative.
```

Worth it?:
```
Now [time], features stop at 14:15. Is this batch worth its marks vs risk? One paragraph: continue, simplify, or skip.
```

Nearly out of time:
```
[X] min until feature freeze. Protect what works. Fix, revert, or go straight to final audit? Decide and do it.
```

Quick test:
```
App is running. Give URL, exact clicks, expected result. Nothing else.
```

Too many credits:
```
Be brief. No re-reading files you've seen, no repeated test runs, no explanations unless asked.
```
