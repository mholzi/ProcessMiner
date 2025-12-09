---
name: 'step-09-validation'
description: 'Final review, AI-driven gap analysis, and completeness check'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/start-new-process'

# File References
thisStepFile: '{workflow_path}/steps/step-09-validation.md'
workflowFile: '{workflow_path}/workflow.md'

# Shared Protocols
protocolsFile: '{module_root}/workflows/shared/protocols/protocols.md'

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
partyModeWorkflow: '{project-root}/.bmad/core/workflows/party-mode/workflow.md'

# Output Files
structuredDataFile: '{current_process_folder}/structured-data.json'
mainDocumentFile: '{current_process_folder}/as-is-process-documentation.md'
exceptionsDetailFile: '{current_process_folder}/exceptions-detail.md'
painPointsDetailFile: '{current_process_folder}/pain-points-detail.md'
controlPointsDetailFile: '{current_process_folder}/control-points-detail.md'
---

# Step 9: Validation & Completeness Check

## STEP GOAL

Perform final review of all captured content. AI analyzes for gaps, ambiguities, and inconsistencies. Address clarification questions. Finalize all output files.

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

### AI-Driven Assessment:
- AI MUST actively analyze captured content
- Surface gaps, ambiguities, inconsistencies
- Ask clarification questions before declaring complete

### Step-Specific Rules
- This is the FINAL step — no step-10 exists
- All 5 output files must be finalized
- SME must confirm completeness

## EXECUTION PROTOCOLS

- Load protocols from `{protocolsFile}`
- AI analyzes all captured data
- Use elicitation for unresolved questions if needed
- Finalize all documents with completion metadata

## CONTEXT BOUNDARIES

- All previous steps (1-8) complete
- All structured IDs assigned (PS#, EX#, PP#, CP#, SYS#)
- All cross-references established

---

## EXECUTION SEQUENCE

### 1. Display Progress and Summary

```
**Progress: Step 9 of 9 - Final Review**

Great work! Let me summarize what we've captured:

**Process Overview:**
- Name: {{process_name}}
- Client Groups: {{client_groups}}
- Purpose: {{process_purpose}}
- Trigger: {{process_trigger}}
- Frequency: {{process_frequency}}

**Captured Elements:**
- {{count_process_steps}} Process Steps (PS# IDs assigned)
- {{count_exceptions}} Process Exceptions (EX# IDs assigned)
- {{count_pain_points}} Pain Points (PP# IDs assigned)
- {{count_controls}} Controls (CP# IDs assigned)
- {{count_systems}} Systems (SYS# IDs assigned)

**Cross-References Established:**
- Exceptions linked to process steps: {{ex_ps_links}}
- Pain points linked to process steps: {{pp_ps_links}}
- Controls linked to process steps: {{cp_ps_links}}
- Systems linked to process steps: {{sys_ps_links}}
```

### 2. AI-Driven Gap Analysis

```
<critical name="AI_ASSESSMENT">
Before asking the user if they're done, the AI MUST actively analyze the captured content
and identify any gaps, ambiguities, or inconsistencies that need clarification.
</critical>

<action>Analyze all captured content across sections and identify:
  1. **Gaps** - Steps without owners, controls without requirements, pain points without severity
  2. **Ambiguities** - Vague descriptions, unclear triggers, unspecified frequencies
  3. **Inconsistencies** - Conflicting information between sections
  4. **Missing Links** - Items not cross-referenced to process steps
  5. **Shallow Areas** - Sections with less depth compared to others
</action>

<action>Generate list of clarification questions (0 to N items)</action>
```

### 3. Handle Clarification Questions (if any)

```
<check if="clarification_questions.length > 0">
  <format>
  ---
  **Review Assessment**

  I've reviewed everything we captured. Before we finalize, I have {{clarification_questions.length}} question(s):
  </format>

  <loop name="clarification_loop" for="each question in clarification_questions">
    <ask response="clarification_response">
    - (a) **Answer directly** — I'll provide the answer
    - (b) **Elicitation** — Let's explore this deeper
    - (c) **Skip** — Not important / I don't know
    </ask>
  </loop>
</check>

<check if="clarification_questions.length == 0">
  <format>
  ---
  **Review Assessment**

  I've reviewed everything we captured — no gaps or inconsistencies found.
  The documentation looks complete and internally consistent.
  </format>
</check>
```

### 4. User Additions

```
<ask response="user_additions">
Anything you'd like to add or correct?

- [ ] Yes, I have additions
- [ ] No, looks good
</ask>
```

### 5. Finalize All Output Files

```
<action>Mark session as complete</action>

<action silent="true">Finalize {structuredDataFile} with:
- validation.status = "COMPLETE"
- validation.completed_at = {{timestamp}}
- session.last_updated = {{timestamp}}
- traceability matrix
- element counts
- confidence assessments
</action>

<action silent="true">Finalize {mainDocumentFile} with completion info</action>
<action silent="true">Finalize {exceptionsDetailFile} with completion info</action>
<action silent="true">Finalize {painPointsDetailFile} with completion info</action>
<action silent="true">Finalize {controlPointsDetailFile} with completion info</action>
```

### 6. Completion Message

```
**Documentation Complete!**

Your process documentation has been saved:

**Structured Data (for downstream agents):**
- {current_process_folder}/structured-data.json

**Main Document:**
- {current_process_folder}/as-is-process-documentation.md

**Detail Documents:**
- {current_process_folder}/exceptions-detail.md
- {current_process_folder}/pain-points-detail.md
- {current_process_folder}/control-points-detail.md

**Summary:**
- {{count_process_steps}} Process Steps documented
- {{count_exceptions}} Process Exceptions documented
- {{count_pain_points}} Pain Points identified
- {{count_controls}} Controls mapped
- {{count_systems}} Systems catalogued
- All cross-references established
- All documents synchronized

**Next Step:**
Review and approve the full draft documentation before finalizing.
```

---

## CRITICAL STEP COMPLETION NOTE

This is the FINAL step. ONLY WHEN [AI gap analysis complete] and [clarifications addressed] and [all 5 output files finalized], will the workflow be complete.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:
- AI performed gap analysis
- Clarification questions addressed
- User confirmed completeness
- All 5 output files finalized with validation.status = "COMPLETE"
- Completion message displayed
- Next steps communicated

### ❌ SYSTEM FAILURE:
- Skipped AI gap analysis
- Did not address clarification questions
- Did not finalize output files
- Did not display completion summary

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
