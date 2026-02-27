---
State_ID: BigInt(0x1)
Git_SHA: HEAD
Grammar_Lock: "@root/hashes/grammar/effect.hash.md"
Fidelity: Signature
---

## @UserRepo

### [Signatures]

```typescript
// Service Tag
class UserRepo extends Context.Tag("UserRepo")<
  UserRepo,
  {
    readonly findByEmail: (email: string) => Effect.Effect<
      Option.Option<User>,
      DbConnectionError
    >
    readonly create: (data: {
      email: string
      passwordHash: HashedPassword
    }) => Effect.Effect<
      User,
      DbConnectionError | DuplicateEmailError
    >
  }
>() {}

// Live Layer (backed by Effect/Sql + Postgres)
const UserRepoLive: Layer.Layer<
  UserRepo,
  never,
  SqlClient.SqlClient
>
```

### [Governance]

- All SQL is parameterized — no string interpolation.
- `create` handles the DB unique-constraint violation and maps it to `DuplicateEmailError`.
- Returned `User` objects are always decoded through `UserSchema`.

### [Linkage]

- Requires: `@root/hashes/domain/.contract.json` (for `User` type and `UserSchema`)
- Consumed by: `@root/hashes/auth/.contract.json`
