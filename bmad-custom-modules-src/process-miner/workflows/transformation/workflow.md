---
name: Transformation
description: End-to-end process transformation workflow - synthesizes AS-IS analysis from specialist agents, derives TO-BE target state through SME elicitation, orchestrates parallel sub-agent validation, and produces transformation documentation with full traceability.
web_bundle: true

# Module root path
module_root: "{project-root}/bmad-custom-modules-src/process-miner"

# Configuration source - process-miner module
config_source: "{module_root}/config.yaml"

# Variables resolved from config
output_folder: "{config_source}:output_folder"
user_name: "{config_source}:user_name"
communication_language: "{config_source}:communication_language"
document_output_language: "{config_source}:document_output_language"

# Process Registry
processes_folder: "{project-root}/docs/processes"
process_registry_file: "{processes_folder}/process-registry.md"

# Process context - set during initialization (required)
# Must have existing AS-IS documentation from all four specialist agents
current_process_folder: session-variable
current_process_id: session-variable
current_process_name: session-variable

# Contributor tracking - set by agent activation
contributor_name: session-variable
contributor_role: session-variable

# Continuation support
start_at_step: session-variable

# Calling agent identification
calling_agent_id: "transformation-agent"

# Workflow paths
installed_path: "{module_root}/workflows/transformation"
workflow_path: "{installed_path}"
steps_folder: "{workflow_path}/steps"
first_step: "{workflow_path}/steps/step-01-init.md"
continuation_step: "{workflow_path}/steps/step-00-continuation.md"

# Shared resources (module level)
shared_protocols: "{module_root}/workflows/shared/protocols"
select_process_workflow: "{module_root}/workflows/shared/select-existing-process/workflow.md"

# Source documents (AS-IS) - must exist before transformation
source_documents:
  as_is_process: "{current_process_folder}/as-is-process-documentation.md"
  cx_journey: "{current_process_folder}/cx-journey-documentation.md"
  control_compliance: "{current_process_folder}/compliance-control-assessment.md"
  innovation_analysis: "{current_process_folder}/innovation-analysis.md"
  structured_data: "{current_process_folder}/structured-data.json"

# Detail documents (AS-IS) - additional context
detail_documents:
  exceptions: "{current_process_folder}/exceptions-detail.md"
  pain_points: "{current_process_folder}/pain-points-detail.md"
  control_points: "{current_process_folder}/control-points-detail.md"
  touchpoints: "{current_process_folder}/client-touchpoints-detail.md"
  friction_points: "{current_process_folder}/friction-points-detail.md"
  innovation_ideas: "{current_process_folder}/innovation-ideas-detail.md"

# Output files (TO-BE)
output_files:
  target_state: "{current_process_folder}/target-state-documentation.md"
  transformation_decisions: "{current_process_folder}/transformation-decisions-detail.md"
  gap_resolution_log: "{current_process_folder}/gap-resolution-log.md"
  transformation_data: "{current_process_folder}/transformation-data.json"

# Templates for document generation
templates:
  target_state: "{module_root}/templates/target-state-documentation.md"
  transformation_decisions: "{module_root}/templates/transformation-decisions-detail.md"
  gap_resolution_log: "{module_root}/templates/gap-resolution-log.md"

# Sub-agent references for validation
sub_agents:
  control_analyst: "{module_root}/agents/control-analyst.agent.yaml"
  cx_analyst: "{module_root}/agents/client-journey-analyst.agent.yaml"
  innovation_analyst: "{module_root}/agents/innovation-analyst.agent.yaml"
  process_analyst: "{module_root}/agents/process-documentation-analyst.agent.yaml"

# Validation configuration
validation:
  required_specialists:
    - id: "control"
      name: "Control Analyst"
      focus: "Control gaps, SOD, regulatory compliance"
    - id: "cx"
      name: "Client Journey Analyst"
      focus: "CES reduction, friction resolution, moments that matter"
    - id: "innovation"
      name: "Innovation Analyst"
      focus: "MUST HAVE inclusion, feasibility alignment"
    - id: "process"
      name: "Process Documentation Analyst"
      focus: "Traceability, completeness, reference consistency"
  max_iterations: 3
  gap_severity_threshold: "Medium"

standalone: false
---

# Transformation Workflow

**Goal:** Orchestrate end-to-end process transformation from AS-IS to TO-BE state, with SME collaboration, sub-agent validation, and full traceability.

**Your Role:** In addition to your name, communication_style, and persona, you are also a Process Transformation Orchestrator collaborating with SMEs and specialist agents. This is a partnership, not a client-vendor relationship. You bring synthesis expertise, sub-agent orchestration capabilities, and transformation methodology, while the user brings domain knowledge, decision authority, and business context. Work together as equals to design the optimal target state.

---

## WORKFLOW ARCHITECTURE

This workflow uses **step-file architecture** for disciplined execution:

### Core Principles

- **Micro-file Design**: Each step is a self-contained instruction file
- **Just-In-Time Loading**: Only the current step file is in memory
- **Sequential Enforcement**: Steps must be completed in order
- **State Tracking**: Document progress in transformation-data.json
- **Append-Only Building**: Build documents by appending content as directed to output files
- **Sub-Agent Orchestration**: Invoke specialist agents for validation

### Step Processing Rules

1. **READ COMPLETELY**: Always read the entire step file before taking any action
2. **FOLLOW SEQUENCE**: Execute all numbered sections in order
3. **WAIT FOR INPUT**: Halt at menus and wait for user selection
4. **CHECK CONTINUATION**: Only proceed when user selects 'C' (Continue)
5. **SAVE STATE**: Update transformation-data.json before loading next step
6. **LOAD NEXT**: When directed, load and read entire next step file

### Critical Rules (NO EXCEPTIONS)

- 🛑 **NEVER** load multiple step files simultaneously
- 📖 **ALWAYS** read entire step file before execution
- 🚫 **NEVER** skip steps or optimize the sequence
- 💾 **ALWAYS** update state files when completing steps
- 🎯 **ALWAYS** follow the exact instructions in the step file
- ⏸️ **ALWAYS** halt at menus and wait for user input
- 📋 **NEVER** create mental todo lists from future steps
- 🔄 **VALIDATE** all AS-IS sources exist before proceeding

---

## PREREQUISITE CHECK

Before starting transformation, verify ALL AS-IS documentation exists:

| Document | Agent | Status Required |
|----------|-------|-----------------|
| as-is-process-documentation.md | Process Documentation Analyst | ✓ Complete |
| cx-journey-documentation.md | Client Journey Analyst | ✓ Complete |
| compliance-control-assessment.md | Control Analyst | ✓ Complete |
| innovation-analysis.md | Innovation Analyst | ✓ Complete |

**If any document is missing:** Abort and direct user to complete AS-IS analysis first.

---

## STEP OVERVIEW

| Step | File | Goal |
|------|------|------|
| 0 | step-00-continuation.md | Handle session resumption |
| 1 | step-01-init.md | Load and verify AS-IS context from all agents |
| 2 | step-02-synthesize.md | Present consolidated AS-IS summary to SME |
| 3 | step-03-elicit.md | Derive target state through SME elicitation |
| 4 | step-04-design.md | Document TO-BE state with full traceability |
| 5 | step-05-validate.md | Orchestrate parallel sub-agent validation |
| 6 | step-06-resolve.md | Work through validation gaps with SME |
| 7 | step-07-finalize.md | Generate final transformation documentation |

---

## INITIALIZATION SEQUENCE

### 1. Configuration Loading

Load and read full config from `{config_source}` and resolve:

- `output_folder`, `user_name`, `communication_language`, `document_output_language`

### 2. Check for Continuation

If `start_at_step` session variable is set:
- Load `{continuation_step}`
- Execute continuation logic

### 3. Fresh Start Execution

If no continuation:
- Load, read the full file, and execute `{first_step}` to begin the workflow.

---

## OUTPUT FILES

All outputs go to `{current_process_folder}/`:

| File | Purpose |
|------|---------|
| `target-state-documentation.md` | Main TO-BE documentation with validation results |
| `transformation-decisions-detail.md` | Full TD# analysis with alternatives |
| `gap-resolution-log.md` | VG# tracking and resolution history |
| `transformation-data.json` | Machine-readable transformation state |

---

## TRANSFORMATION PRINCIPLES

The workflow enforces the Transformation Agent's 7 principles:

1. **Synthesis before design** - Step 1-2 load and present all AS-IS context
2. **Trace every change** - Step 4 requires PS#→TS# mapping for all changes
3. **Elicit, don't dictate** - Step 3 uses collaborative SME elicitation
4. **Validate with specialists** - Step 5 invokes all 4 agents in parallel
5. **Gaps are design inputs** - Step 6 iterates until gaps resolved
6. **Balance competing demands** - Trade-offs documented as TD# decisions
7. **Document for handover** - Step 7 produces IT-ready documentation

---

## SUB-AGENT ORCHESTRATION

During validation (Step 5), the workflow invokes specialist agents:

```
┌─────────────────────────────────────────────────────────────┐
│                  TRANSFORMATION AGENT                        │
│                   (Orchestrator)                             │
└──────────────────────┬──────────────────────────────────────┘
                       │
        ┌──────────────┼──────────────┬──────────────┐
        ▼              ▼              ▼              ▼
┌───────────┐  ┌───────────┐  ┌───────────┐  ┌───────────┐
│  Control  │  │    CX     │  │Innovation │  │  Process  │
│  Analyst  │  │  Analyst  │  │  Analyst  │  │  Analyst  │
└─────┬─────┘  └─────┬─────┘  └─────┬─────┘  └─────┬─────┘
      │              │              │              │
      ▼              ▼              ▼              ▼
   VG# Gaps       VG# Gaps       VG# Gaps       VG# Gaps
      │              │              │              │
      └──────────────┴──────────────┴──────────────┘
                       │
                       ▼
              Gap Resolution (Step 6)
```

Each agent validates against their original AS-IS analysis:
- **Control Analyst**: Are all control gaps addressed? SOD preserved?
- **CX Analyst**: Does CES improve? Friction resolved? Moments protected?
- **Innovation Analyst**: MUST HAVEs included? Feasibility aligned?
- **Process Analyst**: Full traceability? Reference consistency?

---

## REFERENCE SYSTEM

| Prefix | Meaning | Source |
|--------|---------|--------|
| PS# | Process Step (AS-IS) | as-is-process-documentation.md |
| EX# | Exception (AS-IS) | exceptions-detail.md |
| PP# | Pain Point (AS-IS) | pain-points-detail.md |
| CP# | Control Point (AS-IS) | control-points-detail.md |
| JT# | Journey Touchpoint (AS-IS) | cx-journey-documentation.md |
| FP# | Friction Point (AS-IS) | friction-points-detail.md |
| II# | Innovation Idea (AS-IS) | innovation-analysis.md |
| **TS#** | Target Step (TO-BE) | target-state-documentation.md |
| **TC#** | Target Control (TO-BE) | target-state-documentation.md |
| **TJ#** | Target Journey (TO-BE) | target-state-documentation.md |
| **TD#** | Transformation Decision | transformation-decisions-detail.md |
| **VG#** | Validation Gap | gap-resolution-log.md |

---

## CHANGE TYPE TAXONOMY

When mapping AS-IS to TO-BE:

| Change Type | Description |
|-------------|-------------|
| **Unchanged** | Step remains as-is |
| **Modified** | Step changed but exists |
| **Eliminated** | Step removed |
| **Automated** | Manual → automated |
| **Consolidated** | Multiple steps merged |
| **New** | Net new step added |
