---
name: 'step-08-systems'
description: 'Catalog systems and tools with SYS# IDs'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/start-new-process'

# File References
thisStepFile: '{workflow_path}/steps/step-08-systems.md'
nextStepFile: '{workflow_path}/steps/step-09-validation.md'
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

# Step 8: Identify Systems & Tools

## STEP GOAL

Catalog all systems and tools used in the process with unique SYS# IDs, linked to relevant PS# process steps. Each system should have system_type, purpose, integration status, and dependencies documented.

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
  - **If true**: Extract systems from imported documents, SME validates
  - **If false**: Use `smart_options` and `capture_structured_items` protocols

### Step-Specific Rules
- SYS# format: `SYS-{{process_name_abbrev}}-###` (e.g., SYS-CRO-001)
- Each system MUST link to relevant PS# ID(s)
- Each system MUST have system_type (CORE/SUPPORTING/EXTERNAL)
- Include integration status and dependencies
- Focus ONLY on systems — validation happens next

### 🚨 MANDATORY MENU RULE (NO EXCEPTIONS)
**EVERY approval menu MUST include ALL THREE options:**
```
- [Y] Yes, Accept
- [E] Edit
- [R] Rewrite
```

## EXECUTION PROTOCOLS

- Load protocols from `{protocolsFile}`
- Use `smart_options` for contextual option generation
- Use `capture_structured_items` for iterative capture
- Use `adaptive_approval` for content approval

## CONTEXT BOUNDARIES

- Process steps (PS#), exceptions (EX#), pain points (PP#), controls (CP#) all captured
- Systems link to one or more PS# IDs
- This is the last elicitation step before validation

---

## EXECUTION SEQUENCE

### 1. Display Progress

```
**Progress: Step 8 of 9 - Systems & Tools**

Finally, let's catalog the systems and tools used in this process.
We'll note what each system does and how they integrate.
```

### 2. Handle Document-Based Approach

```
<check if="documents_uploaded == true">
  <critical>Extract systems from imported documents.</critical>

  <action>Identify all systems, applications, and tools:
  - System names and vendors
  - Integration points and data flows
  - Link to relevant PS# IDs
  - Assign SYS-{{process_name_abbrev}}-### IDs
  </action>
</check>
```

### 3. Handle Fresh Elicitation Approach

```
<check if="documents_uploaded == false">
  <invoke-protocol name="smart_options">
    <param name="question">What systems or tools are used in this process?</param>
    <param name="context">{current_process_name}</param>
    <param name="option_type">system</param>
  </invoke-protocol>

  <invoke-protocol name="capture_structured_items">
    <param name="item_type">system</param>
    <param name="id_prefix">SYS</param>
  </invoke-protocol>
</check>
```

### 4. Get Approval Using Protocol

```
<approval-menu topic="Systems & Tools">
  <display>
  ---
  **Systems & Tools - Draft:**

  {{content_display}}

  ---
  How would you like to proceed?
  - **[Y] Yes, Accept** — This accurately captures the Systems & Tools
  - **[E] Edit** — I have minor corrections to make
  - **[R] Rewrite** — Let's redraft this together using AI-assisted techniques
  </display>

  <handle option="R">
    - **[A] Advanced Elicitation** — Structured techniques
    - **[P] Party Mode** — Multiple AI perspectives
    - **[B] Brainstorming** — Creative exploration
    - **[Q] Quick Questions** — Targeted questions
    - **[X] Back** — Return to approval menu
  </handle>
</approval-menu>
```

### 5. Update Output Files (Silent) — RECOVERY-SAFE

**🚨 CRITICAL: Incremental Save for Recovery**

After systems are captured, you MUST update BOTH files to enable session recovery:

```
<action silent="true">Update {structuredDataFile}:
  - systems array
  - Each system: id, name, description, system_type, links.process_steps, confidence
  - session.checkpoint.step = 8
  - session.last_updated = {{timestamp}}
</action>

<action silent="true" critical="RECOVERY">Update {mainDocumentFile} - APPEND Section 5:

  APPEND the following content to the main document:

  ---
  ## 5. System Dependencies

  > **About this section:** What technology supports this process?

  ### 5.1 System Summary

  | SYS# | System Name | Purpose | Type | Integration Points |
  |------|-------------|---------|------|-------------------|
  {{Generate table row for each approved system}}

  ### 5.2 System Integration Overview

  {{Generate narrative describing how systems connect and data flows between them}}

  ### 5.3 Data Flow Summary

  {{Generate summary of key data flows: what data moves between which systems}}

  > **Section Confidence:** {{assessed_confidence}} | **Basis:** SME-validated during elicitation

  ---

  This incremental save ensures:
  - If session aborts after Step 8, all systems are recoverable
  - Section 5 preserved in main document
  - SME work is never lost
</action>
```

### 6. Proceed to Next Step

```
**Systems & Tools Complete!**
{{total_systems}} systems documented with SYS# IDs.
Proceeding to Step 9: Final Review...
```

```
<action>Load, read entire file, then execute {nextStepFile}</action>
```

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:
- Systems captured with SYS# IDs
- Each system has system_type
- Each system linked to relevant PS# IDs
- Integration status documented
- Updated structured-data.json
- **APPENDED Section 5 to as-is-process-documentation.md (RECOVERY-SAFE)**
- Ready to proceed to Step 9

### ❌ SYSTEM FAILURE:
- Systems missing SYS# IDs or system_type
- Systems not linked to PS# IDs
- Skipped to validation without systems
- Started validation in this step

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
