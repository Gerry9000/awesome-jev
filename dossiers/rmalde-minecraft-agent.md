# Autonomous Minecraft Speedrun Agent: Dual-System GPT-6 Astra & TypeSafe Jev

#### 1. Post & Repository Overview
* **Author**: Ronak Malde ([`@rronak_`](https://x.com/rronak_)), Co-Founder of Trajectory ([`@TrajectoryLabs`](https://x.com/TrajectoryLabs)), former Google DeepMind, SWE-1 at Windsurf, Stanford.
* **Repository**: [`rmalde/minecraft-agent`](https://github.com/rmalde/minecraft-agent) *(JavaScript, ⭐ 31)*.
* **Canonical Thread**: [`https://x.com/rronak_/status/2101544156757950697`](https://x.com/rronak_/status/2101544156757950697).
* **Demonstration Video**: 39-second gameplay clip rendering native 960 &times; 540 resolution at 20 frames per second with real-time HUD telemetry.

---

#### 2. Cognitive Architecture & Technical Mechanism
* **Dual-System Partitioning**:
  * **System 2 (Strategic Planner)**: `openai/gpt-6-astra` runs asynchronously through standard completion endpoints. It dictates high-level milestones, resource gathering requirements, Nether fortress pathfinding, and dragon perch timing across 35 planner calls.
  * **System 1 (Real-Time Controller)**: `typesafe/jev-1.13` runs through `/api/alpha/decisions`. It evaluates structured game state buffers (health, inventory slots, entity vectors, block raycasts) and selects micro-actions in sub-20 ms forward passes with 0 output tokens across 131 decision cycles.
* **Continual Skill Generation**:
  * When movement routines encounter novel physical obstacles or combat edge cases, Astra synthesizes standalone JavaScript helper scripts (`.mjs` files).
  * These scripts register into the agent's action dictionary, allowing Jev to trigger deterministic subroutines as discrete single-pass options.
* **Protocol & Environment Integration**:
  * Connects to a standard vanilla Minecraft Java Edition 1.16.5 server using the Mineflayer bot framework.
  * Leverages direct packet observation and headless state tracking alongside a synchronized read-only client for real-time viewport capture.

---

#### 3. Empirical Results & Economics
* **Speedrun Completion**:
  * Slew the Ender Dragon in 8 minutes 43.300 seconds on run `nether-final-08` with world seed `8398967436125155523`.
  * Achieved a 40% reduction in elapsed run time compared to monolithic 14-minute LLM baselines per [`Ronak Malde's Benchmark Report`](https://x.com/rronak_/status/2101544156757950697).
* **Combat Performance**:
  * Completed the final dragon confrontation in 152 seconds using 6 timed bed explosions during the initial dragon perch.
  * Sustained zero player deaths and maintained full heart levels throughout the battle.
* **Cost Efficiency**:
  * Total compute cost for the speedrun was under $1.00.
  * System 1 (Jev) consumed $0.01 across 131 real-time evaluations ($0.025 / 1k decisions with 0 output tokens).
  * System 2 (Astra) consumed $0.96 across 35 asynchronous planning invocations.

---

#### 4. Visual Assets & Artifacts
* **Full Teardown Preview**: `media/ronak-minecraft-agent.webp` (high-resolution speedrun HUD frame).
* **Preview Thumbnail**: `media/ronak-minecraft-agent-thumb.webp` (120px popout thumbnail).
