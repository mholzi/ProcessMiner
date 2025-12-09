---
stepsCompleted: [1, 2, 3, 4, 5, 6]
---

# Workflow Creation Plan: start-new-process

## Initial Project Context

- **Module:** process-miner
- **Target Location:** {project-root}/bmad-custom-src/workflows/start-new-process
- **Created:** 2025-12-08
- **Based On:** ProcessMiner2 `elicit-process-knowledge` workflow

## Project Summary

### Purpose
Create a configurable "Start New Process" workflow for the Process Documentation Analyst agent that:
1. Initializes new process documentation sessions
2. Guides SME knowledge elicitation through progressive questioning
3. Produces structured outputs (JSON + markdown documents)
4. Is highly parameterized for reuse by other agents

### Key Requirements

| Requirement | Details |
|-------------|---------|
| **Reusability** | Sub-workflows callable by multiple agents (Transformation Agent, Control Analyst, etc.) |
| **Configuration** | Layered: Module config → Workflow config → Agent runtime data |
| **Sub-workflow candidates** | init-session, import-docs, elicit-overview, elicit-items, validate-session |
| **Output files** | structured-data.json + 4 markdown documents |

### Configuration Architecture (Confirmed)

```
Core Config (inherited)
    ↓
Module Config (process-miner/config.yaml)
    - structured_id_system
    - elicitation_techniques
    - templates_folder
    - shared output paths
    ↓
Workflow Frontmatter (start-new-process/workflow.md)
    - config_source reference
    - steps_folder
    - protocols_file
    - output file patterns
    ↓
Runtime Data (agent menu / session variables)
    - current_process_folder
    - contributor_name
    - contributor_role
    - mode (fresh/resume)
```

### Source Workflow Analysis

**Original:** `/Users/markusholzhaeuser/ProcessMiner2/.bmad/custom/modules/process-miner/workflows/elicit-process-knowledge`

| Component | Files | Reuse Potential |
|-----------|-------|-----------------|
| Steps | 10 files (step-00 to step-09) | High - parameterize paths |
| Protocols | protocols.md with 5 protocols | Very High - extract to shared |
| Templates | 4 document templates | High - reference from module |
| Outputs | 5 files (1 JSON + 4 MD) | Configurable via frontmatter |

### Protocols to Extract (Shared)

1. `smart_options` - Contextual option generation
2. `adaptive_approval` - Y/E/R approval pattern
3. `capture_structured_items` - Item capture with ID linking
4. `progressive_output` - Silent file updates
5. `confidence_assessment` - AI confidence scoring

## Detailed Requirements (Step 2)

### Workflow Classification

| Aspect | Decision |
|--------|----------|
| **Type** | Interactive Workflow + Document Workflow hybrid |
| **Flow Pattern** | Linear with looping capture phases |
| **Interaction** | Highly collaborative - AI drafts, SME validates |
| **Instruction Style** | Mix: Prescriptive structure, intent-based conversation |

### Sub-Workflow Architecture (Party Mode Consensus)

**Decomposition Strategy:** 3 atomic primitives + domain orchestrator

#### Atomic Primitives

| Primitive | Purpose | Reuse Potential |
|-----------|---------|-----------------|
| `init-session` | Session setup, contributor confirmation, file initialization | Any SME elicitation workflow |
| `capture-item` | Generic item capture with ID system (PP#, EX#, CP#, etc.) | Already exists in agent menu |
| `approve-content` | Y/E/R approval loop with Advanced Elicitation/Party Mode options | Universal approval pattern |

#### Interface Contract Pattern

Each sub-workflow declares explicit interface:

```yaml
interface:
  requires:
    - item_type: string       # Required input
    - id_prefix: string       # Required input
    - output_folder: path     # Required input
  optional:
    - link_to_steps: boolean  # Optional enhancement
    - questions_override: array
  provides:
    - captured_items: array   # Output to caller
    - item_count: number
```

### State Management Requirements

| Requirement | Implementation |
|-------------|----------------|
| **Session context** | `session_context` object flows through all sub-workflows |
| **Checkpoint saves** | After each sub-workflow completes, save state |
| **Resume capability** | Sub-workflow aware continuation |
| **Auto-save** | `auto_save: true` with `save_interval: 5_minutes` |

### Input Requirements

| Input | Source | Required |
|-------|--------|----------|
| `current_process_folder` | Agent menu / session | Yes |
| `contributor_name` | Agent activation | Yes |
| `contributor_role` | Agent activation | Yes |
| `existing_docs` | User upload | Optional |
| `mode` | Agent menu | Yes (fresh/resume) |

### Output Specifications

| Output | Format | Purpose |
|--------|--------|---------|
| `structured-data.json` | JSON | Machine-readable for downstream agents |
| `as-is-process-documentation.md` | Markdown | Main human-readable document |
| `exceptions-detail.md` | Markdown | Comprehensive exception analysis |
| `pain-points-detail.md` | Markdown | Comprehensive pain point analysis |
| `control-points-detail.md` | Markdown | Comprehensive control analysis |

### Success Criteria

1. All sections captured with SME approval
2. Structured ID system applied (PS#, EX#, PP#, CP#, SYS#)
3. All 5 output files in sync
4. Session resumable from any checkpoint
5. Seamless SME experience (not disconnected tool calls)

### Protocols to Implement

| Protocol | Location | Purpose |
|----------|----------|---------|
| `smart_options` | Shared | Contextual option generation using elicitation techniques |
| `adaptive_approval` | Shared | Y/E/R approval with elicitation sub-menu |
| `capture_structured_items` | Shared | Item capture with ID linking |
| `progressive_output` | Shared | Silent file updates after approval |
| `confidence_assessment` | Shared | AI confidence scoring per section |

## Tools Configuration (Step 3)

### Core BMAD Tools

| Tool | Status | Integration Points |
|------|--------|-------------------|
| **Party-Mode** | ✅ Included | Y/E/R approval sub-menu (Rewrite option) |
| **Advanced Elicitation** | ✅ Included | Y/E/R approval sub-menu (Rewrite option) |
| **Brainstorming** | ✅ Included | Creative phases, pain point discovery, idea generation |

### LLM Features

| Feature | Status | Use Case |
|---------|--------|----------|
| **File I/O** | ✅ Included | Output file management (1 JSON + 4 markdown) |
| **Sub-Agents** | ❌ Excluded | Direct workflow calls for atomic primitives |
| **Sub-Processes** | ❌ Excluded | Sequential processing sufficient |
| **Web Browsing** | ❌ Excluded | SME knowledge extraction, not web research |

### Memory Systems

| System | Status | Purpose |
|--------|--------|---------|
| **Sidecar File** | ✅ Included | Session state management, resume capability, checkpoint saves |

### External Integrations

None selected - all tools are built-in BMAD with no installation required.

### Installation Requirements

**None** - Zero installation overhead for this workflow.

## Plan Review Findings (Step 4 - Party Mode)

### Session Commands (Required for SME Experience)

| Command | Behavior |
|---------|----------|
| `[pause]` | Save state, exit gracefully, generate resume token |
| `[back]` | Return to previous question within step |
| `[skip]` | Mark as N/A, record skipper, continue workflow |
| `[help]` | Show context, examples, and rationale for question |
| `[status]` | Progress summary: Step X of Y, items captured, time elapsed |

### Failure Handling

| Scenario | Behavior |
|----------|----------|
| "I don't know" response | Record as `[UNKNOWN]`, add to validation checklist, continue |
| Session crash/interruption | Resume from last item (per-item checkpoints) |
| Validation ERROR | Block completion, return to relevant step |
| Validation WARNING | Allow override with SME justification |

### Step-to-Primitive Mapping

| Original Step | New Structure | Primitive Used |
|---------------|---------------|----------------|
| step-00 (continuation) | `shared/continue-session/` | Standalone workflow |
| step-01 (init) | `shared/init-session/` | `init-session` primitive |
| step-02 (existing docs) | `steps/step-02-import.md` | Custom (file handling) |
| step-03 (overview) | `steps/step-03-overview.md` | `approve-content` × 4 topics |
| step-04 (process steps) | `steps/step-04-process-steps.md` | `capture-item` (type=process_step) |
| step-05 (exceptions) | `steps/step-05-exceptions.md` | `capture-item` (type=exception) |
| step-06 (pain points) | `steps/step-06-pain-points.md` | `capture-item` (type=pain_point) |
| step-07 (controls) | `steps/step-07-controls.md` | `capture-item` (type=control) |
| step-08 (systems) | `steps/step-08-systems.md` | `capture-item` (type=system) |
| step-09 (validation) | `steps/step-09-validation.md` | Custom (validation logic) |

### Protocol Location (Decided)

```
{module_root}/workflows/shared/protocols/
├── smart-options.md
├── adaptive-approval.md
├── capture-structured-items.md
├── progressive-output.md
└── confidence-assessment.md
```

### Checkpoint Granularity

- **Level:** Per-item (not per-step)
- **Rationale:** If SME captures 5 pain points and crashes on #6, items #1-5 are preserved
- **Implementation:** Auto-save after each approved item + every 5 minutes

## Output Format Design (Step 5)

### Format Types

| Output File | Format Type | Template Source |
|-------------|-------------|-----------------|
| `structured-data.json` | Strict | New schema (defined below) |
| `as-is-process-documentation.md` | Structured | ProcessMiner2 template |
| `exceptions-detail.md` | Structured | ProcessMiner2 template |
| `pain-points-detail.md` | Structured | ProcessMiner2 template |
| `control-points-detail.md` | Structured | ProcessMiner2 template |

### Markdown Templates

**Source:** Import from ProcessMiner2 at:
- `{module_root}/templates/`

**Template Files:**
- `as-is-process-documentation.md`
- `exceptions-detail.md`
- `pain-points-detail.md`
- `control-points-detail.md`

### JSON Schema: structured-data.json (v1.0.0)

```json
{
  "$schema": "process-miner-structured-data-v1",
  "schema_version": "1.0.0",

  "session": {
    "id": "{{session_id}}",
    "started": "{{timestamp}}",
    "last_updated": "{{timestamp}}",
    "contributor": { "name": "...", "role": "..." },
    "process": { "id": "...", "name": "..." },
    "client_groups": [],
    "checkpoint": {
      "step": 6,
      "last_item_id": "PP-CRO-003"
    }
  },

  "metadata": {
    "purpose": "...",
    "trigger": "...",
    "frequency": "...",
    "volume": "...",
    "confidence": "HIGH|MEDIUM|LOW"
  },

  "process_steps": [{
    "id": "PS-XXX-001",
    "sequence": 1,
    "name": "...",
    "description": "...",
    "owner": "...",
    "rationale": "...",
    "confidence": "HIGH|MEDIUM|LOW"
  }],

  "process_exceptions": [{
    "id": "EX-XXX-001",
    "name": "...",
    "description": "...",
    "frequency": "RARE|OCCASIONAL|FREQUENT",
    "handling": "...",
    "links": { "process_steps": ["PS-XXX-001"] },
    "confidence": "HIGH|MEDIUM|LOW"
  }],

  "pain_points": [{
    "id": "PP-XXX-001",
    "name": "...",
    "description": "...",
    "severity": "HIGH|MEDIUM|LOW",
    "impact": "...",
    "links": { "process_steps": ["PS-XXX-002"] },
    "confidence": "HIGH|MEDIUM|LOW"
  }],

  "controls": [{
    "id": "CP-XXX-001",
    "name": "...",
    "description": "...",
    "control_type": "PREVENTIVE|DETECTIVE|CORRECTIVE",
    "requirement_source": "...",
    "links": { "process_steps": ["PS-XXX-003"] },
    "confidence": "HIGH|MEDIUM|LOW"
  }],

  "systems": [{
    "id": "SYS-XXX-001",
    "name": "...",
    "description": "...",
    "system_type": "CORE|SUPPORTING|EXTERNAL",
    "links": { "process_steps": ["PS-XXX-001", "PS-XXX-002"] },
    "confidence": "HIGH|MEDIUM|LOW"
  }],

  "validation": {
    "status": "COMPLETE|PARTIAL|DRAFT",
    "completed_at": "{{timestamp}}",
    "unknowns": [],
    "overrides": []
  }
}
```

### Schema Design Decisions (Party Mode Consensus)

| Decision | Rationale |
|----------|-----------|
| Separate `session` from `captured_data` | Clear separation of concerns |
| `schema_version` field | Enables schema evolution |
| `checkpoint` in session | Per-item resume capability |
| `links` on all items | Cross-reference traceability (PS# → EX#, PP#, etc.) |
| `confidence` on all items | From confidence_assessment protocol |
| `severity` on pain_points | Required for Transformation Agent prioritization |
| `frequency` on exceptions | Impact assessment for downstream agents |
| `control_type` enum | Categorization for Control Analyst |
| `validation` section | Tracks unknowns and SME overrides |

## Workflow Structure Design (Step 6)

### Step Structure (10 Steps)

| Step | File | Purpose | Primitive/Type |
|------|------|---------|----------------|
| 00 | `step-00-continuation.md` | Resume from checkpoint | Standalone |
| 01 | `step-01-init.md` | Session init, contributor confirm, file setup | `init-session` |
| 02 | `step-02-import.md` | Check/import existing documentation | Custom |
| 03 | `step-03-overview.md` | Capture 4 overview topics | `approve-content` ×4 |
| 04 | `step-04-process-steps.md` | Capture process steps with PS# IDs | `capture-item` |
| 05 | `step-05-exceptions.md` | Capture exceptions with EX# IDs | `capture-item` |
| 06 | `step-06-pain-points.md` | Capture pain points with PP# IDs | `capture-item` |
| 07 | `step-07-controls.md` | Capture controls with CP# IDs | `capture-item` |
| 08 | `step-08-systems.md` | Capture systems with SYS# IDs | `capture-item` |
| 09 | `step-09-validation.md` | Final review, completeness check | Custom |

### Continuation Support

- `step-00-continuation.md` handles resume
- `step-01-init.md` detects if resuming or fresh start
- Every step updates `session.checkpoint` in JSON
- Every step updates `stepsCompleted` in output frontmatter
- Per-item checkpoints (not per-step)

### Interaction Patterns

| Step | User Input | AI Behavior | Menu Pattern |
|------|------------|-------------|--------------|
| 00 | Select checkpoint | Load state | Resume options |
| 01 | Confirm contributor | Greet, setup files | Auto-proceed |
| 02 | Upload docs (optional) | Analyze, extract | Y/N then proceed |
| 03 | Validate 4 topics | Draft from docs OR elicit | **Y/E/R** per topic |
| 04-08 | Validate items | Draft OR elicit, loop | **Y/E/R** + "Add more?" |
| 09 | Review completeness | Present summary | Approve/Return |

### Y/E/R Approval Pattern

- **[Y] Yes, Accept** - Store and continue
- **[E] Edit** - Minor corrections
- **[R] Rewrite** - Sub-menu: [A] Advanced Elicitation, [P] Party Mode, [Q] Quick Questions, [B] Brainstorming

### Session Commands

**REMOVED** - No session commands ([pause], [back], [skip], [help], [status])

### File Structure

```
start-new-process/
├── workflow.md
├── steps/
│   ├── step-00-continuation.md
│   ├── step-01-init.md
│   ├── step-02-import.md
│   ├── step-03-overview.md
│   ├── step-04-process-steps.md
│   ├── step-05-exceptions.md
│   ├── step-06-pain-points.md
│   ├── step-07-controls.md
│   ├── step-08-systems.md
│   └── step-09-validation.md
└── validation-checklist.md

{module_root}/workflows/shared/
├── protocols/
│   ├── smart-options.md
│   ├── adaptive-approval.md
│   ├── capture-structured-items.md
│   ├── progressive-output.md
│   └── confidence-assessment.md
├── init-session/
├── capture-item/
└── continue-session/
```

### Data Flow

```
Session Context → Steps 01-09 → structured-data.json → 4 Markdown Docs
                      ↑                    ↓
                      └── checkpoint saves ─┘
```

## Next Steps

- [x] Gather detailed requirements for each sub-workflow
- [x] Define tools and configuration needs
- [x] Define shared protocol locations
- [x] Map step file parameterization
- [x] Review complete plan (Party Mode)
- [x] Design output format structure
- [x] Design workflow step structure
- [ ] Build workflow files
