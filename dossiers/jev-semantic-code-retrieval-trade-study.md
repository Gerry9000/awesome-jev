# Jev Semantic Code Retrieval: Family Trade Study and Evaluation Scope

## Bottom Line Up Front (BLUF)

Seven open-source tools use TypeSafe Jev to find code by describing its behavior. Most observers mistake them for the same product. They actually occupy three shapes: repository retrieval agents, line-level stream filters, and test-selection predictors.

`dzhng/jevgrep` leads on traversal policy and is the only tool publishing an end-to-end agent cost measurement. That measurement loses a solve, and the project says so openly. The repository is one day old, which tempers every other signal.

Field testing on our own repository found a disqualifying defect. `jg` sent internal operational policy from a tracked manifest to a third-party API, and ships no command capable of previewing that transmission. Do not adopt `jg` on repositories containing operational prose. Run the trade study anyway, because the traversal design is the best in the family and worth stealing.

---

## 1. Scope and Method

This dossier covers tools whose primary function is locating code, source text, or change hunks by natural-language description rather than by exact identifier.

Verification ran on 2026-09-27. I read each repository's `README.md`, plus `docs/architecture.md` and the GitHub releases API for `dzhng/jevgrep`. I re-read star counts from live GitHub API responses and compared them against `data/jev-ecosystem.json` and `RADAR.md`.

Uniqueness claims here are scoped to this candidate set. They make no claim of uniqueness across all 175 curated and 1017 radar entries.

---

## 2. The Candidate Set

| Repository | Language | Install surface | Runtime floor | License | Live stars | Catalog status |
| :--- | :--- | :--- | :--- | :--- | ---: | :--- |
| [`dzhng/jevgrep`](https://github.com/dzhng/jevgrep) | TypeScript | `npm i -g @dzhng/jevgrep` yields `jg` | Node 22+ | MIT | 222, volatile | Absent from curated set and radar |
| [`can1357/jegrep`](https://github.com/can1357/jegrep) | Rust | `cargo install jegrep`, or release binaries | glibc 2.39+ | MIT | 97 | Radar only |
| [`uehaj/jev-semgrep`](https://github.com/uehaj/jev-semgrep) | JavaScript | `npm i -g @uehaj/sys1grep` | Node 20.16+ | Other | 144 | Radar only |
| [`keltokhy/jgrep`](https://github.com/keltokhy/jgrep) | Python | `uv tool install jev-grep` | uv, plus `[code]` extra | MIT | 115 | Radar only |
| [`ellipsis-dev/blink`](https://github.com/ellipsis-dev/blink) | TypeScript | Source checkout, runs `./blink` | Bun 1.3.14+ | Not stated | 84 | Curated |
| [`nassim-arifette/jevgrep`](https://github.com/nassim-arifette/jevgrep) | TypeScript | `npm i -g @nassim-arifette/jevgrep` | Node 24+ | MIT | 80 | Radar only |
| [`kyu1204/jgrep`](https://github.com/kyu1204/jgrep) | TypeScript | `npm i -g jevgrep` yields `jgrep` | Node, zero runtime deps | MIT | 36 | Curated |

Two adjacent curated tools sit outside the study. `supercorp-ai/supercov` (Rust, 106 stars) scores source files to rank refactoring work. `valentynkit/jev.nvim` (Lua, 5 stars) queries the open buffer inside Neovim. Neither retrieves across a repository.

### 2.0 Project Maturity of `dzhng/jevgrep`

Maturity outweighs feature comparison. This section therefore leads.

Per the [GitHub API record](https://api.github.com/repos/dzhng/jevgrep), the repository was created 2026-09-26T04:06:56Z. Last push landed 2026-09-26T21:45:13Z. The project is roughly 24 hours old.

Consequences for the study:

- **Star count is a launch spike, not adoption.** The count moved from 216 to 222 between two reads taken during a single session. Treat any single snapshot as unreliable.
- **Zero open issues carries no signal.** The repository is one day old with 0 subscribers. A clean issue tracker at 24 hours means nobody has filed anything yet.
- **Release artifacts disagree.** GitHub publishes one release, v0.1.0, cut 2026-09-26T16:03:40Z. npm serves version 0.3.0. Versions 0.2.0 and 0.3.0 have no corresponding GitHub release, even though the v0.1.0 notes state that release CI verifies the exact published tarball against registry integrity.
- **The README documents pre-0.3.0 breakage.** It notes that `jg skill` only printed the bundled skill at 0.1.0, and that provider selection requires 0.3.0 or newer.

By contrast `can1357/jegrep`, `nassim-arifette/jevgrep`, and `keltokhy/jgrep` all carry substantial commit history and published changelogs. Age asymmetry, not architecture, may decide this study.

### 2.1 Binary Name Collisions

Six tools expose five distinct binary names. `kyu1204/jgrep` publishes the unscoped npm package `jevgrep` yet installs a binary named `jgrep`. `keltokhy/jgrep` installs a binary named `jgrep` from PyPI. Those two collide on `PATH`. The [`nassim-arifette/jevgrep` README](https://github.com/nassim-arifette/jevgrep) documents this hazard directly.

### 2.2 Runtime Floor Spread

Four tools demand four different minimums: Node 20.16, Node 22, Node 24, and Bun 1.3.14. `can1357/jegrep` alone ships a self-contained binary with no runtime dependency.

---

## 3. Star Drift Between Catalog and Live Sources

Promotion triage keyed on recorded star counts under-ranks this set.

Radar values come from the published [`RADAR.md`](https://github.com/Gerry9000/awesome-jev/blob/main/RADAR.md). Live values come from GitHub API reads taken 2026-09-27.

| Repository | Catalog stars ([`RADAR.md`](https://github.com/Gerry9000/awesome-jev/blob/main/RADAR.md)) | Live stars, 2026-09-27 | Drift |
| :--- | ---: | ---: | ---: |
| `keltokhy/jgrep` | 21 | 115 | 5.5x |
| `kyu1204/jgrep` | 16 | 36 | 2.3x |
| `nassim-arifette/jevgrep` | 54 | 80 | 1.5x |
| `ellipsis-dev/blink` | 65 | 84 | 1.3x |
| `can1357/jegrep` | 83 | 97 | 1.2x |
| `uehaj/jev-semgrep` | 130 | 144 | 1.1x |
| `dzhng/jevgrep` | not recorded | 222 | absent |

The catalog column mirrors counts held in the [radar triage cache](https://github.com/Gerry9000/awesome-jev/blob/main/config/radar-triage-cache.json).

`dzhng/jevgrep` tops this family on stars. It sits in neither the curated set nor the radar. The radar lists three forks instead: `allebee/jevgrep`, `nassim-arifette/jevgrep`, plus mirror watermarks for `sijiaoh/jevgrep` and `thehumanworks/jevgrep`.

### 3.1 Missing Language Field in Radar Records

A `radar_candidates` entry carries only `repo`, `url`, `mirrors`, `stars`, `quality`, `promotion_ready`, `description`, and `category`. No `language` field exists. Language-based triage across the radar therefore requires fetching each repository individually. Curated entries in `data/jev-ecosystem.json` do carry `language`.

---

## 4. What Each Tool Uniquely Does

### 4.1 `dzhng/jevgrep`: the traversal policy

Two mechanisms set it apart. First, local lookahead crosses one intermediate directory before classifying, so a thin wrapper directory cannot hide its descendants. Second, a later discovery pass re-enters the tree from a class-bearing anchor. That pass exists to reconsider a backend or subclass that topical search missed.

Rivals collapse three separate decisions into one. This tool keeps them apart. File usefulness. Declaration leads. Source worth immediate inclusion. Files surface as leads even when no excerpt attaches.

The project's own architecture record calls the anchor heuristic a spike policy. It offers no proof that one anchor works everywhere.

### 4.2 `can1357/jegrep`: the strategy dial and the shared benchmark

It exposes ten selectable exploration strategies: `cascade`, `beam`, `tree`, `window`, `paged`, `budget`, `deep`, `hybrid_window`, `inline`, and `sniff`. It adds multi-round thresholds, a stop-lowering rule, and a `--tree` mode that prints the annotated exploration itself. A `--compact` mode targets LLM readers specifically.

Its decisive contribution is the `benches/` corpus: 40 labeled queries across cpython, kubernetes, linux, and postgres. That dataset alone makes quantitative comparison inside this family possible.

### 4.3 `nassim-arifette/jevgrep`: the consent architecture

It alone runs as a local MCP server, and its safety model depends on that fact. Server-side capabilities include per-repository authorization, `.jevgrepignore`, an explicit `remote_evaluation_enabled` gate, scan caps, and a `--allow-partial` degradation mode. An offline `inspect` command shows exactly which fragments would leave the machine.

It also publishes a `benchmarks/baselines/` ledger of paired runs covering batching reuse and cache behavior. It offers a ledger where most rivals offer one headline number.

### 4.4 `keltokhy/jgrep`: the stream filter and the local models

It is the only true pipe filter. It works under `tail -f` while emitting in input order. It is also the only candidate that runs against self-hosted System One servers (DiffusionGemma, laya-mlx, GLiNER2.5-Decide) at zero marginal cost.

It also accepts arbitrary LLM gateways and enforces a hard dollar budget cap. `--estimate` prices a run without credentials. It parses functions in the most languages here (Python, Go, C). Its git hardening is the most defensive in the set. It confines worktrees and sets `GIT_NO_REPLACE_OBJECTS` plus `protocol.ext.allow=never`.

### 4.5 `uehaj/jev-semgrep`: composable logic and a cost lever

Each meaning returns its own probability. Boolean composition comes free. Set logic needs no heuristic trick. Two cost levers are unique to it. A local regex prefilter gates which lines ever get transmitted. Regex capture groups substitute into the semantic question itself.

Cross-language matching is also unique here. A Japanese meaning retrieves English lines at comparable confidence. The project ships as a single dependency-free file.

### 4.6 `kyu1204/jgrep`: the test-selection predictor

`--tests <ref>` selects test files that a diff plausibly affects. It works in three layers, cheapest first: filename match, import graph, then Jev. Per the author's [measured selection benchmark](https://github.com/kyu1204/jgrep/blob/main/bench/tests/README.md) across five open-source repositories, the tool selects 12% of test files while recovering 92% of the tests each commit's author actually touched. Name and import matching alone recovers 43%.

It alone scores CSV and JSONL records using arbitrary Jev question types. It alone documents a CI exit-code contract that separates matched, unmatched, and error states.

### 4.7 `ellipsis-dev/blink`: content-free scoring

It scores file and folder names only, and never reads file content. Its confidence signal differs structurally from the others: the reported percentage is the fraction of N walkers that converged on a path, so cross-path agreement is the confidence rather than a per-file probability. It retains a full trace artifact per walker for audit.

The project is already curated and should stay as prior art. `dzhng/jevgrep` is a strict superset of its capability.

---

## 5. The Tool Call Versus Shell Axis

A harness already grants the agent a shell, so CLI reachability is settled. Four properties separate a tool call from a shell command.

**Structured return.** `dzhng/jevgrep` deliberately emits one human-readable stdout stream. Its architecture record states the head must stay useful when a caller reads only the head. That optimizes for a person skimming. An agent consuming the full result pays for every decorative line. A tool result exposing named fields (`file`, `line_start`, `line_end`, `score`) costs less to consume and misreads line numbers less often. `can1357/jegrep` already offers that shape through `--json`.

**Consent at the harness boundary.** An MCP server can hold the credential, enforce a per-repository allowlist, and refuse. A CLI cannot stop an agent that already decided to run it. That is the strongest argument for `nassim-arifette/jevgrep`. Its safety story depends on being a server process.

**Approval visibility.** A tool call is a discrete permissionable event. A Bash invocation is one opaque line among hundreds.

**Cross-harness portability.** One server serves Claude Code, Codex, opencode, and cursor. The skill route requires per-harness skill installation and teaches the model a text protocol.

**Counter-argument for the evaluation phase.** A quality study needs none of the above. Use the CLI. The MCP axis matters only if the tool enters a fleet and needs an authorization boundary.

---

## 6. Hard Gates for Any Adoption

1. **Credential handling.** `dzhng/jevgrep` ignores environment variables and endpoint overrides. It does support non-interactive auth through `jg auth --provider typesafe --stdin`, verified working, so a wrapper can pipe a key once. The residual objection is weaker than the README suggests: it stores one credential per machine in an owner-only file, which conflicts with per-job scoped keys. `nassim-arifette/jevgrep` and `keltokhy/jgrep` honor environment variables directly.
2. **Cost disclosure.** `dzhng/jevgrep` reports no per-query retrieval cost. Every other candidate states the $0.042 per million input token rate plus a representative per-search figure. Confirmed by measurement in section 6.5.
3. **Transmission transparency.** A candidate must show, offline, which bytes a search would transmit. Measured in section 6.5: `dzhng/jevgrep` cannot, and `nassim-arifette/jevgrep` can.

Gate 3 blocks production adoption outright. Gates 1 and 2 require upstream change only.

## 6.5 Field Test on Our Own Repositories

I installed three candidates and ran them against `sifs-flywheel`. Every figure below is first-hand measurement, not a quoted claim. Versions: `jg` 0.3.0, `jevgrep` 0.1.1, `sys1grep` 0.5.0-next.0. Host Node 26.7.0. Repository scale: 1,253 tracked files, 3,106 on disk, 283 MB.

**One question with a checkable answer.** I asked how the top-level installer chains ACFS execution into SIFS module execution. Ground truth is `install.sh:178`, which execs `sifs_install.sh` with passthrough arguments.

**Both retrieval tools found the right file first.** `jg` ranked `install.sh` first of 210 relevant files. `jevgrep` returned `install.sh:73-189` at score 0.91, a range that contains ground-truth line 178. Accuracy was not the differentiator. Presentation was.

**`jg` buried the answer.** It emitted 125,731 bytes, roughly 31,400 tokens, across 146 reading-lead blocks. Retrieval costing 31,400 context tokens has thin arithmetic in a single query, since that approaches the size of the file it was meant to help you avoid reading.

**`jevgrep` answered far more cheaply.** It returned 4 excerpts in 9,954 bytes, self-measured at 2,607 tiktoken `cl100k_base` tokens, against `jg`'s 125,731 bytes. It also names its tokenizer and version, making the number reproducible.

**`jg` disclosed internal policy to a third-party API.** Its output reproduced a passage from `sifs.manifest.yaml` holding our internal agent routing notes. Remote classification sent that content off-machine inside the request. `jevgrep` returned no trace of that text under the same question.

Three aggravating details:

- The repository ships no preview command. Nothing in `jg --help` offers an offline scope report.
- The `--include-sensitive` flag defaults to off, meaning sensitive material is withheld by default. The filter still missed this file, because a YAML manifest is not a recognized sensitive filename pattern and the filter appears to key on names.
- The content arrived labeled a `helper` in a `caller, helper` role, so the retrieval pipeline treated operational policy as ordinary source.

This is the decisive finding for fleet use. A retrieval tool that cannot show what it will transmit, pointed at repositories whose manifests and runbooks contain operational prose, is not adoptable at any retrieval quality.

**`jevgrep` refuses, and says why.** Under a 250,000 token scan cap it exited 2 with `SCOPE_EXCEEDS_SCAN_BUDGET` and `PREPARATION_LIMIT`, reporting coverage as 400 of 1190 eligible files and returning 281 bytes. It degraded loudly instead of truncating quietly. `jg` has no equivalent refusal path.

**Offline preview worked, at a price.** Scoped `inspect` over `packages/sifs_manifest` finished in 3.57 s. It reported 48 eligible files of 62 discovered, 207 fragments, and an estimated 172,289 input tokens across 4 provider requests. It declined to emit a USD figure because no dated pricing record is configured, rather than invent one. Run against the whole repository, that same offline command exceeded 180 s without finishing.

Measured comparison, one query each against the same repository:

| Measure | `jg` 0.3.0 | `jevgrep` 0.1.1 uncapped |
| :--- | ---: | ---: |
| Wall time | 27.06 s | 228.69 s |
| Result volume | 125,731 bytes | 9,954 bytes |
| Result tokens | about 31,400 | 2,607, self-measured |
| Units returned | 210 files, 146 lead blocks | 4 excerpts |
| Ground truth ranked | first of 210 | first of 4, range contains line 178 |
| Internal policy in output | yes | no |
| Offline transmission preview | none | `inspect`, 3.57 s scoped |
| Refuses on budget | never | yes, with stop reasons |

**The tradeoff is real, not one-sided.** `jevgrep` took 228.69 s against `jg`'s 27.06 s. That is roughly eight times worse wall clock in exchange for one twelfth the context and a working consent boundary. On a latency-sensitive agent loop the gap matters, and the study should measure whether `--json` or scan tuning closes it.

**A measurement trap worth recording.** Grepping `jg` output for cost figures returned dollar values, and they were ours. Our own manifest quotes dollar amounts, and `jg` had faithfully returned that retrieved text. Retrieval output contaminates cost audits of the retrieval.

---

## 7. Proposed Trade Study Design

Evaluate three retrieval candidates, not seven: `dzhng/jevgrep`, `nassim-arifette/jevgrep`, and `can1357/jegrep`. Add `kyu1204/jgrep` as an orthogonal review and test-selection component rather than a retrieval competitor.

Run all three against the 40-query corpus published in [`can1357/jegrep/benches`](https://github.com/can1357/jegrep/tree/master/benches). That corpus is the only comparable labeled data any candidate has released.

Score the following:

- Recall at k of the correct file, computed per language corpus.
- Cost per query, measured rather than quoted.
- Elapsed time to first usable excerpt, not to first hit.
- Declaration-level line accuracy.
- Agent skill quality, judged from observed retrieval behavior.
- End-to-end agent cost, anchored on the `dzhng/jevgrep` Sol run. Carry its 7 of 10 against 8 of 10 solve result forward without averaging it away.

`keltokhy/jgrep` and `uehaj/jev-semgrep` join only if the study expands to log and stream triage, which is a different problem shape.

---

## 8. Recorded Benchmark Caveat

`dzhng/jevgrep` reports two complete SWE-bench cohorts of ten tasks each. Full Sol costs were $5.5411 and $4.5196 against a saved baseline of $7.6221, excluding Jev spend. Solve rates were 6 of 10 and 7 of 10 against that baseline's 8 of 10. Per the [variance and paired-trace analysis](https://github.com/dzhng/jevgrep/blob/main/specs/done/jevgrep/assets/variance-repeat.md), both runs failed the project's original quality gate, and the documented shipping tradeoff was explicitly accepted. The sample is a tuned Python subset. Baselines were never rerun and outcomes were never pooled.

The honest reading is a cost reduction purchased with a quality regression, at a sample size too small to generalize. It still anchors the study as the only end-to-end agent cost measurement published in this family.

---

## 9. Catalog Actions

1. Evaluate `dzhng/jevgrep` for curated promotion. It meets Prong 1 (identity, mechanism, MIT license) and partially meets Prong 2, since it claims cost but omits per-query figures. Prong 3 splits: the repository ships two usable visual assets (`assets/cover.png` and `assets/how-it-works.png`), but no canonical social thread surfaced in search. A 24-hour-old repository is unlikely to have one yet.
2. Refresh radar star counts via [`scripts/refresh_stars.py`](https://github.com/Gerry9000/awesome-jev/blob/main/scripts/refresh_stars.py). Observed drift spans 1.1x through 5.5x across this set.
3. Add a `language` field to `radar_candidates` records so language-based triage becomes possible.
4. Record `dzhng/jevgrep` in the radar even if promotion is deferred, so its forks stop being tracked without their upstream.

---

## 10. Verification Notes

All star counts, language classifications, and feature claims in this dossier come from live repository metadata read on 2026-09-27. Feature claims derive from each project's own `README.md` and, for `dzhng/jevgrep`, from `docs/architecture.md` and the GitHub releases API.

The following are quoted or closely paraphrased from project sources, and I did not independently reproduce them: all latency and cost figures, the `kyu1204/jgrep` test-selection ratios, the `dzhng/jevgrep` SWE-bench cost results, and the `can1357/jegrep` benchmark corpus contents.

`supercorp-ai/supercov` and `valentynkit/jev.nvim` are described from catalog records only. I did not read either repository during this pass.

No canonical X or Hacker News announcement thread for `dzhng/jevgrep` surfaced during search on 2026-09-27. Per the anti-hallucination directive in [`dossiers/agent-submission-guide.md`](https://github.com/Gerry9000/awesome-jev/blob/main/dossiers/agent-submission-guide.md), I record the absence rather than guess a handle.

This dossier is not yet reachable from the rendered site. [`scripts/build_site_data.py`](https://github.com/Gerry9000/awesome-jev/blob/main/scripts/build_site_data.py) extracts dossier links only from `[Teardown Dossier](dossiers/...)` markers inside `README.md` entry blocks. Curated promotion makes the dossier visible. The P1 evaluation bead gates that promotion.
