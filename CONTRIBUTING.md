# Contributing to Awesome Jev

Thank you for contributing to the curated ecosystem of TypeSafe AI, Jev tools, benchmarks, and production architectures!

---

## Issue-Driven Curation Protocol

To maintain high editorial and technical standards, **we curate additions via GitHub Issues rather than direct pull requests**.

When an issue is submitted, our automated evaluation pipeline and maintainer agents:
1. Inspect the repository for real, active code (rejecting empty placeholders, marketing stubs, or closed wrappers).
2. Audit reported latency profiles, per-decision costs, and benchmark claims against empirical baselines.
3. Extract and optimize demo video clips into lightweight visual previews staged in `media/`.
4. Stage verified entries directly onto the `dev` development branch with full CI synchronization.

### Agentic & Automated Submissions

Autonomous coding agents (and engineers prompting agents) are encouraged to review the **[Agentic Submission Specification](dossiers/agent-submission-guide.md)**.
It provides a machine-parseable YAML schema, explicit research link requirements, and anti-hallucination verification rules.

---

## How to Submit a Tool, Benchmark, or Video Demo

Please open an issue using our **[Resource Submission Template](.github/ISSUE_TEMPLATE/add-resource.yml)** with the following details:

1. **Repository URL:** Public link to the GitHub, GitLab, or Forgejo codebase.
2. **Technical Description:** 1-2 sentences explaining what the tool does and its decision mechanism.
3. **Demo Video Link:** Direct link to an MP4 video, Loom, X clip, or YouTube explainer showing the tool running live.
4. **Social Discussion Thread:** Link to the canonical launch thread or technical discussion on X, Hacker News, or Reddit.
5. **Target Category & Rationale:** The category it belongs in and a brief explanation of why.
6. **Models Utilized:** The System 1 fast classifier (Jev or open model) and any paired System 2 reasoning LLM (or 'None').
7. **Reported Latency & Economics:** Decision latency (e.g. 28 ms), cost breakdown, and demonstrated value gained vs frontier LLMs.
8. **Language & License:** Primary programming language (Python, Rust, TypeScript, Go) and open-source license.

---

## How to Submit a Production Use Case or Architecture Recipe (Non-Repo Suggestions)

Not all breakthroughs are open-source repositories. We actively curate real-world production architectures, proprietary deployment patterns, and applied case studies that engineers can replicate.

Please open an issue using our **[Use Case Submission Template](.github/ISSUE_TEMPLATE/submit-use-case.yml)** with the following details:

1. **Pattern Title:** Clear descriptive name for the production pattern or workflow.
2. **Practitioner or Team:** The engineer, team, or organization that implemented the system.
3. **X or Community Discussion Link:** Canonical link to the public X thread, Hacker News discussion, Reddit thread, or technical blog post.
4. **Demo Video or Media Asset Link:** Direct link to an MP4 video, Loom clip, X video, architecture diagram, or benchmark graphic.
5. **The Bottleneck:** What made traditional generative LLMs, regex heuristics, or manual review impractical.
6. **The Fast-Classifier Recipe:** The exact input state evaluated, the typed schema applied, and the downstream automated action.
7. **Models Utilized:** The System 1 fast classifier used and any paired System 2 reasoning LLM (or 'None / Standalone').
8. **Reported Latency & Economics:** Measured latency in milliseconds, cost breakdown, and value gained vs pure frontier models.
9. **Code or Schema Example:** A minimal copy-pasteable snippet showing how to configure the schema.

---

## Pull Requests

Direct pull requests adding new entries to `README.md` are closed with a request to submit an issue instead.

Pull requests are reserved for:
- Repository tooling and CI workflow fixes.
- Documentation typo corrections.
- Broken link fixes or updated repository URLs.

All pull requests must target the `dev` branch and pass `make validate` locally.

---

## License

By submitting to this repository, you agree that contributions are curated under the [Creative Commons Attribution 4.0 International License (CC BY 4.0)](LICENSE).
