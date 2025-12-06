---
title: "Workflow Edit: control-point-inventory"
workflow: "control-point-inventory"
target_path: "{project-root}/.bmad/custom/modules/process-miner/workflows/control-point-inventory"
goal: "Convert to new BMAD standalone format"
stepsCompleted: [1, 2, 3, 4]
lastStep: 4
conversionStatus: complete
created: 2025-12-04
---

# Workflow Edit: control-point-inventory

## 1. Analysis Findings

### Format Detection

| Attribute | Value |
|-----------|-------|
| **Format Type** | Legacy XML format |
| **Structure** | `workflow.yaml` + `instructions.md` |
| **Migration Needed** | Yes → Standalone (workflow.md + steps/) |

### Workflow Understanding

**Purpose:** Builds a comprehensive control inventory (Sections 2.1-2.3 of Compliance Control Assessment):
- 2.1 Mandatory Controls
- 2.2 Internal Policy Mapping
- 2.3 Audit Requirements

**Workflow Type:** Document workflow (interactive, collaborative)

**Pattern:** Phase 0 (Prerequisites) → Phase 1 (Input Collection) → Phases 2-4 (A: Analyze → B: Research → C: Elicit)

**Steps Count:** 6 steps total (Step 0-5)

### Current Structure

```
control-point-inventory/
├── workflow.yaml        # 443 lines - config + step definitions
└── instructions.md      # 786 lines - XML execution instructions
```

### Target Structure (New BMAD Format)

```
control-point-inventory/
├── workflow.md                     # Entry point
├── steps/
│   ├── step-01-prerequisites.md    # Process selection & validation
│   ├── step-02-input-collection.md # Gather documentation
│   ├── step-03-extract-controls.md # Mandatory controls (Phase A/B/C)
│   ├── step-04-map-policies.md     # Internal policies (Phase A/B/C)
│   ├── step-05-audit-requirements.md # Audit requirements (Phase A/B/C)
│   └── step-06-completion.md       # Workflow summary
└── templates/                      # (If needed for output templates)
```

### Key Conversion Points

| Legacy Element | New Format Equivalent |
|----------------|----------------------|
| `<step n="X">` | Separate `step-XX-name.md` file |
| `<phase_XY>` | Markdown `### Phase XY` sections |
| `<invoke-task>` | Frontmatter variable + inline reference |
| `<output>` | Markdown content blocks |
| `<wait>` | Menu options with halt instructions |
| `<check if="...">` | Menu handling logic |
| `workflow.yaml` config | Frontmatter in `workflow.md` |

### Complexity Assessment

| Aspect | Assessment |
|--------|------------|
| **Step Complexity** | Medium-High (3-phase pattern per step) |
| **Task References** | 5 external tasks (prerequisites, collect, analyze, research, elicit) |
| **Menu Patterns** | Custom review menus (A/M/E/R, A/M/E/G, A/M/E/F) |
| **State Management** | Session variables + incremental document saving |

### External Task Dependencies

| Task | Path | Used In |
|------|------|---------|
| workflow-prerequisites.xml | {project-root}/.bmad/custom/modules/process-miner/tasks/ | Step 1 |
| collect-input-documents.xml | {project-root}/.bmad/custom/modules/process-miner/tasks/ | Step 2 |
| analyze-documentation.xml | {project-root}/.bmad/custom/modules/process-miner/tasks/ | Steps 3-5 |
| external-research.xml | {project-root}/.bmad/custom/modules/process-miner/tasks/ | Steps 3-5 |
| advanced-elicitation.xml | {project-root}/.bmad/core/tasks/ | Steps 3-5 (Elicitation option) |

## 2. Improvement Goals

### Primary Goal
**Format Conversion**: Convert from legacy XML format (workflow.yaml + instructions.md) to new BMAD standalone format (workflow.md + steps/)

### Conversion Requirements

| Requirement | Priority | Notes |
|-------------|----------|-------|
| 1:1 format conversion | CRITICAL | Preserve exact behavior |
| Preserve Phase A/B/C pattern | CRITICAL | Unique pattern to this workflow |
| Add MANDATORY EXECUTION RULES | CRITICAL | New format requirement |
| Add SUCCESS/FAILURE METRICS | CRITICAL | New format requirement |
| Preserve custom menu patterns | HIGH | A/M/E/R, A/M/E/G, A/M/E/F |
| Maintain task references | HIGH | 5 external tasks |
| Add proper frontmatter | HIGH | Path variables per step |

### Structural Changes Required

**From:**
- `workflow.yaml` (443 lines) - config + step definitions
- `instructions.md` (786 lines) - all execution logic

**To:**
- `workflow.md` - entry point with architecture section
- `steps/step-01-prerequisites.md` - Step 0 content
- `steps/step-02-input-collection.md` - Step 1 content
- `steps/step-03-extract-controls.md` - Step 2 content (Phase A/B/C)
- `steps/step-04-map-policies.md` - Step 3 content (Phase A/B/C)
- `steps/step-05-audit-requirements.md` - Step 4 content (Phase A/B/C)
- `steps/step-06-completion.md` - Step 5 content

### Pattern Preservation

The Phase A → B → C pattern will be converted as:
```markdown
## Phase A: Analyze Documentation
[AUTO - NO USER INTERRUPTION]
...

## Phase B: External Research
[AUTO - NO USER INTERRUPTION]
...

## Phase C: User Elicitation
[INTERACTIVE - ONE CONTROL AT A TIME]
...
```

### No Changes Requested
- No new features
- No behavior modifications
- No additional validation
- Pure format migration

## 3. Conversion Log

### Files Created

| File | Lines | Purpose |
|------|-------|---------|
| `workflow.md` | ~95 | Entry point with BMAD architecture |
| `steps/step-01-prerequisites.md` | ~185 | Process selection & validation |
| `steps/step-02-input-collection.md` | ~175 | Document collection |
| `steps/step-03-extract-controls.md` | ~290 | Mandatory controls (Phase A/B/C) |
| `steps/step-04-map-policies.md` | ~250 | Policy mapping (Phase A/B/C) |
| `steps/step-05-audit-requirements.md` | ~260 | Audit requirements (Phase A/B/C) |
| `steps/step-06-completion.md` | ~165 | Workflow summary |

### Legacy Files Archived

Moved to `_legacy/` folder:
- `workflow.yaml` (443 lines)
- `instructions.md` (786 lines)

### Final Structure

```
control-point-inventory/
├── workflow.md                          # NEW - Entry point
├── steps/
│   ├── step-01-prerequisites.md         # NEW - Step 0 content
│   ├── step-02-input-collection.md      # NEW - Step 1 content
│   ├── step-03-extract-controls.md      # NEW - Step 2 (Phase A/B/C)
│   ├── step-04-map-policies.md          # NEW - Step 3 (Phase A/B/C)
│   ├── step-05-audit-requirements.md    # NEW - Step 4 (Phase A/B/C)
│   └── step-06-completion.md            # NEW - Step 5 content
└── _legacy/
    ├── workflow.yaml                    # ARCHIVED - Old config
    └── instructions.md                  # ARCHIVED - Old instructions
```

### Conversion Details

| Element | Legacy Format | New Format |
|---------|---------------|------------|
| Entry point | `workflow.yaml` | `workflow.md` with frontmatter |
| Step container | `<step n="X">` in instructions.md | Individual `step-XX-name.md` files |
| Phase markers | `<phase_XA_analyze>` | `## Phase A: Analyze` sections |
| Task invoke | `<invoke-task>` | Frontmatter variable reference |
| Halt/Wait | `<wait>true</wait>` | Menu with EXECUTION RULES |
| Conditionals | `<check if="...">` | Menu Handling Logic section |
| Output blocks | `<output>...</output>` | Markdown code blocks |
| Critical rules | `<critical>` tags | MANDATORY EXECUTION RULES section |
| Success metrics | Not present | SUCCESS/FAILURE METRICS section |

### Preserved Patterns

- Phase A → B → C execution pattern (unique to this workflow)
- Custom menu options: A/M/E/R, A/M/E/G, A/M/E/F
- External task references (5 tasks)
- Section-by-section document building
- Incremental save pattern
- One-by-one control review pattern

### New Elements Added

- Standard BMAD frontmatter per file
- MANDATORY EXECUTION RULES sections
- EXECUTION PROTOCOLS sections
- CONTEXT BOUNDARIES sections
- SUCCESS/FAILURE METRICS sections
- Proper path variable definitions
