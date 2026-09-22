# Specifying Agentic Submissions and Verifying Research Links

This guide defines the submission standards, machine-parseable schema, and research link requirements for autonomous AI agents (and engineers directing agents) submitting additions to **Awesome Jev & Fast Classifiers**.

---

## Reviewing the Automated Triage Architecture

Our repository maintains an automated intake and verification pipeline.

When an issue is submitted, our triage agents crawl the linked repositories, verify commit activity, audit claimed benchmarks, extract demo media, and format the entry directly onto the `dev` branch.

To ensure your submission passes automated evaluation without rejection, follow the schema and research link requirements below.

---

## Generating the Machine-Parseable Submission Schema

When opening a submission issue, agents should include a fenced YAML code block using the schema below:

```yaml
schema_version: "1.0"
submission_type: "tool" # or "use-case"
name: "project-or-tool-name"
repo_url: "https://github.com/author/project" # or primary documentation URL
target_category: "1. Browser, Desktop, and Mobile Automation"
primary_language: "Rust" # Python, TypeScript, Go, etc.
open_source_license: "MIT" # Apache-2.0, MPL-2.0, etc.

# Models Utilized (System 1 fast classifier + optional System 2 reasoning LLM)
models:
  system_one_model: "TypeSafe Jev" # or NanoJev, SemIf, Solomon-27B, GLiNER, Verdict
  system_two_model: "Claude 3.5 Sonnet" # paired generative/reasoning LLM, or null if standalone

# Empirical Economics & Metrics (Do not estimate; omit if not measured)
economics:
  inference_latency_ms: 28 # System 1 decision latency
  system_one_cost_usd: 0.01 # spend on fast classifier
  system_two_cost_usd: 0.96 # spend on paired LLM (null if standalone)
  total_spend_usd: 0.97 # total demonstrated run spend
  frontier_baseline_cost_usd: 50.00 # estimated spend if performed purely with frontier LLMs
  value_gained: "98% cost reduction while maintaining sub-30 ms reflex latency"
  throughput_fps: null # e.g. 60 FPS for game loops

# Primary Research Links for Triage Agents
research_links:
  canonical_social_thread: "https://x.com/author/status/1234567890"
  raw_video_demo_url: "https://example.com/demo.mp4"
  reproduction_command: "cargo bench --bench latency"
  benchmark_ledger_url: "https://author.github.io/benchmarks"

# Concrete Decision Mechanism
classification_mechanism:
  input_state: "Raw accessibility tree text coordinates"
  typed_primitive: "choice" # noul, choice, or score
  downstream_action: "Dispatches native OS click events via CoreGraphics"

# Concise Summary (1-2 sentences, <= 35 words each, zero em dashes)
technical_description: "DOM element selection evaluating candidate elements via choice in under 100 ms without heavy vision models."
```

---

## Providing Primary Research Links for Triage Agents

Our maintainer agents independently audit every submission. You must provide canonical links allowing our agents to perform the following checks:

### Verifying Codebase Health and Authenticity
- Provide a public GitHub, GitLab, or Forgejo URL.
- Our agents verify that the repository contains active code, a valid open-source LICENSE file, and commits within the last 180 days.
- Empty placeholder repositories, marketing stubs, and closed-source wrappers are automatically rejected.

### Resolving Canonical Social Threads
- Link to the original author announcement or technical breakdown on X (Twitter), Hacker News, or Reddit.
- Use the full status URL with exact numeric tweet ID (`https://x.com/author/status/<id>`).
- Our agents verify that the social handle matches the repository author or affiliated organization.

### Providing Demonstration Media and Video Assets
- Provide a direct link to a live demonstration video (MP4, Loom, X video, YouTube), animated GIF, or benchmark graphic.
- Avoid linking to generic homepages or top-level docs that lack media.
- Our media pipeline automatically downloads the asset, extracts representative poster frames, and encodes an optimized WebP preview into `media/`.

### Reproducing Benchmark Latency and Economics
- If your submission reports latency figures or cost reductions, cite the measurement method per [empirical benchmarks](https://gerryburde.com/articles/my-name-is-jev-summarizing-dozens-of-real-world-use-cases.html#empirical-benchmark-adversarial-invoice-sorting-and-the-certain-and-wrong-trap).
- Include a reproduction command (`python bench.py --runs 100`) or link to a published benchmark ledger.

---

## Enforcing Anti-Hallucination Directives for Submitting Agents

Submitting agents must strictly adhere to these anti-hallucination rules:

1. **Never Invent Social Media Handles:** If no public X announcement exists, leave the field empty. Never guess or fabricate Twitter usernames.
2. **Never Fabricate Performance Numbers:** If latency or cost was not explicitly measured and published, leave the field as `Not reported`.
3. **Strict Inclusion Gate:** The project must explicitly evaluate fast non-generative classification or System One primitives (`noul`, `choice`, `score`). General conversational chatbots and standard RAG pipelines are disqualified.
4. **Zero Em Dashes:** Never emit Unicode em dashes (U+2014) or mdash HTML entities. Use a standard hyphen `-` or double hyphen `--`.
5. **Sentence Length Ceiling:** Keep all descriptive sentences under 35 words.
