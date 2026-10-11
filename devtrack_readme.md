# DevTrack API

DevTrack is a minimal Django-based backend API for tracking engineering issues (bugs, priorities, and statuses), designed as a stripped-down GitHub Issues style tracker.

---

## Prerequisites & Installation

Follow these steps to set up and run the project locally:

1. **Clone or navigate to the project directory:**
   ```bash
   cd devtrack
   ```

2. **Create and activate a virtual environment:**
   ```bash
   python -m venv .venv
   # On Windows:
   .venv\Scripts\activate
   # On Mac/Linux:
   source .venv/bin/activate
   ```

3. **Install dependencies:**
   ```bash
   pip install django djangorestframework
   ```

4. **Run the development server:**
   ```bash
   python manage.py runserver
   ```
   The API will be available at `http://127.0.0.1:8000/`.

---

## API Endpoints

### 1. Reporters (`/api/reporters/`)
* **`POST /api/reporters/`** — Create a new reporter.
  * *Request Body Example:*
    ```json
    {
      "id": 1,
      "name": "Jane Doe",
      "email": "jane@example.com",
      "team": "backend"
    }
    ```
* **`GET /api/reporters/`** — Retrieve all reporters.
* **`GET /api/reporters/?id=1`** — Retrieve a single reporter by ID.

### 2. Issues (`/api/issues/`)
* **`POST /api/issues/`** — Create a new issue (automatically applies subclasses and descriptive messages based on priority).
  * *Request Body Example:*
    ```json
    {
      "id": 1,
      "title": "Login button not working on mobile",
      "description": "Users on iOS 17 cannot tap the login button",
      "status": "open",
      "priority": "critical",
      "reporter_id": 1
    }
    ```
* **`GET /api/issues/`** — Retrieve all issues.
* **`GET /api/issues/?id=1`** — Retrieve a single issue by ID.
* **`GET /api/issues/?status=open`** — Filter issues by status (`open`, `in_progress`, `resolved`, `closed`).

---

## Design Decision

**Decision:** Utilizing flat JSON files (`reporters.json` and `issues.json`) via raw file I/O instead of a traditional relational database (like PostgreSQL or SQLite) with an ORM.

**Why:** This approach keeps the application strictly lightweight, portable, and decoupled from heavy database configurations. It directly matches the minimal requirements of the assignment specification, allowing for fast, transparent state inspection while isolating data access into clean helper functions.

---

## Postman Testing Screenshots

### Success Example (`POST /api/issues/`)
*(Insert screenshot of successful 201 Created response here)*

### Failure Example (`POST /api/issues/` with missing title)
*(Insert screenshot of 400 Bad Request validation failure response here)*