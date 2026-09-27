# Open-Jev: Architecture, S1Bench Pareto Frontiers, and Local Weight Reproductions

## 1. Executive Overview

TypeSafe Jev is a proprietary System One foundation model evaluated via cloud API. In response, open-source researchers have developed **Open-Jev reproductions**. These models provide fast, non-generative decision layers for offline environments, air-gapped robotics, and edge computing.

These open-weight alternatives replace conversational token generation with single-pass logit extraction across three core primitives:
- `choice`: Multi-class categorical decision from candidate options.
- `noul`: Binary proposition evaluation with calibrated truth probability.
- `score`: Continuous or ordinal rubric rating on discrete scales.

This document synthesizes empirical benchmarks, architectural approaches, local deployment patterns, and operational tradeoffs for open reproductions.

---

## 2. S1Bench Leaderboard: Accuracy vs. Speed Frontier

The following empirical measurements are derived from Jake Cuth's independent [`S1Bench Evaluation Dataset`](http://bench.jakecuth.com) (1,999 decisions across 13 problem sets on dedicated NVIDIA DGX Spark hardware) and local Apple Silicon testing.

| Model / Reproduction | Architecture | Macro Accuracy | Throughput | Inference Latency | Calibration Error (ECE) | License |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TypeSafe Jev 1.13.0** | Proprietary Anchor | **[77.5%](https://docs.typesafe.ai/introduction)** | 2.4 dec/s | 420 ms (cloud) | **0.076** | Proprietary API |
| **`simplejev-qwen38-27b`** | Qwen 2.5 27 B Base | [75.8%](https://huggingface.co/Qwen/Qwen3.8-27B) | 1.6 dec/s | 610 ms | 0.121 | Apache 2.0 |
| **`Reflex-4b` (YannQi)** | Distilled 4 B Base | [72.0%](https://huggingface.co/YannQi/R-4B) | 10.0 dec/s | 100 ms | 0.098 | Apache 2.0 |
| **`Decider-2b` (Mapika)** | Distilled 2 B Base | [71.0%](https://huggingface.co/Mapika/decider-2b) | 30.0 dec/s | 33 ms | 0.114 | Open Weights |
| **`daseinlabs/open-jev`** | Apple Silicon MLX | [68.4%](https://github.com/daseinlabs/open-jev) | 45.0 dec/s | 22 ms | 0.135 | MIT |
| **`Verdict-open-jev`** | WebGPU Non-autoregressive | [66.2%](https://github.com/Heman10x-NGU/Verdict-open-jev) | 28.0 dec/s | 35 ms | 0.108 | Apache 2.0 |
| **`open-jev-deberta`** | DeBERTa-v3 435 M | [52.4%](http://bench.jakecuth.com) | 37.0 dec/s | 27 ms | 0.067 | MIT |

---

## 3. Four Dominant Architectural Strategies

Community reproductions implement one of four distinct engineering patterns:

### Pattern A: Non-Autoregressive Logit Extraction (Qwen / LLaMA Bases)
- **Examples**: `simplejev-qwen38-27b`, `Reflex-4b`.
- **Mechanism**: Passes prompt state and options through transformer layers in a single forward pass. Evaluates softmax probabilities directly over option token identifiers (e.g. tokens `A`, `B`, `C` or option strings).
- **Strengths**: Achieves accuracy between 72.0% and 75.8% per [`Reflex-4b Evaluation Benchmark`](https://github.com/Gerry9000/awesome-jev/blob/main/dossiers/cuth-s1bench.md) and [`Qwen Benchmark Dataset`](https://github.com/QwenLM/Qwen), closely tracking proprietary Jev.
- **Weaknesses**: Requires substantial GPU VRAM (4 GB to 32 GB).

### Pattern B: Apple Silicon Unified Memory MLX (`daseinlabs/open-jev`)
- **Examples**: `daseinlabs/open-jev`, `mizorewww/laya-mlx`.
- **Mechanism**: Built directly on Apple MLX. Uses unified memory on M-series chips to eliminate PCIe transfer overhead.
- **Strengths**: Delivers sub-25 ms latency on MacBook Pro hardware without cloud network calls per [`daseinlabs/open-jev Benchmark`](https://github.com/daseinlabs/open-jev).
- **Weaknesses**: Restricted to Apple hardware platforms.

### Pattern C: Bidirectional Encoders (`open-jev-deberta`)
- **Examples**: `open-jev-deberta`, `GLiNER-bi-encoder`.
- **Mechanism**: Uses DeBERTa-v3 cross-attention encoders to compute sequence similarity against candidate choice labels.
- **Strengths**: Extremely low calibration error (ECE 0.067) and high CPU throughput.
- **Weaknesses**: Macro accuracy falls to 52.4% on complex multi-variable reasoning tasks per [`S1Bench Open DeBERTa Evaluation Benchmark`](https://github.com/Gerry9000/awesome-jev/blob/main/dossiers/cuth-s1bench.md).

### Pattern D: In-Browser WebGPU Non-Autoregressive Engines (`Verdict-open-jev`)
- **Examples**: `Heman10x-NGU/Verdict-open-jev`.
- **Mechanism**: Runs 150 M to 500 M distilled ONNX weights directly in browser tabs via WebGPU shaders.
- **Strengths**: Zero server cost and zero user data transmission.
- **Weaknesses**: Lower parameter capacity limits performance on intricate instructions.

---

## 4. Local Deployment Quickstart

### Running Open-Jev on Apple Silicon (MLX)

```python
import mlx.core as mx
from open_jev import JevModel

# Load local 4-bit quantized reflex weights
model = JevModel.from_pretrained("daseinlabs/open-jev-mlx-4bit")

state = "User query: 'Deploying worker failed with exit code 137 (OOMKilled)'"
options = [
    "infrastructure_memory_exhaustion",
    "network_timeout",
    "authentication_failure",
    "syntax_error"
]

decision = model.evaluate_choice(state, options)
print(f"Choice: {decision.selected_option} (confidence: {decision.confidence:.2%})")
```

### Running Open-Jev with Hugging Face Transformers

```python
import torch
from transformers import AutoModelForSequenceClassification, AutoTokenizer

model_id = "YannQi/Reflex-4b"
tokenizer = AutoTokenizer.from_pretrained(model_id)
model = AutoModelForSequenceClassification.from_pretrained(model_id, torch_dtype=torch.float16, device_map="auto")

prompt = "State: PR #402 modifies database migration schema. Question: Does this require manual migration review?"
inputs = tokenizer(prompt, return_tensors="pt").to("cuda")

with torch.no_grad():
    logits = model(**inputs).logits
    probs = torch.softmax(logits, dim=-1)

# Index 0 = False, Index 1 = True (Noul evaluation)
print(f"Noul probability: {probs[0][1].item():.4f}")
```

---

## 5. Decision Matrix: When to Use Open-Jev vs. TypeSafe Jev

- **Choose TypeSafe Jev (Proprietary API) when**:
  - Maximum decision accuracy ([77.5%](https://docs.typesafe.ai/introduction)) is mission-critical.
  - Complex multi-variable instructions require strong general reasoning.
  - Infrastructure maintenance must remain zero.
  - Pricing at $0.042 / MTok input is cheaper than hosting dedicated GPU instances.

- **Choose Open-Jev (Local Weights) when**:
  - Air-gapped privacy or regulatory data sovereignty prohibits cloud API calls.
  - Real-time physical loops (60 FPS gaming, robotics, drone telemetry) demand sub-30 ms latency without network jitter.
  - Zero incremental cost per decision is required at millions of daily evaluations.
  - Offline browser extensions or desktop tools require hermetic local execution.
