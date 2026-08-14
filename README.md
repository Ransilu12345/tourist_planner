# Tourist Day-Visit Planner

A full-stack web app for discovering places within **25 km** of a fixed reference point (Nampamunuwa, Piliyandala): browse by category, inspect details with maps, and assemble a day plan that persists per browser session. An **admin** area manages place records with distance validation against the same reference.

## Prerequisites

| Tool | Version |
|------|---------|
| **Node.js** | 18+ |
| **Python** | 3.11+ |
| **MySQL** | 8.0 |

## Backend setup

From the `backend/` directory:

1. Create a virtual environment (recommended), then install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

2. Configure **`.env`** in `backend/` (adjust for your MySQL instance):

   - `DB_USER`, `DB_PASSWORD`, `DB_HOST`, `DB_PORT`, `DB_NAME` (default database name: `tourist_planner`)

3. Create the MySQL database (empty schema is fine; tables are created on app startup):

   ```sql
   CREATE DATABASE tourist_planner CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
   ```

   Optionally apply `backend/schema.sql` if you prefer explicit DDL; otherwise SQLAlchemy `create_all` runs on startup.

4. Seed sample data (categories, **10** places, default admin). **Run from `backend/`:**

   ```bash
   python scripts/seed.py
   ```

   Expected output when the database is empty:

   `Seeded 10 places, 6 categories, 1 admin user.`

   If categories already exist, the script prints that seeding was skipped.

5. Start the API:

   ```bash
   uvicorn main:app --reload --port 8000
   ```

## Frontend setup

From the `frontend/` directory:

```bash
npm install
npm run dev
```

The dev server proxies `/api` to `http://localhost:8000` (see `vite.config.js`).

## URLs

| Service | URL |
|---------|-----|
| **Frontend** | [http://localhost:5173](http://localhost:5173) |
| **API** | [http://localhost:8000](http://localhost:8000) |
| **Swagger UI** | [http://localhost:8000/docs](http://localhost:8000/docs) |

`GET /` returns a small JSON health payload with API version.

## Default admin credentials

- **Username:** `admin`  
- **Password:** `admin123`  

Change the password in production and restrict admin access appropriately.

## Tech stack

| Layer | Technology |
|-------|------------|
| Frontend | React 18+, Vite, React Router, Axios, Leaflet |
| Backend | FastAPI, Uvicorn, Pydantic v2 |
| Database | MySQL 8.0, SQLAlchemy 2.x |
| Admin auth | JWT (Bearer), bcrypt |

## Seeded places (10)

| # | Place | Category |
|---|--------|----------|
| 1 | Bellanwila Rajamaha Viharaya | Religious |
| 2 | Attidiya Bird Sanctuary | Nature |
| 3 | Mount Lavinia Beach | Nature |
| 4 | Dehiwala Zoological Garden | Wildlife |
| 5 | Sri Lanka Air Force Museum | Museum |
| 6 | Gangaramaya Temple | Religious |
| 7 | Viharamahadevi Park | Leisure |
| 8 | Independence Memorial Hall | Heritage |
| 9 | Galle Face Green | Leisure |
| 10 | Colombo Port City | Leisure |

## Manual testing

See [`TEST_CHECKLIST.md`](TEST_CHECKLIST.md) for step-by-step browser checks (tourist and admin flows).

## API overview (Swagger)

With the backend running, OpenAPI lists **20** operations under `/api` (places, categories, admin, visit plans) plus **`GET /`** for health. Open [http://localhost:8000/docs](http://localhost:8000/docs) to try requests interactively.
