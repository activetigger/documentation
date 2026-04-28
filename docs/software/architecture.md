# ActiveTigger -- Software Architecture

This page describes Active Tigger technical architecture and implementation choices for dev and contributors.

## High-level overview

```
                    +-------------------+
                    |      Nginx        |
                    |  (reverse proxy)  |
                    +--------+----------+
                             |
              +--------------+--------------+
              |                             |
     +--------v--------+         +---------v--------+
     |  React Frontend |         |  FastAPI Backend  |
     |  (TypeScript)   |         |  (Python)         |
     +--------+--------+         +---------+---------+
              |                             |
              |   REST API (OpenAPI)        |
              +-------------+---------------+
                            |
              +-------------+--------------+
              |                            |
     +--------v--------+        +---------v---------+
     |    Database      |        |   File System     |
     | SQLite / Postgres|        | (Parquet, models) |
     +-----------------+         +-------------------+
```

The application follows a classic client-server architecture with three main layers:

- **Frontend**: React 18 single-page application served via Vite.
- **Backend**: FastAPI REST API handling business logic, ML pipelines, and data management.
- **Storage**: A relational database (SQLite or PostgreSQL) for structured data, and the local file system for datasets (Parquet), trained models, and features.

Nginx acts as a reverse proxy, routing `/api/*` requests to the backend and everything else to the frontend.

---

## Backend (`api/activetigger/`)

### Entrypoint and routing

The FastAPI application is defined in `app/main.py` and exposes 13 routers:

| Router | Path prefix | Purpose |
|--------|-------------|---------|
| users | `/users` | Authentication (JWT/OAuth2), account management |
| projects | `/projects` | Project CRUD, configuration |
| annotations | `/annotations` | Save and retrieve annotations |
| schemes | `/schemes` | Annotation scheme management |
| features | `/features` | Feature computation (TF-IDF, FastText, S-BERT) |
| models | `/models` | ML model training and prediction |
| generation | `/generation` | LLM prompting and batch generation |
| bertopic | `/bertopic` | Topic modeling |
| export | `/export` | Data export |
| files | `/files` | File uploads |
| elements | `/elements` | Retrieve elements to annotate |
| messages | `/messages` | In-app notifications |
| monitoring | `/monitoring` | System health metrics |


### Task queue

Long-running operations (model training, feature computation, projections, LLM batch calls) are executed asynchronously via a **Loky-based multiprocessing queue** (`queue_manager.py`). The queue separates CPU-bound and GPU-bound workers:

- **CPU workers** (default: 5): feature extraction, quick model training, projections.
- **GPU workers** (default: 1): BERT fine-tuning and prediction.


### Database layer

The database layer uses **SQLAlchemy ORM** with support for both SQLite (development/local) and PostgreSQL (Docker/production).

**Tables:**

| Table | Purpose |
|-------|---------|
| `users` | User accounts with hashed passwords |
| `projects` | Project metadata (parameters stored as JSON) |
| `schemes` | Annotation schemes per project |
| `annotations` | Individual annotations (user, element, label, optional text spans) |
| `auths` | Project-level access control (user-project-status mapping) |
| `features` | Feature metadata |
| `gen_models` | Generative model configurations |
| `prompts` | LLM prompt templates |
| `generations` | LLM generation results |
| `logs` | Action audit trail |
| `tokens` | API token management |
| `monitoring` | System metrics snapshots |


---

## Frontend (`frontend/src/`)

### Technology stack

| Layer | Technology |
|-------|------------|
| Framework | React 18 + TypeScript 5 |
| Build tool | Vite |
| UI library | React Bootstrap |
| State management | React Context + localStorage |
| Routing | React Router v6 (hash-based) |
| HTTP client | openapi-fetch (typed) + Axios |
| Data visualization | Sigma.js (graphs), Victory (charts), Plotly, ag-Grid (tables) |
| Text annotation | react-text-annotate-blend |


### API client generation

The frontend uses **auto-generated TypeScript types** from the backend's OpenAPI schema:

1. FastAPI generates an OpenAPI spec at `/openapi.json`.
2. `openapi-typescript` converts it to TypeScript definitions (`generated/openapi.d.ts`).
3. `openapi-fetch` provides a fully typed HTTP client.

Run `npm run generate` to regenerate types after backend changes.


## Deployment

### Docker Compose

The application ships with multiple Docker Compose configurations:

| File | Purpose |
|------|---------|
| `docker-compose.yml` | Base service definitions |
| `docker-compose.dev.yml` | Development overrides (hot reload, exposed ports) |
| `docker-compose.prod.yml` | Production settings |
| `docker-compose.nvidia.yml` | GPU support (NVIDIA runtime) |

**Services:**

- **PostgreSQL 15+**: production database.
- **API** (Python/uvicorn): backend server, dependencies installed via `uv`.
- **Frontend** (Node/Vite): SPA dev server or static build.
- **Nginx**: reverse proxy, serves static files, routes API traffic.
