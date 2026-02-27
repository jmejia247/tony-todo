# Todo App Backend (Django + Postgres)

> **Goal:** Build confidence in backend development by designing and implementing a real system—*and understanding why each decision is made.*

This project is intentionally simple on the surface (a Todo app) but deep in learning. The purpose is **not speed**, but to think about the purpose of each step and how each part works in our system.

---

## Project Overview

You are tasked with building the **backend** for a Todo application that allows:

* Multiple users
* Each user to have their own Todo boards
* Each board to contain Todo items
* Full CRUD (Create, Read, Update, Delete) on boards and todos

The backend will expose a REST API that a frontend (TypeScript + Redux Toolkit) can consume later.

---

## Success Criteria

By the end of this project, you should be able to confidently explain:

* Why Django and Postgres are good choices here
* How data flows from HTTP request → backend → database → response
* How authentication and authorization protect user data
* How backend design choices affect scalability, reliability, and developer experience

---

## Tech Stack (Chosen Ahead of Time)

* **Language:** Python
* **Framework:** Django + Django REST Framework
* **Database:** PostgreSQL
* **Auth:** Session-based or Token/JWT (your choice)

> Even though the stack is chosen, you are expected to justify *why* it makes sense.

---

# Backend Roadmap

Each section has:

* **Checkpoint** – what to build
* **Done when** – how you know it’s complete
* **System Design Questions** – write your answers directly in this README

---

## 0. Understanding the Role of the Backend

### Checkpoint

Before writing code, pause and define what the backend is responsible for.

### Done When

* You can answer why you chose python + Django.
* You can explain the difference between API and server

### System Design Questions

* What problems does the backend solve that the frontend should not?
* Why is data validation required on the server even if the frontend validates?
* What does “stateless” mean in the context of HTTP APIs?

**Notes:**

---

## 1. Environment & Project Setup

### Checkpoint

* Create a Git repository
* Set up a Python virtual environment
* Install Django, Django REST Framework, Postgres
* Run the Django development server

### Done when

* `python manage.py runserver` runs without errors
* You can access the default Django page

### System Design Questions

* What is a virtual enviornment?
* Why use a virtual environment?
* Why should secrets (DB password, Django secret key) not be committed to Git?
* What risks arise when environments (dev vs prod) differ?
* What does HTTP stand for?
* What is the difference between HTTP and HTTPS?
* What is latency?
* How does latency fit into the context of our server?
* 

**Notes:**

---

## 2. Django Project & App Structure

### Checkpoint

* Create a Django project
* Create an `api` app
* Enable Django REST Framework
* Add a simple health endpoint: `GET /health`

### Done when

* Visiting `/health` returns `{ "status": "ok" }`

### System Design Questions

* Why does Django separate *projects* and *apps*?
* How would poor project structure slow down a team?
* What is an endpoint?
* 

**Notes:**

---

## 3. Database Setup (Postgres)

### Checkpoint

* Configure Postgres connection
* Run initial migrations
* Verify database access via Django shell

### Done when

* Migrations run successfully
* You can create and query objects from the shell

### System Design Questions

* Why choose Postgres over SQLite or NoSQL here?
* What advantages do relational databases provide for this problem?
* Why are migrations critical in production systems?

✍️ **Notes:**

---

## 4. Data Modeling

### Checkpoint

Design and implement models:

* **User** (Django default)
* **Board**

  * owner → User
  * name
* **Todo**

  * board → Board
  * title
  * description (optional)
  * is_completed
  * timestamps

### Done when

* Models exist and are migrated
* Data can be created via admin or shell

### System Design Questions

* Why should Todos belong to Boards instead of directly to Users?
* What constraints belong at the database level vs application level?
* What would change if Todos could belong to multiple Boards?

✍️ **Notes:**

---

## 5. Serialization & Validation

### Checkpoint

* Create serializers for Board and Todo
* Add validation rules (required fields, formats)

### Done when

* Invalid input returns clear 400 errors
* Valid input creates correct records

### System Design Questions

* Why should validation happen on the backend?
* What makes an error message useful for frontend developers?

✍️ **Notes:**

---

## 6. API Endpoints (CRUD)

### Checkpoint

Implement REST endpoints:

**Boards**

* `GET /api/boards`
* `POST /api/boards`
* `PATCH /api/boards/:id`
* `DELETE /api/boards/:id`

**Todos**

* `GET /api/boards/:id/todos`
* `POST /api/boards/:id/todos`
* `PATCH /api/todos/:id`
* `DELETE /api/todos/:id`

### Done when

* CRUD works via Postman or curl
* Responses are consistent JSON

### System Design Questions

* Why use REST semantics instead of RPC-style endpoints?
* What does idempotency mean for PATCH and DELETE?
* Should deletes be hard or soft deletes? Why?

✍️ **Notes:**

---

## 7. Authentication & Authorization

### Checkpoint

* Add authentication
* Ensure users only access their own data

### Done when

* Unauthenticated requests return 401
* Cross-user access is blocked (403 or 404)

### System Design Questions

* What’s the difference between authentication and authorization?
* Session vs JWT: what are the tradeoffs?
* Why is object-level permission important?

✍️ **Notes:**

---

## 8. Testing

### Checkpoint

Add tests for:

* Board creation
* Todo creation
* Permission enforcement

### Done when

* Tests pass reliably

### System Design Questions

* Why are permission tests high-impact?
* What should tests protect against: bugs or regressions?

✍️ **Notes:**

---

## 9. Reliability & Error Handling

### Checkpoint

* Add logging
* Ensure production-safe error responses

### Done when

* Logs are readable and useful
* Stack traces are hidden from users

### System Design Questions

* What failures should the backend expect?
* Logs vs metrics vs alerts—what’s the difference?

✍️ **Notes:**

---

## 10. Production Readiness (Mental Model)

### Checkpoint

Prepare the app to be deployable:

* Env-based config
* DEBUG off
* CORS support

### Done when

* You can clearly explain what changes in production

### System Design Questions

* Does this app prioritize availability or consistency? Why?
* What breaks first as traffic grows?

✍️ **Notes:**

---

## Final Reflection

Answer honestly:

* What concepts feel clearer now?
* Where did you struggle the most?
* If you were reviewing this PR, what would you comment on?

---

> **Reminder:** Confidence doesn’t come from knowing everything—it comes from knowing *why* you chose what you did.
