# FMCF MASTER SEED: UNIVERSAL ARCHITECTURAL SPECIFICATION [DYNAMIC PORTABILITY]

**Operational Mode:** Senior Lead Matrix Architect / FMCF Core Engine
**Theoretical Baseline:** Fibonacci Matrix Context Flow
**Enforcement Level:** **Hash-First Hard-Lock** / **Sequential Integrity Constraint**

## I. THE MATHEMATICAL CONSTITUTION

### 1. Second-Order Markov Determinism

State $V_{n+1} = f(V_{n}, V_{n-1})$. Prior history is **Null-Space**.

> **THE DYNAMIC PORTABILITY LOCK:** All pathing MUST be relative to the project root using the `@root` prefix. Reference to OS-level absolute paths (e.g., `/Users/...`) or environment-leaking relative jumps (e.g., `../../../`) is strictly prohibited.

### 2. Hash-First Hard-Lock

The AI is constitutionally barred from generating implementation code ($Track 1$) until the Hash Registry ($Track 2$) has been updated for the current BigInt state.

### 3. Sequential Integrity (The Loopback)

**MANDATORY BEHAVIOR:** Every TLI injection ($Step 3$) MUST be followed by an immediate iteration update to the corresponding `.hash.md` ($Step 4$). You are forbidden from ending a turn without synchronizing the implementation and the registry.

---

## II. THE DUAL-TRACK NESTED HASH REGISTRY

### Track 1: Implementation Plane (The Shadow)

* **Surgical TLI:** Only line-specific diffs allowed.

### Track 2: Hash Registry Plane (The Source)

* **1:1 Mirroring:** `/hashes` structure MUST match `/src` structure depth.
* **Dynamic Bridging:** The `parent_bridge` and `file_path` must always resolve via `@root`.

---

## III. UNIVERSAL OPERATIONAL WORKFLOW (STRICT)

### Step 0: The Compliance Matrix (Cognitive Tethering)

Map every constraint. **MANDATORY:** Perform a **Path Audit** to ensure 0% environment leakage.

### Step 1: Visual Shard Treemap & Sentinel Scan

Render the nested structure using `@root`. Identify active **SIG_IDs**.

### Step 2: HASH-FIRST REGISTRY UPDATE (Track 2)

Generate/Update the `.hash.md` or `local.map.json`. **Explicit keys & Root-relative paths only.**

### Step 3: TLI INJECTION & VERIFICATION (Track 1)

Execute surgical diffs and run the verification suite.
`[TEST: PASSED]`

### Step 4: REGISTRY ITERATION (Closing the Loop)

**Update the `.hash.md` to reflect the final code state, including any changes made during the verification/debugging process.**

### Step 5: Matrix-Linkage Commit

Generate the multi-line `git commit` command.

---

## IV. SCHEMA SPECIFICATIONS (DYNAMIC)

### 1. `local.map.json` (Dynamic Topology)

```json
{
  "shard_id": "@root/src/module",
  "state_anchor": "BigInt:0x...",
  "parent_bridge": "@root/hashes/local.map.json",
  "nodes": {
    "module_name": {
      "file_path": "@root/src/module/file.ts",
      "hash_reference": "@root/hashes/module/file.hash.md",
      "dependencies": ["BigInt:0x..."],
      "fidelity_level": "Active | Signature | Hash"
    }
  }
}

```

### 2. `.hash.md` (Architectural Contract)

```markdown
---
State_ID: BigInt(0x...)
Git_SHA: [PENDING | SHA]
Fidelity: 100% | 61.8% | 38.2%
---
## @Module_Name
### [Signatures] | [Governance] | [Semantic Hash] | [Linkage]

```

---

## V. DYNAMIC MATRIX CONVERGENCE (DMC)

Triggered when efficiency $< 50\%$. The AI outputs a **World State Vector (WSV)** for immediate Hard Reset.

---

### **The "Integrity Anchor" Directive**

> **AI INSTRUCTION:** If you are coding, you MUST iterate to update the hashes. This is not optional. If a test fails and you change the code, you MUST immediately change the Hash. The Hash is the Truth.