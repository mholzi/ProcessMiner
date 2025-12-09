---
name: Innovation Analysis
description: Interactive progressive workflow for market research, innovation opportunity identification, and strategic prioritization. Requires existing AS-IS process documentation as a prerequisite. Produces comprehensive innovation analysis with feasibility scoring and transformation handoffs.
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
# Folder pattern: {processes_folder}/{###}-{process-name-kebab-case}
# Example: docs/processes/001-onboarding
current_process_folder: session-variable
current_process_id: session-variable
current_process_name: session-variable
process_abbreviation: session-variable

# Bank/Organization context - set during initialization
bank_name: session-variable
region: session-variable

# Contributor tracking - set by agent activation
contributor_name: session-variable
contributor_role: session-variable

# Continuation support
start_at_step: session-variable

# Prerequisite files (MUST exist before workflow can proceed)
prerequisite_files:
  structured_data: "{current_process_folder}/structured-data.json"
  as_is_documentation: "{current_process_folder}/as-is-process-documentation.md"

# Workflow paths
installed_path: "{module_root}/workflows/innovation-analysis"
workflow_path: "{installed_path}"
steps_folder: "{workflow_path}/steps"
first_step: "{workflow_path}/steps/step-01-init.md"
continuation_step: "{workflow_path}/steps/step-00-continuation.md"

# Shared resources (module level)
shared_protocols: "{module_root}/workflows/shared/protocols"

# Scoring configuration
scoring_config: "{workflow_path}/config/scoring.yaml"

# Output files
output_files:
  innovation_analysis: "{current_process_folder}/innovation-analysis.md"
  innovation_ideas_detail: "{current_process_folder}/innovation-ideas-detail.md"
  innovation_export: "{current_process_folder}/innovation-analysis.json"

# Templates for document generation
templates:
  innovation_analysis: "{module_root}/templates/innovation-analysis-template.md"
  innovation_ideas_detail: "{module_root}/templates/innovation-ideas-detail.md"
  market_analysis: "{module_root}/templates/innovation-market-analysis.md"

standalone: false
---

# Innovation Analysis

**Goal:** Capture market intelligence, identify innovation opportunities, assess feasibility, and produce prioritized recommendations through progressive elicitation. Integrates web research with SME validation to produce actionable innovation analysis for transformation planning.

**Prerequisites:** This workflow REQUIRES existing AS-IS process documentation. The following files must exist:
- `structured-data.json` - Machine-readable process data
- `as-is-process-documentation.md` - Human-readable process documentation

**Your Role:** In addition to your name, communication_style, and persona, you are also an Innovation Analyst collaborating with SMEs. This is a partnership. You bring expertise in market research, innovation methodology, and feasibility assessment, while the SME brings their knowledge of the process domain, organizational context, and strategic priorities.

---

## WORKFLOW ARCHITECTURE

This workflow uses **step-file architecture** for disciplined execution:

### Core Principles

- **Micro-file Design**: Each step is a self-contained instruction file that is part of an overall workflow that must be followed exactly
- **Just-In-Time Loading**: Only the current step file is in memory - never load future step files until told to do so
- **Sequential Enforcement**: Sequence within the step files must be completed in order, no skipping or optimization allowed
- **State Tracking**: Document progress in output file frontmatter using `stepsCompleted` array when a workflow produces a document
- **Append-Only Building**: Build documents by appending content as directed to the output file

### Step Processing Rules

1. **READ COMPLETELY**: Always read the entire step file before taking any action
2. **FOLLOW SEQUENCE**: Execute all numbered sections in order, never deviate
3. **WAIT FOR INPUT**: If a menu is presented, halt and wait for user selection
4. **CHECK CONTINUATION**: If the step has a menu with Continue as an option, only proceed to next step when user selects 'C' (Continue)
5. **SAVE STATE**: Update `stepsCompleted` in frontmatter before loading next step
6. **LOAD NEXT**: When directed, load, read entire file, then execute the next step file

### Critical Rules (NO EXCEPTIONS)

- **NEVER** load multiple step files simultaneously
- **ALWAYS** read entire step file before execution
- **NEVER** skip steps or optimize the sequence
- **ALWAYS** update frontmatter of output files when writing the final output for a specific step
- **ALWAYS** follow the exact instructions in the step file
- **ALWAYS** halt at menus and wait for user input
- **NEVER** create mental todo lists from future steps

---

## WORKFLOW EXTENSIONS

### Three-Phase Pattern

Steps 2-4 follow a consistent three-phase pattern:

- **Phase A (AUTO)**: Analyze existing documentation - no user interruption
- **Phase B (AUTO)**: External web research - no user interruption
- **Phase C (INTERACTIVE)**: User elicitation - topic by topic with approval gates

Step 5 (Validation) is validation and approval only.

### Approval Gates

Each step requires explicit user approval before content is appended to the output document and before proceeding to the next step.

---

## STEP OVERVIEW

| Step | File | Goal | Template Section |
|------|------|------|------------------|
| 0 | step-00-continuation.md | Handle session resumption | - |
| 1 | step-01-init.md | Process selection, prerequisite validation, session initialization | - |
| 2 | step-02-market-research.md | Web research: competitors, fintech, trends, regulatory horizon | Sections 2-3 |
| 3 | step-03-innovation-backlog.md | Generate innovation backlog with 6-dimension feasibility scoring | Section 4 |
| 4 | step-04-priorities.md | MoSCoW prioritization, transformation handoffs, SMART metrics | Sections 5-8 |
| 5 | step-05-validation.md | 20-point checklist, sign-off, JSON export | Sections 1, 9-12 |

## SCHEMA REFERENCE

This workflow produces output aligned with `innovation-analysis-template.md`:

**ID Patterns** (Format: PREFIX-PROCESSABBREV-SEQ):
- Market Trends: `TR-{ABBREV}-###` (e.g., TR-ONB-001)
- Innovation Ideas: `II-{ABBREV}-###` (e.g., II-ONB-001)
- Competitors: `COMP-{ABBREV}-###` (e.g., COMP-ONB-001)
- Fintechs: `FIN-{ABBREV}-###` (e.g., FIN-ONB-001)

**Process Abbreviation**: Derived from process name (e.g., "Onboarding" → "ONB", "Credit Origination" → "CRO")

---

## INITIALIZATION SEQUENCE

### 1. Configuration Loading

Load and read full config from `{config_source}` and resolve:

- `output_folder`, `user_name`, `communication_language`, `document_output_language`

### 2. Check for Continuation

If `start_at_step` session variable is set (from *continue-session command):
- Load `{continuation_step}`
- Execute continuation logic

### 3. Fresh Start Execution

If no continuation:
- Load, read the full file, and execute `{first_step}` to begin the workflow.

---

## PREREQUISITE VALIDATION

**CRITICAL:** Before proceeding past Step 1, the workflow MUST verify:

1. User has selected an existing process from the registry
2. `{current_process_folder}/structured-data.json` EXISTS and is readable
3. `{current_process_folder}/as-is-process-documentation.md` EXISTS and is readable

If prerequisites are not met, the workflow MUST:
- Display a clear error message
- Advise user to run Process Documentation Analyst first
- ABORT the workflow - do not proceed

---

## OUTPUT FILES

All outputs go to `{current_process_folder}/`:

| File | Purpose |
|------|---------|
| `innovation-analysis.md` | Main innovation analysis document |
| `innovation-ideas-detail.md` | Detailed innovation ideas log with feasibility assessments |
| `innovation-analysis.json` | Structured export for Transformation Agent |

---

## DATA FLOW

This workflow READS from existing AS-IS documentation:
- Process steps (PS#) from structured-data.json
- Pain points (PP#) from structured-data.json and pain-points-detail.md
- Exceptions (EX#) from structured-data.json
- Controls (CP#) from structured-data.json
- Systems (SYS#) from structured-data.json

This workflow PRODUCES new innovation-focused data:
- Market Trends (TR#) - industry and technology trends
- Innovation Ideas (II#) - opportunities with feasibility scores
- Competitor Analysis (COMP#) - competitive landscape
- Fintech Disruptors (FIN#) - emerging challengers

---

## CROSS-REFERENCE STRATEGY

All innovation elements must be linked back to AS-IS elements:
- Each II# innovation links to one or more PP# pain points it addresses
- Each II# innovation links to process domain and applicable PS# steps
- Each TR# trend links to II# innovations it enables
- Competitor features link to II# innovations for benchmarking

This ensures traceability from innovation opportunities back to operational pain points and process context.

---

## WEB RESEARCH INTEGRATION

Step 2 (Market Research) performs comprehensive web searches:

### Search Categories
1. **Bank-Specific**: "{bank_name} {process_name} innovation digital transformation"
2. **Competitor**: "{process_name} innovation banking competitors {region}"
3. **Fintech**: "{process_name} fintech startups disrupting banking"
4. **Best Practices**: "{process_name} best practices banking 2024 2025"
5. **Technology Trends**: "{process_name} emerging technology banking AI ML RPA"
6. **Regulatory Horizon**: "banking regulation 2025 2026 {region} {process_name}"

### Research Rules
- Execute searches automatically (Phase B - no user interruption)
- Present findings for validation in Phase C
- User validates, amends, or adds to findings
- Only approved content is appended to document

---

## FEASIBILITY SCORING

See `{scoring_config}` for detailed weighted scoring formula:

### Formula
```
Feasibility Score = (Technical × 0.20) + (Regulatory × 0.25) + (ROI × 0.20) +
                    (Complexity × 0.10) + (Adoption × 0.15) + (Competitive × 0.10)
```

### Scale: 1-4 for each dimension

### Thresholds
- **High Feasibility:** ≥ 3.0
- **Medium Feasibility:** 2.0 - 2.9
- **Low Feasibility:** < 2.0

---

## PRIORITY CRITERIA (MoSCoW)

### MUST HAVE Criteria
- Feasibility Score: ≥ 3.0
- Impact: High
- Strategic Alignment: Yes
- **Special Conditions (any qualifies):**
  - Addresses critical pain point
  - Required for regulatory compliance
  - First mover competitive advantage
  - Foundation for other innovations

### SHOULD HAVE Criteria
- Feasibility Score: ≥ 2.5
- Impact: High or Medium
- Strategic Alignment: Yes or Partial

### COULD HAVE Criteria
- Feasibility Score: ≥ 2.0
- Impact: Medium or Low
- Strategic Alignment: Partial or TBD

### DEFER Criteria (any condition)
- Feasibility Score: < 2.0
- Dependencies not met
- Beyond transformation scope
- Requires proof of concept
- Regulatory not yet in place

### DEFER Phases
- **Phase 2:** 0-12 months post TO-BE
- **Phase 3:** 12-24 months
- **Future:** 24+ months
