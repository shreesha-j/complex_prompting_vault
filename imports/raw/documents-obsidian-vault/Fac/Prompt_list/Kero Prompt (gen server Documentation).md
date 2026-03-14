## Use Multiple chat system
- So for the ai ide i will be giving a single file which has a complex understanding of what needs to be done
	- first is i will give a prompt file which has an proper instruction what needs to be done
	- need in that instrcution i need you to generate a simple summary small one of what is done in that current chat pause like a status of this ai agent generation in a md file 
	- next i will be needing to create another file in which has a context of what files covered and done (operation ) and also that path of that all written in that md file 
	- these above 2 md files can be big so i want you to instead of one md and another md file i need you to create a seperate folder for each of them in which summary/summar_1(what happend),summary_2(what happend) and also readme fiel in that folder tellling a info about what is this summary
	- same with this operation stastus folder in which one md file will contans a path and file name its done generateing documentation for that file so if any agent lost the limit then it will check which part it was doing and continue from that ,like if that documentation generation is done then only consider putting its status done if any issue then in pending state will be there this willl help to the another chat so that (all the time)it will check if any pending state then start from that 
	- this summary folder contains what a successful promtp out put gives like the information of hte what code files done and why it was done and its summary that information should be htere 
	- so we have a foundation in which what previous chat's changes or additions with that what files up was done and which were remaining to be done or if its a large list then in the process of the doing or need to be done or like next 3 file will be 
1. so what i need now is that i need a documentation of the whole large server code in which i need you to check the each file and give me a set of documentation in such a way that
	1. First thing
	2. how it is connected to each file like this can be used somewhere else as well
	3. then since i am using a ide to do this is called kiro which has only limited request per account 
	4. and also per chat it has limited spacing's as well like if this spacing is filled then it will go to the another chat as well
	5. to make that in have a context of previous chat where it was stopped then that can continue from that 
	   
	   
	   
	here’s a single, copy-pasteable **prompt file** you can drop into Kiro for your “multi-chat, resumable documentation run.” it bakes in your summary folder + operation status folder, two per-file outputs, resume logic, and cross-file connections.

---

```text
TITLE: Server Documentation Orchestrator (Resumable, Multi-Chat Safe)

ROLE
You are an orchestration agent that documents a large server codebase over multiple isolated chats with strict request/size limits. You MUST persist state so any later chat can resume exactly where the last one stopped.

INPUTS (fill these once before running)
- REPO_ROOT: <absolute or relative repo path, e.g., ./server>
- LANGUAGE_SET: ["python"]                       # add others if needed
- INCLUDE_GLOBS: ["**/*.py"]                     # modify as needed
- EXCLUDE_GLOBS: ["**/venv/**","**/.git/**"]     # modify as needed
- PER_CHAT_FILE_BUDGET: 25                       # how many files to fully process this chat
- SOFT_TOKEN_BUDGET: "stop when near limit"      # Kiro has limited tokens; checkpoint early
- RUN_TAG: auto-generate UTC timestamp ID per chat (e.g., RUN_2025-09-27_13-05-49)

OUTPUT ROOTS (create if missing)
- ./docs/                                   # final deliverables per source file
  - per-file/
- ./summaries/                              # rolling chat-by-chat summaries
  - README.md
  - summary_###.md
- ./status/                                 # single source of truth for progress
  - README.md
  - progress.csv
  - xref.json
  - xref.md
  - backlog.txt

FOLDER CREATION RULES
If ./summaries or ./status do not exist, create them with README.md that explains:
- what the folder is for,
- how to resume,
- file format contracts below.

FILE NAMING CONTRACTS (do not deviate)
For each processed source file at path {REL} relative to REPO_ROOT and base name {BASE} without extension:
1) Documentation file:
   ./docs/per-file/{REL}.DOC.md
2) Improvements / industry-grade analysis:
   ./docs/per-file/{REL}.IMPROVE.md

Ensure directories exist; replace path separators with "/" in output paths. Preserve case. If {REL} contains "/", mirror that structure under ./docs/per-file/.

STATUS TRACKING CONTRACTS
- ./status/progress.csv is authoritative. If absent, initialize with header:
  file_path,lang,doc_status,improve_status,last_run,chunk_note,notes
  # status values: pending|in_progress|done|error
  # chunk_note format when partially processed: "lines a-b" or "chunk k/n"
- ./status/backlog.txt (optional): plain list of file paths still pending, updated each chat.
- ./status/xref.json: adjacency map for cross-file links:
  {
    "<file_path>": {
      "imports": ["<file_path>", ...],
      "imported_by": ["<file_path>", ...]
    },
    ...
  }
- ./status/xref.md: human-readable summary table mirroring xref.json.

SUMMARY CONTRACTS
- Each chat writes ./summaries/summary_###.md with the next integer ### starting at 001.
- Each summary file must contain:
  - RUN_TAG, timestamp (UTC), repo root
  - Count of files processed this chat
  - List of file paths completed (both DOC and IMPROVE)
  - List of file paths partially processed with chunk_note and why paused
  - Next-actions section: “Start with these N files next chat” (the first N pending from progress.csv)
- ./summaries/README.md explains the above in 5–7 lines.

CROSS-FILE CONNECTIONS
While processing a file, detect imports / references (e.g., Python `import`, `from x import y`, relative imports, dynamic usage hints). Update xref.json and xref.md incrementally. In each per-file DOC.md, include a **Related files** section derived from xref.

IDEMPOTENCY & RESUME RULES
1) On start of any chat:
   - Load or create ./status/progress.csv.
   - If any row has doc_status=="in_progress" or improve_status=="in_progress", resume those first using chunk_note.
   - Otherwise, build an ordered list of target files:
       * All rows with any "pending"
       * If progress.csv is empty, scan REPO_ROOT using INCLUDE/EXCLUDE and seed CSV with "pending".
   - Process up to PER_CHAT_FILE_BUDGET files (respect token/size limits). Always checkpoint updates to CSV after each file.
2) When a chat is nearing limits:
   - Immediately write a summary_###.md with RUN_TAG, partial results, and exact continue_from pointer(s).
   - Ensure all in-flight rows are saved as "in_progress" with chunk_note so the next chat can resume.
3) If something fails:
   - Mark the row as error with notes. Include in summary’s “Issues” list.
4) Finishing conditions:
   - When both statuses for a file are “done”, include it in the Completed list in the current summary.

PROCESS ORDER (to maximize usefulness)
- Sort targets by depth (top-level modules first), then alphabetically.
- Always prioritize files that are imported by many others (degree centrality from xref) if known.

WHAT TO WRITE IN EACH OUTPUT FILE

A) {REL}.DOC.md (concise, accurate, reusable)
   # {BASE} – Module Documentation
   - **Location:** {REL}
   - **Primary purpose:** one-paragraph overview
   - **Public API:** functions/classes with signatures and short descriptions
   - **Key behaviors & invariants**
   - **Inputs/Outputs & data shapes** (types, schemas, env vars, config keys)
   - **Side effects:** I/O, network, DB, file system, caches, external services
   - **Error handling & edge cases**
   - **Performance notes:** complexity hotspots, expected throughput/latency
   - **Security & safety considerations**
   - **Related files (from xref):** list with one-line why it relates
   - **Example usage:** minimal code or call flow
   - **Change risks:** what breaks if signatures or behavior change

B) {REL}.IMPROVE.md (why/what to change; industry grade)
   # {BASE} – Improvements & Roadmap
   - **Why current design works / trade-offs**
   - **Code smells & risks** (dead code, global state, tight coupling, flaky I/O, race conditions)
   - **Refactor plan** (incremental, safe, with milestones)
   - **Architecture improvements** (modularity boundaries, layering, dependency inversion)
   - **Performance optimizations** (data structures, caching, batching, async, vectorization)
   - **Reliability/ops** (observability, metrics, tracing, health checks, graceful shutdown)
   - **Security** (input validation, authz/authn, secrets handling, dependency hygiene)
   - **Testing strategy** (unit/contract/integration/e2e; fixtures; golden tests)
   - **Docs & maintainability** (README stubs, decision records)
   - **Migration plan** (risk, rollback, flags)
   - **ROI & priority table** with Effort(Lo/Md/Hi) × Impact(Lo/Md/Hi)

PER-FILE WORKFLOW (each selected file)
1) Mark row -> in_progress for doc_status (and later improve_status).
2) Parse source:
   - Extract definitions, public API, I/O points, config, errors.
   - Detect imports and update xref.{json,md}.
3) Write {REL}.DOC.md exactly to path.
4) Set doc_status=done, last_run=RUN_TAG.
5) Produce {REL}.IMPROVE.md following the template.
6) Set improve_status=done, last_run=RUN_TAG.
7) Append any notable notes to progress.csv “notes”.

SUMMARY WRITING (end of chat or when stopping early)
- Create ./summaries/summary_###.md with:
  # Run {RUN_TAG}
  - **When:** UTC timestamp
  - **Processed:** X files completed, Y partial, Z pending
  - **Completed files:** bullet list (relative paths)
  - **Partials:** table (file → chunk_note → reason)
  - **Issues:** brief bullets with file → error note
  - **Next actions:** first K pending files to pick up next chat
- Update ./status/backlog.txt with remaining pending list (one path per line).
- Ensure progress.csv is flushed to disk and internally consistent.

PROGRESS.CSV EXAMPLE ROWS (for clarity; do not rewrite header once created)
file_path,lang,doc_status,improve_status,last_run,chunk_note,notes
api/auth.py,python,done,done,RUN_2025-09-27_13-05-49,,"OK"
core/db/session.py,python,in_progress,pending,RUN_2025-09-27_13-26-10,"lines 1-600","stop: token budget"
jobs/worker.py,python,pending,pending,,,

XREF.JSON SHAPE EXAMPLE
{
  "core/db/session.py": {"imports":["sqlalchemy","core/config.py"],"imported_by":["api/auth.py"]},
  "api/auth.py": {"imports":["core/db/session.py"],"imported_by":[]}
}

QUALITY GUARDS
- Keep each DOC.md under ~800–1200 words unless the module is huge; then summarize and reference related modules.
- Prefer precise, terse sentences. No fluff.
- Do not duplicate content between DOC.md and IMPROVE.md; the former describes, the latter critiques and plans.
- Never mark a file “done” unless both DOC.md and IMPROVE.md are written successfully.

STARTUP SEQUENCE (run this every chat)
1) Ensure ./summaries and ./status exist with READMEs (create if missing).
2) Load progress.csv; seed if empty by scanning REPO_ROOT (INCLUDE/EXCLUDE).
3) Resume any “in_progress” rows using chunk_note.
4) Process up to PER_CHAT_FILE_BUDGET new files.
5) Stop early if near Kiro limits; checkpoint, write summary_###.md; exit cleanly.

END.
```

---

### optional seed README contents (paste once)

**`./summaries/README.md`**

```md
# Summaries
This folder stores per-chat run summaries for the documentation program. Each `summary_###.md` records what was completed, what is partial, issues, and the exact next files to process. A new chat should read the latest summary to get context, then continue from the first pending items in `../status/progress.csv`.
```

**`./status/README.md`**

```md
# Status (Authoritative)
`progress.csv` is the single source of truth for file states.
- Status values: `pending | in_progress | done | error`
- A chat must update the row after every file step.
- `chunk_note` tells where to resume if the last chat stopped mid-file.
`xref.json` and `xref.md` capture cross-file relationships used by docs.
```

---

if you want, I can also generate empty folders with these README files and a starter `progress.csv` header for you.











So for the ai ide i will be giving a single file which has a complex understanding of what needs to be done
	- first is i will give a prompt file which has an proper instruction what needs to be done
	- need in that instrcution i need you to generate a simple summary small one of what is done in that current chat pause like a status of this ai agent generation in a md file 
	- next i will be needing to create another file in which has a context of what files covered and done (operation ) and also that path of that all written in that md file 
	- these above 2 md files can be big so i want you to instead of one md and another md file i need you to create a seperate folder for each of them in which summary/summar_1(what happend),summary_2(what happend) and also readme fiel in that folder tellling a info about what is this summary
	- same with this operation stastus folder in which one md file will contans a path and file name its done generateing documentation for that file so if any agent lost the limit then it will check which part it was doing and continue from that ,like if that documentation generation is done then only consider putting its status done if any issue then in pending state will be there this willl help to the another chat so that (all the time)it will check if any pending state then start from that 
	- this summary folder contains what a successful promtp out put gives like the information of hte what code files done and why it was done and its summary that information should be htere 
	- so we have a foundation in which what previous chat's changes or additions with that what files up was done and which were remaining to be done or if its a large list then in the process of the doing or need to be done or like next 3 file will be 
1. so what i need now is that i need a documentation of the whole large server code in which i need you to check the each file and give me a set of documentation in such a way that
	1. First thing
	2. how it is connected to each file like this can be used somewhere else as well
	3. then since i am using a ide to do this is called kiro which has only limited request per account 
	4. and also per chat it has limited spacing's as well like if this spacing is filled then it will go to the another chat as well
	5. to make that in have a context of previous chat where it was stopped then that can continue from that 



give me a prompt file for this exactly what i want it to do its a kiro ide in whcih i am using it so when it stops it needs to know wherere it has stopped so that from that point i an continue with 



my reason to do this is i have a hude server in which i need 2 things one server code file i will get one  documentation of that code and another a better information why this any better and industory level enchansments better apporach etc only for that ,and there appropriate naming for those 2 files based on that python file name


