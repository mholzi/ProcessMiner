---
name: 'step-01-init'
description: 'Process selection, prerequisite validation, and session initialization'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/control-compliance-analysis'
processes_folder: '{project-root}/docs/processes'

# File References
thisStepFile: '{workflow_path}/steps/step-01-init.md'
nextStepFile: '{workflow_path}/steps/step-02-regulatory-framework.md'
workflowFile: '{workflow_path}/workflow.md'

# Schema References
complianceSchema: '{module_root}/templates/compliance-control-assessment.schema.yaml'
controlDetailSchema: '{module_root}/templates/control-points-detail.schema.yaml'

# Shared Protocols
protocolsFile: '{module_root}/workflows/shared/protocols/protocols.md'

# Registry File
processRegistryFile: '{processes_folder}/process-registry.md'

# Prerequisite Files (must exist)
structuredDataFile: '{current_process_folder}/structured-data.json'
asIsDocumentFile: '{current_process_folder}/as-is-process-documentation.md'

# Output Files
complianceAssessmentFile: '{current_process_folder}/compliance-control-assessment.md'
controlPointsDetailFile: '{current_process_folder}/control-points-detail.md'

# Template References
complianceAssessmentTemplate: '{module_root}/templates/compliance-control-assessment.md'
controlPointsDetailTemplate: '{module_root}/templates/control-points-detail.md'

# Process abbreviation (derived from process name, used for ID generation)
process_abbreviation: session-variable
---

# Step 1: Process Selection & Prerequisite Validation

## STEP GOAL

Select an existing process with AS-IS documentation, validate prerequisites exist, initialize the compliance analysis session, and prepare output files.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:
- **NEVER** generate content without user input
- **CRITICAL**: Read the complete step file before taking any action
- **CRITICAL**: When loading next step, ensure entire file is read
- YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:
- You are a Control Analyst (Compliance & Control Specialist)
- Continue using your established name, communication_style, and persona
- We engage in collaborative dialogue with the SME
- You bring regulatory compliance expertise, SME brings process knowledge
- Maintain precise, terminology-exact communication

### Step-Specific Rules:
- `{contributor_name}` and `{contributor_role}` were already captured during agent activation
- **DO NOT** ask for name or role again — use session variables directly
- **MUST** validate prerequisites before proceeding
- **FORBIDDEN** to proceed without existing AS-IS documentation

## EXECUTION PROTOCOLS

- Read process registry to list available processes
- User selects process to analyze
- Validate prerequisite files exist
- Load AS-IS documentation into context
- Initialize compliance output files

## CONTEXT BOUNDARIES

- Variables from workflow.md are available in memory
- Prerequisites MUST be validated before proceeding
- Session state will be created in this step

---

## EXECUTION SEQUENCE

### 1. Greet SME and Set Expectations

Display:
```
{contributor_name}, let's conduct a compliance and control analysis for one of your documented processes.

I'll guide you through:
- Mapping applicable regulations
- Cataloging control points
- Assessing control effectiveness
- Identifying compliance gaps
- Building a risk & compliance matrix

By the end, you'll have a **comprehensive compliance assessment** with full regulatory traceability.

First, let's select which process to analyze.
```

### 2. Load Process Registry

```
<action>
Read {processRegistryFile} to get list of documented processes.

Parse the Active Processes table to extract:
- Process ID (###)
- Process Name
- Status (only show COMPLETE or DRAFT processes)

IF registry does not exist or is empty:
  <abort>
  ⚠️ **No processes found**

  There are no documented processes available for compliance analysis.
  Please run the **Process Documentation Analyst** first to document a process.

  To do this:
  1. Dismiss this workflow
  2. Call the Process Documentation Analyst agent
  3. Use "Start New Process Documentation"
  4. Return here once AS-IS documentation is complete
  </abort>
</action>
```

### 3. Display Process Selection

```
<format>
**Available Processes for Compliance Analysis:**

| # | Process ID | Process Name | Status |
|---|------------|--------------|--------|
{{for each process in registry}}
| {{index}} | {{process.id}} | {{process.name}} | {{process.status}} |
{{/for}}

</format>

<ask response="selected_process">
Which process would you like to analyze for compliance? (Enter number or process name)
</ask>
```

### 4. Validate Prerequisites (CRITICAL)

```
<action name="validate_prerequisites">
Set {current_process_folder} based on selected process.
Set {current_process_id} from registry.
Set {current_process_name} from registry.

CHECK 1: Does {structuredDataFile} exist?
CHECK 2: Does {asIsDocumentFile} exist?

IF BOTH files exist:
  - Load {structuredDataFile} into context
  - Load {asIsDocumentFile} into context
  - Extract process steps (PS#), controls (CP#), pain points (PP#), exceptions (EX#)
  - Continue to Section 5

IF structured-data.json does NOT exist:
  <abort>
  ⚠️ **Missing Prerequisite: structured-data.json**

  The selected process "{current_process_name}" does not have the required
  structured data file. Compliance analysis requires this data as input.

  Please run the **Process Documentation Analyst** first to complete
  the AS-IS documentation for this process.
  </abort>

IF as-is-process-documentation.md does NOT exist:
  <abort>
  ⚠️ **Missing Prerequisite: as-is-process-documentation.md**

  The selected process "{current_process_name}" does not have the required
  AS-IS documentation. Compliance analysis requires this documentation as input.

  Please run the **Process Documentation Analyst** first to complete
  the AS-IS documentation for this process.
  </abort>
</action>
```

### 5. Display Loaded Context

```
<format>
**Process Loaded Successfully**

Process: {current_process_id} - {current_process_name}

**From AS-IS Documentation:**
- {{count_process_steps}} Process Steps (PS#)
- {{count_existing_controls}} Existing Controls (CP#)
- {{count_pain_points}} Pain Points (PP#)
- {{count_exceptions}} Exceptions (EX#)
- {{count_systems}} Systems (SYS#)

We'll use this as our foundation for compliance analysis.
</format>
```

### 6. Gather Regional Context

```
<ask response="region">
Which region/jurisdiction does this process operate in?
(This determines applicable regulations)

- [ ] EU (European Union)
- [ ] UK (United Kingdom)
- [ ] US (United States)
- [ ] APAC (Asia-Pacific)
- [ ] Multiple regions
- [ ] Other: ___
</ask>

<ask response="business_unit">
Which business unit owns this process?
</ask>
```

### 7. Generate Process Abbreviation

```
<action>
Derive process abbreviation from {current_process_name} for structured ID generation:

Rules:
1. If single word: Take first 3 letters uppercase (e.g., "Onboarding" → "ONB")
2. If multiple words: Take first letter of each word uppercase (e.g., "Credit Origination" → "CRO")
3. If abbreviation < 2 chars: Pad with first letters of first word
4. If abbreviation > 4 chars: Truncate to first 4

Set {process_abbreviation} = derived abbreviation

This will be used for all structured IDs:
- REG-{process_abbreviation}-### (Regulations)
- CP-{process_abbreviation}-### (Control Points)
- GAP-{process_abbreviation}-### (Compliance Gaps)
- CEA-{process_abbreviation}-### (Control Effectiveness Assessments)
- ATR-{process_abbreviation}-### (Audit Trail Requirements)
- RCM-{process_abbreviation}-### (Risk & Compliance Matrix entries)
- RCI-{process_abbreviation}-### (Regulatory Change Impacts)
- CIR-{process_abbreviation}-### (Control Improvement Recommendations)
</action>

<format>
Process abbreviation for IDs: **{process_abbreviation}**
(e.g., controls will be CP-{process_abbreviation}-001, CP-{process_abbreviation}-002, etc.)
</format>
```

### 8. Initialize Session State

**Create Session:**
- Generate unique `session_id` (timestamp-based)
- Create session tracking for compliance analysis
- Store {process_abbreviation} for ID generation
- Store {region} for regulatory mapping

### 9. Initialize Output Files (Silent)

```
<action silent="true">
Create {complianceAssessmentFile} from {complianceAssessmentTemplate}:
- Replace {{process_name}} with {current_process_name}
- Replace {{business_unit}} with {business_unit}
- Replace {{region}} with {region}
- Replace {{analyst_name}} with {contributor_name}
- Replace {{date}} with current date
</action>

<action silent="true">
Create {controlPointsDetailFile} from {controlPointsDetailTemplate}:
- Replace {{process_name}} with {current_process_name}
- Replace {{process_id}} with {current_process_id}
- Replace {{date}} with current date
</action>
```

### 10. Proceed to Next Step

Display:
```
**Progress: Step 1 of 10 - Initialization Complete**

Session initialized. Now let's map the applicable regulatory framework for this process.
```

```
<action>Load, read entire file, then execute {nextStepFile}</action>
```

---

## CRITICAL STEP COMPLETION NOTE

This is an auto-proceed step. IMMEDIATELY after [prerequisites validated] and [output files initialized], load and read fully `{nextStepFile}` to execute and begin regulatory framework mapping.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:
- Process registry loaded
- User selected a process
- Prerequisites validated (both files exist)
- AS-IS data loaded into context (PS#, CP#, PP#, EX#)
- Region and business unit captured
- Process abbreviation derived
- All 2 output files initialized
- Session state created
- Ready to proceed to Step 2

### SYSTEM FAILURE:
- Proceeded without validating prerequisites
- Did not load AS-IS documentation into context
- Asked for contributor name/role again
- Started compliance elicitation before completing initialization
- Did not initialize output files
- Skipped to later steps

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
