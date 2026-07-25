# Anji English

Anji English is a collection of beginner-friendly English learning materials and reusable Codex practice skills. The lessons focus on clear grammar, familiar vocabulary, and child-appropriate examples.

## Learning Materials

- [Sentence Patterns](grammar/sentence-patterns.md): Common ways to build simple English sentences.
- [Clauses](grammar/clauses.md): Beginner clause lessons, currently focused on attributive (relative) clauses with **who**, **that**, and **where**.
- [Tenses](grammar/tenses.md): The simple present, present continuous, and simple past tenses.
- [Topics](topics/topics.md): Topic names for beginner speaking and writing practice.
- Vocabulary: Preferred words for examples and generated practice in [Words 1](vocab/words-1.txt) and [Words 2](vocab/words-2.txt).

## Practice Skills

The repository includes five project skills under `.agents/skills/`. Codex reads these skills when working in this repository.

| Skill | Purpose | Example |
| --- | --- | --- |
| `$sentence-pattern-practice` | Generate 20–30 sentences for one sentence pattern. | `$sentence-pattern-practice pattern 5` |
| `$clause-practice` | Generate 20–30 sentences for one clause lesson. | `$clause-practice Attributive Clause (Relative Clause)` |
| `$topic-practice` | Generate a topic monologue or a requested dialog using the available grammar. | `$topic-practice Home` |
| `$learn-a-word` | Explain a word's meanings in depth with grammar-controlled examples. | `$learn-a-word cool` |
| `$repo-consistency-audit` | Find and safely repair mismatches across repository content, references, skills, and documentation. | `$repo-consistency-audit audit this repository` |

You can add restrictions to a request when needed:

```text
$sentence-pattern-practice pattern 8 using the past tense
$topic-practice Food using only the simple present tense
$topic-practice Telephone Calls as a dialog
$learn-a-word cool
$repo-consistency-audit check the repository after a file rename
```

Each skill reads its relevant current files in `grammar/`, `topics/`, and `vocab/` when it runs. New learning content is therefore available to the skills without copying it into their instructions.

## Adding Learning Content

- Add sentence structures to the appropriate category in `grammar/sentence-patterns.md` as numbered `###` sections. Add a new `##` category only when none of the existing groups fit.
- Add clauses to `grammar/clauses.md` as separate `##` sections, with `###` subsections when helpful.
- Add tenses to `grammar/tenses.md` only when they are ready to be taught.
- Keep `topics/topics.md` as a list of topic names only.
- Put vocabulary words in `vocab/*.txt`, one word or phrase per line. Unit labels such as `unit-1` may be used to organize them.

Keep all explanations and examples natural, concise, and suitable for a beginner learner.
