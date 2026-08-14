# Dev Log

A running log of small daily notes on this project (ideas, tweaks, TODOs, observations). One entry per day, added automatically.

## 2026-07-29

Set up automated daily devlog + commit workflow.

## 2026-07-31

Noticed TEST_CHECKLIST.md's manual test table skips TC-10 and re-lists TC-06/07/08 again as TC-23/24/25 — worth renumbering next time that file is touched.

## 2026-08-01

Noticed README's seed script output line ("Seeded 6 categories, 10 places, 1 admin user.") doesn't match what `backend/scripts/seed.py` actually prints (`Seeded {seeded_count} places, 6 categories, 1 admin user.` — places and categories swapped in order). Small doc drift worth fixing when the seed script or README is next touched.

## 2026-08-05

Noticed a typo in `.github/workflows/deploy.yml`: the Node setup step has `node-node-version: '20'` instead of `node-version: '20'`, so the pin to Node 20 is silently ignored. Left unfixed here since the repo's push token lacks the `workflow` scope needed to update files under `.github/workflows/`.

## 2026-08-06

Fixed the README/seed.py output mismatch noted on 2026-08-01: swapped the order in README's expected seed output line to `Seeded 10 places, 6 categories, 1 admin user.`, matching what `backend/scripts/seed.py` actually prints.

## 2026-08-07

Noticed TC-01 in TEST_CHECKLIST.md ("Login with correct credentials", admin/admin123) is filed under the "Tourist flow" table even though it's clearly an admin login case -- worth moving to the admin section next time that file gets renumbered (see the 2026-07-31 note on the TC-10/TC-23-25 gap).

## 2026-08-08

Noticed the repo's git history only tracks `DEVLOG.md`, `README.md`, and `.github/workflows/deploy.yml` — `TEST_CHECKLIST.md`, `backend/`, and `frontend/` (all referenced by README, e.g. the `[TEST_CHECKLIST.md]` link) were never actually committed, so that link 404s on GitHub. Worth `git add`-ing the real source tree next time it's touched.

## 2026-08-11

Re-checked `.github/workflows/deploy.yml`: the `node-node-version` typo from 2026-08-05 is still there, still silently ignoring the Node 20 pin. Still can't fix it directly — push token has no `workflow` scope — so leaving it as a standing reminder here until someone edits it manually via the GitHub UI.

## 2026-08-14

Counted the route decorators in `backend/routes/` and got 20 operations under `/api` (6 places, 5 plans, 5 admin, 4 categories), but README's "API overview (Swagger)" section still claims **16** — stale since routes were added. Updated that number to 20 in the same commit.
