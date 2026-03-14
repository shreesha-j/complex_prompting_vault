# Repository Curation Instruction Template

Use the repository-curation standard below as the governing instruction for this task.

Note: `Project-listing_handler` was not discoverable from the current workspace search, so the target repo and workspace placeholders below are intentionally left for manual replacement.

## Standard Prompt

### Multi-Repository Knowledge Workspace Standardizer

Use this prompt when you need to curate a workspace like `Jess/Git` where multiple repositories must be turned into organized knowledge libraries.

#### Objective

Standardize all target repositories so they are easy to browse, maintain, and reuse. Preserve original material where appropriate, isolate curated structures by meaning, and produce navigation docs plus migration and commit records.

#### Target repositories

1. `Notes`
2. `Context-Database_Handler`
3. `complex_prompting_vault`
4. The workspace-level `Jess/Git/index.md`

#### Operating model

- Inspect before editing.
- Infer the meaning of files from names and representative contents.
- Prefer stable domain-based taxonomy over source-path mirroring, except in raw preservation layers.
- Never intentionally drop content. If something is empty or ambiguous, preserve it and document it.

#### Repository requirements

##### 1. Notes

- Convert the repo into a domain-based note library.
- Normalize folder and file names to lowercase kebab-case.
- Create `README.md` and `index.md` in the root and every curated folder.
- Separate assets and workspace files from note bodies when needed.
- When moving or renaming existing files, generate `path-migration-map.md`.
- When defining structured commit codes, generate `commit-code-reference.md`.
- If the repo sits inside a larger workspace, update the workspace index so the key records are easy to find.

##### 2. Context-Database_Handler

- Use a two-layer model:
  - `imports/raw/` for preserved source copies.
  - `context_library/` for curated, isolated context bundles grouped by project and purpose.
- Give each curated bundle its own folder and `README.md`.
- Maintain machine-readable indexes in `catalog/`.
- Track duplicates separately if they exist.
- Use meaningful project and group names instead of dumping raw directory names directly into the curated layer.

##### 3. complex_prompting_vault

- Use a two-layer model:
  - `imports/raw/` for preserved source prompt files.
  - `prompt_library/` for curated prompt concepts grouped by meaning.
- Give each prompt concept its own isolated folder with a `README.md` explaining why it exists and what it contains.
- Keep category-level `README.md` files updated.
- Maintain `catalog/prompt-manifest.json`.
- If a prompt is created directly inside the vault, record it clearly as vault-authored instead of pretending it came from a raw import.

##### 4. Workspace index

- Maintain a top-level `index.md` under the parent workspace folder.
- Link each curated repo plus its most important records: root README, manifests, migration map, commit code reference, duplicate index, and other high-signal navigation docs.

#### Documentation standards

- Every curated folder should answer:
  - why this folder exists
  - what it contains
  - how it should be used
- `index.md` should be navigation-first.
- `README.md` should be explanation-first.
- Use concise, explicit naming.
- Keep support files like images or workspace configs in isolated subfolders.

#### Catalog and manifest rules

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

#### Migration and safety rules

- Preserve content first, reorganize second.
- If old paths disappear because of moves, document the mapping.
- Remove only folders that become empty after the move.
- If a note is empty but belongs in the structure, retain it as a documented placeholder rather than silently dropping it.

#### Output expectations

- A clean curated tree for each repo
- README/index coverage across the curated structure
- Updated manifests and catalogs
- Path migration documentation where moves occurred
- Commit-code documentation if structured commit codes are used
- A final commit message with stable change codes when requested

#### Final deliverable style

At the end, summarize:

- what changed in each repository
- which docs or manifests were added or updated
- whether files were moved, copied, or authored in-vault
- the final commit message if needed

---

## Task

Apply that standard to this target repository:

`/absolute/path/to/target-repo`

This repository is part of this workspace:

`/absolute/path/to/workspace-root`

Reference repositories whose curation style should be treated as precedent:

- `/Users/sreeshaj/Documents/Work/temp/Local_project/Jess/Git/Notes`
- `/Users/sreeshaj/Documents/Work/temp/Local_project/Jess/Git/Context-Database_Handler`
- `/Users/sreeshaj/Documents/Work/temp/Local_project/Jess/Git/complex_prompting_vault`

---

## Required Execution Rules

- Inspect the repository first and infer the meaning of the files before changing structure.
- Reorganize it into clear, meaning-based folders, not a random dump of source paths.
- Normalize folder and file names to lowercase kebab-case where appropriate.
- Add `README.md` and `index.md` in the root and in every curated folder.
- Keep explanation-first docs in `README.md` and navigation-first docs in `index.md`.
- Preserve content. Do not silently delete files.
- If files are moved or renamed, create `path-migration-map.md`.
- If commit codes are used, create `commit-code-reference.md`.
- Separate support assets like images, configs, workspace files, binaries, and media into isolated folders when needed.
- If the repo needs a raw-preservation layer and a curated layer, use both.
- If manifests or catalogs are needed, generate and update them.
- If empty files exist but still belong in the structure, keep them as documented placeholders.
- Remove only directories that become empty after the move.
- Update the parent workspace index if this repo is part of a larger curated workspace.

---

## Additional Operating Constraints

- Prefer move/rename over copy unless a raw-preservation layer is required.
- Do not alter content semantics unless explicitly required for documentation, indexing, or manifest generation.
- Preserve tooling-required names, paths, and special files where needed; document all exceptions.
- Ignore or document generated/cache/vendor folders unless they are explicitly in scope for curation.
- Preserve binary and media assets; relocate them only into clearly named support-asset folders when appropriate.
- If any referenced path cannot be read, state that explicitly in the final output and proceed with available inputs only.
- Before making structural changes, infer repository intent from file contents, file names, adjacency, and existing organization.
- Treat the structure and documentation style of the precedent repositories as the model for quality and consistency.

---

## Repo Profile

Fill this before running:

- **Target repo path:** `/absolute/path/to/target-repo`
- **Workspace root path:** `/absolute/path/to/workspace-root`
- **Purpose of repo:** `...`
- **Main content types:** `docs / code / prompts / assets / notes / mixed`
- **Tooling stack:** `python / node / obsidian / none / mixed`
- **Files or folders that must remain tool-compatible:** `...`
- **Folders to ignore from curation:** `node_modules, .git, dist, build, .cache, .venv, ...`
- **Whether raw + curated dual-layer is expected:** `yes / no / only if needed`
- **Parent workspace index to update:** `/absolute/path/to/workspace-root/index.md`
- **Commit-code convention in use:** `yes / no / unknown`
- **Special naming exceptions:** `...`

---

## Deliverables

Final output must include:

1. **What changed**
   - summary of the restructuring
   - reasoning behind the organization

2. **What was moved vs copied**
   - moved files/folders
   - copied files/folders
   - why copying was necessary, if used

3. **What was renamed**
   - original path
   - new path
   - reason for rename

4. **Docs and manifests added**
   - all `README.md`
   - all `index.md`
   - catalogs, manifests, inventories, or other generated docs

5. **Migration and commit-reference docs**
   - path to `path-migration-map.md`, if created
   - path to `commit-code-reference.md`, if created

6. **Exceptions**
   - tooling compatibility exceptions
   - naming exceptions
   - files intentionally left in place
   - unreadable paths or inaccessible references

7. **Final commit message**
   - one clean finalized commit message suitable for git

---

## Execution Style

Do the work in this order:

1. Inspect the repository structure and contents.
2. Infer semantic groupings from the actual materials.
3. Decide whether the repo needs:
   - direct curation only, or
   - both raw-preservation and curated layers.
4. Reorganize into meaning-based folders.
5. Normalize names where safe.
6. Add or update `README.md`, `index.md`, and any required manifests.
7. Create migration/reference docs if needed.
8. Remove only directories that are empty after the move.
9. Update the parent workspace index if applicable.
10. Report the final result using the required deliverables format.

Do not skip the inspection step.
Do not silently discard content.
Do not invent structure without grounding it in repository meaning.
