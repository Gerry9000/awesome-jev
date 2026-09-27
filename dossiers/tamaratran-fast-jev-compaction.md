# Fast Jev Compaction: Neural Session Pruning & Architectural Traps

#### 1. Repository & Project Overview
* **Repository**: [`tamaratran/fast-jev-compaction`](https://github.com/tamaratran/fast-jev-compaction)
* **Author**: Tamara Tran ([`@tamaratran`](https://github.com/tamaratran))
* **Primary Language**: TypeScript (6,356 GitHub Stars)
* **Core Artifact**: [`Hermes-Agent PR #116246`](https://github.com/NousResearch/hermes-agent/pull/116246) evaluated by Nous Research
* **Visual Telemetry**: Real-world evaluation report and community critique (`media/teknium-compaction-tweet.webp`)

---

#### 2. Cognitive Architecture & Technical Mechanism
* **Context Pruning Engine**:
  * Evaluates sliding token windows of agent conversation history using TypeSafe Jev `choice` and `noul` primitives.
  * Designed to identify low-entropy terminal spam, verbose compiler stack traces, redundant file reads, and repetitive tool stdout.
  * Attempts to condense 32 k token agent trajectories down to under 8 k tokens in sub-50 ms passes without waiting for expensive frontier LLM summarization.
* **Primitive Invocation Profile**:
  * Employs categorical `choice` to classify conversation blocks into `essential_code`, `diagnostic_trace`, or `disposable_stdout`.
  * Invokes `noul` to gate irreversible pruning actions before committing edits to agent memory.

---

#### 3. Empirical Results & Community Controversy
* **Performance Telemetry**:
  * **Latency**: Sub-50 ms per window evaluation on standard CPU runtimes.
  * **Token Generation**: 0 generated output tokens, bypassing generative latency bottlenecks.
  * **Pricing**: Operating at baseline reflex tier ($0.042 / M input tokens).
* **The Context Compaction Anti-Pattern ([Nous Research Evaluation](https://github.com/NousResearch/hermes-agent/pull/116246))**:
  * While theoretically attractive, empirical audits by Teknium (Nous Research) revealed major architectural traps:
  * **Cache Invalidation Trap**: Dynamically editing or pruning prior conversation turns breaks prefix prompt caching across Claude, OpenAI, and DeepSeek. Rerunning full context without cache hits costs 4--10x more than preserving raw unpruned history.
  * **Information Loss on Edge Regressions**: Removing seemingly verbose compiler output often strips subtle environment details needed by later debugging passes.
  * **Rule Degeneration**: Complex heuristic compaction rules often degrade into brittle string matching rather than true semantic comprehension.

---

#### 4. Visual Assets & Artifacts
* **Nous Research Critique**: `media/teknium-compaction-tweet.webp` (analysis of session compaction risks and cache penalties).
* **Thumbnail Asset**: `media/tamaratran-fast-jev-compaction-thumb.webp`.
