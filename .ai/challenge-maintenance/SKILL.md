---
name: challenge-maintenance
description: Guidelines for adding, updating, and verifying OWASP Juice Shop challenge documentation based on challenges.yml.
---

# Challenge Maintenance Skill

Use this skill when you need to add new challenges, update existing ones, or verify that the documentation is in sync with the source of truth: `docs/modules/ROOT/assets/data/challenges.yml`.

## Core Principles

1. **Source of Truth**: Always use `challenges.yml` as the authoritative source for challenge names, descriptions, categories, difficulties, and hints.
2. **Alphabetical Order**: Maintain strict alphabetical order by challenge name in all summary tables (README.adoc, category files).
3. **Consistency**: Ensure hints and solution placeholders exist for every challenge.
4. **Cross-Referencing**: Use consistent anchor names derived from section headers.
5. **Quality Descriptions**: Write unique prose for challenge descriptions. Do not copy the description from `challenges.yml` 1:1, and do not just concatenate hints.

## Adding a New Challenge

When a new challenge is added to `challenges.yml`, follow these steps:

### 1. Identify the Target Files
- **Category File**: Locate the `.adoc` file in `docs/modules/ROOT/pages/part2/` corresponding to the challenge's category (e.g., `injection.adoc` for 'Injection').
- **Hints File**: Hint partials are managed by the `partialize_hints.yml` pipeline. AI agents must not create or modify them.
- **Master List**: Update `docs/modules/ROOT/pages/part2/README.adoc`.
- **Solutions**: Update `docs/modules/ROOT/pages/appendix/solutions.adoc`.

### 2. Update the Category File
- Add a row to the "Challenges covered in this chapter" table.
- Add a detailed section:
    ```asciidoc
    [[_{anchor_name}]]
    == {Section Header}

    {Description}

    include::../../partials/hints/{challengeKey}.adoc[]
    ```
- **{Description}**: A paragraph introducing the challenge. This should be original text, not a verbatim copy of the YAML description or a mere mash-up of the hints.
- **Section Header**: Usually the first sentence of the description or a concise instruction.
- **Anchor Name**: Lowercase version of the Section Header with spaces replaced by underscores and special characters removed.

### 3. Hint Partials
- Hint partials in `docs/modules/ROOT/partials/hints/` are managed exclusively by the `partialize_hints.yml` pipeline.
- AI agents MUST NOT create or modify these files.
- **Exception**: The 'Score Board' challenge (`scoreBoardChallenge`) does not have hints and must NEVER have a hint partial file.

### 4. Update the README.adoc
- Add the challenge to the "Challenge hunting" table in alphabetical order.
- Add the challenge to the "Challenge hunting (CTF mapping)" table in alphabetical order.
- Use `xref` links to the category file and the solution section.

### 5. Update the Solutions Appendix
- Locate the section for the challenge's difficulty (e.g., `== ⭐⭐⭐ Challenges`).
- Add a subsection `=== {Section Header}`.
- Add the placeholder: `// TODO Add solution for {challengeKey}`.
- Ensure subsections are sorted alphabetically within the difficulty level.

### 6. Update Tags (if necessary)
- If the challenge introduces a new tag not yet documented, update `docs/modules/ROOT/pages/part1/challenges.adoc` in alphabetical order.

## Verification & Cleanup

When asked to verify if the documentation is up to date:
1. **Gaps**: Compare `challenges.yml` with `README.adoc`. Identify any missing challenges.
2. **Leftovers**: Identify sections or files referring to challenges no longer in `challenges.yml`.
3. **Desyncs**: Check if descriptions or hints in the docs match the latest YAML content.
4. **Broken Links**: Verify that all `xref` and `<<anchor>>` links point to existing targets.

See `checklists/challenge_verification.md` for a detailed verification procedure.
