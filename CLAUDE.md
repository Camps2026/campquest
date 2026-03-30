# PopCamps — Project Context for Claude

## What this project is
PopCamps (popcamps.one) is a Washington state summer camp directory. Parents search for camps by city, age, and date range. The owner is not a developer — always explain changes clearly before making them.

## Rules — read these first
- **Single file only**: All code lives in `index.html`. No separate JS or CSS files, ever.
- **No build tools**: No npm, no webpack, no frameworks. CDN links only.
- **Always push to GitHub after every change** — don't wait to be asked.
- **Never use the Supabase secret key** in frontend code.

## Tech stack
- Frontend: `index.html` (single file, all inline CSS + JS)
- Database: Supabase (PostgreSQL)
- Deployment: GitHub Pages → custom domain `popcamps.one`
- GitHub repo: https://github.com/Camps2026/popcamps
- Local repo: `~/Documents/campquest/`

## Supabase (publishable — safe for frontend)
- URL: `https://ikhvkrbwwnapeofqpxdb.supabase.co`
- Publishable key: `sb_publishable_YPY0o2fRbGoDP1CBFoZb-A_11ucDenw`
- Table: `camps` — 995+ rows, RLS disabled (public read, intentional)

## Formspree form endpoints
- List Your Camp: `https://formspree.io/f/mdapagpg`
- Claim Your Camp: `https://formspree.io/f/xqegeqgl`

## Testing
- Use **MCP Chrome DevTools** to visually verify changes on mobile before and after edits
- Always test at 390x844 mobile viewport (iPhone size)
- Use `mcp__chrome-devtools__emulate` + `mcp__chrome-devtools__take_screenshot` to check layout
- Use `mcp__chrome-devtools__evaluate_script` to force-show UI states (e.g. calendar with dummy data)

## Current site state
- Title: `popcamps | Washington Summer Camp Directory`
- H1: `Washington Summer Camp Directory`
- SEO: meta description, canonical, Open Graph, Twitter Card, Schema.org, sitemap all in place
- og:image: `https://popcamps.one/og-image.png` (1200×630px, already pushed)
- Footer: dark green, "Listings updated regularly for summer 2026. · © 2026 PopCamps"
- My Calendar page: full summer toggle + empty week click-to-search
- Mobile: Show Filters button visible, calendar fits on screen (Mon–Fri only, no horizontal scroll)
- No Best Match sort dropdown (removed)
- Camp owner portal: LIVE — magic link login, edit form, photo uploads, admin review queue
- Admin review page: LIVE — approve/reject edits before they go live
- "Updated" badge: appears on camp cards within 30 days of owner-approved edit

## Supabase tables (added for owner portal)
- `camp_owners` — links `auth.users.id` to `camps.id` (plain integer, no FK)
- `site_admins` — stores admin user_id; RLS disabled (publicly readable)
- `camp_edit_requests` — staging table for owner edits pending admin review
- `camps` table: new columns `description`, `photos` (text[]), `owner_updated_at` (timestamptz)
- Storage bucket: `camp-photos` (public)

## Admin user
- user_id: `db121d42-e139-4e4d-ab01-ab360c7010ed` (inserted into `site_admins`)
- Login: magic link via the "Camp Owner Login" section on the Portal page

## How to approve a camp owner claim
1. Claim arrives via Formspree → your email
2. Supabase → Authentication → Users → "Invite User" → enter their email
3. Copy their `user_id` from the users list
4. Table Editor → `camp_owners` → Insert Row: `user_id` + `camp_id`
5. Done — owner can log in and edit

## Planned future work
- Google Analytics (deferred until real traffic)
- Remaining session_dates cleanup (~66 camps still have non-date text)

## Work log
Full history of all changes: `~/Documents/campquest/CAMPQUEST_WORK_LOG.md`
