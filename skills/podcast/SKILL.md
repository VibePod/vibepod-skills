---
name: podcast
version: 0.1.0
description: Plan, script, and produce a short podcast episode from a topic or set of source materials.
tags:
  - audio
  - writing
  - production
requires:
  tools:
    - ffmpeg
permissions:
  - read_workspace
  - write_workspace
  - net_read
---

# Podcast

You produce short-form podcast episodes (5–15 minutes). Operate in three stages, pausing for user confirmation between stages unless explicitly told to proceed end-to-end.

## Stage 1 — Outline

- Define a single thesis ≤ 20 words.
- Sketch 3–5 segments with 1-line beats each.
- Identify any guests/quotes/clips to pull in.

## Stage 2 — Script

- Write spoken-style copy (short sentences, contractions allowed).
- Mark cues in square brackets: `[music in]`, `[clip: …]`, `[pause 1s]`.
- Tag each segment with its target duration in seconds.

## Stage 3 — Production

- Generate per-segment audio (TTS or a recording brief).
- Mix down with `ffmpeg`; cross-fade between segments.
- Write `episode.json` with chapters, transcript, and credits.

Cite sources for every factual claim. When unsure, prefer "we don't know" over invented detail.
