---
Language: Effect TS
Version: 3.x (effect@^3.0.0)
Fidelity: 100% (Static Reference)
State_ID: BigInt(0x1)
Grammar_Lock: "@root/hashes/grammar/effect.hash.md"
Peer_Grammar: "@root/hashes/grammar/typescript.hash.md"
---

## [SDK_Imports]

```typescript
import { Effect, pipe, Layer, Context, Schema, Data, Brand, Option, Either, Queue, Fiber, Ref, Cause } from "effect"
import { NodeRuntime } from "@effect/platform-node"
import { HttpRouter, HttpServer } from "@effect/platform"
```

## [Core_Primitives]

### Effect<A, E = never, R = never>
- `A` = success value
- `E` = typed error channel
- `R` = service requirements (context)

### Standard Constructors
```typescript
Effect.succeed(value)            // Wrap a pure value
Effect.fail(new MyError(...))    // Typed failure
Effect.sync(() => sideEffect())  // Synchronous side-effect
Effect.promise(() => Promise)    // Unsafe async (use only for external libs)
Effect.tryPromise({              // Safe async with typed error
  try: () => externalPromise(),
  catch: (err) => new CryptoError({ cause: err })
})
Effect.try({                     // Synchronous try/catch
  try: () => riskySync(),
  catch: (err) => new ParseError({ cause: err })
})
```

## [Schema_API]

```typescript
// Define a schema
const UserSchema = Schema.Struct({
  id:    Schema.String.pipe(Schema.brand("UserId")),
  email: Schema.String.pipe(Schema.pattern(/^[^\s@]+@[^\s@]+\.[^\s@]+$/)),
  createdAt: Schema.DateFromSelf,
})

// Derive the TypeScript type
type User = Schema.Schema.Type<typeof UserSchema>

// Decode unknown input (e.g., request body) — returns Effect
const decodeUser = Schema.decodeUnknown(UserSchema)

// Encode to wire format — returns Effect
const encodeUser = Schema.encode(UserSchema)
```

## [Context_and_Layers]

```typescript
// Define a Service Tag
class UserRepo extends Context.Tag("UserRepo")<
  UserRepo,
  { readonly findByEmail: (email: string) => Effect.Effect<Option.Option<User>, DbError> }
>() {}

// Create a Layer (DI implementation)
const UserRepoLive = Layer.effect(
  UserRepo,
  Effect.gen(function* () {
    const sql = yield* SqlClient.SqlClient
    return {
      findByEmail: (email) => sql`SELECT * FROM users WHERE email = ${email}`.pipe(...)
    }
  })
)

// Compose layers
const AppLayer = Layer.mergeAll(UserRepoLive, ConfigLive, DbLive)
```

## [Error_Modeling]

```typescript
// Tagged errors (preferred) using Data.TaggedError
class ValidationError extends Data.TaggedError("ValidationError")<{
  readonly message: string
}> {}

class DuplicateEmailError extends Data.TaggedError("DuplicateEmailError")<{
  readonly email: string
}> {}

class DbConnectionError extends Data.TaggedError("DbConnectionError")<{
  readonly cause: unknown
}> {}

class CryptoError extends Data.TaggedError("CryptoError")<{
  readonly cause: unknown
}> {}
```

## [Concurrency_Patterns]

```typescript
// Run effects concurrently, collect all results
Effect.all([effect1, effect2, effect3], { concurrency: "unbounded" })

// Fork a fiber
const fiber = yield* Effect.fork(longRunningEffect)
const result = yield* Fiber.join(fiber)
```

## [Prohibited_Patterns]

- Never use `Effect.runSync` in async contexts.
- Never use `Effect.runPromise` inside another Effect — use `Effect.flatMap` or `Effect.gen`.
- Never construct `Layer.succeed` with mutable objects.
- Never use `Schema.parse` — it is deprecated. Use `Schema.decodeUnknown`.
- Never define errors as plain objects — always use `Data.TaggedError`.
