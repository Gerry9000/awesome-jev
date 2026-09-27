# SlopCheck: Hybrid AST & Semantic Code Review Pipeline

#### 1. Project & Creator Overview
* **Author**: TJ Klug ([`@tj_klug on X`](https://x.com/tj_klug/status/2100695837495992737))
* **Primary Language**: TypeScript / Node.js
* **Canonical Demonstration**: [`https://x.com/tj_klug/status/2100695837495992737`](https://x.com/tj_klug/status/2100695837495992737)
* **Visual Telemetry**: Pipeline architecture and GitHub Action workflow diagram (`media/slopcheck-code-review-pipeline.webp`)

---

#### 2. Cognitive Architecture & Technical Mechanism
* **Dual-Stage Review Funnel**:
  * **Stage 1 (Deterministic AST Filtering)**: Parses Git diffs using the TypeScript compiler API / Babel parser in sub-10 ms. Identifies changed function signatures, missing error handling branches, docstring modifications, and Cyclomatic Complexity hotspots.
  * **Stage 2 (Semantic Jev Scoring)**: Feeds extracted candidate AST nodes into TypeSafe Jev `score` and `choice` primitives to evaluate code quality, semantic regressions, and security anti-patterns without invoking expensive generative LLMs.
* **Reflex Decision Boundary**:
  * Replaces slow multi-second frontier model reviews (costing $0.05--$0.20 per file) with a single calibrated 42 ms evaluation.
  * Employs calibrated probability thresholds to flag PRs: blocks merges when quality scores fall below 0.75 or when refusal complements indicate hostile pattern matches.

---

#### 3. Empirical Results & Economics
* **Review Latency**: 42 ms end-to-end evaluation time per changed source file.
* **Token Overhead**: 0 generated output tokens, eliminating streaming latency and nondeterministic review comments.
* **Cost Efficiency**: Operates at $0.042 / M input tokens, achieving a ~120x cost reduction compared to GPT-4o / Claude 3.5 Sonnet PR review bots.
* **CI Integration**: Runs as a lightweight pre-commit hook and native GitHub Action gate with zero cloud dependency requirements when using local reflex models.

---

#### 4. Visual Assets & Artifacts
* **Pipeline Architecture**: `media/slopcheck-code-review-pipeline.webp` (AST extraction to Jev decision graph).
* **Thumbnail Asset**: `media/tjklug-slopcheck-thumb.webp`.
