Here’s a copy-paste-ready **“master prompt file”** you can use to turn *any* long transcript into a complete, production-grade documentation collection using your Kiro methodology. I’ve also added quick rationale and reputable references for the standards baked into this prompt (writing style, structure, citations, security, and Markdown conformance).

---

```markdown
---
title: "Course: <TOPIC FROM TRANSCRIPT> - Comprehensive Technical Documentation Generator"
description: >-
  A single, deterministic prompt that ingests a transcript and produces a complete,
  production-ready documentation collection (20–25+ files; 1000+ lines per file),
  with code examples, performance analysis, troubleshooting, and best practices—organized
  using the Kiro methodology and the Diátaxis documentation model.
author: <YOUR NAME / ORG>
source: >-
  Inputs: <TRANSCRIPT_FILE or pasted transcript text>
  Methodology: Kiro methodology (this prompt), Diátaxis model, Google & Microsoft documentation style guides.
created: "<YYYY-MM-DD>"
tags:
  - documentation
  - technical-writing
  - knowledge-engineering
  - diataxis
  - reproducible-research
  - performance
---

# Kiro Documentation Generator — Master Prompt

## Purpose
You are a **documentation engineer**. From a single transcript, generate a complete documentation set that follows Kiro’s methodology:
- 20–25 files minimum, each **1000+ lines** with extensive **working code examples**.
- Robust **production guidance**, **performance/benchmarking**, **troubleshooting**, **security**, **monitoring**, and **best practices**.
- Organize by modules with cross-links and a master README table of contents.
- Ensure **clear citations and links** to reputable official sources for every factual claim and referenced API/spec.

## Inputs (Variables you MUST honor)
- `TRANSCRIPT`: The raw transcript you are given (verbatim; may include Q&A, code, logs, or brainstorms).
- `TOPIC_HINT` (optional): If provided, use it to sharpen scope/taxonomy.
- `OUTPUT_ROOT`: The folder name to create (default: `<CanonicalizedTopic>/`).

## Output (Filesystem Contract)
Create the following structure (you may extend to 25+ files if needed):

```

<OUTPUT_ROOT>/
├── README.md (Master table of contents)
├── 01-Introduction-Overview.md
├── 02-Core-Concepts.md
├── 03-Implementation-Details.md
├── 04-Advanced-Patterns.md
├── 05-Performance-Optimization.md
├── 06-Benchmarking-Methodology.md
├── 07-Scalability-and-Architecture.md
├── 08-Storage-and-Data-Models.md
├── 09-API-Design-and-Contracts.md
├── 10-Configuration-and-Environment.md
├── 11-Security-Considerations.md
├── 12-Authentication-Authorization.md
├── 13-Observability-Monitoring-Logging.md
├── 14-Testing-Strategy-and-Fixtures.md
├── 15-CI-CD-and-Release-Engineering.md
├── 16-Incident-Response-and-Rollback.md
├── 17-Migration-and-Compatibility.md
├── 18-Integrations-and-Plugins.md
├── 19-Reference-Guide.md
├── 20-Troubleshooting-Guide.md
├── 21-Best-Practices.md
├── 22-Production-Deployment.md
├── 23-Monitoring-Debugging.md
├── 24-Security-Playbooks.md
└── 25-Reference-Materials.md

````

> **File naming rule:** `NN-Title-With-Dashes.md` (two-digit index, descriptive, stable).

> **Front matter rule:** Every file MUST begin with the YAML block below (customize `title`, `description`, `tags` per file):
```yaml
---
title: "Course: <TOPIC> - <File Subtitle>"
description: >-
  <1–3 line purpose summary + learning objectives for this file>
author: <YOUR NAME / ORG>
source: >-
  <Primary official sources linked here; plus transcript ref>
created: "<YYYY-MM-DD>"
tags:
  - <relevant-1>
  - <relevant-2>
  - <relevant-3>
---
````

## Methodology (You MUST follow this pipeline)

### Phase 0 — Ingestion & Normalization

1. **Parse `TRANSCRIPT`**: extract entities, systems, versions, commands, stack (languages, frameworks), architecture diagrams (describe textually), and all code blocks.
2. **Canonicalize the topic** → produce `<TOPIC>` and `<OUTPUT_ROOT>`.
3. **Source intent map**: classify each transcript segment into Diátaxis types—**Tutorials**, **How-To Guides**, **Reference**, **Explanation**—and tag them for routing into the right files.

### Phase 1 — Master Plan & TOC

1. Emit **README.md** with:

   * Executive summary, audience, prerequisites.
   * A 20–25 file **table of contents** with 1-line summaries each.
   * “How to use this course” with Diátaxis anchors: what content is tutorial vs how-to vs reference vs explanation.
   * Glossary of key terms and acronyms.
2. Insert global **style rules** (short sentences, active voice, bias-free terminology, consistent terminology) and link to the style guides in **References**.

### Phase 2 — File Stubs (≤ 50 lines each)

For each planned file:

* Create a skeleton with the required **front matter**, a short outline, and **placeholders** for:

  * Concepts → Code → Exercises → Checklists → Pitfalls → Benchmarks → Troubleshooting → References.
* **Cross-link** sibling files in “See also”.

> Use `fsAppend` to expand content in subsequent passes.

### Phase 3 — Deep Expansion (1000+ lines per file)

For every file:

* Fill each section with **detailed text** and **10+ runnable code examples** (with input, output, and notes).
* Provide **real-world scenarios** and **step-by-step implementations**.
* Add **performance sections** with: goals, methodology, environment, datasets, metrics, and reproducible commands.
* Add **security** notes and **threat models** (STRIDE or similar), with secure defaults and hardening steps.
* Include **observability** (metrics, logs, traces), **testing**, **CI/CD**, and **migration** notes where relevant.
* Close with **Troubleshooting** (symptom → diagnosis → root cause → fix) and **References** with **linked citations**.

### Phase 4 — Review & Quality Gates

Every file MUST pass this checklist:

* [ ] **Length** ≥ 1000 lines (excluding front matter).
* [ ] **Examples** ≥ 10 runnable code samples with expected outputs.
* [ ] **Diátaxis**: indicate whether content is tutorial/how-to/reference/explanation and keep the boundaries clean.
* [ ] **Citations**: every non-trivial fact links to official docs/specs; include permanent links where possible.
* [ ] **Benchmarks**: reproducible steps + environment + raw results summarized.
* [ ] **Security**: concrete controls, checklists, and references to standards.
* [ ] **Troubleshooting**: symptoms, commands/logs to run, decision trees.
* [ ] **Cross-references**: “See also” links to at least 3 related local files.
* [ ] **Style**: active voice, consistent terminology, accessibility notes.

## Writing & Style Requirements (HARD RULES)

1. **Diátaxis model**: Partition content into Tutorials, How-To Guides, Reference, and Explanation; do not mix purposes in the same section. ([diataxis.fr][1])
2. **Style guides**: Prefer **Google Developer Documentation Style Guide** and **Microsoft Writing Style Guide** for tone, grammar, UI terms, and procedure formatting. Include links in each file’s References. ([Google for Developers][2])
3. **Normative keywords**: When specifying requirements/prescriptions in docs, use **RFC 2119/BCP 14** keywords (“MUST”, “SHOULD”, “MAY”) in uppercase and only when truly normative. ([IETF Datatracker][3])
4. **Markdown compliance**: Use **CommonMark**-compatible Markdown; prefer tables and fenced code blocks; avoid non-portable syntax. ([commonmark.org][4])
5. **Security**: Tie security guidance to recognized frameworks like **NIST SSDF**; link controls/checklists accordingly. ([NIST Computer Security Resource Center][5])
6. **Accessibility & inclusion**: Follow bias-free language guidance (Microsoft Style Guide); provide alt text for images and explain diagrams in text. ([Microsoft Learn][6])

## Citations Policy (HARD RULES)

* **Always cite** official sources for APIs, standards, protocols, and claims.
* Use this format at the end of a paragraph or bullet:

  * `[Label — Publisher] (URL)` e.g., `[Diátaxis — diataxis.fr](https://diataxis.fr/)`.
* Prefer primary sources (specs, official docs) over blogs; if a blog is used to explain an official concept, **cite both**.
* Each file MUST have a **References** section at bottom with categorized links:

  * *Official Specs & Standards*, *Vendor Docs*, *Academic/Whitepapers*, *Community Guides*.

## Cross-Linking & Navigation

* Every file has a **“See Also”** section with at least 3 intra-repo links.
* README maintains a **bidirectional index**: each file links back to README and to related files.

## Code Examples (HARD RULES)

* Provide **complete, runnable** examples with inputs and expected outputs.
* Include **environment matrix** (OS, language version, CPU/Memory) and any prerequisites.
* Add **variant approaches** (e.g., “pure Python”, “Rust FFI”, “Kubernetes Job”, etc.) if relevant.
* Annotate with **failure modes** and **debugging tips** *inline*.

## Performance & Benchmarking

* Document **setup**, **dataset**, **metrics**, **commands**, and **raw output**.
* Provide **baseline vs tuned** comparisons; explain **trade-offs** (latency, throughput, cost).
* Include charts or tables (Markdown) plus text interpretations.

## Security Sections (per file where relevant)

* Threat model (actors, assets, attack surfaces).
* Secure-by-default configuration.
* Code scanning/linting rules; secrets handling; SBOM & supply-chain notes.
* Links to SSDF controls/practices. ([NIST Computer Security Resource Center][5])

## Observability & Operations

* Metrics to export, logging fields, exemplar traces.
* Health checks, SLO/SLA suggestions, alert playbooks.

## fsAppend Expansion Strategy

When token/length limits are near:

1. **Create stubs** (≤ 50 lines) for all planned files.
2. **Iteratively expand** each section with `fsAppend` in small chunks (numbered “Chunk 01/NN” comments).
3. **Validate after each append**: links, code fences, headings, and YAML front matter.

## Error Handling

* If the transcript lacks details, infer sanely and label with a **“[Assumption]”** callout.
* If an external fact is uncertain, add a **“[To Verify]”** note with a suggested official source to confirm.

## Deliverables (strict)

* A fully populated `<OUTPUT_ROOT>/` directory.
* Every file 1000+ lines, 10+ runnable code examples.
* README with executive summary, audience, prerequisites, and complete TOC.
* All files with **front matter** + **References**.
* No placeholder text like “TBD” left anywhere.

---

# Execution Steps (the exact steps you take)

1. **Summarize the transcript** (≤ 20 bullets) → paste as “Transcript Summary” at the top of `README.md`.
2. **Propose the TOC** (20–25 files) → write in `README.md`.
3. **Generate stubs** for all files with front matter → create files 01–25 with section scaffolds and cross-links.
4. **Deep-fill each file** to 1000+ lines with code, performance, security, troubleshooting, and references.
5. **Run quality gates** (the checklist above) and fix gaps.
6. **Emit a final “Verification Report”** at end of `README.md` showing pass/fail per gate for each file.

---

# Templates (reuse across files)

## Section Layout (repeat per file)

````
## Overview
<What this file teaches and why it matters.>

## Theory / Explanation
<Deep conceptual model; diagrams described in text.>

## Reference
<APIs, CLI, configs with parameter tables.>

## How-To Guides
<Step-by-step tasks; one task per subheading; imperative voice.>

## Tutorials
<End-to-end walkthroughs; from zero to working result.>

## Working Code Examples
### Example 1 — <Title>
```<language>
# Prereqs
# Steps
# Expected output
````

<Notes / gotchas.>
… (≥ 10 total examples)

## Performance & Benchmarking

* Environment, dataset, metrics, commands, results tables, interpretations.

## Security Considerations

* Threats, controls, secure defaults, links to SSDF practices.

## Observability, Monitoring & Debugging

* Metrics, logs, traces, dashboards, common failure signals.

## Troubleshooting

* Symptom → Command/Log → Diagnosis → Fix
* Decision tree for ambiguous issues.

## Best Practices & Anti-Patterns

* Short, prescriptive bullets with rationale.

## See Also

* [Link to related file 1](./NN-Related-File.md)
* [Link to related file 2](./NN-Related-File.md)
* [Link to README](./README.md)

## References

* Official specs & standards:

  * [Diátaxis — diataxis.fr](https://diataxis.fr/)
  * [Google Developer Documentation Style Guide](https://developers.google.com/style)
  * [Microsoft Writing Style Guide](https://learn.microsoft.com/style-guide/welcome/)
  * [CommonMark Spec](https://commonmark.org/)
  * [NIST SSDF SP 800-218](https://csrc.nist.gov/pubs/sp/800/218/final)
* Vendor docs:

  * <Add official vendor links relevant to this file.>
* Community/Explanations:

  * <Add high-quality secondary resources if needed, plus the official primary link above.>

```

---

# Style Quick Rules (keep visible while writing)
- Short sentences, active voice; avoid idioms; consistent terminology. :contentReference[oaicite:7]{index=7}
- Procedures as ordered steps; format UI terms consistently. :contentReference[oaicite:8]{index=8}
- Use uppercase **MUST/SHOULD/MAY** only when setting normative requirements; otherwise avoid. :contentReference[oaicite:9]{index=9}
- All Markdown must be **CommonMark**-compatible. :contentReference[oaicite:10]{index=10}
- Security sections should reference **SSDF** practices. :contentReference[oaicite:11]{index=11}

```

---

## Why this prompt is “production-grade” (and the sources behind it)

* **Structure & purpose clarity** come from the **Diátaxis** framework, which distinguishes tutorials, how-to guides, reference, and explanation—helpful for keeping files focused and discoverable. ([diataxis.fr][1])
* **Style, tone, and procedures** follow **Google’s Developer Documentation Style Guide** and **Microsoft’s Writing Style Guide**, which emphasize clarity, active voice, bias-free language, and consistent procedure formatting. ([Google for Developers][2])
* **Normative language** uses **RFC 2119/BCP 14** keywords so requirements are unambiguous and standardized across specs and engineering docs. ([IETF Datatracker][3])
* **Markdown compatibility** with **CommonMark** ensures your content renders consistently across platforms and static site generators. ([commonmark.org][4])
* **Security guidance** aligns with **NIST SSDF SP 800-218**, a recognized baseline for integrating security throughout the SDLC. ([NIST Computer Security Resource Center][5])

If you want, I can tailor the templates (e.g., programming language defaults, CI runners, benchmark harness) to your exact stack—just share a small sample of your transcript and preferred toolchain.

[1]: https://diataxis.fr/start-here/?utm_source=chatgpt.com "Start here - Diátaxis in five minutes"
[2]: https://developers.google.com/style?utm_source=chatgpt.com "About this guide | Google developer documentation style ..."
[3]: https://datatracker.ietf.org/doc/html/rfc2119?utm_source=chatgpt.com "RFC 2119 - Key words for use in RFCs to Indicate ..."
[4]: https://commonmark.org/?utm_source=chatgpt.com "CommonMark"
[5]: https://csrc.nist.gov/pubs/sp/800/218/final?utm_source=chatgpt.com "Secure Software Development Framework (SSDF) Version 1.1"
[6]: https://learn.microsoft.com/en-us/style-guide/welcome/?utm_source=chatgpt.com "Welcome - Microsoft Writing Style Guide"
