# Quick Repository Curation Instruction Template

Use the repository-curation standard below and apply it to this repo.

Note: `Project-listing_handler` was not discoverable from the current workspace search, so the target repo and workspace placeholders below are intentionally left for manual replacement.

## Standard Prompt

### Multi-Repository Knowledge Workspace Standardizer

Use this prompt when you need to curate a workspace like `Jess/Git` where multiple repositories must be turned into organized knowledge libraries.

#### Objective

Standardize all target repositories so they are easy to browse, maintain, and reuse. Preserve original material where appropriate, isolate curated structures by meaning, and produce navigation docs plus migration and commit records.

#### Operating model

- Inspect before editing.
- Infer the meaning of files from names and representative contents.
- Prefer stable domain-based taxonomy over source-path mirroring, except in raw preservation layers.
- Never intentionally drop content. If something is empty or ambiguous, preserve it and document it.

#### Repository requirements

- Add `README.md` and `index.md` in the root and every curated folder where applicable.
- Use raw-preservation and curated layers where the repository needs both provenance and meaning-based navigation.
- Generate migration and commit-reference docs when moves, renames, or structured commit codes are involved.
- Keep manifests, catalogs, and workspace indexes aligned with the curated structure.

#### Migration and safety rules

- Preserve content first, reorganize second.
- If old paths disappear because of moves, document the mapping.
- Remove only folders that become empty after the move.
- If a note is empty but belongs in the structure, retain it as a documented placeholder rather than silently dropping it.

#### Output expectations

- A clean curated tree
- README/index coverage
- Updated manifests and catalogs where needed
- Path migration documentation where moves occurred
- Commit-code documentation if structured commit codes are used
- A final commit message when requested

---

Target repo:
`/absolute/path/to/target-repo`

Workspace root:
`/absolute/path/to/workspace-root`

Precedent repos:
- `/Users/sreeshaj/Documents/Work/temp/Local_project/Jess/Git/Notes`
- `/Users/sreeshaj/Documents/Work/temp/Local_project/Jess/Git/Context-Database_Handler`
- `/Users/sreeshaj/Documents/Work/temp/Local_project/Jess/Git/complex_prompting_vault`

Rules:
- Inspect first, then infer meaning before restructuring.
- Reorganize into meaning-based folders.
- Normalize names to lowercase kebab-case where safe.
- Add `README.md` and `index.md` in root and every curated folder.
- Preserve content; do not silently delete files.
- Create `path-migration-map.md` for moved/renamed paths.
- Create `commit-code-reference.md` if commit codes are used.
- Use raw + curated layers if needed.
- Isolate support assets where appropriate.
- Remove only empty directories after the move.
- Update parent workspace index if applicable.
- Preserve tooling-required filenames/paths and document exceptions.
- Prefer move/rename over copy unless raw-preservation requires copying.

Final output must include:
- what changed
- what was moved vs copied
- what docs/manifests were added
- any migration-map or commit-code docs created
- any tooling/naming exceptions kept
- finalized commit message
