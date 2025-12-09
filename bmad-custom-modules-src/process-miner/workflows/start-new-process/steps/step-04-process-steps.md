---
name: 'step-04-process-steps'
description: 'Identify and document process steps with PS# IDs and flow diagram'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/start-new-process'

# File References
thisStepFile: '{workflow_path}/steps/step-04-process-steps.md'
nextStepFile: '{workflow_path}/steps/step-05-exceptions.md'
workflowFile: '{workflow_path}/workflow.md'

# Shared Protocols
protocolsFile: '{module_root}/workflows/shared/protocols/protocols.md'

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
partyModeWorkflow: '{project-root}/.bmad/core/workflows/party-mode/workflow.md'
brainstormingWorkflow: '{project-root}/.bmad/core/workflows/brainstorming-session/workflow.md'

# Output Files
structuredDataFile: '{current_process_folder}/structured-data.json'
mainDocumentFile: '{current_process_folder}/as-is-process-documentation.md'
---

# Step 4: Identify Process Steps

## STEP GOAL

Capture all process steps with unique PS# IDs, descriptions, owners, and rationale. Generate a process flow diagram. Target 5-15 major steps.

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

### Adaptive Approach:
- Behavior differs based on `documents_uploaded` flag:
  - **If true**: Extract steps from imported documents, SME validates
  - **If false**: Offer capture approach options, elicit from SME

### Step-Specific Rules
- Each step MUST have: name, description, owner, rationale, PS# ID
- PS# format: `PS-{{process_name_abbrev}}-###` (e.g., PS-CRO-001)
- Generate Mermaid flowchart after steps are approved
- Focus ONLY on process steps — no exceptions, pain points, etc.

### 🚨 MANDATORY MENU RULE (NO EXCEPTIONS)
**EVERY approval menu MUST include ALL THREE options:**
```
- [Y] Yes, Accept
- [E] Edit
- [R] Rewrite
```

## EXECUTION PROTOCOLS

- Load protocols from `{protocolsFile}`
- Use `smart_options` for owner/rationale elicitation
- Use `adaptive_approval` for content approval with elicitation option

## CONTEXT BOUNDARIES

- Process overview captured in Step 3
- `documents_uploaded` flag determines approach
- Steps captured here will be linked by future steps (EX#, PP#, CP#, SYS#)

---

## EXECUTION SEQUENCE

### 1. Display Progress

```
**Progress: Step 4 of 9 - Process Steps**

Now let's map out the process steps. We're looking for 5-15 major steps.
Each step will have a unique PS# ID for cross-referencing.
```

### 2. Handle Document-Based Approach

```
<check if="documents_uploaded == true">
  <critical>Draft process flow from imported documents.</critical>

  <action>Extract and organize all process steps from documents:
  - Sequential order
  - Include owner and rationale where available
  - Assign PS-{{process_name_abbrev}}-### IDs
  </action>

  <format>
  ---
  **Process Steps - Current Understanding:**

  | PS# | Step Name | Description | Owner | Rationale |
  |-----|-----------|-------------|-------|-----------|
  {{drafted steps from documents}}

  {{2-3 paragraphs about overall flow, handoffs, decision points}}
  ---
  </format>
</check>
```

### 3. Handle Fresh Elicitation Approach

```
<check if="documents_uploaded == false">
  <ask response="step_approach">
  How would you like to capture the process steps?

  - [ ] Walk me through it step-by-step (I'll ask questions)
  - [ ] Show me a draft list to review and refine
  - [ ] Start with major phases, then break down each
  </ask>

  <!-- Handle each approach option -->
  <action>Compile all steps into summary table with narrative</action>
</check>
```

### 4. Get Approval Using Protocol

```
<approval-menu topic="Process Steps">
  <display>
  ---
  **Process Steps - Draft:**

  {{content_display}}

  ---
  How would you like to proceed?
  - **[Y] Yes, Accept** — This accurately captures the Process Steps
  - **[E] Edit** — I have minor corrections to make
  - **[R] Rewrite** — Let's redraft this together using AI-assisted techniques
  </display>

  <handle option="R">
    <display>
    - **[A] Advanced Elicitation** — Structured techniques
    - **[P] Party Mode** — Multiple AI perspectives
    - **[B] Brainstorming** — Creative exploration
    - **[Q] Quick Questions** — Targeted questions
    - **[X] Back** — Return to approval menu
    </display>
  </handle>
</approval-menu>
```

### 5. Update Output Files (Silent) — RECOVERY-SAFE

**🚨 CRITICAL: Incremental Save for Recovery**

After process steps are approved, you MUST update BOTH files to enable session recovery:

```
<action silent="true">Update {structuredDataFile}:
  - process_steps array with all steps
  - Each step: id, sequence, name, description, owner, rationale, confidence
  - session.checkpoint.step = 4
  - session.last_updated = {{timestamp}}
</action>

<action silent="true" critical="RECOVERY">Update {mainDocumentFile} - APPEND Section 2:

  APPEND the following content to the main document:

  ---
  ## 2. Process Steps

  > **About this section:** The step-by-step flow of this process from start to finish.

  ### 2.1 Process Step Summary

  | PS# | Step Name | Owner | System(s) | Rationale |
  |-----|-----------|-------|-----------|-----------|
  {{Generate table row for each approved step}}

  ### 2.2 Process Flow Diagram

  ```mermaid
  graph TD
      {{Generate Mermaid flowchart from approved steps}}
  ```

  ### 2.3 Step Details

  {{Brief narrative describing the flow, key handoffs, and decision points}}

  > **Section Confidence:** {{assessed_confidence}} | **Basis:** SME-validated during elicitation

  ---

  This incremental save ensures:
  - If session aborts after Step 4, Section 2 is recoverable from the MD file
  - Process steps preserved with Mermaid diagram
  - SME work is never lost
</action>
```

**🚨 MANDATORY: Mermaid Diagram Generation**

You MUST generate a Mermaid diagram from the approved steps using `graph TD` format.

### 6. Proceed to Next Step

Display:
```
**Process Steps Complete!**
{{total_steps}} steps documented with PS# IDs.
Process flow diagram generated.
Proceeding to Step 5: Process Exceptions...
```

```
<action>Load, read entire file, then execute {nextStepFile}</action>
```

---

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN [process steps approved] and [Mermaid flowchart generated] and [output files updated], will you then load and read fully `{nextStepFile}` to execute and begin capturing process exceptions.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:
- 5-15 process steps captured with PS# IDs
- Each step has name, description, owner, rationale
- Steps approved using adaptive_approval protocol
- Mermaid flowchart generated
- Updated structured-data.json
- **APPENDED Section 2 to as-is-process-documentation.md (RECOVERY-SAFE)**
- Ready to proceed to Step 5

### ❌ SYSTEM FAILURE:
- Less than 5 steps or missing required fields
- Proceeded without approval
- Started capturing exceptions in this step
- Flowchart not generated
- Skipped to later steps

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
