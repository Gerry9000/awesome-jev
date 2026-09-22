# Adaptive Sparse Attention for Video Generation: J-GAS Acceleration on MiniMax H3

#### 1. Post & Project Overview
* **Author**: Kamimoto / かみもと ([`@sep_is_heim`](https://x.com/sep_is_heim)), Software and R&D Engineer.
* **Project**: J-GAS (Jev-Guided Adaptive Sparsity) for MiniMax H3 Video Generation.
* **Repository**: [`sepiablue-ai/ComfyUI-MiniMax-H3-W4A4-VSA`](https://github.com/sepiablue-ai/ComfyUI-MiniMax-H3-W4A4-VSA/tree/exp/jev-adaptive-vsa) (branch `exp/jev-adaptive-vsa`).
* **Canonical Thread**: [`https://x.com/sep_is_heim/status/2101603192664740330`](https://x.com/sep_is_heim/status/2101603192664740330).
* **Technical Docs**: [`JEV_ADAPTIVE.md`](https://github.com/sepiablue-ai/ComfyUI-MiniMax-H3-W4A4-VSA/blob/exp/jev-adaptive-vsa/JEV_ADAPTIVE.md).
* **Demonstration Media**: 10.3-second video sample demonstrating fluid motion and character detail (`media/kamimoto-minimax-h3.mp4` and `media/kamimoto-minimax-h3-preview.gif`).
* **Verified Cost Evidence**: TypeSafe API billing dashboard screenshot (`media/kamimoto-minimax-h3-billing.webp`).

---

#### 2. Cognitive Architecture & Technical Mechanism
* **Diffusion Transformer Attention Bottleneck**:
  * Large-scale multimodal video generation models like MiniMax H3 incur severe computational bottlenecks in DiT (Diffusion Transformer) attention layers.
  * Uniform static sparse attention (SLA) risks degrading fine character details or temporal coherence if pruned evenly across all layers.
* **Dynamic Sparsification with System 1 Runtime Judging**:
  * J-GAS integrates TypeSafe Jev directly into ComfyUI as an adaptive runtime judge (`H3 v2 Streaming VSA` node).
  * The pipeline executes 4 Turbo steps across 50 layers with policy `layer_v5`.
  * Step 1 runs at a fixed 5% keep rate while permanently protecting prefix tokens in block0 and block1.
  * For steps 2 to 4, Jev evaluates layer sensitivity across shallow layers (2%, 5%, 7.5%), middle layers (1%, 5%, 7.5%), and the final 5 layers (3%, 5%, 10%).
  * Jev also selects the overall budget (2.5%, 3%, 3.5%) using single-pass forward evaluations with 0 output tokens.
* **Fail-Closed Resiliency**:
  * If API confidence drops below 0.40 or requests encounter network timeouts, execution safely reverts to the standard 5% keep rate with 0 retries.

---

#### 3. Empirical Results & Verified Economics
* **Generation Latency & Speedup**:
  * Measured on a consumer workstation with Windows 11 and an NVIDIA GeForce RTX 4070 (12 GB VRAM).
  * Baseline generation time: 6 minutes 07 seconds (367.72 seconds).
  * J-GAS accelerated generation time: 3 minutes 34 seconds (213.89 seconds).
  * Total wall-clock reduction: **41.7% speedup (153.83 seconds saved per video)**.
* **Live Measured Cost from TypeSafe Console**:
  * Kamimoto published the live TypeSafe billing dashboard after running 20 to 30 video generations in one session.
  * **Total Session Spend**: **$0.0392** (under 4 cents).
  * **Total Tokens Processed**: **1,037,063 tokens** (1.037 M tokens).
  * **Effective Cost Per Video**: **$0.0013--$0.0019 per video** (under 1/5 of a cent).
* **Cloud GPU Rental Economics**:
  * On cloud instances (RunPod or Lambda L4 / RTX 4090 at $0.40--$0.75 / hr), saving 153.8 seconds saves **$0.017--$0.032 in compute rental**.
  * Spending ~$0.0015 on Jev API decisions yields an immediate **10x--20x net financial return** in cloud compute savings alone.

---

#### 4. Visual Assets & Artifacts
* **Full Teardown Preview**: `media/kamimoto-minimax-h3-video.webp` (high-resolution video frame preview).
* **Animated Video Clip**: `media/kamimoto-minimax-h3-preview.gif` (animated clip of generated video).
* **Full Video File**: `media/kamimoto-minimax-h3.mp4` (10.3-second h264 video).
* **Preview Thumbnail**: `media/kamimoto-minimax-h3-thumb.webp` (compact preview icon).
* **Billing Dashboard Screenshot**: `media/kamimoto-minimax-h3-billing.webp` (TypeSafe API usage report showing $0.0392 for 1,037,063 tokens).
