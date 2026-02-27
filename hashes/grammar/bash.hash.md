---
Language: Bash
Version: 5.x (POSIX-compatible)
Fidelity: 100% (Static Reference)
State_ID: BigInt(0x7)
Grammar_Lock: "@root/hashes/grammar/bash.hash.md"
---

## [Syntax_Rules]

- **Strict mode mandatory:** Every script MUST begin with `set -euo pipefail`.
  - `-e` exit on error
  - `-u` exit on unbound variable
  - `-o pipefail` exit on pipe failure
- **`#!/usr/bin/env bash`:** Always use env-resolved shebang. Never `/bin/bash` (non-portable).
- **Double-quote all variables:** `"${VAR}"` not `$VAR` — prevents word splitting.
- **`SCRIPT_DIR` pattern:** Resolve script directory relative to itself, not CWD.
- **No `cd` without error handling:** `cd /some/dir || exit 1`.

## [Naming_Conventions]

- **Environment variables:** `UPPER_SNAKE_CASE` (e.g. `PGHOST`, `JWT_SECRET`).
- **Local variables:** `lower_snake_case`.
- **Functions:** `lower_snake_case_verb_noun`.

## [Standard_Patterns]

```bash
#!/usr/bin/env bash
set -euo pipefail

# Resolve script directory
SCRIPT_DIR="$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)"

# Safe default with override
VAR="${ENV_VAR:-default_value}"

# Iterate files safely
for file in "${DIR}"/*.sql; do
  [[ -f "${file}" ]] || continue   # skip if glob matches nothing
  process "${file}"
done

# Export sensitive values via env, never echo
export PGPASSWORD
```

## [Prohibited_Patterns]

- `#!/bin/bash` — not portable across macOS/Linux.
- `$VAR` without quotes — word splitting hazard.
- `ls | grep` — use `find` or glob patterns.
- `echo ${SECRET}` — never echoes credentials to stdout.
- Scripts without `set -euo pipefail`.
