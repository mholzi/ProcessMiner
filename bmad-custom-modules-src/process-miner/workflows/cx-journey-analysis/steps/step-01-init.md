---
name: 'step-01-init'
description: 'Process selection, prerequisite validation, and session initialization'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/cx-journey-analysis'
processes_folder: '{project-root}/docs/processes'

# File References
thisStepFile: '{workflow_path}/steps/step-01-init.md'
nextStepFile: '{workflow_path}/steps/step-02-journey-overview.md'
workflowFile: '{workflow_path}/workflow.md'
schemaFile: '{module_root}/templates/cx-journey-documentation.schema.yaml'

# Process abbreviation (derived from process name, used for ID generation)
# Examples: "Onboarding" → "ONB", "Credit Origination" → "CRO"
process_abbreviation: session-variable

# Shared Protocols
protocolsFile: '{module_root}/workflows/shared/protocols/protocols.md'

# Registry File
processRegistryFile: '{processes_folder}/process-registry.md'

# Prerequisite Files (must exist)
structuredDataFile: '{current_process_folder}/structured-data.json'
asIsDocumentFile: '{current_process_folder}/as-is-process-documentation.md'

# Output Files (CX-focused)
cxJourneyFile: '{current_process_folder}/cx-journey-documentation.md'
frictionPointsFile: '{current_process_folder}/friction-points-detail.md'
clientTouchpointsFile: '{current_process_folder}/client-touchpoints-detail.md'

# Template References
cxJourneyTemplate: '{module_root}/templates/cx-journey-documentation.md'
frictionPointsTemplate: '{module_root}/templates/friction-points-detail.md'
clientTouchpointsTemplate: '{module_root}/templates/client-touchpoints-detail.md'

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
---

# Step 1: Process Selection & Prerequisite Validation

## STEP GOAL

Select an existing process with AS-IS documentation, validate prerequisites exist, initialize the CX analysis session, and prepare output files.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:
- **NEVER** generate content without user input
- **CRITICAL**: Read the complete step file before taking any action
- **CRITICAL**: When loading next step, ensure entire file is read
- YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:
- You are a Client Journey Analyst
- Continue using your established name, communication_style, and persona
- We engage in collaborative dialogue with the SME
- You bring CX analysis expertise, SME brings process experience
- Maintain professional, supportive tone throughout

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
- Initialize CX output files

## CONTEXT BOUNDARIES

- Variables from workflow.md are available in memory
- Prerequisites MUST be validated before proceeding
- Session state will be created in this step

---

## EXECUTION SEQUENCE

### 1. Greet SME and Set Expectations

Display:
```
Hey {contributor_name}, let's analyze the client experience for one of your documented processes.

I'll walk you through capturing the client journey — touchpoints, friction, effort scores. By the end, you'll have a **complete CX analysis** ready for transformation planning.

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

  There are no documented processes available for CX analysis.
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
**Available Processes for CX Analysis:**

| # | Process ID | Process Name | Status |
|---|------------|--------------|--------|
{{for each process in registry}}
| {{index}} | {{process.id}} | {{process.name}} | {{process.status}} |
{{/for}}

</format>

<ask response="selected_process">
Which process would you like to analyze? (Enter number or process name)
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
  - Extract process overview, steps, pain points, exceptions, controls
  - Continue to Section 5

IF structured-data.json does NOT exist:
  <abort>
  ⚠️ **Missing Prerequisite: structured-data.json**

  The selected process "{current_process_name}" does not have the required
  structured data file. CX analysis requires this data as input.

  Please run the **Process Documentation Analyst** first to complete
  the AS-IS documentation for this process.
  </abort>

IF as-is-process-documentation.md does NOT exist:
  <abort>
  ⚠️ **Missing Prerequisite: as-is-process-documentation.md**

  The selected process "{current_process_name}" does not have the required
  AS-IS documentation. CX analysis requires this documentation as input.

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
- {{count_pain_points}} Pain Points (PP#)
- {{count_exceptions}} Exceptions (EX#)
- {{count_controls}} Controls (CP#)
- {{count_systems}} Systems (SYS#)

We'll use this as our foundation for CX analysis.
</format>
```

### 6. Extract Client Segment from AS-IS Data

```
<action silent="true">
Extract {client_segment} from the loaded structured-data.json:
- Read client_groups array from structured data
- Set {client_segment} = client_groups value(s)
- If multiple groups: join with ", " (e.g., "BizBanking, MidCap")
- If empty or missing: set to "All segments"
</action>
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
- JT-{process_abbreviation}-### (Journey Touchpoints)
- FP-{process_abbreviation}-### (Friction Points)
- CH-{process_abbreviation}-### (Channels)
- EI-{process_abbreviation}-### (Enhancement Ideas)
</action>

<format>
Process abbreviation for IDs: **{process_abbreviation}**
(e.g., touchpoints will be JT-{process_abbreviation}-001, JT-{process_abbreviation}-002, etc.)
</format>
```

### 8. Initialize Session State

**Create Session:**
- Generate unique `session_id` (timestamp-based)
- Create session tracking for CX analysis
- Store {process_abbreviation} for ID generation

### 9. Initialize Output Files (Silent)

```
<action silent="true">
Create {cxJourneyFile} from {cxJourneyTemplate}:
- Replace {{process_name}} with {current_process_name}
- Replace {{process_id}} with {current_process_id}
- Replace {{client_segment}} with selected segment
- Replace {{analyst_name}} with {contributor_name}
- Replace {{date}} with current date
</action>

<action silent="true">
Create {frictionPointsFile} from {frictionPointsTemplate}:
- Replace {{process_name}} with {current_process_name}
- Replace {{process_id}} with {current_process_id}
- Replace {{date}} with current date
</action>

<action silent="true">
Create {clientTouchpointsFile} from {clientTouchpointsTemplate}:
- Replace {{process_name}} with {current_process_name}
- Replace {{process_id}} with {current_process_id}
- Replace {{date}} with current date
</action>
```

### 10. Proceed to Next Step

Display:
```
**Progress: Step 1 of 8 - Initialization Complete**

Session initialized. Now let's understand this journey from the client's perspective.
```

```
<action>Load, read entire file, then execute {nextStepFile}</action>
```

---

## CRITICAL STEP COMPLETION NOTE

This is an auto-proceed step. IMMEDIATELY after [prerequisites validated] and [output files initialized], load and read fully `{nextStepFile}` to execute and begin journey overview.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:
- Process registry loaded
- User selected a process
- Prerequisites validated (both files exist)
- AS-IS data loaded into context
- Client segment extracted from structured-data.json
- All 3 CX output files initialized
- Session state created
- Ready to proceed to Step 2

### SYSTEM FAILURE:
- Proceeded without validating prerequisites
- Did not load AS-IS documentation into context
- Asked for contributor name/role again
- Started CX elicitation before completing initialization
- Did not initialize output files
- Skipped to later steps

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
