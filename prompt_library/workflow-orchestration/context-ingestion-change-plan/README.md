# Context Ingestion Change Plan

This folder isolates one prompt concept so you can understand what it is for without mixing it with unrelated prompt assets.

## Why this folder exists

Keeps the context-then-instruction workflow prompt separate because it governs how a chat should process large context dumps before making changes.

## What it contains

A staged workflow prompt that waits for `STOP-IT`, summarizes context, and only then moves into actual implementation planning.

## Files in this folder

- `Context Prompt.md`: Obsidian context workflow prompt; source `/Users/sreeshaj/Documents/obsidian_vault/Fac/Prompt_list/Context Prompt.md`; sha256 `e8dea930356b`

## Notes

Useful when you want the model to absorb context first and avoid premature edits.
