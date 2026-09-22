# Franka Robotic Arm Motion Primitive Selection in ManiSkill Physics

#### 1. Post & Repository Overview
* **Author**: Tarun Tomar ([`@TarunTomar122`](https://x.com/TarunTomar122)), Robotics and Reinforcement Learning Engineer.
* **Repository**: [`TarunTomar122/jev-askable-arm`](https://github.com/TarunTomar122/jev-askable-arm) *(Python, ⭐ 4)*.
* **Canonical Thread**: [`https://x.com/TarunTomar122/status/2100651234567890123`](https://x.com/TarunTomar122/status/2100651234567890123).
* **Demonstration Media**: ManiSkill Franka Panda arm physics simulation screenshot (`media/franka-arm-simulation.webp`).

---

#### 2. Cognitive Architecture & Technical Mechanism
* **Physical Robot Simulation**:
  * Simulates a 7-DOF Franka Emika Panda robotic arm inside the ManiSkill robotics physics engine.
  * Encodes object coordinates, gripper distances, and target table zones into structured floating-point state representations.
* **Motion Primitive Selection**:
  * Instead of calculating low-level joint motor torques with a neural network, Jev scores discrete motion primitives (reach, grasp, lift, move to bin, release).
  * Evaluates geometric scene states via the [`TypeSafe Jev API`](https://docs.typesafe.ai/introduction) in 28 ms forward passes with 0 output tokens.
  * Native inverse kinematics solvers calculate collision-free trajectory waypoints once a primitive is selected.

---

#### 3. Empirical Results & Economics
* **Task Success Rates**:
  * Achieved 94.6% task completion across pick-and-place trials in the [`ManiSkill Evaluation Suite`](https://github.com/TarunTomar122/jev-askable-arm).
* **Inference Latency**:
  * Sustained 28 ms latency per primitive decision cycle without generation lag.
* **Marginal Cost**:
  * Cost per pick-and-place sequence averaged $0.00004 ($0.025 / 1k evaluations), or $0.00 when evaluated on local GPU edge instances per the [`Robotics Cost Audit`](https://github.com/TarunTomar122/jev-askable-arm).

---

#### 4. Visual Assets & Artifacts
* **Simulation Workspace Preview**: `media/franka-arm-simulation.webp` (high-resolution ManiSkill simulation view).
