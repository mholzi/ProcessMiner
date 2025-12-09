---
name: 'step-03-overview'
description: 'Capture high-level process overview: purpose, trigger, frequency, volume'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/start-new-process'

# File References
thisStepFile: '{workflow_path}/steps/step-03-overview.md'
nextStepFile: '{workflow_path}/steps/step-04-process-steps.md'
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

# Step 3: High-Level Process Overview

## STEP GOAL

Capture the high-level process overview by eliciting four key topics: Purpose, Trigger, Frequency, and Volume. Each topic must be approved before proceeding.

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
  - **If true**: Draft from imported documents, SME validates
  - **If false**: Use `smart_options` protocol to elicit from SME

### Step-Specific Rules
- All 4 topics (Purpose, Trigger, Frequency, Volume) MUST be approved before proceeding
- Use `adaptive_approval` protocol for each topic
- Focus ONLY on process overview — no process steps yet

### 🚨 MANDATORY MENU RULE (NO EXCEPTIONS)
**EVERY approval menu MUST include ALL THREE options:**
```
- [Y] Yes, Accept
- [E] Edit
- [R] Rewrite
```
**FORBIDDEN:** Showing only [Y]/[E] without [R]. The [R] Rewrite option opens the AI-assisted sub-menu (Advanced Elicitation, Party Mode, Brainstorming, Quick Questions).

## EXECUTION PROTOCOLS

- Load protocols from `{protocolsFile}`
- Use `smart_options` for contextual option generation
- Use `adaptive_approval` for content approval with elicitation option

## CONTEXT BOUNDARIES

- `documents_uploaded` flag set in Step 2
- Imported data available if documents were uploaded
- Process name and ID established in Step 1

---

## EXECUTION SEQUENCE

### 1. Display Progress

```
**Progress: Step 3 of 9 - Process Overview**

Let's capture the big picture of this process. We'll cover 4 key aspects:
1. Process Purpose
2. Process Trigger
3. Process Frequency
4. Process Volume

Each one will be drafted and reviewed before moving on.
```

### 2. Process Topics

The four topics to cover:

| # | Topic | Response Variable | Question |
|---|-------|-------------------|----------|
| 1 | Process Purpose | process_purpose | What is the primary purpose of this process? |
| 2 | Process Trigger | process_trigger | What typically triggers this process to start? |
| 3 | Process Frequency | process_frequency | How often does this process run? |
| 4 | Process Volume | process_volume | What's the typical volume? |

### 3. Iterate Through Each Topic

For each topic (Purpose, Trigger, Frequency, Volume):

```
<iterate for="each topic">
  <format>**Topic {{topic_number}} of 4: {{topic_name}}**</format>

  <check if="documents_uploaded == true">
    <!-- Draft from imported documents -->
    <critical>Do NOT ask questions - draft from imported documents.</critical>
    <action>Write 2-3 paragraphs summarizing {{topic_name}} based on imported docs and banking context</action>
  </check>

  <check if="documents_uploaded == false">
    <!-- Elicit from SME using smart_options -->
    <action>Use smart_options protocol to generate contextual options for {{topic_name}}</action>

    <invoke-protocol name="smart_options">
      <param name="question">{{topic_question}}</param>
      <param name="context">{current_process_name}</param>
      <param name="option_type">{{topic_type}}</param>
    </invoke-protocol>

    <action>Based on response, write 2-3 paragraphs summarizing {{topic_name}}</action>
  </check>

  <!-- Get approval using adaptive_approval protocol -->
  <approval-menu topic="{{topic_name}}">
    <display>
    ---
    **{{topic_name}} - Draft:**

    {{content_display}}

    ---
    How would you like to proceed?
    - **[Y] Yes, Accept** — This accurately captures the {{topic_name}}
    - **[E] Edit** — I have minor corrections to make
    - **[R] Rewrite** — Let's redraft this together using AI-assisted techniques
    </display>

    <handle option="Y">
      Store content in session_state.captured_data.metadata.{{topic_response}}
      Mark {{topic_name}} as approved
      Display: "{{topic_name}} approved."
    </handle>

    <handle option="E">
      Ask: "Please provide your corrections:"
      Incorporate corrections into content
      Present updated content
      Ask: "Does this now accurately reflect the {{topic_name}}? [Y/N]"
      If Y: Store and return approved
      If N: Loop until approved
    </handle>

    <handle option="R">
      <display>
      ---
      ## Rewrite: {{topic_name}}

      You've selected Rewrite. How would you like to approach this?

      - **[A] Advanced Elicitation** — Structured techniques (Five Whys, Socratic questioning)
      - **[P] Party Mode** — Multiple AI perspectives discuss
      - **[B] Brainstorming** — Creative exploration and idea generation
      - **[Q] Quick Questions** — 3-5 targeted questions
      - **[X] Back** — Return to approval menu
      </display>

      <handle option="A">
        Invoke {advancedElicitationTask} with context about {{topic_name}}
        After elicitation: Generate new draft, return to approval menu
      </handle>

      <handle option="P">
        Invoke {partyModeWorkflow} with context about {{topic_name}}
        After party mode: Generate new draft, return to approval menu
      </handle>

      <handle option="B">
        Invoke {brainstormingWorkflow} with context about {{topic_name}}
        After brainstorming: Generate new draft, return to approval menu
      </handle>

      <handle option="Q">
        Ask 3-5 targeted questions based on topic type
        After user answers: Synthesize into new draft, return to approval menu
      </handle>

      <handle option="X">
        Return to approval menu
      </handle>
    </handle>
  </approval-menu>
</iterate>
```

### 4. Verify All Topics Approved

```
<action>Verify all topics approved: Purpose, Trigger, Frequency, Volume</action>
```

### 5. Update Output Files (Silent) — RECOVERY-SAFE

**🚨 CRITICAL: Incremental Save for Recovery**

After ALL 4 topics are approved, you MUST update BOTH files to enable session recovery:

```
<action silent="true">Update {structuredDataFile}:
  - metadata section with all 4 topics (purpose, trigger, frequency, volume)
  - metadata.confidence = assess confidence level
  - session.checkpoint.step = 3
  - session.last_updated = {{timestamp}}
</action>

<action silent="true" critical="RECOVERY">Update {mainDocumentFile} - APPEND Section 1:

  APPEND the following content to the main document:

  ---
  ## 1. Process Overview

  > **About this section:** Foundational context - what this process is, who owns it, and what business need it serves.

  ### 1.1 Process Identification

  | Attribute | Value |
  |-----------|-------|
  | **Process Name** | {{process_name}} |
  | **Process ID** | {{process_id}} |
  | **Process Category** | Banking Operations |
  | **Process Owner** | {{from session or TBD}} |

  ### 1.2 Purpose and Trigger

  {{process_purpose - the approved content}}

  {{process_trigger - the approved content}}

  ### 1.3 Operational Characteristics

  {{process_frequency - the approved content}}

  {{process_volume - the approved content}}

  > **Section Confidence:** {{assessed_confidence}} | **Basis:** SME-validated during elicitation

  ---

  This incremental save ensures:
  - If session aborts after Step 3, Section 1 is recoverable from the MD file
  - JSON and MD stay in sync
  - SME work is never lost
</action>
```

### 6. Proceed to Next Step

Display:
```
**Process Overview Complete!**
All 4 topics approved. Proceeding to Step 4: Process Steps...
```

```
<action>Load, read entire file, then execute {nextStepFile}</action>
```

---

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN [all 4 topics approved] and [output files updated], will you then load and read fully `{nextStepFile}` to execute and begin capturing process steps.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:
- All 4 topics captured and approved
- Used correct approach based on `documents_uploaded` flag
- Updated structured-data.json with metadata
- **APPENDED Section 1 to as-is-process-documentation.md (RECOVERY-SAFE)**
- Ready to proceed to Step 4

### ❌ SYSTEM FAILURE:
- Proceeded without approving all 4 topics
- Used wrong approach for `documents_uploaded` state
- Started capturing process steps in this step
- Skipped to later steps

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
