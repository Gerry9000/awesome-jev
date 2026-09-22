# Jev-Ultrafast: Sub-100 ms DOM Action Extraction Without Heavy Vision Models

#### 1. Post & Repository Overview
* **Author**: Alex Hitt ([`@browser-use`](https://github.com/browser-use)), Autonomous Web Agent Researcher.
* **Repository**: [`browser-use/jev-ultrafast`](https://github.com/browser-use/jev-ultrafast) *(Python, ⭐ 115)*.
* **Demonstration Media**: High-speed interactive browser execution sequence (`media/jev-ultrafast-browser-use.gif`).

---

#### 2. Cognitive Architecture & Technical Mechanism
* **DOM Pruning & Structural Extraction**:
  * Extracts accessibility trees and interactive DOM elements (buttons, inputs, links) using Playwright.
  * Strips redundant HTML boilerplate, CSS classes, and decorative elements down to clean candidate action lists.
* **Single-Pass Action Selection**:
  * Feeds parsed interactive element lists to TypeSafe Jev via the [`TypeSafe API`](https://docs.typesafe.ai/introduction).
  * Evaluates user intent against interactive targets using categorical `choice` in under 100 ms with 0 output tokens.
  * Eliminates screenshot rendering and vision-language model inference latencies.

---

#### 3. Empirical Results & Economics
* **End-to-End Execution Speed**:
  * Navigates multi-step web forms in 2 s end-to-end compared to 15--25 s required by visual LLM agents per the [`Browser-Use Latency Study`](https://github.com/browser-use/jev-ultrafast).
* **Cost Multipliers**:
  * Evaluates web pages for $0.0003 per page compared to $0.0400 per page on multimodal vision models.
  * Demonstrates a 130x cost reduction across 10,000 automated browser workflows in the [`Jev-Ultrafast Economic Benchmark`](https://github.com/browser-use/jev-ultrafast).

---

#### 4. Visual Assets & Artifacts
* **Animated Execution Capture**: `media/jev-ultrafast-browser-use.gif` (real-time automated form filling and button selection).
* **Teardown Thumbnail**: `media/jev-ultrafast-video-thumb.webp` (video poster frame).
