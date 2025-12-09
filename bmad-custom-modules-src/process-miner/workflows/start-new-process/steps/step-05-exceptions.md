---
name: 'step-05-exceptions'
description: 'Capture process exceptions and variations with EX# IDs'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/start-new-process'

# File References
thisStepFile: '{workflow_path}/steps/step-05-exceptions.md'
nextStepFile: '{workflow_path}/steps/step-06-pain-points.md'
workflowFile: '{workflow_path}/workflow.md'

# Shared Protocols
protocolsFile: '{module_root}/workflows/shared/protocols/protocols.md'

# Related Workflows
captureItemWorkflow: '{module_root}/workflows/shared/capture-item/workflow.md'

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
partyModeWorkflow: '{project-root}/.bmad/core/workflows/party-mode/workflow.md'
brainstormingWorkflow: '{project-root}/.bmad/core/workflows/brainstorming-session/workflow.md'

# Output Files
structuredDataFile: '{current_process_folder}/structured-data.json'
mainDocumentFile: '{current_process_folder}/as-is-process-documentation.md'
exceptionsDetailFile: '{current_process_folder}/exceptions-detail.md'
---

# Step 5: Identify Process Exceptions & Variations

## STEP GOAL

Capture all process exceptions and variations with unique EX# IDs, linked to relevant PS# process steps. Each exception should have trigger, handling procedure, and frequency.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:
- 🛑 **NEVER** generate content without user input
- 📖 **CRITICAL**: Read the complete step file before taking any action
- 🔄 **CRITICAL**: When loading next step, ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:
- ✅ You are a Process Documentation Analyst
- ✅ Continue using your established name, communication_style, and persona
- ✅ We engage in collaborative dialogue with the SME
- ✅ You bring documentation expertise, SME brings domain knowledge
- ✅ Maintain professional, supportive tone throughout

### Reuse Pattern:
- This step invokes the `capture-item` workflow for consistent capture experience
- Ensures narrative-first approach and core BMAD elicitation

### Step-Specific Rules
- EX# format: `EX-{{process_name_abbrev}}-###` (e.g., EX-CRO-001)
- Each exception MUST link to relevant PS# ID(s)
- Handle "no exceptions" case gracefully
- Focus ONLY on exceptions — no pain points, controls, etc.

## EXECUTION PROTOCOLS

- Load protocols from `{protocolsFile}`
- Invoke `capture-item` workflow for each exception
- Update both main document and exceptions-detail.md

## CONTEXT BOUNDARIES

- Process steps (PS#) captured in Step 4
- Exceptions link to one or more PS# IDs
- `documents_uploaded` flag may influence initial draft

---

## EXECUTION SEQUENCE

### 1. Display Progress

```
**Progress: Step 5 of 9 - Process Exceptions**

Now let's capture any exceptions or variations from the standard flow.
These are alternative paths that happen when something unusual occurs.
```

### 2. Check for Existing Exceptions (from Import)

```
<action>Load existing exceptions from {structuredDataFile} and {exceptionsDetailFile}</action>

<check if="existing_exceptions.length > 0">
  <!-- Complete imported exceptions -->
</check>

<check if="existing_exceptions.length == 0">
  <ask response="exceptions_exist">
  Does this process have exception paths or variations from the standard flow?

  - **[A] Add** — I know an exception to document
  - **[E] Explore** — Help me discover exceptions using elicitation techniques
  - **[N] None** — Mostly standard flow, rare exceptions only
  </ask>
</check>
```

### 3. Handle "No Exceptions"

```
<check if="exceptions_exist == 'N' or 'None'">
  <format>Noted — minimal exception handling, primarily standard flow.</format>
  <action>Store empty process_exceptions array with note</action>
</check>
```

### 4. Capture Exceptions (Fresh or Additional)

```
<loop name="exception_capture" until="user indicates no more exceptions">
  <!-- Invoke the capture-item workflow for each exception -->
  <invoke-workflow path="{captureItemWorkflow}">
    <param name="item_type">exception</param>
    <param name="current_process_folder">{current_process_folder}</param>
    <param name="mode">create</param>
  </invoke-workflow>

  <ask response="more_exceptions">
  Any other exceptions to capture?

  - **[A] Add another** — I know another exception to document
  - **[E] Explore** — Help me discover more exceptions
  - **[D] Done** — No more exceptions
  </ask>
</loop>
```

### 5. Update Output Files (Silent) — RECOVERY-SAFE

**🚨 CRITICAL: Incremental Save for Recovery**

After exceptions are captured (or noted as none), you MUST update ALL THREE files to enable session recovery:

```
<action silent="true">Update {structuredDataFile}:
  - process_exceptions array
  - Each exception: id, name, description, frequency, handling, links.process_steps, confidence
  - session.checkpoint.step = 5
  - session.last_updated = {{timestamp}}
</action>

<action silent="true" critical="RECOVERY">Update {mainDocumentFile} - APPEND Section 3:

  APPEND the following content to the main document:

  ---
  ## 3. Exception Paths and Variations

  > **About this section:** Summary of exceptions. For full details including root cause analysis and handling procedures, see [Exception Details](./exceptions-detail.md).

  ### 3.1 Exception Summary

  {{exceptions_summary_paragraph}}

  ### 3.2 Exception Summary Table

  | EX# | Exception | Trigger | Affected Steps | Frequency | Impact |
  |-----|-----------|---------|----------------|-----------|--------|
  {{Generate table row for each approved exception}}

  ### 3.3 Exception Statistics

  | Metric | Value |
  |--------|-------|
  | Total Exceptions | {{total_exceptions}} |
  | High-Impact Exceptions | {{count high impact}} |
  | Frequently Occurring | {{count frequent}} |

  > **Full Analysis:** [View Exception Details](./exceptions-detail.md)
  >
  > **Section Confidence:** {{assessed_confidence}} | **Basis:** SME-validated during elicitation

  ---
</action>

<action silent="true" critical="RECOVERY">Update {exceptionsDetailFile} - WRITE FULL CONTENT:

  WRITE the full exceptions-detail.md file with ALL captured exception data:

  # Exception Paths & Variations: {{process_name}}

  **Process ID:** {{process_id}}
  **Document Type:** Exception Detail Analysis
  **Last Updated:** {{date}}
  **Related Document:** [AS-IS Process Documentation](./as-is-process-documentation.md)

  ---

  ## Executive Summary

  {{exceptions_executive_summary}}

  ---

  ## Exception Summary Table

  | EX# | Exception Name | Trigger Condition | Affected Steps | Frequency | Business Impact | Handling Owner |
  |-----|----------------|-------------------|----------------|-----------|-----------------|----------------|
  {{Generate full table}}

  ---

  ## Detailed Exception Analysis

  {{For each exception, generate full detail block with:
    - Overview table (ID, Name, Category, Affected Steps, Frequency, Impact, Owner)
    - Trigger Conditions
    - Current Handling Procedure
    - Root Cause Analysis (if captured)
    - Improvement Opportunities (if captured)
  }}

  ---

  This incremental save ensures:
  - If session aborts after Step 5, all exceptions are recoverable
  - Both summary (main doc) and detail (exceptions-detail.md) are saved
  - SME work is never lost
</action>
```

### 6. Proceed to Next Step

```
**Process Exceptions Complete!**
{{total_exceptions}} exceptions documented with EX# IDs.
Proceeding to Step 6: Pain Points & Challenges...
```

```
<action>Load, read entire file, then execute {nextStepFile}</action>
```

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:
- Exceptions captured with EX# IDs (or noted none exist)
- Each exception linked to relevant PS# IDs
- Updated structured-data.json
- **APPENDED Section 3 to as-is-process-documentation.md (RECOVERY-SAFE)**
- **WROTE full exceptions-detail.md (RECOVERY-SAFE)**
- Ready to proceed to Step 6

### ❌ SYSTEM FAILURE:
- Exceptions not linked to PS# IDs
- Updated JSON but not exceptions-detail.md (or vice versa)
- Started capturing pain points in this step

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
