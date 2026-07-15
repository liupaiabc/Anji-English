---
name: sentence-pattern-practice
description: Generate 20–30 varied beginner English practice sentences from a requested heading in grammar/sentence-patterns.md, using project vocabulary and optionally applying a tense or other grammar restriction documented in the grammar folder. Use when the user asks for sentence examples, drills, or practice for a numbered sentence pattern or supplies a pattern title such as "### 5. Someone or something is doing an action"
---

# Sentence Pattern Practice

Generate beginner-friendly sentences for one selected pattern from the project grammar guide.

## Input

Treat the requested sentence-pattern title as the `pattern_title` parameter. Accept any of these forms:

- The complete Markdown heading, such as `### 5. Someone or something is doing an action`
- The heading text without Markdown markers
- The pattern number, such as `5`

If the request clearly identifies one heading, proceed without asking for confirmation. If it matches no heading or more than one heading, list the matching headings briefly and ask the user to choose one.

Also accept an optional `grammar` restriction, such as `simple past tense`, `present tense`, or a documented clause. Map `present tense` to **Simple Present Tense** and `past tense` to **Simple Past Tense** unless the user names a different present or past form explicitly.

## Workflow

1. Locate the project root containing `grammar/` and `vocab/`. Search the current workspace if the paths are not present in the working directory.
2. Read every `.md` file directly inside `grammar/` on every invocation so the skill follows the latest patterns and can enforce requested grammar restrictions.
3. Match `pattern_title` to one numbered `###` heading. Ignore category headings and `## Quick Practice`.
4. Read the selected heading's entire section, stopping at the next `###` or `##` heading. Follow its pattern, examples, notes, and restrictions.
5. Resolve an optional grammar restriction against the current grammar headings and rules. If it is unavailable, list the closest documented choices instead of using unsupported grammar.
6. Read all `.txt` files directly inside `vocab/`. Treat unit labels such as `unit-1` as headings, not vocabulary.
7. Generate 25 sentences by default. Generate another count only when the user requests one, and keep it from 20 through 30 inclusive.
8. Check every sentence against the selected structure, every requested grammar restriction, and the quality rules below before responding.

## Sentence Rules

- Write complete, natural, beginner-level sentences.
- Prefer words from `vocab/`. Add familiar beginner words when needed, including names and words such as `dog`, `cat`, `boat`, `book`, `school`, and `ball`.
- Keep sentences clear and easy for a beginner to understand, but vary their length naturally.
- Vary vocabulary and meaning; do not produce near-duplicates by changing only a name or pronoun.
- Use ordinary, positive, child-appropriate situations unless the selected pattern requires something else.
- Preserve correct capitalization, punctuation, articles, plurals, verb forms, and subject–verb agreement.
- When the user supplies a grammar restriction, apply it to every sentence without changing the selected sentence pattern.
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
