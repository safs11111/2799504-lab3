# Exam rules for the agent

Timed exam. Goal: max marks, polished app that runs from a fresh clone. Speed matters. Be brief in replies.

## Stack (fixed unless the spec requires otherwise)
- One repo, npm workspaces. Root `package.json`: `"workspaces": ["client","server"]`, script `"dev": "concurrently -n server,client -c blue,green \"npm run dev -w server\" \"npm run dev -w client\""`.
- `client/`: React + Vite (JavaScript, not TS), react-router-dom, lucide-react icons. Port 5173. Vite proxy `/api` → `http://localhost:3001`.
- `server/`: Node + Express (ES modules), port 3001, `"dev": "node --watch src/index.js"`. Structure: `src/index.js`, `src/db.js`, `src/routes/*.js`.
- DB: SQLite via `better-sqlite3`. File `server/data/app.db` (gitignored, auto-created). `src/db.js` runs `schema.sql` (CREATE TABLE IF NOT EXISTS) on start and seeds demo data if tables are empty.
  - If better-sqlite3 fails to install, use built-in `node:sqlite` (Node ≥ 22.13). Tell me first.
  - If the spec REQUIRES Postgres/MySQL/Docker: use `pg` + `docker-compose.yml`, and start.sh runs `docker compose up -d` first.
- Auth (only if spec needs it): `bcryptjs` (not bcrypt) + `jsonwebtoken` in an httpOnly cookie or Authorization header.
- Tests (only if spec needs them): vitest + supertest.
- Fonts via npm (Google Fonts may be firewalled): `@fontsource-variable/fraunces`, `@fontsource/ibm-plex-sans`, `@fontsource/ibm-plex-mono`.
- No other deps unless required. If any package won't install (firewall), stop and tell me.

## Design system — "Clay & Ink" (editorial, Swiss-grid, calm)
All colours/spacing as CSS variables in `client/src/styles/tokens.css`. Plain CSS, no CSS framework.
- Background `#F5F2EC` (warm stone) · Surface `#FFFFFF` · Sunken `#EDE8DF`
- Ink `#1B1D1F` · Muted text `#6B6F72` · Border `#E3DED5`
- Accent terracotta `#C4532D`, hover `#A8431F`, accent tint `#F6E3DA`
- Success `#2F7D5B` · Warning `#B7791F` · Danger `#B42318`
- Dark mode (same tokens, overridden under `:root[data-theme="dark"]`):
  Background `#141312` · Surface `#1C1B19` · Sunken `#24221F` · Ink `#EDE8E0` · Muted `#9A958D` · Border `#2F2C28`
  Accent `#E0714A`, hover `#EA8762`, accent tint `#3A251C`, accent text `#F0916C`, text on accent buttons `#1A0E08` (not white) · Success `#5BBF8E` · Warning `#E0A543` · Danger `#F07A6A`
  - Toggle: sun/moon icon button at the bottom of the sidebar. Default = OS `prefers-color-scheme`; choice saved in localStorage; set `data-theme` on `<html>` before first paint (inline script in index.html) so there's no flash.
  - Never hard-code colours in components — only tokens — so both themes always work. Check every page in both themes.
- Headings: Fraunces (serif), tight letter-spacing. Body: IBM Plex Sans 16px/1.55. Numbers, IDs, dates: IBM Plex Mono.
- Small uppercase labels: 12px, letter-spacing 0.08em, muted.
- Radius 6px. 1px borders instead of shadows (one soft shadow only for modals/dropdowns). 8px spacing scale.
- Layout: fixed left sidebar (app name in Fraunces + nav with icons, active item = terracotta left bar + tint), content max-width 1100px, page header = title + one-line description + primary action on the right.
- Buttons: primary = solid terracotta, white text; secondary = white with border; danger = text-only red until confirm.
- Tables: no zebra stripes, row hover in Sunken, mono for numbers, right-align numbers.
- Every list/page has: empty state (icon + one sentence + action), loading state, error message. Every action gives feedback (small toast bottom-right). Forms: visible labels, inline validation messages, disabled submit while saving. Destructive actions need confirm.
- FORBIDDEN: gradients, glassmorphism, purple/indigo, neon, emoji as icons, giant rounded cards, centered-everything hero layouts.
- Must look right at 1366×768 and stay usable on mobile width.

## Coding
- Smallest change that works. No refactors, no extra features, no TypeScript migration.
- Names EXACTLY as in the spec (routes, JSON fields, files, ports, labels).
- Validate input on the server; return JSON errors `{ error: "message" }` with correct status codes.
- Config via env with defaults; `.env.example` if any env vars.
- `.gitignore`: node_modules, .env, server/data/*.db, dist.
- Read only files relevant to the current task. Use PLAN.md and REQUIREMENTS.md instead of re-reading the spec.

## Running things
- You run all terminal commands. Keep `npm run dev` running when you hand back.
- Reuse the running dev server (watch mode reloads). No duplicate servers. curl health checks, never fixed sleeps. Never run a command that blocks forever.
- Server has `GET /api/health` → `{ ok: true }`.

## Files you maintain
- `README.md`: what the app does, prerequisites (Node version), `./start.sh` or `npm install && npm run dev`, URLs, env vars, DB notes, demo login if any.
- `start.sh`: `#!/usr/bin/env bash` · `set -e` · `npm install` · `npm run dev`. chmod +x.
- `REQUIREMENTS.md`: every spec requirement, one row: ID | requirement | marks | batch | exact names | status TODO/DONE/VERIFIED. Update as you go.
- `PLAN.md`: data model, API, pages, flows. Update if the design changes.

## Git
- Commit after every working change; push after every task. Messages: `feat:`, `fix:`, `style:`, `docs:`, `chore:`.
- Never commit secrets, .env or the .db file.

## Finishing a task
Verify with fast checks (build, curl the API, tests if any). Commit + push when green. Reply ONLY:
1. URL (app running) 2. shortest click-through test + expected result 3. anything unverified.
Then stop. Never start the next task by yourself.
