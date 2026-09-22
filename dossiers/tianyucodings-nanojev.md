# NanoJev: 0.6 B Parameter Open Jev Replica for Real-Time Edge Control

#### 1. Post & Repository Overview
* **Author**: Tianyu ([`@TianyuCodings`](https://x.com/TianyuCodings)), Machine Learning Systems Engineer.
* **Repository**: [`TianyuCodings/NanoJev`](https://github.com/TianyuCodings/NanoJev) *(Python, ⭐ 1,074)*.
* **Canonical Thread**: [`https://x.com/TianyuCodings/status/2100731234567890123`](https://x.com/TianyuCodings/status/2100731234567890123).
* **Demonstration Media**: Side-by-side benchmark comparison against untuned models and API backends (`media/nanojev-benchmark-motion.gif`).

---

#### 2. Cognitive Architecture & Technical Mechanism
* **Weight Distillation & Backbone**:
  * Distills non-generative choice heads into the open Qwen3-0.6B model architecture.
  * Trains on synthetic choice pairs to extract normalized probability distributions across arbitrary categorical options.
* **Prefill-Only Forward Pass**:
  * Evaluates structured context prompts in a single tensor forward pass without maintaining KV caches.
  * Discards autoregressive text decoding to guarantee sub-millisecond per-token processing overhead.
* **Edge Hardware Deployment**:
  * Runs fully offline on embedded robotics platforms, Apple Silicon M-series chips, and consumer GPUs with 4 GB VRAM.

---

#### 3. Empirical Results & Economics
* **Throughput & Latency**:
  * Sustains 256 decisions/s on local Apple Silicon hardware in the [`NanoJev Benchmark Report`](https://github.com/TianyuCodings/NanoJev).
  * Achieves 12--18 ms median latency per decision batch on local RTX 3060 GPUs.
* **Task Accuracy**:
  * Scored 91.2% success navigating dynamic procedural mazes without wall collisions.
* **Marginal Economics**:
  * Incurs $0.00 in ongoing API expenses with zero external network dependencies per the [`NanoJev Architecture Docs`](https://github.com/TianyuCodings/NanoJev).

---

#### 4. Visual Assets & Artifacts
* **Animated Evaluation Sequence**: `media/nanojev-benchmark-motion.gif` (live comparison of NanoJev versus untuned models).
* **Static Architecture Diagram**: `media/nanojev-benchmark-static.webp` (distillation loss and output tensor mapping).
