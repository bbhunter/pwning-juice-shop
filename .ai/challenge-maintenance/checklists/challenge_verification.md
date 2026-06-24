# Challenge Documentation Verification Checklist

Follow these steps to verify that the documentation is in sync with `challenges.yml` and clean up any leftovers.

## 1. Inventory Check
- [ ] Load all challenges from `docs/modules/ROOT/assets/data/challenges.yml`.
- [ ] List all challenge names and keys.

## 2. Master List Verification (`README.adoc`)
- [ ] Verify that every challenge from the inventory is present in the "Challenge hunting" table.
- [ ] Verify that every challenge from the inventory is present in the "Challenge hunting (CTF mapping)" table.
- [ ] Ensure both tables are sorted alphabetically by challenge name.
- [ ] Check for "Ghost Challenges": Entries in the tables that are not in the inventory. Remove them.

## 3. Category Files Verification (`part2/*.adoc`)
- [ ] For each challenge, verify it is listed in the summary table of its respective category file.
- [ ] Verify that the category file has a detailed section (Header + Description + Hints Include) for the challenge.
- [ ] Ensure the detailed section has a correctly named anchor.
- [ ] Verify that the description in the detailed section is high-quality prose and NOT a verbatim copy of the YAML description or a mash-up of hints.
- [ ] Remove any detailed sections for challenges that no longer exist.

## 4. Hints Verification (`partials/hints/*.adoc`)
- [ ] Verify that a hint file `{challengeKey}.adoc` exists for every challenge EXCEPT 'Score Board' (`scoreBoardChallenge`).
- [ ] Ensure hint files are NOT modified by AI agents. They are managed by the `partialize_hints.yml` pipeline.
- [ ] Identify and delete orphan hint files (those whose key is not in the inventory).

## 5. Solutions Verification (`solutions.adoc`)
- [ ] Verify that every challenge has a subsection in `docs/modules/ROOT/pages/appendix/solutions.adoc`.
- [ ] Verify that challenges are in the correct difficulty section (⭐ to ⭐⭐⭐⭐⭐⭐).
- [ ] Ensure subsections are sorted alphabetically within each difficulty level.
- [ ] Check for missing solution placeholders: Every entry should have either a solution or a `// TODO Add solution for {challengeKey}`.
- [ ] Standardize TODOs: Use `// TODO Add solution for {challengeKey}` for consistency.

## 6. Tags Verification (`part1/challenges.adoc`)
- [ ] List all unique tags used in `challenges.yml`.
- [ ] Verify that every tag is documented in `docs/modules/ROOT/pages/part1/challenges.adoc`.
- [ ] Ensure the tag list is sorted alphabetically.

## 7. Cross-Reference Audit
- [ ] Check for broken `xref` links in `README.adoc`.
- [ ] Check for broken `<<anchor>>` links throughout the documentation.
- [ ] Ensure `ifeval` blocks (like for the 'Tutorial' tag) are correctly preserved and functional.
