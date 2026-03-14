# Multi-Repository Knowledge Workspace Standardizer

Use this prompt when you need to curate a workspace like `Jess/Git` where multiple repositories must be turned into organized knowledge libraries.

## Objective

Standardize all target repositories so they are easy to browse, maintain, and reuse. Preserve original material where appropriate, isolate curated structures by meaning, and produce navigation docs plus migration and commit records.

## Target repositories

1. `Notes`
2. `Context-Database_Handler`
3. `complex_prompting_vault`
4. The workspace-level `Jess/Git/index.md`

## Operating model

- Inspect before editing.
- Infer the meaning of files from names and representative contents.
- Prefer stable domain-based taxonomy over source-path mirroring, except in raw preservation layers.
- Never intentionally drop content. If something is empty or ambiguous, preserve it and document it.

## Repository requirements

### 1. Notes

- Convert the repo into a domain-based note library.
- Normalize folder and file names to lowercase kebab-case.
- Create `README.md` and `index.md` in the root and every curated folder.
- Separate assets and workspace files from note bodies when needed.
- When moving or renaming existing files, generate `path-migration-map.md`.
- When defining structured commit codes, generate `commit-code-reference.md`.
- If the repo sits inside a larger workspace, update the workspace index so the key records are easy to find.

### 2. Context-Database_Handler

- Use a two-layer model:
  - `imports/raw/` for preserved source copies.
  - `context_library/` for curated, isolated context bundles grouped by project and purpose.
- Give each curated bundle its own folder and `README.md`.
- Maintain machine-readable indexes in `catalog/`.
- Track duplicates separately if they exist.
- Use meaningful project and group names instead of dumping raw directory names directly into the curated layer.

### 3. complex_prompting_vault

- Use a two-layer model:
  - `imports/raw/` for preserved source prompt files.
  - `prompt_library/` for curated prompt concepts grouped by meaning.
- Give each prompt concept its own isolated folder with a `README.md` explaining why it exists and what it contains.
- Keep category-level `README.md` files updated.
- Maintain `catalog/prompt-manifest.json`.
- If a prompt is created directly inside the vault, record it clearly as vault-authored instead of pretending it came from a raw import.

### 4. Workspace index

- Maintain a top-level `index.md` under the parent workspace folder.
- Link each curated repo plus its most important records: root README, manifests, migration map, commit code reference, duplicate index, and other high-signal navigation docs.

## Documentation standards

- Every curated folder should answer:
  - why this folder exists
  - what it contains
  - how it should be used
- `index.md` should be navigation-first.
- `README.md` should be explanation-first.
- Use concise, explicit naming.
- Keep support files like images or workspace configs in isolated subfolders.

## Catalog and manifest rules

- Update counts when folders or files are added.
- Keep category descriptions aligned with the actual folder purpose.
- When applicable, record:
  - title
  - slug
  - category
  - library path
  - why
  - contains
  - notes
  - source or origin
  - file hashes and sizes if a manifest already uses them

## Migration and safety rules

- Preserve content first, reorganize second.
- If old paths disappear because of moves, document the mapping.
- Remove only folders that become empty after the move.
- If a note is empty but belongs in the structure, retain it as a documented placeholder rather than silently dropping it.

## Output expectations

- A clean curated tree for each repo
- README/index coverage across the curated structure
- Updated manifests and catalogs
- Path migration documentation where moves occurred
- Commit-code documentation if structured commit codes are used
- A final commit message with stable change codes when requested

## Final deliverable style

At the end, summarize:

- what changed in each repository
- which docs or manifests were added or updated
- whether files were moved, copied, or authored in-vault
- the final commit message if needed
