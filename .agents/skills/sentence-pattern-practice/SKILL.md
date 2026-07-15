---
name: sentence-pattern-practice
description: Generate 20–30 varied beginner English practice sentences from a requested heading in grammar/sentence-patterns.md, using vocabulary from the project's vocab folder plus familiar simple words. Use when the user asks for sentence examples, drills, or practice for a numbered sentence pattern or supplies a pattern title such as "## 5. Someone or something is doing an action."
---

# Sentence Pattern Practice

Generate beginner-friendly sentences for one selected pattern from the project grammar guide.

## Input

Treat the requested sentence-pattern title as the `pattern_title` parameter. Accept any of these forms:

- The complete Markdown heading, such as `## 5. Someone or something is doing an action`
- The heading text without Markdown markers
- The pattern number, such as `5`

If the request clearly identifies one heading, proceed without asking for confirmation. If it matches no heading or more than one heading, list the matching headings briefly and ask the user to choose one.

## Workflow

1. Locate the project root containing `grammar/sentence-patterns.md` and `vocab/`. Search the current workspace if the paths are not present in the working directory.
2. Read `grammar/sentence-patterns.md` on every invocation so the skill follows the latest patterns.
3. Match `pattern_title` to one `##` heading. Ignore `## Quick Practice`.
4. Read the selected heading's entire section, stopping at the next `##` heading. Follow its pattern, examples, notes, and restrictions.
5. Read all `.txt` files directly inside `vocab/`. Treat unit labels such as `unit-1` as headings, not vocabulary.
6. Generate 25 sentences by default. Generate another count only when the user requests one, and keep it from 20 through 30 inclusive.
7. Check every sentence against the selected structure and the quality rules below before responding.

## Sentence Rules

- Write complete, natural, beginner-level sentences.
- Prefer words from `vocab/`. Add familiar beginner words when needed, including names and words such as `dog`, `cat`, `boat`, `book`, `school`, and `ball`.
- Keep sentences clear and easy for a beginner to understand, but vary their length naturally.
- Vary vocabulary and meaning; do not produce near-duplicates by changing only a name or pronoun.
- Use ordinary, positive, child-appropriate situations unless the selected pattern requires something else.
- Preserve correct capitalization, punctuation, articles, plurals, verb forms, and subject–verb agreement.
- Do not introduce a different sentence pattern merely to increase variety.
- Do not add translations, grammar explanations, blanks, or answers unless the user asks for them.

## Subject Variety

Across the full set, use a natural mixture of:

- First and second person: `I`, `you`, `we`
- Third-person pronouns: `he`, `she`, `it`, `they`
- People and possessive noun phrases: `Tom`, `Lucy`, `my mom`, `his friend`, `the teacher`
- Singular animals or things: `the dog`, `a cat`, `the boat`
- Plural or coordinated subjects: `the children`, `my parents`, `Tom and Lucy`, `a boy and a girl`

Do not force every subject type when it conflicts with the selected pattern. For patterns using **be**, verify agreement carefully: `I am`, singular subjects `is`, and plural/coordinated subjects `are`.

## Output

Return:

1. The matched pattern heading.
2. A numbered list containing only the generated sentences.

Do not mention which words came from the vocabulary files. Keep the response ready to use directly as a practice sheet.
