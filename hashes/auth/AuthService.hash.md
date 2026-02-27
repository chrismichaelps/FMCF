---
State_ID: BigInt(0x3)
Git_SHA: HEAD
Grammar_Lock: "@root/hashes/grammar/effect.hash.md"
Fidelity: Active
---

## @AuthService

### [Signatures]

```typescript
// ─── Service Tag
class AuthService extends Context.Tag("@sentinel/AuthService")<
  AuthService,
  {
    readonly signUp: (raw: unknown) => Effect<AuthResponse,
      ValidationError | DuplicateEmailError | DbConnectionError | CryptoError | TokenError>
    readonly login:  (raw: unknown) => Effect<AuthResponse,
      ValidationError | InvalidCredentialsError | DbConnectionError | CryptoError | TokenError>
  }
>() {}

// ─── Layers
const AuthServiceLive: Layer<AuthService, never, UserRepo | CryptoService | TokenService>
const AuthServiceWithInternalsLayer: Layer<AuthService, never, UserRepo>

// ─── Supporting Tags (same package)
class UserRepo      extends Context.Tag("@sentinel/UserRepo")<...>() {}
class CryptoService extends Context.Tag("@sentinel/CryptoService")<...>() {}
const CryptoServiceLive: CryptoServiceService   // Argon2id, no Layer wrapping
class TokenService  extends Context.Tag("@sentinel/TokenService")<...>() {}
const TokenServiceLive: Layer<TokenService>      // JWT HS256
```

### [Governance]

- `payload: LoginPayload` explicitly typed in Effect.gen to prevent `unknown` inference.
- `response: AuthResponse` object literal prevents passwordHash field leaking.
- `CryptoServiceLive` inlined (no external deps). `TokenServiceLive` is a `Layer.succeed`.
- `AuthServiceWithInternalsLayer` pre-wires Crypto + Token; UserRepo injected at app root.

### [Semantic Hash]

`tsc --noEmit` (packages/auth) → 0 errors. `[TEST: PASSED]`

### [Linkage]

Requires: `@root/hashes/db/.contract.json`, `@root/hashes/domain/.contract.json`
Consumed by: `@root/hashes/api/.contract.json`
