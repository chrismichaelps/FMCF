### **The FMCF Token-Thrift Auditor Prompt**

Inject this prompt whenever the AI's responses become wordy, or if the "attention drift" begins to cause hallucinations.

---

 **DIRECTIVE: EXECUTE TOKEN-THRIFT AUDIT [Mode: Compression]**
 **Task:** Act as the **Matrix Controller**. Your objective is to audit the current session's token efficiency against the **FMCF $\mathcal{O}(1)$ Asymptotic Bounding Law**. You must treat every unnecessary token as a **System Leak**.
 **I. DENSITY REVIEW:**
 1. **$\phi$-Pruning Audit:** Verify that $F_{n-1}$ (Adjacency) and $F_{n-2}$ (Cold Storage) are properly decayed. Identify any @Module that is incorrectly maintaining 100% fidelity outside the **Active Delta**.
 2. **Null-Space Verification:** Ensure that conversational history prior to the last two states is being treated as **Null-Space** (ignored).
 3. **Pointer Check:** Identify repetitive logic that can be replaced by a `SIG_ID` or a Semantic Pointer.
 
 
 **II. OPTIMIZATION MANDATES:**
 * **Shorthand Enforcement:** Replace all descriptive prose about modules with `@Module` references and `SIG_ID` invariants.
 * **TLI Leak Detection:** Scan the last 3 generations for full-file re-writes or redundant "boilerplate" code. Flag violations.
 * **Shard Depth Sync:** Verify the `/hashes` treemap reflects mandatory nesting depth without overhead.
 
 
 **III. OUTPUT REQUIREMENTS (Audit Only):**
 1. **Token Efficiency Score (0-100%):** Based on the ratio of *Instructional Value* to *Token Count*.
 2. **The Treemap:** An ultra-minimalist treemap showing only the [A]ctive shard and parent pointers.
 3. **DMC Trigger Analysis:** Calculate current context volume $\tau$. If $\tau $ model threshold or efficiency $< 50\%$, output the **World State Vector (WSV)** for immediate Hard Reset.
 
 
 **DO NOT generate code. Perform ONLY the Audit. Acknowledge and proceed.**