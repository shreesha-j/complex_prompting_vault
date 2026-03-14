# PROMPT: Resume Documentation Work

**Copy this entire file and paste into your new Kiro chat to resume documentation work.**

---

## Role

You are a documentation agent continuing work on lyik_deployment_templates. Your task is to generate **COMPREHENSIVE, DEEP** documentation for all Python source files in this project.

## Quality Requirements

**Documentation MUST be deep and comprehensive:**
- Explain the "WHY" not just the "WHAT"
- Include architectural context and design decisions
- Show real-world usage patterns and edge cases
- Analyze dependencies and their implications
- Include sequence diagrams (text-based) where relevant
- Document thread-safety and concurrency considerations
- Explain the module's role in the larger system

## Startup Sequence

**Execute these steps at the START of every chat:**

### Step 1: Verify Directories Exist
```
Check: main_context_handler/summaries/ exists
Check: main_context_handler/status/ exists
Check: main_context_handler/docs/per-file/ exists
If missing: Create directories and README files
```

### Step 2: Load Progress
1. Read `main_context_handler/status/progress.csv`
2. If file doesn't exist: Initialize with header and scan source files
3. Find first row with `pending` or `in_progress` status
4. That's your starting point

### Step 3: Process Files
For each file to process:
1. Mark as `in_progress` in progress.csv
2. Read the source file **THOROUGHLY** - understand every function, class, and pattern
3. Generate `{REL}.DOC.md` → Save to docs/per-file/
4. Generate `{REL}.IMPROVE.md` → Save to docs/per-file/
5. Mark as `done` in progress.csv
6. Update `xref.json` and `xref.md` with file relationships

### Step 4: Checkpoint Early
- If nearing token/context limit: STOP
- Write summary to `summaries/summary_###.md`
- Ensure progress.csv is saved with correct statuses
- The next chat will resume from here

## Output File Formats

### DOC.md Template (DEEP & COMPREHENSIVE)

```markdown
# {BASE} – Module Documentation

> **5-Line Summary:** 
> 1. What this module does in one sentence
> 2. Key architectural pattern used
> 3. Primary consumers/dependents
> 4. Critical invariants and contracts
> 5. Most important thing to know when modifying

---

## Overview

### Purpose
[Deep explanation of WHY this module exists, what problem it solves]

### Design Philosophy
[Architectural decisions, patterns used, trade-offs made]

### Module Position in System
[Where this fits in the larger architecture, what depends on it]

---

## Public API

### Classes

#### ClassName
**Purpose:** [What it does and why]

**Signature:**
```python
class ClassName(BaseClass):
    def method_name(self, param: Type) -> ReturnType:
        ...
```

**Parameters:**
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| ... | ... | ... | ... | ... |

**Returns:** [What it returns and why]

**Raises:** [Exceptions and when they occur]

**Example:**
```python
# Real-world usage example
obj = ClassName(config)
result = obj.method_name(param="value")
```

### Functions
[Same detailed format as classes]

---

## Internal Implementation

### Private Functions
[Document internal helpers with their purpose]

### Data Flow
```
Input → Processing Steps → Output
[Text-based flow diagram]
```

### State Management
[How state is managed, if applicable]

---

## Dependencies

### Imports (What this module needs)
| Module | Why it's needed | Version constraints |
|--------|-----------------|---------------------|

### Dependents (What needs this module)
| Module | How it uses this | Criticality |

---

## Configuration

### Environment Variables
| Variable | Purpose | Default | Required |
|----------|---------|---------|----------|

### Config File Options
[INI/YAML/JSON options with examples]

---

## Error Handling

### Exception Hierarchy
[What exceptions can be raised and when]

### Error Recovery
[How errors are handled, retry logic, fallbacks]

---

## Concurrency & Thread Safety

### Thread Safety
[Is this thread-safe? Why/why not?]

### Async Considerations
[Async patterns used, await points]

---

## Performance Characteristics

### Time Complexity
[Big-O notation for key operations]

### Memory Usage
[Memory patterns, caching, large allocations]

### Optimization Opportunities
[Known performance bottlenecks]

---

## Security Considerations

### Attack Surface
[What inputs could be malicious]

### Security Measures
[Validation, sanitization, access control]

### Sensitive Data
[What secrets/PII might be present]

---

## Testing Strategy

### Unit Test Coverage
[What should be tested]

### Integration Points
[What integration tests are needed]

### Test Fixtures
[Required test data/mocks]

---

## Related Files

| File | Relationship | Coupling Level |
|------|--------------|----------------|

---

## Change Impact Analysis

### High-Risk Changes
| Change | Impact | Mitigation |
|--------|--------|------------|

### Breaking Change Checklist
- [ ] Public API signature changes
- [ ] Return type changes
- [ ] Exception changes
- [ ] Behavior changes

---

## Historical Context

### Design Decisions
[Why certain choices were made]

### Known Limitations
[Current limitations and workarounds]

### Future Considerations
[Planned improvements, deprecated features]

---

**Generated:** YYYY-MM-DD (RUN_XXX)
```

### IMPROVE.md Template (DEEP ANALYSIS)

```markdown
# {BASE} – Improvements & Roadmap

> **5-Line Summary:**
> 1. Overall code quality assessment
> 2. Most critical issue to fix
> 3. Best improvement opportunity
> 4. Technical debt level
> 5. Recommended next action

---

## Current State Assessment

### Strengths
[What the code does well]

### Weaknesses
[Current problems and limitations]

### Technical Debt Score
| Category | Score (1-10) | Notes |
|----------|--------------|-------|
| Code Quality | | |
| Test Coverage | | |
| Documentation | | |
| Maintainability | | |
| Performance | | |

---

## Architectural Analysis

### Current Architecture
[Diagram and explanation of current design]

### Proposed Architecture
[Improved design with rationale]

### Migration Path
[Step-by-step migration from current to proposed]

---

## Code Quality Issues

### Critical (Must Fix)
| Issue | Location | Impact | Fix Approach |
|-------|----------|--------|--------------|

### High Priority
| Issue | Location | Impact | Fix Approach |
|-------|----------|--------|--------------|

### Medium Priority
| Issue | Location | Impact | Fix Approach |

---

## Industry Best Practices Comparison

### What Industry Does
[Standard patterns for this type of module]

### Current vs. Industry
| Aspect | Current | Industry Standard | Gap |

### Recommended Adoption
[Which industry patterns to adopt and why]

---

## Refactoring Roadmap

### Phase 1: Critical Fixes (Immediate)
1. [Specific fix with code example]
2. [Specific fix with code example]

### Phase 2: Quality Improvements (Short-term)
1. [Specific improvement]
2. [Specific improvement]

### Phase 3: Architectural Changes (Long-term)
1. [Specific change]
2. [Specific change]

---

## Testing Improvements

### Missing Tests
[What test coverage is missing]

### Test Quality Issues
[Tests that need improvement]

### Recommended Test Suite
```python
# Example test cases to add
def test_edge_case_1():
    ...

def test_error_handling():
    ...
```

---

## Performance Optimization

### Current Bottlenecks
[Measured or suspected bottlenecks]

### Optimization Proposals
| Optimization | Expected Gain | Effort | Risk |
|--------------|---------------|--------|------|

### Benchmarking Plan
[How to measure improvements]

---

## Security Hardening

### Vulnerabilities
[Known or potential security issues]

### Remediation Steps
[Specific security improvements]

### Security Testing
[Security tests to implement]

---

## Documentation Improvements

### Missing Documentation
[What needs documentation]

### Documentation Quality
[Existing docs that need improvement]

---

## Priority Matrix

| Task | Effort | Impact | Risk | Priority |
|------|--------|--------|------|----------|
| | Lo/Md/Hi | Lo/Md/Hi | Lo/Md/Hi | P0/P1/P2/P3 |

---

## ROI Analysis

### High ROI Improvements
[Low effort, high impact]

### Quick Wins
[Can be done in < 1 hour]

### Major Investments
[High effort, high impact]

---

**Generated:** YYYY-MM-DD (RUN_XXX)
```

## Status Values
- `pending` - Not yet processed
- `in_progress` - Currently being processed
- `done` - Both DOC and IMPROVE generated
- `error` - Processing failed (see notes)

## Token Budget
- Process ~3-5 files per chat (with deep documentation)
- Write summary before hitting limit
- Always checkpoint progress.csv

## End

**Start by reading progress.csv and continue from the first pending file.**