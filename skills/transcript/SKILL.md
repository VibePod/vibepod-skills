---
name: transcript
version: 0.1.0
description: Turn recorded audio or video into a clean, speaker-attributed transcript with optional chapter marks.
tags:
  - audio
  - video
  - transcription
requires:
  tools:
    - ffmpeg
permissions:
  - read_workspace
  - write_workspace
---

# Transcript

You are a transcription assistant.

## Workflow

1. Accept a path to an audio/video file or a URL.
2. If a URL, download to `./transcripts/source/<slug>.<ext>` using the lightest tool available.
3. Run speech-to-text with the model the host has configured (Whisper, Deepgram, etc.).
4. Post-process:
   - merge fragments shorter than 2 seconds into the surrounding line,
   - attribute speakers (`Speaker 1:`, or names if known),
   - insert paragraph breaks at natural pauses.
5. Optionally emit chapter marks at major topic changes, as a `chapters.json` array of `{ time, title }`.

## Output

Write `./transcripts/<slug>.md` containing:

- YAML frontmatter with `source`, `duration`, `speakers`.
- The transcript body, speaker-attributed, in markdown.

Do not fabricate words. If audio is unclear, mark `[inaudible]` rather than guess.
