---
name: 'step-07-controls'
description: 'Capture controls and compliance requirements with CP# IDs'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/start-new-process'

# File References
thisStepFile: '{workflow_path}/steps/step-07-controls.md'
nextStepFile: '{workflow_path}/steps/step-08-systems.md'
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
controlPointsDetailFile: '{current_process_folder}/control-points-detail.md'
---

# Step 7: Identify Controls & Compliance Requirements

## STEP GOAL

Capture all compliance controls and regulatory requirements with unique CP# IDs, linked to relevant PS# process steps. Each control must trace to a regulatory requirement — banking compliance is non-negotiable.

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

### Banking Compliance Principle:
- **Banking compliance is non-negotiable**
- Every control MUST trace to a requirement
- Every step rationale must be documented

### Reuse Pattern
- This step invokes the `capture-item` workflow for consistent capture experience

### Step-Specific Rules
- CP# format: `CP-{{process_name_abbrev}}-###` (e.g., CP-CRO-001)
- Each control MUST link to relevant PS# ID(s)
- Each control MUST have control_type (PREVENTIVE/DETECTIVE/CORRECTIVE)
- Each control MUST have regulatory requirement traceability
- Handle "standard controls only" case appropriately
- Focus ONLY on controls — no systems yet

## EXECUTION PROTOCOLS

- Load protocols from `{protocolsFile}`
- Invoke `capture-item` workflow for each control
- Update both main document and control-points-detail.md

## CONTEXT BOUNDARIES

- Process steps (PS#) captured in Step 4
- Exceptions (EX#) captured in Step 5
- Pain points (PP#) captured in Step 6
- Controls link to one or more PS# IDs

---

## EXECUTION SEQUENCE

### 1. Display Progress

```
**Progress: Step 7 of 9 - Controls & Compliance**

Now let's document the compliance controls and regulatory requirements.
In banking, every control must trace to a requirement — this is non-negotiable.
```

### 2. Check for Existing Controls (from Import)

```
<action>Load existing controls from {structuredDataFile} and {controlPointsDetailFile}</action>

<check if="existing_controls.length > 0">
  <!-- Complete imported controls -->
</check>

<check if="existing_controls.length == 0">
  <ask response="controls_exist">
  Are there compliance controls or regulatory requirements in this process?

  - **[A] Add** — I know a control to document
  - **[E] Explore** — Help me discover controls using elicitation techniques
  - **[S] Standard only** — Standard controls apply (we'll note that)
  </ask>
</check>
```

### 3. Handle "Standard Controls Only"

```
<check if="controls_exist == 'S' or 'Standard'">
  <format>Noted — standard controls apply. We can add specific controls later if needed.</format>
  <action>Store controls array with note: "Standard controls apply"</action>
</check>
```

### 4. Capture Controls (Fresh or Additional)

```
<loop name="control_capture" until="user indicates no more controls">
  <!-- Invoke the capture-item workflow for each control -->
  <invoke-workflow path="{captureItemWorkflow}">
    <param name="item_type">control_point</param>
    <param name="current_process_folder">{current_process_folder}</param>
    <param name="mode">create</param>
  </invoke-workflow>

  <ask response="more_controls">
  Any other controls to capture?

  - **[A] Add another** — I know another control to document
  - **[E] Explore** — Help me discover more controls (Regulatory Scan, Party Mode)
  - **[D] Done** — No more controls
  </ask>
</loop>
```

### 5. Update Output Files (Silent)

```
<action silent="true">Update {structuredDataFile}:
  - controls array
  - Each control: id, name, description, control_type, requirement_source, links.process_steps, confidence
  - session.checkpoint.step = 7
  - session.last_updated = {{timestamp}}
</action>
```

### 6. Proceed to Next Step

```
**Controls & Compliance Complete!**
{{total_controls}} control points documented with CP# IDs.
Proceeding to Step 8: Systems & Tools...
```

```
<action>Load, read entire file, then execute {nextStepFile}</action>
```

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:
- Controls captured with CP# IDs (or noted standard only)
- Each control has control_type and requirement traceability
- Each control linked to relevant PS# IDs
- Updated BOTH structured-data.json AND control-points-detail.md
- Ready to proceed to Step 8

### ❌ SYSTEM FAILURE:
- Controls missing control_type or requirement traceability
- Controls not linked to PS# IDs
- Updated JSON but not control-points-detail.md (or vice versa)
- Started capturing systems in this step

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
