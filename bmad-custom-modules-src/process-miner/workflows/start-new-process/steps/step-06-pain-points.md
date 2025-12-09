---
name: 'step-06-pain-points'
description: 'Capture pain points and challenges with PP# IDs'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/start-new-process'

# File References
thisStepFile: '{workflow_path}/steps/step-06-pain-points.md'
nextStepFile: '{workflow_path}/steps/step-07-controls.md'
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
painPointsDetailFile: '{current_process_folder}/pain-points-detail.md'
---

# Step 6: Identify Pain Points & Challenges

## STEP GOAL

Capture all process pain points and challenges with unique PP# IDs, linked to relevant PS# process steps. Each pain point should have severity, impact assessment, and root cause.

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
- PP# format: `PP-{{process_name_abbrev}}-###` (e.g., PP-CRO-001)
- Each pain point MUST link to relevant PS# ID(s)
- Each pain point MUST have severity (HIGH/MEDIUM/LOW) and impact
- Handle "no pain points" case gracefully
- Focus ONLY on pain points — no controls, systems, etc.

## EXECUTION PROTOCOLS

- Load protocols from `{protocolsFile}`
- Invoke `capture-item` workflow for each pain point
- Update both main document and pain-points-detail.md

## CONTEXT BOUNDARIES

- Process steps (PS#) captured in Step 4
- Exceptions (EX#) captured in Step 5
- Pain points link to one or more PS# IDs

---

## EXECUTION SEQUENCE

### 1. Display Progress

```
**Progress: Step 6 of 9 - Pain Points**

Now let's identify any challenges, bottlenecks, or pain points in this process.
These are issues that make the process difficult, slow, or error-prone.
```

### 2. Check for Existing Pain Points (from Import)

```
<action>Load existing pain points from {structuredDataFile} and {painPointsDetailFile}</action>

<check if="existing_pain_points.length > 0">
  <!-- Complete imported pain points -->
</check>

<check if="existing_pain_points.length == 0">
  <ask response="pain_points_exist">
  Are there any challenges, bottlenecks, or pain points in this process?

  - **[A] Add** — I know a pain point to document
  - **[E] Explore** — Help me discover pain points using elicitation techniques
  - **[N] None** — No significant issues, process runs smoothly
  </ask>
</check>
```

### 3. Handle "No Pain Points"

```
<check if="pain_points_exist == 'N' or 'None'">
  <format>Noted — no significant pain points identified for this process.</format>
  <action>Store empty pain_points array with note</action>
</check>
```

### 4. Capture Pain Points (Fresh or Additional)

```
<loop name="pain_point_capture" until="user indicates no more pain points">
  <!-- Invoke the capture-item workflow for each pain point -->
  <invoke-workflow path="{captureItemWorkflow}">
    <param name="item_type">pain_point</param>
    <param name="current_process_folder">{current_process_folder}</param>
    <param name="mode">create</param>
  </invoke-workflow>

  <ask response="more_pain_points">
  Any other pain points to capture?

  - **[A] Add another** — I know another pain point to document
  - **[E] Explore** — Help me discover more pain points (Shadow Work Mining, Party Mode)
  - **[D] Done** — No more pain points
  </ask>
</loop>
```

### 5. Update Output Files (Silent) — RECOVERY-SAFE

**🚨 CRITICAL: Incremental Save for Recovery**

After pain points are captured (or noted as none), you MUST update ALL THREE files to enable session recovery:

```
<action silent="true">Update {structuredDataFile}:
  - pain_points array
  - Each pain point: id, name, description, severity, impact, links.process_steps, confidence
  - session.checkpoint.step = 6
  - session.last_updated = {{timestamp}}
</action>

<action silent="true" critical="RECOVERY">Update {mainDocumentFile} - APPEND Section 9:

  APPEND the following content to the main document:

  ---
  ## 9. Pain Points and Improvement Opportunities

  > **About this section:** Summary of pain points. For full analysis including root causes and improvement ideas, see [Pain Point Details](./pain-points-detail.md).

  ### 9.1 Pain Points Summary

  {{pain_points_summary_paragraph}}

  ### 9.2 Pain Point Summary Table

  | PP# | Pain Point | Category | Affected Steps | Impact | Frequency | Priority |
  |-----|------------|----------|----------------|--------|-----------|----------|
  {{Generate table row for each approved pain point}}

  ### 9.3 Pain Point Statistics

  | Metric | Value |
  |--------|-------|
  | Total Pain Points | {{total_pain_points}} |
  | High-Impact | {{count high impact}} |
  | Client-Facing | {{count client facing}} |
  | Quick Win Opportunities | {{count quick wins}} |

  > **Full Analysis:** [View Pain Point Details](./pain-points-detail.md)
  >
  > **Section Confidence:** {{assessed_confidence}} | **Basis:** SME-validated during elicitation

  ---
</action>

<action silent="true" critical="RECOVERY">Update {painPointsDetailFile} - WRITE FULL CONTENT:

  WRITE the full pain-points-detail.md file with ALL captured pain point data:

  # Pain Points & Challenges: {{process_name}}

  **Process ID:** {{process_id}}
  **Document Type:** Pain Point Detail Analysis
  **Last Updated:** {{date}}
  **Related Document:** [AS-IS Process Documentation](./as-is-process-documentation.md)

  ---

  ## Executive Summary

  {{pain_points_executive_summary}}

  ---

  ## Pain Point Summary Table

  | PP# | Pain Point | Category | Affected Steps | Severity | Impact | Frequency |
  |-----|------------|----------|----------------|----------|--------|-----------|
  {{Generate full table}}

  ---

  ## Detailed Pain Point Analysis

  {{For each pain point, generate full detail block with:
    - Overview table (ID, Name, Category, Affected Steps, Severity, Impact, Frequency)
    - Description
    - Root Cause Analysis (if captured)
    - Current Workarounds
    - Improvement Opportunities
  }}

  ---

  This incremental save ensures:
  - If session aborts after Step 6, all pain points are recoverable
  - Both summary (main doc) and detail (pain-points-detail.md) are saved
  - SME work is never lost
</action>
```

### 6. Proceed to Next Step

```
**Pain Points Complete!**
{{total_pain_points}} issues documented with PP# IDs.
Proceeding to Step 7: Controls & Compliance...
```

```
<action>Load, read entire file, then execute {nextStepFile}</action>
```

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:
- Pain points captured with PP# IDs (or noted none exist)
- Each pain point has severity and impact
- Each pain point linked to relevant PS# IDs
- Updated structured-data.json
- **APPENDED Section 9 to as-is-process-documentation.md (RECOVERY-SAFE)**
- **WROTE full pain-points-detail.md (RECOVERY-SAFE)**
- Ready to proceed to Step 7

### ❌ SYSTEM FAILURE:
- Pain points missing severity or impact
- Pain points not linked to PS# IDs
- Updated JSON but not pain-points-detail.md (or vice versa)
- Started capturing controls in this step

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
