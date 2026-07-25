---
name: learn-a-word
description: Explain an English word in depth by covering its distinct modern meanings across parts of speech, figurative uses, conversational uses, and important phrases, with 3–5 beginner-friendly example sentences for every meaning. Use when the user asks to learn, define, explore, understand, or practise one word and wants comprehensive meanings with examples restricted to the grammar available in this repository.
---

# Learn a Word

Teach one English word comprehensively in clear English and demonstrate every meaning with grammar from the project.

## Input

Treat the supplied word as the required `word` parameter. Accept capitalization and an inflected form, but organize the answer under the standard dictionary form when appropriate.

If no word is supplied, ask for one. If the input could be more than one word or part of speech, explain the interpretation briefly and cover each valid interpretation.

Also accept an optional example count from 3 through 5. Use four examples per meaning by default.

## Workflow

1. Locate the project root containing `grammar/` and `vocab/`. Search the current workspace if these paths are not present in the working directory.
2. Read every `.md` file directly inside `grammar/` on every invocation. Ignore sections named **Quick Practice** when building the grammar allowlist.
3. Read every `.txt` file directly inside `vocab/`. Treat labels such as `unit-1` as headings, not vocabulary.
4. Identify the word's standard form, relevant inflected forms, and parts of speech.
5. Build a meaning inventory before writing. Include:
   - Distinct common literal meanings
   - Common figurative and conversational meanings
   - Meanings from each modern part of speech
   - Important phrasal verbs, fixed phrases, and idioms in which the word changes meaning
   - Notable less-common, informal, regional, or specialized meanings, clearly labeled
6. Keep genuinely different meanings separate, but group tiny contextual variations that share the same core idea. Order meanings from most common and beginner-useful to less common.
7. Explain each meaning in simple English, state its part of speech, add a usage label when helpful, and generate the requested number of examples.
8. Audit every example against the current grammar files and the checks below.

## Meaning Coverage

- Aim for comprehensive coverage of established modern English without inventing a sense merely because the word can appear in a special context.
- Do not omit a meaning because it is figurative, informal, or a different part of speech.
- Include an idiom or phrasal verb only when the target word contributes a distinct meaning that a learner should know.
- Treat a fixed expression as evidence for its established meaning only; do not invent a broader sense by replacing part of the expression with an unusual word or amount.
- Separate homographs when the same spelling represents unrelated words.
- For a word with an unusually large number of technical or domain-specific senses, cover all common meanings and the important specialized groups. Add a short coverage note instead of pretending that every profession-specific use is finite.
- Do not confuse a derived word with a meaning of the requested word. Mention a derived form only when it helps explain usage.

## Explanations

- Write definitions and usage notes in plain, beginner-friendly English.
- Distinguish close meanings by explaining the context in which each one is used.
- Identify the part of speech for every meaning, such as **noun**, **verb**, **adjective**, **adverb**, or **interjection**.
- Add concise labels such as **informal**, **less common**, **regional**, or **technical** only when accurate and useful.
- Do not add translations unless the user requests them.

## Example Sentences

- Give four examples for every meaning by default, or the user's requested count from 3 through 5.
- Use only sentence patterns, clauses, tense forms, question forms, negatives, and connectors documented in `grammar/`.
- Treat connectors and embedded clauses as grammar. With the current files, use only **and**, **but**, and **because** to join ideas, plus relative **who**, **that**, and **where** as documented. Do not use **when**, **after**, **before**, **if**, **so**, or another clause introducer unless it is added to `grammar/`.
- Use the target word, an appropriate inflected form, or the complete target phrase in every example. Bold that occurrence.
- Make the intended meaning clear from context and do not let an example accidentally demonstrate a different sense.
- For an idiom, phrasal verb, informal expression, or specialized meaning, preserve its normal wording, complements, register, and collocations in every example. Do not create examples by analogy when native speakers would not normally use the expression that way.
- Prefer vocabulary from `vocab/`, but add familiar beginner words such as `dog`, `cat`, `book`, `school`, and `ball` when needed.
- Vary subjects, situations, sentence patterns, and tenses naturally while keeping every sentence child-appropriate.
- Preserve correct capitalization, punctuation, articles, plurals, verb forms, and subject–verb agreement.
- For an interjection or another form normally used alone, place it in a simple documented carrier sentence when needed, such as `Tom says, "**Cool!**"`
- Do not use an unsupported grammar construction merely to make a difficult meaning easier to demonstrate.

## Output

Return:

1. A heading with the standard form of the word.
2. A one-line overview listing its parts of speech.
3. One numbered meaning section per distinct sense, using a short meaning label and the part of speech.
4. A simple English explanation and any necessary usage label.
5. A bulleted list of 3–5 example sentences under every meaning.
6. A brief coverage note only when the word has an open-ended set of rare technical meanings.

Keep the result organized as a reusable study sheet. Do not mention which words came from the vocabulary files.
