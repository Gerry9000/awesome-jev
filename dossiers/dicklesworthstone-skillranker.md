# SkillRanker: Jev-Powered Dynamic Skill and Tool Ranking in Rust

#### 1. Post & Repository Overview
* **Author**: Jeffrey Emanuel ([`@Dicklesworthstone`](https://github.com/Dicklesworthstone)), Systems Architect and AI Tooling Engineer.
* **Repository**: [`Dicklesworthstone/skillranker`](https://github.com/Dicklesworthstone/skillranker) *(Rust, ⭐ 61)*.
* **Demonstration Media**: Terminal TUI displaying ranked skill lists and token savings telemetry (`media/skillranker-terminal-tui.webp`).

---

#### 2. Cognitive Architecture & Technical Mechanism
* **Context Overload Problem in Coding Agents**:
  * Modern autonomous agents maintain dozens of skills and tool schemas, often consuming 15,000+ system prompt tokens before user interaction begins.
  * Ingesting the entire skill catalog on every turn degrades reasoning accuracy and balloons API costs.
* **Jev-Powered Dynamic Triage Engine**:
  * SkillRanker parses incoming user prompts and scores skill relevance using TypeSafe Jev via the [`TypeSafe API`](https://docs.typesafe.ai/introduction).
  * Evaluates candidate skills across categorized relevance brackets in sub-5 ms without generative decoding.
  * Injects only the top 3--5 relevant skill descriptions into the active prompt window.

---

#### 3. Empirical Results & Economics
* **Context Token Reduction**:
  * Slashes prompt token overhead by more than 80% across 500 test scenarios in the [`SkillRanker Benchmark`](https://github.com/Dicklesworthstone/skillranker).
* **Execution Throughput**:
  * Rust binary evaluates prompt-to-skill matching in sub-5 ms with negligible memory overhead.
* **Operational Savings**:
  * Saves $0.02--$0.08 per conversational turn on frontier model inference while Jev evaluation costs under $0.00004 per ranking cycle per the [`Context Optimization Study`](https://github.com/Dicklesworthstone/skillranker).

---

#### 4. Visual Assets & Artifacts
* **Terminal TUI Interface**: `media/skillranker-terminal-tui.webp` (Rust ratatui interface showing ranked skill distributions).
