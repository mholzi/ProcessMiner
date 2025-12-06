---
workflowName: capture-item
targetModule: process-miner
workflowType: Interactive + Document Hybrid
flowPattern: Branching with loops
date: 2025-12-03
user_name: ProcessMiner
stepsCompleted: [1, 2, 3, 4, 5, 6, 7, 8, 9]
lastStep: design
targetWorkflowPath: '{project-root}/.bmad/custom/modules/process-miner/workflows/capture-item'
customWorkflowLocation: '{project-root}/.bmad/custom/modules/process-miner/workflows'
---

# Workflow Creation Plan: capture-item

**Created:** 2025-12-03
**Author:** ProcessMiner
**Module:** process-miner
**Type:** Interactive + Document Hybrid (Rebuild from old format)

## Executive Summary

Rebuild the existing `capture-item` workflow from the old monolithic format (workflow.yaml + instructions.md) to the new BMAD 6.0 step-based architecture. This parameterized workflow captures and enhances three item types (Pain Points PP#, Exceptions EX#, Control Points CP#) for banking process documentation through narrative-first elicitation.

---

## Requirements Analysis

### 1. Purpose & Scope

| Aspect | Detail |
|--------|--------|
| **Problem Solved** | Capture and enhance pain points, exceptions, and control points for banking process documentation |
| **Primary User** | Process Documentation Analyst agent (invokes this workflow) |
| **End Users** | SMEs providing domain knowledge |
| **Main Outcome** | Fully documented items synchronized across structured JSON and markdown documents |

### 2. Workflow Type Classification

- **Primary:** Interactive Workflow (guided elicitation with SME)
- **Secondary:** Document Workflow (produces synchronized documentation)
- **Parameterized:** Single workflow handles 3 item types via `item_type` variable

### 3. Flow Pattern

**Branching with Loops:**

```
┌─────────────────────────────────────────────────────────────┐
│  Step 1: INIT - Load & Assess                               │
│  • Load existing items from structured-data.json            │
│  • Calculate completeness scores                            │
│  • Display items with status (Complete/Needs Detail/Minimal)│
│  • Present choice: Enhance / Create / Cancel                │
└─────────────────────────┬───────────────────────────────────┘
                          │
          ┌───────────────┼───────────────┐
          ▼               ▼               ▼
    ┌─────────┐     ┌─────────┐     ┌─────────┐
    │ ENHANCE │     │ CREATE  │     │ CANCEL  │
    │ (Step 3)│     │ (Step 4)│     │ → Exit  │
    └────┬────┘     └────┬────┘     └─────────┘
         │               │
         │  ┌────────────┘
         │  │ (Duplicate check may redirect to Enhance)
         ▼  ▼
┌─────────────────────────────────────────────────────────────┐
│  Step 5: ELICIT - Narrative-First Approach                  │
│  • 5a: Capture initial narrative (user tells story)         │
│  • 5b: AI synthesizes understanding (2-3 paragraphs)        │
│  • 5c: Amendments loop (if user wants corrections)          │
│  • 5d: Brainstorming deep dive (optional, uses core BMAD)   │
│  • 5e: Extract fields & present package                     │
│  └── Loop back to 5b/5c until approved                      │
└─────────────────────────┬───────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────────┐
│  Step 6: SAVE - Synchronize Documents                       │
│  • Update structured-data.json                              │
│  • Update detail document (pain-points-detail.md, etc.)     │
│  • Update main document summary table                       │
│  • Add change log entries                                   │
│  • Offer: Add Another / Return to Menu                      │
└─────────────────────────────────────────────────────────────┘
```

### 4. Interaction Style

| Aspect | Specification |
|--------|---------------|
| **User Input Level** | High - narrative-based elicitation |
| **Collaboration** | Highly collaborative - AI drafts, user validates |
| **Decision Points** | Multiple: Enhance/Create, Approve/Amend/Brainstorm, Save/Edit/Cancel |
| **Adaptability** | Adapts to user responses, loops until satisfied |

### 5. Instruction Style

**Mix of Both:**
- **Intent-based** for elicitation (Step 5) - natural conversation flow
- **Prescriptive** for structured operations (Steps 1, 6) - exact data handling

### 6. Input Requirements

| Input | Required | Source |
|-------|----------|--------|
| `item_type` | Yes | Agent menu command (pain_point / exception / control_point) |
| `current_process_folder` | Yes | Session variable from agent |
| `current_process_id` | Yes | Session variable from agent |
| `current_process_name` | Yes | Session variable from agent |
| `contributor_name` | Yes | Captured by agent on activation |
| `contributor_role` | Yes | Captured by agent on activation |
| `structured-data.json` | Yes | Must exist in process folder |

### 7. Output Specifications

| Output | Format | Auto-Save |
|--------|--------|-----------|
| **Primary:** Item data | JSON (in structured-data.json array) | Yes, on approval |
| **Secondary:** Detail documentation | Markdown (pain-points-detail.md, etc.) | Yes, on approval |
| **Tertiary:** Main doc summary | Markdown section update | Yes, on approval |
| **Audit:** Change log entries | Table rows in all modified docs | Yes, on approval |

### 8. Technical Constraints

| Constraint | Detail |
|------------|--------|
| **Dependencies** | Requires process-miner module context |
| **Integration** | Uses core BMAD advanced-elicitation.xml for brainstorming |
| **Atomic Updates** | All document updates must succeed or none |
| **ID Generation** | Must generate unique IDs (PP-XXX-001, EX-XXX-002, etc.) |
| **Standalone** | No - module workflow requiring agent context |

### 9. Success Criteria

- [ ] Item captured with narrative documentation
- [ ] Structured fields extracted from narrative
- [ ] All three output documents synchronized
- [ ] Change log entry added with contributor info
- [ ] No duplicate items created
- [ ] Completeness score improved (for enhance path)

### 10. Key Features to Preserve

1. **Parameterized Design** - Single workflow for 3 item types
2. **Completeness Assessment** - Weighted scoring with thresholds
3. **Duplicate Prevention** - Semantic similarity check
4. **Narrative-First Elicitation** - User describes, AI extracts
5. **Advanced Elicitation Integration** - Core BMAD brainstorming
6. **Document Synchronization** - Atomic multi-file updates
7. **Contributor Tracking** - Audit trail for all changes

---

## Tool Requirements Summary

**Core BMAD Tools:**
- ✅ `advanced-elicitation` — Critical evaluation, Socratic questioning, counterfactual analysis
- ✅ `party-mode` — Multi-persona collaborative idea generation
- ✅ `brainstorming` — Divergent thinking, targeted questions

**LLM Features:**
- ✅ `file-io` — Read/write JSON and markdown documents
- ✅ `web-browsing` — Real-time lookups when needed for context

**Memory Requirements:**
- ✅ `structured-data.json` — Primary state storage (existing pattern)
- ❌ No additional persistent memory needed

**External Tools:**
- ❌ No MCP integrations required

**Tool Integration Points in Workflow:**
- Step 5d (Elicit): User can choose `advanced-elicitation`, `party-mode`, or `brainstorming`
- Step 5b (Synthesize): Web browsing available for context enrichment

## Core Tools Configuration

### Workflows & Tasks

| Tool | Status | Integration Points |
|------|--------|-------------------|
| **Party-Mode** | ✅ Included | Step 5d — Multi-persona exploration for diverse perspectives |
| **Advanced Elicitation** | ✅ Included | Step 5d — Socratic questioning, counterfactual analysis |
| **Brainstorming** | ✅ Included | Step 5d — Divergent thinking, idea generation |

### LLM Tool Features

| Feature | Status | Integration Points |
|---------|--------|-------------------|
| **Web-Browsing** | ✅ Included | Step 5b — Regulatory lookups, best practices, terminology |
| **File I/O** | ✅ Included | Step 1 (load), Step 6 (save) — JSON and markdown operations |
| **Sub-Agents** | ❌ Excluded | Not needed for synchronous workflow |
| **Sub-Processes** | ❌ Excluded | No parallel operations required |

### Tool-Memory

| Memory Type | Status | Use Case |
|-------------|--------|----------|
| **Sidecar File** | ❌ Excluded | `structured-data.json` serves this purpose |

### Step 5d Menu Enhancement

Enhanced exploration options for narrative elicitation:
```
- **(a) Approve** — This captures it well
- **(m) Amend** — I have corrections or additions
- **(e) Explore Deeper** — Opens sub-menu:
  - [1] Advanced Elicitation (critical evaluation)
  - [2] Party Mode (multi-persona discussion)
  - [3] Brainstorming (divergent thinking)
```

## Memory Configuration

**Memory Requirements:** None additional — `structured-data.json` serves as persistent state.

## External Tools Configuration

**MCP Integrations:** None required — workflow operates within module context.

---

## Detailed Design

### File Structure

```
capture-item/
├── workflow.md                    # Orchestrator with item_type config
├── steps/
│   ├── step-01-init.md           # Load, assess, present choices
│   ├── step-02-enhance.md        # Enhance existing item path
│   ├── step-03-create.md         # Create new item path
│   ├── step-04-elicit.md         # Narrative elicitation (loops)
│   └── step-05-save.md           # Synchronize all documents
└── templates/
    └── item-package.md           # Final package presentation format
```

### Step Specifications

#### Step 1: INIT — Load & Assess

| Aspect | Design |
|--------|--------|
| **Goal** | Load existing items, calculate completeness, present action choice |
| **Inputs** | `item_type`, `current_process_folder`, session variables |
| **Actions** | 1. Resolve item config 2. Load JSON 3. Calculate scores 4. Display table |
| **Menu** | `[A] Enhance` `[B] Create New` `[C] Cancel` |
| **Next** | A→Step 2, B→Step 3, C→Exit |

#### Step 2: ENHANCE — Select Existing Item

| Aspect | Design |
|--------|--------|
| **Goal** | Select item to enhance, show current state and gaps |
| **Inputs** | Items list from Step 1 |
| **Actions** | 1. Select by # or ID 2. Load full data 3. Show fields 4. Identify gaps |
| **Menu** | `[C] Continue` `[X] Cancel` |
| **Next** | C→Step 4 (mode=enhance), X→Exit |

#### Step 3: CREATE — Initialize New Item

| Aspect | Design |
|--------|--------|
| **Goal** | Get initial description, check duplicates, initialize new item |
| **Inputs** | Process context |
| **Actions** | 1. Get initial pointer 2. Duplicate check 3. Generate ID 4. Initialize |
| **Menu** | Auto-proceed |
| **Next** | →Step 4 (mode=create) |

#### Step 4: ELICIT — Narrative-First Elicitation

| Aspect | Design |
|--------|--------|
| **Goal** | Capture narrative, synthesize, extract fields, approve |
| **Inputs** | `current_item`, `mode`, `fields_to_elicit` |
| **Substeps** | 4a: Capture → 4b: Synthesize → 4c: Amend → 4d: Explore → 4e: Package |
| **Menu (4b)** | `[A] Approve` `[M] Amend` `[E] Explore` |
| **Menu (4d)** | `[1] Advanced Elicitation` `[2] Party Mode` `[3] Brainstorming` |
| **Menu (4e)** | `[A] Save` `[E] Edit Fields` `[N] Edit Narrative` `[X] Cancel` |
| **Next** | A (4e)→Step 5, X→Exit |

#### Step 5: SAVE — Synchronize Documents

| Aspect | Design |
|--------|--------|
| **Goal** | Atomic update of all documents with change log |
| **Inputs** | `current_item` (finalized) |
| **Actions** | 1. Update JSON 2. Update detail doc 3. Update main doc 4. Add change logs |
| **Menu** | `[A] Add Another` `[M] Menu` |
| **Next** | A→Step 1, M→Exit |

### Data Flow

```
Agent → item_type → Step 1 (Load)
                        ↓
              ┌─────────┼─────────┐
              ↓         ↓         ↓
          Step 2    Step 3    Cancel
          (Enhance) (Create)
              ↓         ↓
              └────┬────┘
                   ↓
             Step 4 (Elicit)
             [Loop: Narrative → Synthesize → Approve]
                   ↓
             Step 5 (Save)
             [Atomic: JSON + Detail + Main + Logs]
                   ↓
           ┌───────┴───────┐
           ↓               ↓
      Add Another      Exit
           ↓
       Step 1
```

### Key Design Decisions

1. **5 steps** — Consolidated from original 7 (merged route logic)
2. **Substeps in Step 4** — Self-contained elicitation loop
3. **Single template** — Package presentation only
4. **Config in workflow.md** — Item type definitions centralized
5. **Three exploration tools** — Advanced Elicitation, Party Mode, Brainstorming

## Implementation Plan

### Files to Generate

| File | Lines (Est.) | Content |
|------|--------------|---------|
| `workflow.md` | ~150 | Orchestrator, item configs, completeness criteria |
| `step-01-init.md` | ~200 | Load, assess, display, menu routing |
| `step-02-enhance.md` | ~120 | Select item, show gaps |
| `step-03-create.md` | ~150 | Initial pointer, duplicate check, ID generation |
| `step-04-elicit.md` | ~400 | Narrative loop with substeps, tool integration |
| `step-05-save.md` | ~200 | Atomic sync, change logs, completion |
| `templates/item-package.md` | ~50 | Package display format |

### Migration Notes

- Preserve all completeness criteria from `workflow.yaml`
- Preserve all field definitions from `instructions.md`
- Keep item_configs structure for parameterization
- Maintain sync_behavior logic for atomic updates

## Review and Validation

[Review results will be appended after plan approval]

---

## Final Configuration

### Output Files to Generate

- **workflow.md**: Main orchestrator file
- **steps/step-01-init.md**: Load items, assess completeness, present choices
- **steps/step-02-enhance.md**: Select existing item, show gaps
- **steps/step-03-create.md**: Initial pointer, duplicate check, initialize new
- **steps/step-04-elicit.md**: Narrative elicitation with loops
- **steps/step-05-save.md**: Synchronize all documents

### Target Location

- **Folder**: `{project-root}/.bmad/custom/modules/process-miner/workflows/capture-item`
- **Module**: process-miner
- **Action**: Rebuild in place (replace old format)

### Final Checklist

- [x] All requirements documented
- [ ] Workflow designed and approved
- [ ] Files generated successfully
- [ ] Workflow tested and validated

## Ready for Implementation

When you approve this plan, I'll generate all the workflow files in the specified location with the exact structure and content outlined above.
