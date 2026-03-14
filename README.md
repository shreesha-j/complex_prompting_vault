# complex_prompting_vault

This vault now contains a curated copy of the prompt files you created across `Documents/Work` and your Obsidian vaults.

## What is inside

- `imports/raw/`: direct copies of the original prompt files, kept close to their original path structure.
- `prompt_library/`: organized prompt folders grouped by meaning, with one isolated folder per prompt concept.
- `catalog/`: an index of what was imported, including a machine-readable manifest and duplicate detection notes.

## Category layout

- `documentation-generation/`: Prompts that turn transcripts, codebases, or broad topics into large documentation sets. (4 folders)
- `fac-form-generation/`: Prompts used by the FAC generation flow to load context, map requirements, and generate code. (3 folders)
- `workflow-orchestration/`: Prompts that control chat handoff, context loading, checkpointing, and resumable work. (3 folders)

## Why this structure exists

You asked for all of your prompt files to live in this repo, but also to be separated clearly with an explanation of what each prompt folder means. The vault therefore has two layers:

1. Preservation layer: `imports/raw/` keeps the original files together inside this repo without changing the source locations.
2. Meaning layer: `prompt_library/` reorganizes the same prompt material by use case so it is easier to browse and reuse.

## Current scope

- Imported raw files: 12
- Curated prompt folders: 10
- Source roots scanned: `Documents/Work`, `Documents/obsidian_vault`, `Documents/Synthing/obsidian_vault`

## Notes

- Source files were copied, not moved.
- Exact duplicate prompt files are documented in `catalog/README.md`.
- Each prompt folder includes its own `README.md` describing why it exists and what it contains.
