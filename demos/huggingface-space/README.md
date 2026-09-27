---
title: Awesome Jev Intent Search & Ecosystem Explorer
emoji: ⚡
colorFrom: indigo
colorTo: purple
sdk: static
pinned: false
tags:
  - typesafe
  - systemone
  - jev
  - classifiers
  - search
  - decision-models
---

# ⚡ Awesome Jev Intent Search & Ecosystem Explorer

An interactive, natural language intent search engine and candidate surfacing directory for the [Awesome Jev](https://awesomejev.org) ecosystem.

## Overview

Unlike generative conversational AI search that generates unpredictable text tokens, this search engine evaluates typed non-generative decisions using **TypeSafe System One models (Jev, Jev Fast, Valen)** and local fast classifiers.

Users describe what engineering problem or tool they need (e.g. *"triage incoming PRs for security bugs without burning OpenAI tokens"*, *"fast DOM scraper without browser overhead"*), and the system maps the intent into canonical directories and surfaces matching curated tools.

## Architecture & Data Flow

This Hugging Face Space runs client-side and dynamically synchronizes with the authoritative dataset on [awesomejev.org](https://awesomejev.org):
1. **Dynamic Catalog Ingestion**: Fetches `https://awesomejev.org/data/jev-ecosystem.json` on initialization.
2. **Multi-Model Intent Evaluation**: Calls `https://awesomejev.org/api/search` supporting multiple System One decision models (`jev-latest`, `jev-fast`, `valen-vision`, `tinyjev-0.6b`) and the offline `edge-heuristic` engine.
3. **Search Scope Toggle**: "Curated" searches only the vetted tools. "All Tools" adds the uncurated radar candidates, each badged as an unvetted radar candidate.
4. **Offline Fallback**: An in-browser keyword scoring engine returns results from the same scope when the search API is unreachable.

The Space searches only the Awesome Jev dataset. It never triages external mirrors; that remains internal offline tooling.

## Links

- **Authoritative Directory**: [https://awesomejev.org](https://awesomejev.org)
- **GitHub Repository**: [https://github.com/Gerry9000/awesome-jev](https://github.com/Gerry9000/awesome-jev)
- **Deep Research Report**: [https://gerryburde.com/articles/my-name-is-jev-summarizing-dozens-of-real-world-use-cases.html](https://gerryburde.com/articles/my-name-is-jev-summarizing-dozens-of-real-world-use-cases.html)
- **TypeSafe AI**: [https://typesafe.ai](https://typesafe.ai)
