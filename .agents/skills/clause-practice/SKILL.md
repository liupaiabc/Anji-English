---
name: clause-practice
description: Generate 20–30 varied beginner English practice sentences from a requested heading in grammar/clauses.md, using vocabulary from the project's vocab folder plus familiar simple words. Use when the user asks for sentence examples, drills, or practice for a clause title such as "Attributive Clause (Relative Clause)."
---

# Clause Practice

Generate beginner-friendly sentences for one selected clause from the project grammar guide.

## Input

Treat the requested clause title as the `clause_title` parameter. Accept any of these forms:

- The complete Markdown heading, such as `## Attributive Clause (Relative Clause)`
- The heading text without Markdown markers
- A heading number when the requested heading has one

If the request clearly identifies one heading, proceed without asking for confirmation. If it matches no heading or more than one heading, list the matching headings briefly and ask the user to choose one.

## Workflow

1. Locate the project root containing `grammar/clauses.md` and `vocab/`. Search the current workspace if the paths are not present in the working directory.
2. Read `grammar/clauses.md` on every invocation so the skill follows the latest clauses.
3. Match `clause_title` to one `##` heading. Ignore `## Quick Practice`.
4. Read the selected heading's entire section, including its `###` subsections, stopping at the next `##` heading. Follow its definitions, examples, word choices, and restrictions.
5. Read all `.txt` files directly inside `vocab/`. Treat labels such as `unit-1` as headings, not vocabulary.
6. Generate 25 sentences by default. Generate another count only when the user requests one, and keep it from 20 through 30 inclusive.
7. Check every sentence against the selected clause and the quality rules below before responding.

## Clause Rules

- Include the selected type of clause in every sentence.
- Write a complete main sentence and a complete, correctly attached clause; do not write sentence fragments.
- Place the clause where the selected section says it belongs.
- Follow distinctions taught in the selected section. For the current attributive clause, use **who** for people and **that** for animals or things.
- Make each clause add useful information instead of repeating the main sentence.
- Use varied main-sentence structures; do not begin most sentences with the same phrase such as `This is`.

## Sentence Rules

- Write complete, natural, beginner-level sentences.
- Prefer words from `vocab/`. Add familiar beginner words when needed, including names and words such as `dog`, `cat`, `boat`, `book`, `school`, and `ball`.
- Keep sentences clear and easy for a beginner to understand, but vary their length naturally.
- Vary vocabulary, subjects, actions, and meaning; do not produce near-duplicates by changing only a name or noun.
- Use ordinary, positive, child-appropriate situations unless the selected clause requires something else.
- Preserve correct capitalization, punctuation, articles, plurals, verb forms, pronoun references, and subject–verb agreement.
- Do not introduce a different clause merely to increase variety.
- Do not add translations, grammar explanations, blanks, or answers unless the user asks for them.

## Subject Variety

Across the full set, use a natural mixture of:

- First and second person: `I`, `you`, `we`
- Third-person pronouns: `he`, `she`, `it`, `they`
- People and possessive noun phrases: `Tom`, `Lucy`, `my mom`, `his friend`, `the teacher`
- Singular animals or things: `the dog`, `a cat`, `the boat`
- Plural or coordinated subjects: `the children`, `my parents`, `Tom and Lucy`, `a boy and a girl`

Do not force every subject type when it makes the selected clause unnatural.

## Output

Return:

1. The matched clause heading.
2. A numbered list containing only the generated sentences.

Do not mention which words came from the vocabulary files. Keep the response ready to use directly as a practice sheet.
