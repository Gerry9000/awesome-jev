# Laya MLX: Sub-35 ms Local Decision Engine on Apple Silicon

#### 1. Post & Repository Overview
* **Author**: Mizore ([`@mizorewww`](https://x.com/mizorewww)), Systems and MLX Framework Researcher.
* **Repository**: [`mizorewww/laya-mlx`](https://github.com/mizorewww/laya-mlx) *(Python)*.
* **Canonical Thread**: [`https://x.com/mizorewww/status/2100761234567890123`](https://x.com/mizorewww/status/2100761234567890123).
* **Demonstration Media**: Apple Silicon benchmark playback clip (`media/laya-mlx-benchmark.gif`).

---

#### 2. Cognitive Architecture & Technical Mechanism
* **Apple Silicon MLX Acceleration**:
  * Implements the Laya non-autoregressive decision architecture natively in Apple's MLX machine learning framework.
  * Exploits unified memory architecture (UMA) across CPU and Metal GPU cores, avoiding PCI-e tensor transfer bottlenecks.
* **Logit Extraction & Parallel Choice Scoring**:
  * Takes unstructured text contexts paired with discrete choice lists.
  * Extracts normalized categorical logit tensors in a single forward pass without autoregressive token generation.
  * Operates completely air-gapped and local on MacBook Pro and Mac Studio hardware.
* **Historical S1 Precursor**:
  * Serves as an early open-source benchmark for non-generative classification, preceding recent distilled System One models.

---

#### 3. Empirical Results & Economics
* **Inference Speed & Throughput**:
  * Sustains 34.8 ms end-to-end latency and 11.4 decisions/s on Apple M3 Max hardware per the [`Laya MLX Benchmark Suite`](https://github.com/mizorewww/laya-mlx).
  * Evaluated on NVIDIA GB10 GPUs in [`Jake Cuth's S1Bench Benchmark Suite`](http://bench.jakecuth.com), achieving 62.5% macro accuracy.
* **Resource Consumption**:
  * Requires under 4 GB unified memory footprint during active inference batches.
* **Marginal Cost**:
  * $0.00 per decision with 0 generated output tokens, enabling local embedded applications and offline robotics.

---

#### 4. Visual Assets & Artifacts
* **Animated MLX Benchmark**: `media/laya-mlx-benchmark.gif` (real-time Apple Silicon execution and latency profile).
