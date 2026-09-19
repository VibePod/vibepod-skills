# Skill Authoring Guide

A VibePod skill is a folder containing at minimum a `SKILL.md`. Optional sibling directories let a skill ship scripts, assets, or reference material.

## Minimum layout

```text
my-skill/
  SKILL.md
```

## Recommended layout

```text
my-skill/
  SKILL.md
  scripts/      # optional — non-executable by default
  assets/       # optional — images, audio, templates
  references/   # optional — extended reference docs the skill may quote
```

## SKILL.md contract

YAML frontmatter (required fields **bold**):

| Field         | Type            | Notes                                                       |
|---------------|-----------------|-------------------------------------------------------------|
| **name**      | string          | Lowercase letters, digits, hyphens (≤ 64 chars); match the folder name. Becomes the install ID by default. |
| **description** | string        | One-sentence purpose. Shown in `vp skills list`.           |
| version       | string          | Semver recommended. Stored in the lockfile.                 |
| tags          | string[]        | Free-form discovery hints.                                  |
| requires.tools | string[]       | External CLI tools the skill expects (ffmpeg, git, …).     |
| permissions   | string[]        | Coarse capability hints (`read_workspace`, `net_read`, …). |

Body: free-form Markdown instructions for the skill. Must not be empty.

## ID derivation

`vp skills add` assigns the install ID as:

1. `--id <value>` if passed.
2. Otherwise `slugify(frontmatter.name)`.
3. Otherwise the source folder basename.

IDs only live in `skills.json` / `skills-lock.json` — never in locators or paths.

## Local development

Iterate on a skill without re-publishing:

```bash
vp skills add ./skills/my-skill --link
# edit my-skill/SKILL.md; changes are visible immediately
```

`--link` skills are excluded from sync's drift detection.

## Validating before commit

Run the engine's `validate` command on every skill in CI (see [`.github/workflows/validate.yml`](../.github/workflows/validate.yml)). It checks:

1. SKILL.md exists.
2. Frontmatter is parseable YAML.
3. `name` and `description` are present.
4. Body is non-empty.
