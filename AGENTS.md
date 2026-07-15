# Repository Guidance

## Purpose and Audience

This repository contains English lessons and practice generators for a beginner learner. Keep teaching material clear, natural, child-appropriate, and easy to practise aloud.

## Sources of Truth

- `grammar/` defines the grammar that project skills may use. Do not introduce new sentence patterns, clauses, or tenses unless the user asks for them.
- `topics/topics.md` contains topic names only. Keep one topic per Markdown list item.
- `vocab/*.txt` contains preferred vocabulary. Keep one word or phrase per line and do not treat unit labels as vocabulary.
- `.agents/skills/` contains repository-local Codex skills. Skills should read the learning files at runtime instead of duplicating their contents.

## Content Guidelines

- Prefer short explanations, familiar situations, and varied examples.
- Preserve correct capitalization, punctuation, articles, plurals, verb forms, pronoun references, and subject–verb agreement.
- Use **every day** for frequency; reserve **everyday** for the adjective meaning ordinary.
- Keep examples positive and age-appropriate unless the lesson requires a different form.
- Avoid adding advanced grammar to beginner examples when it is not documented in `grammar/`.
- Preserve the requested output count and format for generated practice.

## Skill Guidelines

- Keep each `SKILL.md` focused on one reusable workflow.
- Keep the YAML frontmatter limited to `name` and `description`.
- Keep `agents/openai.yaml` synchronized with the skill's purpose and default prompt.
- When a skill selects content by title, ignore sections named `Quick Practice` unless the user explicitly requests them.
- After changing a skill, run the available skill validator and test at least one realistic invocation.
- After renaming files or changing grammar scope, run `$repo-consistency-audit` to synchronize references, skills, README content, and repository guidance.

## Markdown Guidelines

- Use descriptive headings and blank lines around headings, lists, tables, and code blocks.
- Keep examples directly below the rule they demonstrate.
- Use relative links when linking between repository files.
