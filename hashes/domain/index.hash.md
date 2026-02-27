---
State_ID: BigInt(0x2)
Git_SHA: HEAD
Grammar_Lock: "@root/hashes/grammar/effect.hash.md"
Fidelity: Active
---

## @Domain

### [Signatures]

```typescript
// ─── Branded Types ────────────────────────────────────────────────────────
type UserId = string & Brand.Brand<"UserId">
const UserId: Brand.BrandConstructor<UserId>

type HashedPassword = string & Brand.Brand<"HashedPassword">
const HashedPassword: Brand.BrandConstructor<HashedPassword>

type JwtToken = string & Brand.Brand<"JwtToken">
const JwtToken: Brand.BrandConstructor<JwtToken>

// ─── Schemas ──────────────────────────────────────────────────────────────
const UserSchema: Schema.Struct<{
  id: Schema.brand<Schema.Schema<string>, "UserId">
  email: Schema.filter<Schema.Schema<string>>       // /email regex + minLength(1)
  passwordHash: Schema.brand<Schema.Schema<string>, "HashedPassword">
  createdAt: Schema.Schema<Date>
}>
type User = Schema.Schema.Type<typeof UserSchema>

const LoginPayload: Schema.Struct<{
  email: Schema.filter<Schema.Schema<string>>
  password: Schema.filter<Schema.Schema<string>>    // minLength(8)
}>
type LoginPayload = Schema.Schema.Type<typeof LoginPayload>

const AuthResponse: Schema.Struct<{
  id: Schema.brand<Schema.Schema<string>, "UserId">
  email: Schema.Schema<string>
  token: Schema.brand<Schema.Schema<string>, "JwtToken">
  createdAt: Schema.Schema<Date>
}>
type AuthResponse = Schema.Schema.Type<typeof AuthResponse>

// ─── Errors ───────────────────────────────────────────────────────────────
class ValidationError        extends Data.TaggedError("ValidationError")<{ message: string; field?: string }> {}
class DuplicateEmailError    extends Data.TaggedError("DuplicateEmailError")<{ email: string }> {}
class InvalidCredentialsError extends Data.TaggedError("InvalidCredentialsError")<{}> {}
class DbConnectionError      extends Data.TaggedError("DbConnectionError")<{ cause: unknown }> {}
class CryptoError            extends Data.TaggedError("CryptoError")<{ cause: unknown }> {}
class TokenError             extends Data.TaggedError("TokenError")<{ cause: unknown }> {}
```

### [Governance]

- `AuthResponse` structurally excludes `passwordHash` (independent struct, not a pick).
- Errors defined here to prevent circular imports.
- `Data.TaggedError` enables exhaustive `Match` via `_tag` discriminant.

### [Semantic Hash]

Verification: `tsc --noEmit` → 0 errors. `[TEST: PASSED]`

### [Linkage]

Consumed by: `@root/hashes/auth/.contract.json`, `@root/hashes/api/.contract.json`, `@root/hashes/db/.contract.json`
