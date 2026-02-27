---
Language: PostgreSQL
Version: 16.x
Fidelity: 100% (Static Reference)
State_ID: BigInt(0x7)
Grammar_Lock: "@root/hashes/grammar/sql.hash.md"
---

## [Syntax_Rules]

- **Idempotency:** All DDL MUST use `CREATE TABLE IF NOT EXISTS`, `CREATE INDEX IF NOT EXISTS`.
- **No DROP:** DROP TABLE / DROP COLUMN forbidden in forward migrations. Additive-only.
- **UUID Primary Keys:** Always use `gen_random_uuid()` (built-in since PG 13 — no pgcrypto needed).
- **Timestamps:** Always `TIMESTAMPTZ NOT NULL DEFAULT now()` — never bare `TIMESTAMP`.
- **Text over VARCHAR:** Use `TEXT` for unbounded strings. `VARCHAR(n)` only when constraint is a schema invariant.
- **Named constraints:** All `UNIQUE` and `CHECK` constraints must be named for safe future drops.
- **`ON_ERROR_STOP=1`:** All psql migrations MUST set this flag — no partial applies.

## [Column Naming Convention]

- **snake_case** for all column names (`password_hash`, `created_at`).
- **`_at` suffix** for timestamps (`created_at`, `updated_at`, `deleted_at`).
- **`_id` suffix** for foreign keys (`user_id`, `account_id`).

## [Standard Table Pattern]

```sql
CREATE TABLE IF NOT EXISTS entity_name (
  id         UUID        PRIMARY KEY DEFAULT gen_random_uuid(),
  -- domain columns
  created_at TIMESTAMPTZ NOT NULL DEFAULT now(),
  updated_at TIMESTAMPTZ NOT NULL DEFAULT now()
);

CREATE UNIQUE INDEX IF NOT EXISTS entity_name_lookup_idx ON entity_name (lookup_column);
```

## [Prohibited_Patterns]

- `SERIAL` or `BIGSERIAL` — use `UUID` with `gen_random_uuid()`.
- `TIMESTAMP` without timezone — always `TIMESTAMPTZ`.
- Inline `UNIQUE` on column definition without a named constraint.
- `DROP TABLE`, `DROP COLUMN`, `TRUNCATE` in migration files.
- Raw `psql` without `--set ON_ERROR_STOP=1`.

## [Standard_Library_Signatures]

```sql
-- UUID generation (PG 13+, no extension needed)
gen_random_uuid()

-- Current timestamp
now()

-- Existence check (used in DO $$ blocks for post-migration validation)
SELECT 1 FROM information_schema.tables
  WHERE table_schema = 'public' AND table_name = 'target'

-- Unique violation code (referenced in application layer)
-- SQLSTATE: 23505
```
