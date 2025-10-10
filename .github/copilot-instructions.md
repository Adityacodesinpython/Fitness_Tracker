# Copilot Instructions for Fitness Tracker

## Project Architecture
- **Monorepo structure:**
  - `backend/`: Python Flask REST API, MongoDB integration, JWT authentication, OTP email verification.
  - `frontend/`: React SPA (Create React App), communicates with backend via REST endpoints.
- **Backend:**
  - Main entry: `backend/app.py` (Flask app, MongoDB connection, JWT setup, API routes)
  - Config: `backend/config.py` (environment-based config classes)
  - Utility: `backend/otp_utils.py` (OTP generation/email)
  - Database test/view: `backend/test_db.py`, `backend/view_db.py`
  - Models, routes, services, utils: folders exist for future expansion (currently empty)
- **Frontend:**
  - Main entry: `frontend/src/`
  - Components: `components/` (e.g., `ExerciseEntryForm.js`)
  - Pages: `pages/` (e.g., `ExerciseLog.js`)
  - Services: `services/` (API calls, e.g., `exerciseService.js`)

## Data Flow & Integration
- **Frontend** calls backend REST endpoints (e.g., `/api/exercise`) using Axios (`exerciseService.js`).
- **Backend** exposes REST endpoints, handles JWT authentication, and stores data in MongoDB (`fitness_tracker` DB).
- **OTP-based email verification** for user authentication (see `/api/auth/request-otp` and `/api/auth/verify-otp` in `app.py`).
- **Environment variables** (see `.env` and `config.py`) control secrets and connection strings.

## Developer Workflows
- **Backend:**
  - Install dependencies: `pip install -r requirements.txt`
  - Run server: `python app.py` (Flask dev server)
  - Test DB connection: `python test_db.py`
  - View DB contents: `python view_db.py`
- **Frontend:**
  - Install dependencies: `npm install`
  - Start dev server: `npm start` (runs on port 3000)
  - Run tests: `npm test`
  - Build for production: `npm run build`

## Project-Specific Patterns
- **API endpoints** follow `/api/[resource]` convention (e.g., `/api/exercise`).
- **JWT authentication** required for protected routes (see `@jwt_required` in `app.py`).
- **MongoDB collections:** `users`, `food_entries`, `exercise_entries`.
- **Frontend** uses `withCredentials: true` for Axios requests to support cookies/JWT.
- **Exercise types** are mapped to icons in UI (`ExerciseEntryForm.js`).

## External Dependencies
- **Backend:** Flask, Flask-CORS, Flask-JWT-Extended, pymongo, python-dotenv, gunicorn
- **Frontend:** React, Axios, date-fns

## Conventions & Tips
- Keep secrets and connection strings in `.env` (never hardcode in code).
- Extend backend by adding new routes/services in respective folders.
- Use `serialize_doc` helper to convert MongoDB ObjectId to string for frontend compatibility.
- For new API endpoints, follow the RESTful pattern and update frontend services accordingly.

## Example: Adding a New Exercise Entry
- Frontend: Call `addExerciseEntry` in `exerciseService.js` with form data.
- Backend: Handle POST `/api/exercise` in `app.py`, store entry in `exercise_entries` collection.

---

If any section is unclear or missing, please provide feedback to improve these instructions.