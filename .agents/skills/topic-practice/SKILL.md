---
name: topic-practice
description: Generate a 10–20-sentence beginner English monologue or requested dialog about one topic listed in topics/topics.md, using project vocabulary and only grammar documented in the grammar folder. Use when the user requests topic-based speaking or sentence practice, optionally limited to specific grammar such as the simple present tense, present continuous tense, past tense, an attributive clause, or a numbered sentence pattern.
---

# Topic Practice

Generate beginner-friendly practice sentences for one project topic while enforcing the project's grammar boundaries.

## Input

Treat the requested topic as the required `topic` parameter. Match it case-insensitively to a bullet in `topics/topics.md`.

Also accept these optional controls:

- `grammar`: One or more grammar headings, common grammar names, or sentence-pattern numbers
- `count`: A number from 10 through 20
- `format`: `monologue` or `dialog`; default to `monologue`

Examples:

- `Food`
- `Food, using only the simple present tense`
- `Animals, using sentence patterns 1 and 2`
- `Family, using the simple past tense and attributive clauses, 12 sentences`
- `Telephone Calls, as a dialog using the simple present tense`

If the topic clearly matches one list item, proceed without confirmation. If it does not match or matches more than one item, show the closest topic names briefly and ask the user to choose.

## Workflow

1. Locate the project root containing `topics/topics.md`, `grammar/`, and `vocab/`. Search the current workspace if these paths are not present in the working directory.
2. Read `topics/topics.md`, every `.md` file directly inside `grammar/`, and every `.txt` file directly inside `vocab/` on every invocation.
3. Match `topic` to one topic-list item. Do not invent a new topic.
4. Resolve each grammar limit against the current grammar headings and their common names. Map `present tense` to **Simple Present Tense**, `past tense` to **Simple Past Tense**, and `attributive clause` to **Attributive Clause (Relative Clause)**. Keep **Present Continuous Tense** separate unless the user explicitly requests it.
5. Build an allowlist from the grammar files. Ignore sections named **Quick Practice** when defining the allowlist.
6. Apply each requested grammar limit within its category:
   - A tense limit controls which documented tense forms may be used.
   - A sentence-pattern limit controls which numbered sentence structures may be used.
   - A clause limit controls which documented clause forms may be used.
   - Leave unspecified categories available when they are compatible with every requested limit.
7. If a requested grammar form is missing from `grammar/`, say that it is not currently available and list the closest documented choices. Do not generate the sentences using unsupported grammar.
8. Use a monologue unless the user explicitly requests a dialog or dialogue.
9. Generate 15 sentences by default. Use a requested count only when it is from 10 through 20 inclusive. For a dialog, count the spoken sentences rather than the speaker labels.
10. Check every sentence for topic relevance, allowed grammar, and the quality rules below.

## Grammar Boundary

- Use only sentence structures, clauses, and tense forms explicitly taught or demonstrated in `grammar/`.
- Do not introduce future forms, perfect tenses, passive voice, conditionals, or other constructions unless they are added to the grammar files later.
- Treat connecting words and embedded clauses as grammar, not just vocabulary. Build their allowlist from `grammar/`. Currently, use only **and**, **but**, and **because** to join ideas, plus relative **who** for people, **that** for animals or things, and **where** for places. Do not use unsupported clause introducers such as **so**, **if**, **when**, **after**, **before**, or **although**. Use **what**, **when**, **why**, and **how** only in the question patterns documented in `grammar/sentence-patterns.md`, not as unsupported embedded clauses.
- Use statements, negatives, questions, and short answers only when the allowed grammar documents those forms.
- Satisfy all requested grammar limits at the same time. If two limits are incompatible, explain the conflict briefly and ask the user which limit to change.
- Keep the main meaning centered on the selected topic even when using vocabulary from another topic.

## Vocabulary and Sentence Quality

- Prefer words from all `.txt` files in `vocab/`. Treat labels such as `unit-1` as headings, not vocabulary.
- Add familiar beginner words when needed, including simple words such as `dog`, `cat`, `easy`, `book`, `school`, and `ball`.
- Write complete, natural, child-appropriate sentences that are easy for a beginner to understand.
- Vary sentence length naturally, vocabulary, subjects, and meaning.
- Avoid near-duplicates that change only a name, pronoun, or one noun.
- Preserve correct capitalization, punctuation, articles, plurals, verb forms, and subject–verb agreement.
- For a monologue, make the sentences flow naturally as one connected passage about the topic.
- For a dialog, choose two or three simple names and write one complete spoken sentence per line. Make the speakers respond naturally to each other and reuse the same names throughout.
- Do not add translations, blanks, answers, or grammar explanations unless the user asks for them.

## Output

Return:

1. A heading containing the matched topic.
2. A short `Grammar:` line only when the user supplied a grammar limit.
3. The practice in the requested format:
   - **Monologue:** Put all sentences together in one paragraph. Do not number or bullet them.
   - **Dialog:** Put each turn on its own line as `Name: Sentence.` Do not number or bullet the lines. Randomly choose two or three simple speaker names.

Do not mention which words came from the vocabulary files. Keep the result ready to use as a practice sheet.
