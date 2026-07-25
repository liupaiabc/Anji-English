---
name: clause-practice
description: Generate 20–30 varied beginner English practice sentences from a requested heading or subsection in grammar/clauses.md, using project vocabulary and optionally applying a tense or other grammar restriction documented in the grammar folder. Use when the user asks for sentence examples, drills, or practice for a clause title such as "Attributive Clause (Relative Clause)" or a subsection such as "Use who for people."
---

# Clause Practice

Generate beginner-friendly sentences for one selected clause from the project grammar guide.

## Input

Treat the requested clause title as the `clause_title` parameter. Accept any of these forms:

- The complete Markdown heading, such as `## Attributive Clause (Relative Clause)`
- A complete subsection heading, such as `### Use **who** for people`
- The heading text without Markdown markers
- A heading number when the requested heading has one

If the request clearly identifies one heading, proceed without asking for confirmation. If it matches no heading or more than one heading, list the matching headings briefly and ask the user to choose one.

Also accept an optional `grammar` restriction, such as `simple past tense` or `present tense`. Map `present tense` to **Simple Present Tense** and `past tense` to **Simple Past Tense** unless the user names a different form explicitly.

## Workflow

1. Locate the project root containing `grammar/` and `vocab/`. Search the current workspace if the paths are not present in the working directory.
2. Read every `.md` file directly inside `grammar/` on every invocation so the skill follows the latest clauses and can enforce requested grammar restrictions.
3. Match `clause_title` to one `##` or `###` heading in `grammar/clauses.md`. Ignore headings named **Quick Practice**.
4. Read the selected material:
   - For a `##` heading, read its entire section, including its `###` subsections, stopping at the next `##` heading.
   - For a `###` heading, read its parent `##` definition and only the selected subsection, stopping at the next `###` or `##` heading.
5. Resolve an optional grammar restriction against the current grammar headings and rules. If it is unavailable, list the closest documented choices instead of using unsupported grammar.
6. Read all `.txt` files directly inside `vocab/`. Treat labels such as `unit-1` as headings, not vocabulary.
7. Generate 25 sentences by default. Generate another count only when the user requests one, and keep it from 20 through 30 inclusive.
8. Check every sentence against the selected clause or subsection, every requested grammar restriction, and the quality rules below before responding.

## Clause Rules

- Include the selected type of clause in every sentence.
- Write a complete main sentence and a complete, correctly attached clause; do not write sentence fragments.
- Place the clause where the selected section says it belongs.
- Follow distinctions taught in the selected section. For the current attributive clause, use **who** for people, **that** for animals or things, and **where** for places.
- Make each clause add useful information instead of repeating the main sentence.
- Use varied main-sentence structures; do not begin most sentences with the same phrase such as `This is`.

## Sentence Rules

- Write complete, natural, beginner-level sentences.
- Prefer words from `vocab/`. Add familiar beginner words when needed, including names and words such as `dog`, `cat`, `boat`, `book`, `school`, and `ball`.
- Keep sentences clear and easy for a beginner to understand, but vary their length naturally.
- Vary vocabulary, subjects, actions, and meaning; do not produce near-duplicates by changing only a name or noun.
- Use ordinary, positive, child-appropriate situations unless the selected clause requires something else.
- Preserve correct capitalization, punctuation, articles, plurals, verb forms, pronoun references, and subject–verb agreement.
- When the user supplies a grammar restriction, apply it to every sentence without changing the selected clause.
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
