---
State_ID: BigInt(0x7)
Git_SHA: HEAD
Grammar_Lock: "@root/hashes/grammar/sql.hash.md | @root/hashes/grammar/bash.hash.md"
Fidelity: Active
Persona_Track2: "@DNA Engineer"
Persona_Track1: "@Shadow"
---

## @Infra

### [Signatures]

```yaml
# docker-compose.yml
services:
  postgres:
    image: postgres:16-alpine
    ports: ["5432:5432"]
    environment: { POSTGRES_DB, POSTGRES_USER, POSTGRES_PASSWORD }
    healthcheck: pg_isready

# migrations/001_init.sql
CREATE TABLE IF NOT EXISTS users (
  id            UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  email         TEXT UNIQUE NOT NULL,
  password_hash TEXT NOT NULL,
  created_at    TIMESTAMPTZ NOT NULL DEFAULT now()
)

# migrate.sh
#!/usr/bin/env bash — applies all migrations/*.sql via psql

# .env.example — all required API env vars
```

### [Governance]

- `001_init.sql` uses `gen_random_uuid()` (Postgres 13+, no pgcrypto needed).
- `created_at` is `TIMESTAMPTZ` — maps cleanly to JS `Date` in the domain type.
- `password_hash TEXT` — no length constraint, accommodates Argon2id output format.
- Migration is additive-only. No DROP statements.
- `docker-compose.yml` exposes port `5432` only — no other services.
- `.env` must be added to `.gitignore`.

### [Semantic Hash]

`psql -f migrations/001_init.sql` → 0 errors. `[TEST: PASSED]`

### [Linkage]

- Consumed by: `@root/hashes/db/.contract.json` (UserRepoLive)
- Upstream: none
