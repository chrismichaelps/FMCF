Important: For better undestanding in how the effect library works check: `effect-library-lms-full.txt`

# 🚀 Technical Specification: Sentinel-Auth MVP (Effect Edition)

This MVP is designed to be a resilient, highly-typed authentication system that serves as the ultimate stress test for the **FMCF** framework.

## I. Infrastructure & Runtime (The DNA)

To ensure absolute environment parity, the following constraints are non-negotiable:

* **Runtime:** Node.js `v23.3.0` (Enforced via `nvm use v23.3.0`).
* **Package Manager:** `pnpm` (Leveraging workspaces for shared schema distribution).
* **Core Paradigm:** Functional Programming (FP) using **Effect TS**.
* **Database:** PostgreSQL `v16.x` (Local instance).

---

## II. The Effect Technology Stack

We bypass traditional "standard" libraries in favor of the **Effect Ecosystem** to ensure native integration and unified error handling:

* **Logic Engine:** `effect` (Core for fibers, dependency injection, and concurrency).
* **Data Modeling:** `import { Schema } from "effect"` (Single source of truth for TS types, runtime validation, and serialization).
* **API Layer:** `@effect/platform-node` or `Effect HTTP` (Composable, type-safe routing).
* **Database Access:** `Effect/Sql` (Postgres) or Prisma wrapped in an **Effect Layer**.
* **Frontend:** React `v18+` (Vite) + `@effect/platform-browser`.

---

## III. Data Architecture (Schema Shards)

In this MVP, we define the **Domain** via Schemas. These schemas act as the "Master Seed" for both the Backend and Frontend.

### 1. Identity Domain

* **User Schema:** Defines the core entity (`Id`, `Email`, `PasswordHash`, `CreatedAt`).
* **Branded Types:** We use Branded Types for `Id` (UUID) and `HashedPassword` to ensure they are never mixed with raw strings at the type level.

### 2. Transactional Schemas (The Wire)

* **`LoginPayload`**: Validates incoming raw JSON and transforms it into internal credentials.
* **`AuthResponse`**: A "Selective" schema that guarantees sensitive data (like `PasswordHash`) is **never** leaked to the client.

---

## IV. Functional Workflow (The Pipe Logic)

Business logic is defined as a series of pure transformations using `pipe`. This eliminates deeply nested `try/catch` blocks and provides explicit error channels.

### Sign-Up Logic Flow:

1. **Parse:** `Schema.decode` the request body.
2. **Verify:** Check for existing users via a `UserRepo` Tag.
3. **Hash:** Apply Argon2 hashing within an `Effect.try` block.
4. **Persist:** Atomically store the user in Postgres using `Effect/Sql`.
5. **Respond:** `Schema.encode` the result back to the public-facing DTO.

### Error Channels ($E$ in `Effect<R, E, A>`):

All failures are explicitly typed:

* `ValidationError`: Schema mismatch.
* `DuplicateEmailError`: DB constraint violation.
* `DbConnectionError`: Infrastructure failure.
* `CryptoError`: Failed hashing or signing.

---

## V. Project Structure (@root)

---

## VI. FMCF Integrity Audit Goals

By using `Effect`, we enable a higher level of **Forensic Auditing**:

1. **Strict Contract Enforcement:** If a schema in `packages/domain` changes, the `Effect` compiler will flag every broken service across the entire workspace.
2. **Dependency Transparency:** Every service explicitly lists its requirements (e.g., `UserRepo`, `Config`, `Clock`) in its type signature, making the **Impact Audit** in FMCF extremely precise.