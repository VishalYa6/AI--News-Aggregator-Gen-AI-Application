# AI News Aggregator

A lightweight news aggregation project that collects content from feeds and video transcripts, processes it with generative AI agents, stores results in a database, and can send digests via email.

**Key features**

- Feed & YouTube scraping
- Processing using configurable agents (curator, digest, email)
- PostgreSQL-backed storage via SQLAlchemy
- Docker Compose for local development

**Quick Links**

- Project root: `README.md`
- Main entrypoint: `main.py`
- App package: `app/` (configuration, runners, agents)
- Example env: `app/example.env`
- Docker Compose: `docker/docker-compose.yml`

**Requirements**

- Python: `>=3.12` (see `pyproject.toml`)
- PostgreSQL (for production/local DB)
- Optional: Docker & Docker Compose

**Install (local dev)**

1. Create a virtual environment and activate it:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

2. Install the project in editable mode:

```powershell
pip install -e .
```

3. Install any dev dependencies (optional):

```powershell
pip install -r requirements-dev.txt  # if you create one
```

**Configuration**

- Copy `app/example.env` to `.env` (or set environment variables directly). This file contains placeholders for API keys (OpenAI/Anthropic), database URL, and email settings.
- The app loads configuration from `app/config.py` (which reads env vars). Review that file to see all configurable keys.

**Running**

- Run the main script:

```powershell
python main.py
```

- Run a specific runner from the `app` package (example):

```powershell
python -m app.daily_runner
```

**Docker (local)**

- Start services with Docker Compose:

```powershell
docker compose -f docker\docker-compose.yml up --build
```

- Tear down:

```powershell
docker compose -f docker\docker-compose.yml down
```

**Project Layout (brief)**

- `app/`
  - `config.py` - configuration loading
  - `runner.py`, `daily_runner.py` - orchestrators for scheduled runs
  - `agent/` - agent implementations (`curator_agent.py`, `digest_agent.py`, `email_agent.py`)
  - `database/` - connection, models, repository helpers
  - `scrapers/` - scraping/adapters for OpenAI, Anthropic, YouTube
  - `services/` - processing helpers (email, digest, etc.)
- `docker/` - compose files and Docker-related config

**Development notes**

- Database schema: see `app/database/create_tables.py` and `app/database/models.py`.
- Environment variables are critical for API keys and DB connections. Never commit secrets.
- If you add automated tests, a suggested layout is `tests/` with pytest and a `requirements-dev.txt`.

**Next steps / suggestions**

- Add a `requirements-dev.txt` and CI configuration for linting/tests.
- Add example `.env` values (redacted) in `app/example.env` for clearer onboarding.
- Add a small script to seed the DB for local development.

**License**

This project currently has no license file. Add a `LICENSE` if you wish to set terms.

---

If you'd like, I can:
- Add badges (build/test) and a `Contributing` section.
- Create a `requirements-dev.txt` and basic `pytest` setup.
- Add a LICENSE (MIT/Apache) template.

