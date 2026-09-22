# JevChess: Real-Time Move Prediction and Blunder Detection Without Tree Search

#### 1. Post & Repository Overview
* **Author**: Choxos ([`@choxos`](https://github.com/choxos)), Systems and Game AI Engineer.
* **Repository**: [`choxos/jevchess`](https://github.com/choxos/jevchess) *(Python, ⭐ 42)*.
* **Demonstration Media**: Live chess engine match preview (`media/choxos-jevchess-demo.gif`).

---

#### 2. Cognitive Architecture & Technical Mechanism
* **State Representation**:
  * Formats active game positions as standard Forsyth-Edwards Notation (FEN) strings accompanied by legal candidate move lists.
  * Avoids generating verbose algebraic move notations or natural language chain-of-thought analysis.
* **Single-Pass Move Evaluation**:
  * Jev evaluates all candidate legal moves simultaneously across a categorical choice distribution.
  * Assigns calibrated probabilities to each candidate move in under 30 ms with 0 output tokens.
  * Replaces compute-intensive alpha-beta minimax tree search with direct pattern recognition over board state tensors.
* **Blunder Interception**:
  * Computes entropy across candidate move distributions. High uncertainty signals tactical complications, triggering deeper evaluation only when needed.

---

#### 3. Empirical Results & Economics
* **Inference Latency**:
  * Consistent sub-30 ms response time across all phases of the game (opening, middlegame, endgame).
* **Search Overhead**:
  * 0 node expansions required per decision compared to millions of nodes evaluated by Stockfish or traditional chess engines.
* **Token & Financial Cost**:
  * Zero generated tokens per move evaluation.
  * Evaluates moves at $0.00002 per turn, enabling continuous online analysis of blitz and bullet games without API rate limit bottlenecks.

---

#### 4. Visual Assets & Artifacts
* **Animated Game Preview**: `media/choxos-jevchess-demo.gif` (real-time board move evaluation and win probability tracking).
