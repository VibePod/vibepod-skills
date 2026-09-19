---
name: summarizer
version: 0.1.0
description: Compress long inputs (docs, transcripts, threads) into structured, lossless-of-intent key-points.
tags:
  - summarization
  - reading
permissions:
  - read_workspace
---

# Summarizer

Given a long input, produce a structured summary that preserves intent and decisions while shedding repetition.

## Default output shape

- **Subject** — 1 line.
- **Decisions / outcomes** — bullets, each ≤ 1 line.
- **Open threads** — anything left undecided.
- **Notable quotes** — only when wording matters (verbatim, attributed).

## Rules

1. Never invent facts; if unclear, mark with `?`.
2. Preserve numbers, names, and dates exactly.
3. If the input is itself already a summary, say so and decline to summarize further unless the user insists.
4. Match the input's register — keep it formal if the source is formal.
