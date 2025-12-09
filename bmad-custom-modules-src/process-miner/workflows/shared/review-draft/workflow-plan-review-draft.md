---
stepsCompleted: [1, 2, 3, 4, 5, 6, 7, 8]
---

# Workflow Creation Plan: review-draft

## Initial Project Context

- **Module:** process-miner (custom module)
- **Target Location:** /Volumes/My Passport/ProcessMiner3/bmad-custom-modules-src/process-miner/workflows/review-draft/
- **Created:** 2025-12-08
- **Approach:** Hybrid (Auto-discovery + Optional Schema)

## Core Concept

A template-agnostic document review workflow that:
1. Auto-discovers sections from any markdown document (## headers)
2. Optionally loads a `schema.yaml` companion file for advanced features
3. Enables SME review, corrections, and approval of any structured document

## Key Design Decisions

- **No hardcoded sections** - discovers structure at runtime
- **Optional schema file** - enables sync rules, detail docs, confidence rules when present
- **Works immediately** on any markdown document without configuration
- **Reusable** across Process Documentation, Client Journey, and future templates

## Requirements (Gathered via Party Mode)

### Workflow Type
- **Type:** Interactive + Document Workflow
- **Pattern:** Iterative review loop with sync capabilities

### Schema Resolution Chain
1. **Primary:** Check document frontmatter for `template:` field → load schema from module's templates folder
2. **Override:** Check for `schema.yaml` in document's folder → local override
3. **Fallback:** Neither found → pure auto-discovery mode (sections only, no sync)

### Schema Structure (v1.0)
```yaml
schema_version: "1.0"
template_name: "template-identifier"
template_description: "Human readable description"

sections:
  - title_pattern: "regex pattern to match section title"
    detail_document: "optional-detail-doc.md"
    structured_id_prefix: "ID"  # e.g., EX, PP, CP
    sync_enabled: true/false

confidence_rules:
  high_threshold: 90
  required_fields: ["field1", "field2"]
```

### Schema Philosophy
- **Schema defines enhancements only** - not all sections
- **All ## sections auto-discovered** from document
- **Schema adds special behavior** (sync, detail docs, IDs) to specific sections
- **Schemas are developer artifacts** - each template ships with its schema

### Data Persistence
- **Change log:** Appended to document (existing pattern)
- **Review state:** JSON file in document's folder (`review-state.json`)

### Input Requirements
| Input | Required | Source |
|-------|----------|--------|
| Document path | Yes | User selection or session context |
| Contributor name/role | Yes | User input at start |
| Schema | No | Auto-resolved via chain |

### Output Specifications
- Updated document with corrections
- Change log entry with contributor attribution
- Review state JSON for resumable sessions
- Optional: Review summary export (MD/CSV)

### Success Criteria
- All sections reviewed (approved, corrected, or explicitly skipped)
- Change log updated with session summary
- Confidence scores updated where applicable
- Document saved with all changes

## Tools Configuration

### Core BMAD Tools
- **Party-Mode**: Excluded - not needed for SME review workflow
- **Advanced Elicitation**: Optional - can be invoked for clarification question generation
- **Brainstorming**: Excluded - not needed for review workflow

### LLM Features
- **File I/O**: Required - reading documents, writing updates, managing review-state.json
- **Web-Browsing**: Excluded - not needed
- **Sub-Agents**: Excluded - single workflow context
- **Sub-Processes**: Excluded - sequential review

### Memory Systems
- **Sidecar File**: Excluded - review-state.json provides sufficient state management

### External Integrations
- None required

### Installation Requirements
- No additional installations needed - all tools are built-in

## Output Format Design

**Format Type**: Structured Editing (preserve structure, update content)

### Output Files

| Output | Format | Purpose |
|--------|--------|---------|
| Target Document | Markdown | Modified with corrections, confidence updates, change log |
| review-state.json | JSON | Session state for resumable reviews |
| Review Summary | MD/CSV (optional) | Export of review session results |

### Change Log Format
Appended to document:
```markdown
## Change Log
| Date | Contributor | Role | Changes |
|------|-------------|------|---------|
| {date} | {name} | {role} | Reviewed: X approved, Y corrected. {confidence_summary} |
```

### review-state.json Structure
```json
{
  "document_path": "string",
  "schema_path": "string|null",
  "contributor": { "name": "string", "role": "string" },
  "started": "ISO8601",
  "last_updated": "ISO8601",
  "sections": [
    { "id": "number", "title": "string", "status": "pending|in_progress|approved|corrected|skipped" }
  ]
}
```

### Review Summary Export
Optional export includes:
- Section-by-section results
- Confidence score changes (before/after)
- Correction summary (not full history)

## Workflow Structure Design

### Step Overview

| Step | Name | Purpose |
|------|------|---------|
| 01 | step-01-init.md | Load document, resolve schema, gather contributor info, detect existing session |
| 01b | step-01b-continue.md | Resume existing review session from review-state.json |
| 02 | step-02-sync.md | Document sync check (conditional - only if schema has sync rules) |
| 03 | step-03-review-loop.md | Section-by-section, subsection-by-subsection review |
| 04 | step-04-summary.md | Review summary, change log update, export options |

### Flow

```
step-01-init → [existing session?] → YES → step-01b-continue
                                  → NO  → step-02-sync (if schema has sync) → step-03-review-loop → step-04-summary
```

### Step 01: Initialization
- Load target document (from path or user selection)
- Parse frontmatter for `template:` field
- Execute schema resolution chain
- Gather contributor name and role
- Check for existing review-state.json → branch to 01b
- Discover all ## sections from document
- Initialize review-state.json

### Step 01b: Continue Session
- Load review-state.json
- Show session status
- Offer: Resume | Start fresh | Review specific section
- Branch to step-02 or step-03

### Step 02: Document Sync (Conditional)
- Only runs if schema defines sync-enabled sections
- Compare main doc vs detail documents
- Identify new items, orphans, conflicts
- Present sync decisions, apply changes
- Skip entirely if no sync rules

### Step 03: Review Loop
- Present section menu with status
- User selects section (or priority/sequential)
- Subsection-by-subsection review
- Confidence scoring + clarification questions
- Review options: approve, correct, elicit, skip
- Save progress to review-state.json

### Step 04: Summary
- Calculate final statistics
- Show confidence changes
- Generate and append change log entry
- Offer export options (MD/CSV)
- Mark review complete

### Continuation Support
- Enabled via step-01b
- review-state.json tracks progress
- Sessions can span multiple interactions

### File Structure
```
review-draft/
├── workflow.md
├── steps/
│   ├── step-01-init.md
│   ├── step-01b-continue.md
│   ├── step-02-sync.md
│   ├── step-03-review-loop.md
│   └── step-04-summary.md
└── validation-checklist.md
```

## Build Summary

### Files Generated

| File | Path | Size |
|------|------|------|
| workflow.md | /bmad-custom-modules-src/process-miner/workflows/review-draft/workflow.md | ~2.5KB |
| step-01-init.md | /bmad-custom-modules-src/process-miner/workflows/review-draft/steps/step-01-init.md | ~6KB |
| step-01b-continue.md | /bmad-custom-modules-src/process-miner/workflows/review-draft/steps/step-01b-continue.md | ~6KB |
| step-02-sync.md | /bmad-custom-modules-src/process-miner/workflows/review-draft/steps/step-02-sync.md | ~7KB |
| step-03-review-loop.md | /bmad-custom-modules-src/process-miner/workflows/review-draft/steps/step-03-review-loop.md | ~9KB |
| step-04-summary.md | /bmad-custom-modules-src/process-miner/workflows/review-draft/steps/step-04-summary.md | ~6KB |
| validation-checklist.md | /bmad-custom-modules-src/process-miner/workflows/review-draft/validation-checklist.md | ~3KB |

### Key Features Implemented

- Template-agnostic design with schema resolution chain
- Session continuation support (step-01b)
- Conditional sync step (only runs if schema has sync-enabled sections)
- Confidence-driven review with clarification questions
- Subsection-by-subsection review pattern
- Standard 5-option review menu
- Change log integration
- Export options (MD/CSV)
- Comprehensive validation checklist

### Installation Requirements
- No additional installations needed
- All tools are built-in BMAD features

### Next Steps for Testing
1. Create a test document with frontmatter `template:` field
2. Create a matching schema.yaml in the module's templates folder
3. Run the workflow via agent command
4. Test continuation by interrupting mid-review
5. Verify sync functionality with detail documents

## Review Findings

### Validation Results

| Category | Result |
|----------|--------|
| Configuration validation | PASSED |
| Step compliance | PASSED |
| Cross-file consistency | PASSED |
| Requirements verification | PASSED |
| Best practices adherence | PASSED |

### Issues Found
- **Critical Issues:** None
- **Warnings:** None
- **Suggestions:** Consider adding example schema.yaml for reference

### Final Approval
- Status: APPROVED
- Date: 2025-12-08
- Reviewer: BMad Builder

## Deployment Guide

### Installation
No additional installation required - workflow is ready to use.

### Invocation
- Via agent command: `*review-draft`
- Provide document path when prompted, or let workflow scan for documents

### Testing Checklist
- [ ] Test with document that has frontmatter template reference
- [ ] Test with document that has local schema.yaml
- [ ] Test with document without any schema (auto-discovery)
- [ ] Test session continuation (interrupt and resume)
- [ ] Test sync functionality with detail documents
- [ ] Test export options (MD and CSV)
