# JevPilot: Autonomous Driving Decision Simulator in Three.js

#### 1. Post & Repository Overview
* **Authors**: standardagents and J. P. Schroeder ([`@standardagents`](https://github.com/standardagents)), Autonomous Vehicle and Web Simulation Researchers.
* **Repository**: [`standardagents/jevpilot`](https://github.com/standardagents/jevpilot) *(JavaScript, ⭐ 6)*.
* **Demonstration Media**: Three.js highway simulator rendering real-time vehicle velocity and obstacle telemetry (`media/driving-simulator-demo.webp`).

---

#### 2. Cognitive Architecture & Technical Mechanism
* **Browser-Native 3D Driving Environment**:
  * Implemented using Three.js and WebGL to simulate highway driving, lane markers, and dynamic vehicles.
  * Measures vehicle speed, lane deviation, and relative distance to preceding vehicles in real time.
* **Reflexive Action Evaluation**:
  * Queries TypeSafe Jev via the [`Jev Decision API`](https://docs.typesafe.ai/introduction) with categorical maneuver choices (accelerate, coast, brake, change lane left, change lane right).
  * Evaluates telemetry vectors in 24 ms forward passes with 0 output tokens.
  * Dispatches selected vehicle throttle and steering actuations directly into the Three.js physics tick loop.

---

#### 3. Empirical Results & Economics
* **Reaction Latency**:
  * Achieved 24 ms average response time per decision cycle in the [`JevPilot Benchmark Evaluation`](https://github.com/standardagents/jevpilot).
* **Collision Avoidance**:
  * Successfully avoided rear-end collisions in 99.2% of cut-in test scenarios across 250 simulated highway trials.
* **Inference Economics**:
  * Cost per driving decision remained stable at $0.00004 ($0.025 / 1k evaluations).
  * Enables continuous simulation testing without consuming token generation budgets per the [`StandardAgents Cost Study`](https://github.com/standardagents/jevpilot).

---

#### 4. Visual Assets & Artifacts
* **Full Teardown Preview**: `media/driving-simulator-demo.webp` (high-resolution Three.js driving simulator HUD capture).
