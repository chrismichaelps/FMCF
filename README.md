
<p align="center">
  <img src="./public/fmcf_token_leakage_diagram.png" alt="FMCF Token Leakage Diagram" width="50%" />
</p>

<p align="center">Bounding LLM Context Toxicity: The Fibonacci
Matrix Context Flow (FMCF) for Infinite-Scale
Agentic Workflows</p>

> [Paper](https://github.com/chrismichaelps/FMCF/blob/main/Bounding_LLM_Context_Toxicity__The_Fibonacci_Matrix_Context_Flow__FMCF__for_Infinite_Scale_Agentic_Workflows.pdf)
> 


## FMCF Master Architectural Specification: [n=∞]

The FMCF Master Seed is the architectural root ($F_1$) that initializes a Large Language Model as a deterministic Matrix Engine rather than a chatbot. It enforces the mathematical laws of $\phi$-Bounded Pruning and the Dual-Track Hash Registry to ensure $O(1)$ token efficiency and infinite architectural scaling.

[FMCF Master Seed](https://github.com/chrismichaelps/FMCF/blob/main/FMCF-MASTER-SEED.md)


## The Token-Thrift Auditor

The **Token-Thrift Auditor** is a specialized sub-protocol within the FMCF designed to act as a "Financial Controller" for your agentic session. While the Master Seed sets the rules, the Auditor ensures those rules haven't "drifted" over time—saving you from the accidental context bloat that often happens during complex refactors.

[FMCF Token-Thrift Auditor](https://github.com/chrismichaelps/FMCF/blob/main/FMCF-TOKEN-THRIFT-AUDITOR-PROMPT.md)

## The High-Density Matrix-Linkage Commit Prompt

The **High-Density Matrix-Linkage Commit Prompt** is a specialized sub-protocol within the FMCF designed to act as a "Git Commit Generator" for your agentic session. While the Master Seed sets the rules, the Commit Generator ensures those rules haven't "drifted" over time—saving you from the accidental context bloat that often happens during complex refactors.

[FMCF High-Density Matrix-Linkage Commit Prompt](https://github.com/chrismichaelps/FMCF/blob/main/THE-FMCF-HIGH-DENSITY-MATRIX-LINKAGE-COMMIT-PROMPT.md)


### Bug in our codebase?
This is exactly where the **FMCF Matrix** proves its worth. If you don't know where the bug is, you don't guess—you initiate a **Matrix Search & Rescue**.

Since every file has a corresponding hash, you can tell the AI to act as an **Inspector** to find the "Fidelity Breach" across your entire state history.

---

 **DIRECTIVE: INITIATE MATRIX-WIDE FIDELITY AUDIT**
 
 **The Issue:** I am receiving `{"name": "chris"}` but the application expects `{"id": 1}`. I am unsure which state ID ($F_n$) or file contains this mismatch.

 **Task:**  1. **Scan the Registry:** Look through all `.hash.md` files and the `deps.map.json`.
 
 2. **Identify the Culprit:** Find any state ID that defines a `User` or `API Response` schema.
 
 3. **Trace the Leak:** Determine which state initialized the `id: number` assumption.
 
 4. **Report:** Tell me the exact **BigInt ID** and the file path where the reality (the API) and the Matrix (the code) have diverged.
 **Do not propose a fix yet. Just identify the corrupted State ID.**

---

## Output  Example

The [`hashes/`](https://github.com/chrismichaelps/FMCF/tree/main/hashes) folder in this repo was generated from the [Auth MVP](https://github.com/chrismichaelps/FMCF/blob/main/MVP.md) — a full-stack authentication system built with Effect TS, Postgres, and React 18.

### How it works in practice

**Session Zero — Bootstrap (F1)**

The first session is intentionally expensive. You trigger it with a single directive:

```
"Before starting any coding, press F1 and begin defining the hash folder."
```

The AI reads the FMCF Master Seed and your spec, then generates the entire `hashes/` scaffold — grammar shards, topology map, shard contracts, and logic blueprints — **before writing a single line of source code**. This is the one-time cost that eliminates all future redundancy.

```
hashes/
├── grammar/          ← Linguistic DNA (TypeScript, Effect, SQL, Bash rules)
├── local.map.json    ← Full project topology with fidelity levels
├── .atlas.graph      ← Dependency impact graph
├── .chronos.json     ← Temporal ledger of every change and why
├── domain/           ← Schema shard contracts
├── auth/             ← Service shard contracts
├── api/              ← HTTP layer contracts
└── db/               ← Database layer contracts
```

> [!NOTE]
> **Iterative Construction:** This structure is NOT generated in a single monolithic call. The AI builds it "1+1" — progressively scaffolding shards as the project evolves through Fibonacci states (F1 → F2 → ...). 


**Every subsequent session — O(1) continuation**

In any new session, the AI does **not** re-read your source code. It reads three core files:

| File | What it provides |
|------|-----------------|
| `hashes/local.map.json` | Current state anchor (`BigInt:0xN`), topology, and grammar refs |
| `hashes/.chronos.json` | Full history of *what* changed and *why* at each state |
| `hashes/grammar/*.hash.md` | Syntax rules and SDK patterns — no training-data drift |

This means the AI picks up exactly where it left off — even across sessions, days, or team members — without re-parsing thousands of lines of source.

**Parallel evolution — hashes and code stay in sync**

Every implementation step advances the state anchor and updates the corresponding `.hash.md`:

```
F1 → hashes/ scaffold only (no src/)           BigInt:0x1
F2 → packages/domain/src/index.ts              BigInt:0x2
F3 → packages/auth/src/AuthService.ts          BigInt:0x3
F4 → packages/db/ + packages/api/              BigInt:0x4
F5 → packages/client/ (React SPA)              BigInt:0x5
F6 → packages/infra/ (SQL migrations + Docker) BigInt:0x6
F7 → Forensic audit remediation                BigInt:0x7
```

**Starting a new session mid-project**

```
@FMCF-MASTER-SEED.md  @hashes/local.map.json  @hashes/.chronos.json

Continue from BigInt:0x7. Implement [next feature].
```

No source files required. The AI reconstructs the mental model from the registry alone.