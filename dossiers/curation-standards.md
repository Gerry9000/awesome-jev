# Curation Standards: The Three-Prong Enhancement Architecture

This document formalizes the editorial, architectural, and empirical standards required for all entries within **Awesome Jev & Fast Classifiers**.

---

## 1. Architectural Philosophy

Standard "awesome lists" frequently degenerate into unvetted link dumps where broken repositories, abandoned experiments, and generic wrappers sit alongside production breakthroughs.

This directory enforces an empirical, three-prong evaluation standard for every curated item. Rather than merely listing a GitHub link and a brief blurb, every entry must demonstrate:
1. **Verifiable Identity & Technical Mechanism** (Prong 1)
2. **Measured Economics & Performance Results** (Prong 2)
3. **Social Media Validation & Interactive Visual Demonstrations** (Prong 3)

---

## 2. The Three Prongs Detailed

### Architectural Tiers of Decision Systems

To preserve empirical rigor while reflecting real-world engineering architectures, entries belong to one of three tiers:

- **Tier 1: Pure Reflex Classifiers (Zero-Token / Sub-50 ms):** Single forward pass emitting probability tensors, categorical scores, or logit heads directly (`choice`, `noul`, `score`, ModernBERT, SetFit). Strict 0-token output budget and sub-50 ms latency.
- **Tier 2: Bounded-Thinking Classifiers (Thinking Budget / Micro-Reasoning):** Small language models operating under strict thinking-budget caps (<= 256 tokens) to resolve ambiguity before emitting a categorical choice.
- **Tier 3: Dual-Process Orchestrations (System 1 + System 2):** Asymmetric pipelines where a fast reflex classifier acts as a high-frequency supervisor or router alongside a frontier reasoning model.

### Prong 1: Repository Identity, Codebase & Mechanism
- **Canonical Repository Link**: Full URL to the public code repository or production SaaS endpoint.
- **Language & Star Count**: Standardized badge: `*(Language, ⭐ N)*`.
- **Classification Mechanism**: The description must explain the concrete classification or decision mechanism:
  - What state or context is fed to the model (DOM tree, git diff, video transcript, game state, AST).
  - Which typed primitive or representation head is evaluated (`noul` boolean, `choice` categorical, `score` rubric, or ModernBERT logit).
  - How downstream software consumes the typed probability tensor without arbitrary text parsing.
- **Strict Inclusion Gate**: Only genuine classification engines, System One models, and typed probability systems qualify. Unfiltered conversational chatbots, generic wrappers, and unstructured text generation are excluded.

### Prong 2: Quantitative Results, Throughput & Economics
- **Latency Profile**: Verified inference latency in milliseconds (`sub-20 ms`, `28 ms`, `12--50 ms`).
- **Throughput & Frame Rates**: Measured in `FPS` (e.g. `60 FPS`), `decisions/s`, or operations per minute.
- **Token Budget**: Documented output budget (0 generated tokens for Tier 1; explicit thinking budget <= 256 tokens for Tier 2).
- **Cost Economics**: Exact per-decision or volume pricing (`$0.042 / M input`, `$0.025 / 1k decisions`, `$0.0003/page`, `$0.00004/eval`, or `$0.00 marginal cost` on self-hosted local weights).
- **Comparative Advantage**: Quantified multiplier against generative LLMs (e.g. 130x cheaper, 95% latency reduction, $0.92 vs $430+ on GPT-4o).

### Prong 3: Social Media Validation & Expandable Pop-out Visual Preview
- **Canonical Social Thread**: Where available, link directly to the primary author announcement or technical teardown thread on X (Twitter):
  `&middot; [🐦 Thread](https://x.com/...)`
- **Pop-out Expandable Preview**: For featured entries with visual or video demonstrations, provide a native HTML `<details>` accordion:
  ```markdown
  <details>
  <summary><img src="media/<slug>-thumb.webp" height="20" align="absmiddle" alt="preview thumbnail"> 🎬 <b>View Demo</b> <i>(Click to pop out full size)</i></summary>
  <p align="center">
    <a href="<canonical-url>" target="_blank" rel="noopener noreferrer">
      <img src="media/<slug>.<gif|webp>" alt="<Description>" width="680">
    </a>
  </p>
  </details>
  ```
- **Popout Navigation Anchor**: Prepend an anchor tag before language: `<a href="#demo-<slug>" title="Jump to visual teardown">🎬</a>`.

---

## 3. Tooling & Verification Workflow

1. **Browser Metadata Audit**:
   - Audits repository health, verifies active star counts, and confirms live web application availability.
2. **Social Media Thread Validation**:
   - Validates canonical author announcement threads and primary technical demonstrations.
3. **Automated Quality Gates**:
   - Enforces table of contents anchor integrity, media asset availability, and copyediting standards.
