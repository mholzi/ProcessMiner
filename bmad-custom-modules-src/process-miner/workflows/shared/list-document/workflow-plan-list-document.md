---
stepsCompleted: [1, 2, 3, 4, 6, 7, 8]
status: complete
---

# Workflow Creation Plan: list-document

## Initial Project Context

- **Module:** process-miner
- **Target Location:** {project-root}/bmad-custom-modules-src/process-miner/workflows/shared/list-document
- **Created:** 2025-12-08

## Purpose

List all utilized documents uploaded into the selected process Project folder with a link to each document. Documents are originally stored via the import-existing-docs workflow into `{current_process_folder}/source-documentation/`.

## User Flow

1. Check process registry for active processes
2. Allow user to select which process to view documents for
3. Scan `source-documentation/` folder and display table with document links

## Reference Patterns

- Uses continue-session steps 1-2 pattern for process selection
- Documents stored at: `{current_process_folder}/source-documentation/`
- Registry at: `{output_folder}/process-registry.md`

---

## Gathered Requirements

### Workflow Type

- **Classification:** Action Workflow
- **Nature:** Lookup/display action - no document generation

### Workflow Structure

| Step | Name | Goal |
|------|------|------|
| 1 | Registry Check | Verify active processes exist in registry |
| 2 | Process Selection | Let user pick which process to view |
| 3 | Document Listing | Scan source-documentation folder & display table |

### Input Requirements

- Process registry file at `{output_folder}/process-registry.md`
- User selection of process
- Access to `{current_process_folder}/source-documentation/` folder

### Output Specifications

- **Primary Output:** Table displayed in conversation (not saved to file)
- **Table Columns:** Document Name, Type, Link
- **Link Format:** Relative path to document file

### User Interaction Style

- Minimal interaction
- Single process selection
- Display results and end (no loop back)

### Success Criteria

- Active processes correctly identified from registry
- User can select a process
- All documents in source-documentation folder are listed
- Links are valid relative paths to documents

### Flow Pattern

- **Linear:** Step 1 → Step 2 → Step 3 → End
- **No loops or branching**
- Steps 1-2 mirror continue-session pattern

### Instruction Style

- **Intent-Based:** Steps describe goals, AI adapts naturally
- Keep it simple - this is a utility workflow

---

## Tools Configuration

### Core BMAD Tools

- **Party-Mode**: Excluded - No creative phases needed
- **Advanced Elicitation**: Excluded - No quality gates required
- **Brainstorming**: Excluded - Simple lookup, no ideation

### LLM Features

- **Web-Browsing**: Excluded - All data is local
- **File I/O**: Included - Required for scanning source-documentation folder
- **Sub-Agents**: Excluded - Single linear flow
- **Sub-Processes**: Excluded - No parallel processing needed

### Memory Systems

- **Sidecar File**: Excluded - No session state needed

### External Integrations

- None required

### Installation Requirements

- No additional installations required
- All capabilities are native to the LLM environment

---

## Workflow Design

### Continuation Support

- **Needed:** No
- **Reason:** Quick utility workflow, single session

### File Structure

```
workflows/shared/list-document/
├── workflow.md
├── workflow-plan-list-document.md
└── steps/
    ├── step-01-registry-check.md
    ├── step-02-process-selection.md
    └── step-03-list-documents.md
```

### Step Outline

| Step | Name | Goal | Menu Type |
|------|------|------|-----------|
| 01 | Registry Check | Verify active processes exist | Auto-proceed |
| 02 | Process Selection | Let user pick process | Wait → Auto-proceed |
| 03 | List Documents | Scan folder & display table | End workflow |

### Step Details

**Step 01: Registry Check**
- Load `{output_folder}/process-registry.md`
- Parse Active Processes table
- Zero processes → exit workflow
- 1+ processes → auto-proceed to step 02
- Pattern: Mirrors continue-session/step-01

**Step 02: Process Selection**
- Display numbered list of active processes
- Wait for user selection
- Set: `{current_process_id}`, `{current_process_name}`, `{current_process_folder}`
- Auto-proceed to step 03
- Pattern: Mirrors continue-session/step-02

**Step 03: List Documents**
- Scan `{current_process_folder}/source-documentation/`
- Build markdown table: Document Name, Type, Link
- Display table to user
- End workflow

### Data Flow

Step 01 → (active process list) → Step 02 → (folder path) → Step 03

### Role Definition

- Role: Session utility specialist
- Tone: Brief, helpful, action-oriented
- Style: Minimal dialogue

### Error Handling

| Scenario | Handling |
|----------|----------|
| No registry file | Inform user, exit |
| Zero active processes | Inform user, suggest starting process |
| Empty source-documentation | Display "No documents found" |
| Invalid selection | Re-prompt |

---

## Build Summary

### Files Created

| File | Path | Size |
|------|------|------|
| workflow.md | `workflows/shared/list-document/workflow.md` | Main config |
| step-01-registry-check.md | `workflows/shared/list-document/steps/step-01-registry-check.md` | Registry verification |
| step-02-process-selection.md | `workflows/shared/list-document/steps/step-02-process-selection.md` | Process picker |
| step-03-list-documents.md | `workflows/shared/list-document/steps/step-03-list-documents.md` | Document scanner |

### Build Notes

- No templates needed (display-only workflow)
- No continuation support (single session utility)
- Mirrors continue-session pattern for steps 1-2
- Step 3 is custom for document scanning

### Next Steps

1. Review generated files for accuracy
2. Test workflow execution
3. Register in process-miner agent menu (optional)

---

## Review Summary

### Validation Results

| Check | Status |
|-------|--------|
| File Structure | PASSED |
| Configuration | PASSED |
| Step Compliance | PASSED |
| Cross-File Consistency | PASSED |
| Requirements Met | PASSED |

### Issues Found

None - All validations passed.

### Completion Status

- **Status:** COMPLETE
- **Date:** 2025-12-08
- **Files Created:** 4 (workflow.md + 3 step files)
