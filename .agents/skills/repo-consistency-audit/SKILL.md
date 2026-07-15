---
name: repo-consistency-audit
description: Audit and safely repair cross-repository inconsistencies in file references, Markdown links, learning-content scope, skill instructions, skill metadata, examples, counts, names, and repository guidance. Use after files are renamed, grammar/topics/vocabulary are added or removed, skills change, documentation becomes stale, or the user asks to check, sync, reconcile, or fix mismatched data across this English-learning repository.
---

# Repository Consistency Audit

Compare the repository's files as one system, repair safe mismatches, and report anything that requires a content decision.

## Default Behavior

Audit the whole repository and fix unambiguous inconsistencies unless the user asks for report-only mode. Do not stop after finding the first mismatch. Re-audit after edits because one fix can expose another stale reference.

## Workflow

1. Find the repository root and read every applicable `AGENTS.md` before evaluating files.
2. Inspect `git status --short` and preserve all existing user changes. Never discard, reset, or overwrite unrelated work.
3. Inventory files with `rg --files --hidden -g '!.git/**'`. Include hidden repository skills under `.agents/`.
4. Read the current source material:
   - `README.md` and repository guidance
   - Every `.md` file in `grammar/`
   - `topics/topics.md`
   - Every `.txt` file in `vocab/`
   - Every skill's `SKILL.md` and `agents/openai.yaml`
5. Build current facts from the files rather than relying on remembered names, counts, headings, or scope.
6. Run every audit category below, make safe fixes with `apply_patch`, and record ambiguous findings.
7. Repeat the inventory and targeted searches after editing. Confirm that stale values no longer appear except where they are intentionally historical.
8. Run relevant validation, including Markdown-link checks, skill validation for changed skills, and `git diff --check` when available.

## Audit Categories

### File and Path References

- Resolve every relative Markdown link from the file containing it and flag missing targets.
- Search all text files for explicit repository paths and filenames, including inline code, examples, YAML, and skill instructions.
- Detect references to renamed or deleted files. When one replacement is unambiguous, update every live reference to the current path.
- Use hidden-file searches such as `rg --hidden --glob '!.git/**'` so skill references are not missed.
- Check filename case as well as spelling.
- Do not replace a stale name blindly when more than one current file is a plausible target; report the candidates.

### Learning-Content Scope

- Derive the current sentence-pattern, clause, and tense scope from headings in `grammar/`.
- Keep README summaries, examples, and statements of current scope aligned with those headings.
- Check hard-coded grammar allowlists or mappings in skills against the latest grammar files.
- When a new grammar section is added, confirm that title-matching workflows can select it and that documentation does not still claim an older limited scope.
- Check heading levels, numbering, duplicate headings, and gaps that would break title- or number-based skill selection.
- Keep `topics/topics.md` as topic names only and detect duplicate or malformed items.
- Check vocabulary-file discovery rules and direct vocabulary links against the actual files in `vocab/`. Treat unit labels as organization, not vocabulary.

### Skill Consistency

For every directory under `.agents/skills/`, verify:

- The directory name, `SKILL.md` frontmatter `name`, `$skill-name` references, and `agents/openai.yaml` default prompt agree.
- Frontmatter contains the required `name` and `description`, and the body matches that description.
- `display_name`, `short_description`, and `default_prompt` still describe the implemented behavior.
- Referenced source files and directories exist.
- Input forms, selectable heading levels, default counts, allowed ranges, grammar restrictions, and output formats agree across the description, workflow, examples, metadata, and README.
- Runtime source-loading rules cover newly added files instead of relying on obsolete fixed filenames.
- Sections named `Quick Practice` are excluded when the skill promises to ignore them.

### Documentation and Guidance

- Ensure README learning-material links, skill lists, skill counts, usage examples, and extension instructions match the repository.
- Ensure `AGENTS.md` guidance matches current layout and does not contradict a skill or README promise.
- Detect old names copied into prose after a file, heading, topic, or skill is renamed.
- Update documentation when a new skill or learning-material category changes a statement such as a count or list.

### Data and Contract Integrity

- Check duplicate list entries, conflicting defaults, contradictory ranges, mismatched examples, and inconsistent terminology.
- Check topic names, grammar headings, and vocabulary entries for obvious data-entry typos. Fix only when the intended value is unambiguous; otherwise report the suspected typo without changing it.
- Verify that examples reference real topics, grammar headings, clause headings, sentence-pattern numbers, and skill names.
- Compare generated-output promises such as monologue versus dialog, numbered versus unnumbered output, and sentence counts across all places where they are documented.
- Treat obvious cross-file spelling variants in identifiers or paths as mismatches. Do not rewrite ordinary lesson prose solely for style during a consistency audit.

## Fix Policy

- Fix safe, local, mechanically supported mismatches without asking first.
- Prefer updating references to match the current filesystem and source content. Do not rename or delete current source files merely to preserve stale documentation.
- Preserve the user's intended educational scope. Do not add new grammar, topics, or vocabulary to make an old claim true.
- Do not perform broad search-and-replace without inspecting every match in context.
- Do not modify generated practice content unless it is part of the repository and contradicts a documented source.
- If intent is ambiguous, leave files unchanged for that item and report the exact conflict, affected files, and available choices.

## Output

Lead with the audit outcome, then report:

- Files updated and the mismatches fixed
- Validation performed
- Remaining ambiguous or unresolved inconsistencies

If no mismatch exists, say that the repository is consistent and list the checks completed. Keep the report concise and link to changed files.
