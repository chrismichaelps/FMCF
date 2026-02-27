---
State_ID: BigInt(0x5)
Git_SHA: HEAD
Grammar_Lock: "@root/hashes/grammar/typescript.hash.md"
Fidelity: Active
---

## @Client

### [Signatures]

```typescript
// ─── API Client (src/api.ts)
type ApiError = { readonly status: number; readonly message: string }

const signUp: (email: string, password: string) => Promise<AuthResponse>
const login:  (email: string, password: string) => Promise<AuthResponse>
// Both throw ApiError on non-2xx responses

// ─── Auth State (src/store.ts)
type AuthState =
  | { readonly tag: "idle" }
  | { readonly tag: "authenticated"; readonly user: AuthResponse }

const useAuthStore: () => {
  state: AuthState
  setAuthenticated: (r: AuthResponse) => void
  logout: () => void
}

// ─── Components
const AuthForm: (props: {
  mode: "signup" | "login"
  onSuccess: (r: AuthResponse) => void
}) => JSX.Element

const App: () => JSX.Element
```

### [Governance]

- No Effect runtime imports — browser bundle uses plain fetch + async/await.
- `AuthResponse` imported as `type` only from `@sentinel/domain`.
- No default exports anywhere.
- Auth state is in-memory only (no localStorage) for MVP.
- All API errors surface as visible UI messages (no silent catch).
- Premium dark-mode glassmorphism UI with micro-animations.

### [Semantic Hash]

`tsc --noEmit` (packages/client) → 0 errors. `[TEST: PASSED]`

### [Linkage]

- Requires: `@root/hashes/domain/.contract.json`
- Upstream: `domain → client` (SCHEMA_CONTRACT, MEDIUM)
- Consumed by: End user (browser)
