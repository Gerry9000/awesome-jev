# S1Bench: Empirical Evaluation of 30 Jev Alternatives Against TypeSafe Jev

#### 1. Post & Repository Overview
* **Author**: Jake Cuth ([`@ItsCuthulhu`](https://x.com/ItsCuthulhu)), Georgia Tech Analytics Lead.
* **Project & Dashboard**: S1Bench Live Benchmark ([`bench.jakecuth.com`](http://bench.jakecuth.com)).
* **Canonical Threads**: [`https://x.com/ItsCuthulhu/status/2101491913866055821`](https://x.com/ItsCuthulhu/status/2101491913866055821) and [`https://x.com/ItsCuthulhu/status/2101387385871470637`](https://x.com/ItsCuthulhu/status/2101387385871470637).
* **Visual Telemetry**: 24 plotted candidate models across decisions/s vs macro accuracy on NVIDIA DGX Spark with real-time leaderboard tracking.

---

#### 2. Cognitive Architecture & Technical Mechanism
* **Benchmark Structure & Workload**:
  * Evaluates candidates across 1,999 decision tasks spanning 13 distinct problem subsets in the [`S1Bench Evaluation Dataset`](http://bench.jakecuth.com).
  * Records macro accuracy, inference latency (seconds per item), decision throughput (decisions/s on a logarithmic scale), and Expected Calibration Error (ECE).
  * Automated queue continuously ingests and runs candidates submitted by community practitioners on X.
* **Hardware & Runtime Environment**:
  * Runs on dedicated NVIDIA DGX Spark infrastructure supplemented by local GPU workers and CPU worker pools.
  * Evaluates both hosted API endpoints and local self-hosted weight configurations.
* **Candidate Taxonomy**:
  * **Frontier Anchor**: TypeSafe Jev 1.13.0 API evaluated across categorical choice sets up to K <= 255.
  * **Large Open-Weight Foundation Models**: `simplejev-qwen38-27b` and `simplejev-qwen36-35b-a3b` using non-autoregressive logit extraction heads.
  * **Distilled Small Fast Classifiers**: `Reflex-4b` (Apache 2.0, YannQi) and `Decider-2b` (Mapika, 2 B parameter base).
  * **Bidirectional Encoder Architectures**: `open-jev-deberta` (435 M weights) and `GLiNER` variants (`small` 74 M, `base` 194 M, `multi` 287 M).
  * **Historical Baselines**: `Laya` (MLX / GPU) and `Jeff` (400 M GLiFormer).

---

#### 3. Empirical Results & Economics
* **Accuracy vs Speed Frontier ([S1Bench Benchmark Telemetry](http://bench.jakecuth.com))**:
  * **TypeSafe Jev (Anchor)**: 77.5% macro accuracy at 2.4 decisions/s (0.42 s/item, ECE 0.076, 0 errors) per [`TypeSafe Jev API Benchmark`](https://docs.typesafe.ai/introduction).
  * **`simplejev-qwen38-27b`**: 75.8% macro accuracy at 1.6 decisions/s (0.61 s/item, ECE 0.121) per [`SimpleJev Qwen 3.8 27 B Benchmark`](https://huggingface.co/Qwen/Qwen3.8-27B). Requires 27 B parameters and substantial VRAM.
  * **`Reflex-4b`**: 72.0% macro accuracy at 10 decisions/s per [`Reflex-4B Evaluation Report`](https://huggingface.co/YannQi/R-4B). Delivers 2--3x higher throughput than Jev with an acceptable 5.5% accuracy delta under an Apache 2.0 license.
  * **`Decider-2b`**: 71.0% macro accuracy at 30 decisions/s per [`Decider-2B Benchmark Study`](https://huggingface.co/Mapika/decider-2b). Runs 10x faster than Jev, completing the entire 1,999-item test suite in roughly 4 minutes on local hardware.
  * **`open-jev-deberta`**: 52.4% macro accuracy at 37 decisions/s (0.03 s/item, ECE 0.067) per [`S1Bench Open DeBERTa Evaluation`](http://bench.jakecuth.com). High CPU throughput with a 25.1% accuracy collapse.
  * **`Laya`**: 62.5% macro accuracy on GB10 GPU hardware per [`Laya MLX Benchmark Baseline`](https://github.com/mizorewww/laya-mlx), trailing modern distilled alternatives in both speed and precision.
* **Economic Tradeoffs**:
  * No evaluated open-weight candidate currently surpasses TypeSafe Jev in both accuracy and speed simultaneously on the [`S1Bench Leaderboard`](http://bench.jakecuth.com).
  * For local workstations requiring privacy and zero API spend, `Decider-2b` and `Reflex-4b` offer the strongest Pareto efficiency.
  * For high-stakes production pipelines where decision accuracy below 70% is unacceptable per [`S1Bench Operational Guidelines`](http://bench.jakecuth.com), TypeSafe Jev remains the lowest-friction solution without cluster infrastructure costs.

---

#### 4. Visual Assets & Artifacts
* **Decisions/s vs Macro Accuracy Bubble Chart**: `media/s1bench-cuth-benchmark.webp` (high-resolution candidate matrix).
* **Live Telemetry Dashboard**: `media/s1bench-dashboard.webp` (progress tracker across running, done, and queued models).
* **Detailed Leaderboard Table**: `media/s1bench-leaderboard-table.webp` (exact macro accuracy, delta Jev, s/item, and ECE values).
