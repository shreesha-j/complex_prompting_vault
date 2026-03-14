# FAC Context Loader

This folder isolates one prompt concept so you can understand what it is for without mixing it with unrelated prompt assets.

## Why this folder exists

Separates the first-stage FAC context prompt from the downstream prompts because it serves as the bootstrap for the rest of the FAC generation chain.

## What it contains

The prompt that loads FAC framework knowledge and establishes the system role before requirement analysis or code generation.

## Files in this folder

- `context_prompt.txt`: FAC context prompt; source `/Users/sreeshaj/Documents/Work/lyik_meta/fac_generator/llm/prompts/context_prompt.txt`; sha256 `6a55d6496593`

## Notes

This is the Level 1 prompt in the FAC generation pipeline.
