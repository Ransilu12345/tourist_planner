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
