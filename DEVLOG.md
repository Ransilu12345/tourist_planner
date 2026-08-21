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

## 2026-08-15

`frontend/src/components/MapboxRoute.jsx` and `MapboxMultiStopRoute.jsx` both do `import mapboxgl from 'mapbox-gl'`, but `mapbox-gl` and `@mapbox/mapbox-sdk` are only declared in the *root* `package.json` — `frontend/package.json` lists just `leaflet`/`react-leaflet`. So the README's "from `frontend/`: `npm install`" path leaves those two route views unresolvable; the deps should move into `frontend/package.json`. Also updated README's tech-stack row to name Mapbox GL JS alongside Leaflet, since both are actually in use.

## 2026-08-16

Grepped `backend/` for `bcrypt`/`jwt` and found zero hits — admin auth is actually Firebase ID tokens verified through `firebase_admin_setup.verify_firebase_token`, with `auth.py` gating on an `ADMIN_EMAIL` match, so README's tech-stack row claiming "JWT (Bearer), bcrypt" was wrong; corrected it in this commit. Also noticed the backend `.env` list only documents the `DB_*` vars while the code additionally reads `ADMIN_EMAIL`, `FIREBASE_CREDENTIALS_PATH` and `MAPBOX_TOKEN`, so added those to the same bullet. Still stale and left for another day: the "Default admin credentials admin/admin123" section, which no longer reflects a Firebase-based login.

## 2026-08-18

Cleared the last item flagged on 2026-08-16: README's "Default admin credentials" section still advertised `admin`/`admin123`, but `backend/scripts/seed.py` seeds the admin row with `password_hash="firebase-auth"` and pulls the account from `ADMIN_EMAIL` (default `admin@touristplanner.lk`), so there is no password at all. Rewrote it as "Default admin account" describing the Firebase/`ADMIN_EMAIL` setup. `TEST_CHECKLIST.md` still references admin/admin123 in TC-01 and the login checklist — next thing to fix there.

## 2026-08-19

Finished the TEST_CHECKLIST.md cleanup queued yesterday: TC-01's Input column and the admin-login checkbox both still said `admin / admin123`, which no longer exists now that auth goes through Firebase, so both now point at the `ADMIN_EMAIL` account instead. Also committing `TEST_CHECKLIST.md` itself for the first time — the 2026-08-08 note flagged that README links to it but the file was never tracked, so that link has been 404ing on GitHub.

## 2026-08-20

README's Prerequisites table asked for **Node.js 18+**, but `frontend/package.json` pins `vite: ^8.0.1`, which won't install or run on Node 18 — and `.github/workflows/deploy.yml` already sets up Node 20, so CI and the docs disagreed. Bumped the table to 20+ in this commit. Also corrected the tech-stack row from "React 18+, Vite" to "React 19, Vite 8", since the frontend deps are `react ^19.2.4` / `vite ^8.0.1`.

## 2026-08-21

`.github/workflows/deploy.yml` runs `npm install && npm run test` from the repo root, but the root `package.json` has no `scripts` block at all (just three deps: `mapbox-gl`, `@mapbox/mapbox-sdk`, `firebase`) — so that step fails with "Missing script: test". The real suite is `vitest` in `frontend/package.json`, backing 10 `*.test.jsx`/`*.test.js` files under `frontend/src/`, so the job needs a `working-directory: ./frontend`. Can't patch the workflow from here (push token has no `workflow` scope, same blocker as 2026-08-11), but README's testing section only ever mentioned the manual checklist, so documented the automated suite there in this commit.
