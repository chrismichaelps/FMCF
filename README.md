
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