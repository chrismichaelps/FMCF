---
Language: TypeScript
Version: 5.x
Fidelity: 100% (Static Reference)
State_ID: BigInt(0x1)
Grammar_Lock: "@root/hashes/grammar/typescript.hash.md"
---

## [Syntax_Rules]

- **Strict Mode:** Always enable `"strict": true`, `"exactOptionalPropertyTypes": true`, `"noUncheckedIndexedAccess": true` in `tsconfig.json`.
- **No `any`:** Forbidden. Use `unknown` and narrow via type guards.
- **No Non-Null Assertions (`!`):** Forbidden unless immediately preceded by a type guard that proves safety.
- **No Default Exports:** All exports are named. `export { Foo }` only.
- **No Mutations:** All data structures are `readonly` or `as const`. Prefer `Readonly<T>` and `ReadonlyArray<T>`.
- **Functional Composition over Classes:** Pure functions and `pipe` are preferred. Classes are only allowed for `Context.Tag` extensions in Effect.
- **Named Imports Only:** `import { Effect, pipe, Schema } from "effect"` — never `import * as`.
- **No `namespace` blocks:** Use module-level exports instead.

## [Naming_Conventions]

- **Types/Interfaces:** PascalCase (`UserSchema`, `LoginPayload`).
- **Functions/Variables:** camelCase (`parseUser`, `authService`).
- **Constants:** UPPER_SNAKE_CASE for top-level primitives (`MAX_RETRY_COUNT`), or camelCase if typed object.
- **Files:** kebab-case (`auth-service.ts`) for utilities; PascalCase for Effect `Layer`/`Service` files (`AuthService.ts`).

## [Import_Order]

1. Node built-ins (`node:fs`, `node:crypto`)
2. Effect ecosystem (`effect`, `@effect/platform-node`)
3. Internal packages (`@sentinel/domain`, `@sentinel/auth`)
4. Relative imports (`./utils`)

## [Prohibited_Patterns]

- `as any` — forbidden.
- `// @ts-ignore` — forbidden. Use `// @ts-expect-error` with a justification comment if absolutely necessary.
- `Object.assign` for merging — use spread `{ ...a, ...b }` or Effect data structures.
- `Promise` chains (`.then`, `.catch`) — wrap in `Effect.tryPromise` instead.
- Nested `try/catch` — all errors must flow through the `E` channel of `Effect<R, E, A>`.

## [Standard_Library_Signatures]

```typescript
// Correct pipe usage
pipe(value, transform1, transform2)

// Correct Effect.gen usage
Effect.gen(function* () {
  const result = yield* someEffect
  return result
})

// Schema decode (runtime validation)
Schema.decodeUnknown(MySchema)(rawInput)

// Schema encode (serialize to wire format)
Schema.encode(MySchema)(typedValue)

// Branded type construction
import { Brand } from "effect"
type UserId = string & Brand.Brand<"UserId">
const UserId = Brand.nominal<UserId>()
```
