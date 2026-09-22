# Paweł Huryn's 50-Edge-Case Adversarial Invoice Benchmark

#### 1. Post & Repository Overview
* **Author**: Paweł Huryn ([`@PawelHuryn`](https://x.com/PawelHuryn)), Author of The Product Compass and Product Discovery Coach.
* **Repository**: [`phuryn/experiments`](https://github.com/phuryn/experiments) *(Python, ⭐ 52)*.
* **Canonical Thread**: [`https://x.com/PawelHuryn/status/2101213026204401921`](https://x.com/PawelHuryn/status/2101213026204401921).
* **Demonstration Media**: Infographic benchmark matrix comparing Jev against frontier LLMs across 50 deceptive documents (`media/pawel-huryn-invoice-benchmark.webp`).

---

#### 2. Cognitive Architecture & Technical Mechanism
* **Adversarial Test Corpus Construction**:
  * Curated 50 challenging enterprise invoices across six distinct document classifications.
  * 32 documents contain deliberate deceptive signals (proforma bills for goods already shipped, quotes labeled invoices, payment receipts).
  * Incorporates 10 languages, synthetic OCR transcription corruptions, written-out numbers, and informal email billing statements.
* **Zero-Definition Single-Pass Classification**:
  * Evaluates documents using TypeSafe Jev via the [`TypeSafe Jev API`](https://docs.typesafe.ai/introduction) with only category names and zero prompt definitions.
  * Extracts confidence probabilities to test calibration and uncertainty detection.

---

#### 3. Empirical Results & Economics
* **Accuracy Breakdown**:
  * **TypeSafe Jev**: 50/50 correct (100% accuracy) at $0.025 per 1,000 decisions in the [`Product Compass Invoice Benchmark`](https://productcompass.pm).
  * **Claude Haiku 4.5**: 50/50 correct at $0.39 per 1,000 decisions.
  * **Claude Opus 5**: 49/50 correct at $2.83 per 1,000 decisions.
  * **Gemini 3.8 Flash**: 49/50 correct at $1.03 per 1,000 decisions.
  * **GPT-OSS 20 B**: 48/50 correct at $0.030 per 1,000 decisions.
  * **Ministral 8 B**: 48/50 correct at $0.031 per 1,000 decisions.
* **Latency & Cost Multipliers**:
  * Jev achieved 30 ms response times with 0 output tokens.
  * Delivered a 113x cost reduction compared to Claude Opus 5 per the [`Invoice Cost Study`](https://github.com/phuryn/experiments).

---

#### 4. Visual Assets & Artifacts
* **Full Benchmark Infographic**: `media/pawel-huryn-invoice-benchmark.webp` (high-resolution model comparison matrix).
