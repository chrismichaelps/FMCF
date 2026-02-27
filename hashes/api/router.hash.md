---
State_ID: BigInt(0x1)
Git_SHA: HEAD
Grammar_Lock: "@root/hashes/grammar/effect.hash.md"
Fidelity: Signature
---

## @AppRouter

### [Signatures]

```typescript
// HTTP Router using @effect/platform HttpRouter
const AppRouter: HttpRouter.HttpRouter<AuthService>

// POST /auth/signup
// body: LoginPayload (Schema validated)
// response 201: AuthResponse
// response 400: ValidationError JSON
// response 409: DuplicateEmailError JSON

// POST /auth/login
// body: LoginPayload (Schema validated)
// response 200: AuthResponse
// response 400: ValidationError JSON
// response 401: InvalidCredentialsError JSON

// Live Layer
const AppRouterLive: Layer.Layer<HttpServer.HttpServer, never, AuthService>
```

### [Governance]

- All request bodies are decoded via `Schema.decodeUnknown` before reaching handler logic.
- All error types are mapped to HTTP status codes in a centralized error handler.
- No business logic in route handlers — delegate to `AuthService`.

### [Linkage]

- Requires: `@root/hashes/auth/.contract.json`
- Consumed by: entry point `server.ts`
