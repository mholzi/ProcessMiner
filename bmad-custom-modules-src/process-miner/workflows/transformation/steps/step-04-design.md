---
name: 'step-04-design'
description: 'Document TO-BE state with full AS-IS traceability'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/transformation'

# File References
thisStepFile: '{workflow_path}/steps/step-04-design.md'
nextStepFile: '{workflow_path}/steps/step-05-validate.md'
workflowFile: '{workflow_path}/workflow.md'

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
partyModeWorkflow: '{project-root}/.bmad/core/workflows/party-mode/workflow.md'

# Output Files (MUST persist after each element review)
transformationDataFile: '{current_process_folder}/transformation-data.json'
targetStateFile: '{current_process_folder}/target-state-documentation.md'
transformationDecisionsFile: '{current_process_folder}/transformation-decisions-detail.md'
gapResolutionFile: '{current_process_folder}/gap-resolution-log.md'

# Template References
targetStateTemplate: '{module_root}/templates/target-state-documentation.md'
decisionsTemplate: '{module_root}/templates/transformation-decisions-detail.md'
gapLogTemplate: '{module_root}/templates/gap-resolution-log.md'
---

# Step 4: Document TO-BE State

## STEP GOAL

Transform the elicited target state vision into structured TO-BE documentation with full AS-IS traceability (PS#→TS#, CP#→TC#, JT#→TJ#).

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:
- 🛑 **NEVER** generate content without user input
- 📖 **CRITICAL**: Read the complete step file before taking any action
- 🔄 **CRITICAL**: When loading next step, ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:
- ✅ You are a Process Transformation Orchestrator
- ✅ **TRACE EVERY CHANGE** - Every TO-BE element must map to AS-IS source
- ✅ Use structured references consistently (TS#, TC#, TJ#)
- ✅ Document for handover - IT inherits context, not just diagrams

### Step-Specific Rules:
- Focus on DOCUMENTING the agreed target state
- **FORBIDDEN** to introduce new decisions without SME confirmation
- Every TS# must trace to PS# (or be marked as NEW)
- Apply change type taxonomy consistently

---

## 🔴 CRITICAL: PERSISTENCE PROTOCOL

> **DATA LOSS PREVENTION:** After EVERY element review (step, control, touchpoint), you MUST write to output files AND validate the write succeeded. If the session ends unexpectedly, all reviewed elements must be recoverable from the output files.

### Persistence Rules:

1. **AFTER EVERY APPROVED/EDITED ELEMENT:**
   - Write to `{targetStateFile}` - the appropriate section
   - Write to `{transformationDecisionsFile}` - if TD# involved
   - Write to `{gapResolutionFile}` - if gaps addressed
   - Update `{transformationDataFile}` - JSON state tracking

2. **VALIDATE EVERY WRITE:**
   - Read back the section just written
   - Confirm data matches what was approved
   - Display confirmation to user

3. **RECOVERY CAPABILITY:**
   - If session resumes, check output files for progress
   - Resume from last persisted element
   - Never re-review already-persisted elements

### Output File Mapping:

| Element Type | Target Section in targetStateFile | Also Update |
|--------------|-----------------------------------|-------------|
| Process Step (TS#) | Section 3.4 (Process Step Details) | Section 2.1 (Reconciliation) |
| Control (TC#) | Section 4.2-4.4 (Control tables) | gapResolutionFile if gap closed |
| Touchpoint (TJ#) | Section 5.3-5.4 (Touchpoint tables) | gapResolutionFile if friction resolved |
| Decision (TD#) | Section 7.2 (Decisions Log) | transformationDecisionsFile (full detail) |
| Innovation (II#) | Section 6.2-6.4 (Innovation tables) | - |

---

## EXECUTION PROTOCOLS

- Build target state documentation section by section
- Maintain full traceability to AS-IS references
- Apply change types: Unchanged, Modified, Eliminated, Automated, Consolidated, New
- Generate structured reference IDs (TS#, TC#, TJ#)
- **PERSIST after every element review - never batch writes**

## CONTEXT BOUNDARIES

- Target state vision confirmed from Step 3
- All TD# decisions captured
- This step creates the formal documentation

---

## EXECUTION SEQUENCE

### 1. Set Documentation Context

Display:
```
{contributor_name}, now let's document the target state formally.

I'll structure this as:
1. **Reconciliation tables** - How AS-IS maps to TO-BE
2. **Target process steps** - The new flow with TS# references
3. **Control design** - How controls change (TC# references)
4. **CX design** - How the journey improves (TJ# references)

Every element will trace back to its AS-IS source. This is your transformation blueprint.
```

### 2. Interactive Process Step Design Review

```
<format>
## Process Step Design

{contributor_name}, let's walk through each step of the target state together.

For each step, I'll explain:
- **What changed** from AS-IS and why
- **What problems it solves** (control gaps, pain points, friction)
- **What innovations it enables**

You'll have the chance to approve, edit, or brainstorm alternatives for each step before we move on.

**Total Steps to Review:** {{total_steps}} ({{modified_count}} modified, {{automated_count}} automated, {{new_count}} new, {{eliminated_count}} eliminated)
</format>

<action>
Prepare the step review queue:
1. Load all AS-IS process steps (PS#) from as-is-process-documentation.md
2. Load all transformation decisions (TD#) from transformation-data.json
3. Map each AS-IS step to its TO-BE disposition based on decisions
4. Include any NEW steps identified in elicitation
5. Order steps by logical process sequence
</action>
```

### 3. Step-by-Step Design Walkthrough

```
<for_each step in="target_steps" order="sequential">

<format>
---
## Step {{loop.index}} of {{total_steps}}: {{step.tobe_name}}

| Reference | Change Type |
|-----------|-------------|
| **TO-BE:** {{step.tobe_ref}} | {{step.change_type}} |
| **AS-IS:** {{step.asis_ref}} | |

---

### 📖 What This Step Does (TO-BE)

{{step.tobe_description}}

---

### 🔄 How This Compares to AS-IS

**Before (AS-IS):**
{{step.asis_description}}

**After (TO-BE):**
{{step.tobe_summary}}

**Key Differences:**
{{step.verbal_differences}}

---

### 🎯 Why We're Making This Change

**Driving Decision(s):** {{step.td_refs}}

{{step.rationale_explanation}}

---

### ✅ Problems This Addresses

{{#if step.addresses_any}}
| Type | Reference | Problem | How This Step Resolves It |
|------|-----------|---------|---------------------------|
{{#each step.control_gaps}}
| 🛡️ Control Gap | {{this.ref}} | {{this.description}} | {{this.resolution}} |
{{/each}}
{{#each step.pain_points}}
| 😤 Pain Point | {{this.ref}} | {{this.description}} | {{this.resolution}} |
{{/each}}
{{#each step.friction_points}}
| 🚧 CX Friction | {{this.ref}} | {{this.description}} | {{this.resolution}} |
{{/each}}
{{else}}
This step maintains existing functionality without addressing specific documented issues.
{{/if}}

---

### 💡 Innovations Enabled

{{#if step.innovations}}
| II# | Innovation | How This Step Enables It |
|-----|------------|--------------------------|
{{#each step.innovations}}
| {{this.ref}} | {{this.name}} | {{this.enablement}} |
{{/each}}
{{else}}
No specific innovations are directly tied to this step.
{{/if}}

---

### 📊 Step Attributes

| Attribute | AS-IS | TO-BE |
|-----------|-------|-------|
| **Owner** | {{step.asis_owner}} | {{step.tobe_owner}} |
| **System(s)** | {{step.asis_systems}} | {{step.tobe_systems}} |
| **Automation Level** | {{step.asis_automation}} | {{step.tobe_automation}} |
| **Input(s)** | {{step.asis_inputs}} | {{step.tobe_inputs}} |
| **Output(s)** | {{step.asis_outputs}} | {{step.tobe_outputs}} |
| **Controls** | {{step.asis_controls}} | {{step.tobe_controls}} |
</format>

<ask response="step_{{loop.index}}_review">
**Your input on {{step.tobe_ref}} - {{step.tobe_name}}:**

- **[A]** Approve - This step is correct as designed
- **[E]** Edit - I want to modify something about this step
- **[B]** Brainstorm - Let's explore alternative approaches
- **[Q]** Question - I have questions before deciding
- **[S]** Skip - Come back to this step later
</ask>

<check if="response == 'A'">
  <action>
  Mark {{step.tobe_ref}} as APPROVED.
  </action>

  <!-- 🔴 MANDATORY PERSISTENCE - DO NOT SKIP -->
  <persist critical="true">
    <step n="1" file="{targetStateFile}" section="3.4">
      Write/update the step detail block for {{step.tobe_ref}}:

      #### {{step.tobe_ref}}: {{step.tobe_name}}

      | Attribute | Value |
      |-----------|-------|
      | **Step Name** | {{step.tobe_name}} |
      | **Owner** | {{step.tobe_owner}} |
      | **System(s)** | {{step.tobe_systems}} |
      | **Automation Level** | {{step.tobe_automation}} |
      | **Input(s)** | {{step.tobe_inputs}} |
      | **Output(s)** | {{step.tobe_outputs}} |
      | **AS-IS Reference** | {{step.asis_ref}} |
      | **Change Type** | {{step.change_type}} |

      **Description:**
      {{step.tobe_description}}

      **Rationale for Change:**
      {{step.rationale_explanation}}

      **Problems Addressed:** {{step.problems_addressed_summary}}

      **Controls at this Step:** {{step.tobe_controls}}
    </step>

    <step n="2" file="{targetStateFile}" section="2.1">
      Add/update reconciliation row:
      | {{step.asis_ref}} | {{step.asis_name}} | {{step.change_type}} | {{step.tobe_ref}} | {{step.tobe_name}} | {{step.rationale_brief}} |
    </step>

    <step n="3" file="{transformationDataFile}">
      Update JSON:
      step_reviews[{{step.tobe_ref}}] = {
        status: "approved",
        timestamp: "{{now}}",
        persisted: true,
        asis_ref: "{{step.asis_ref}}",
        change_type: "{{step.change_type}}",
        problems_addressed: {{step.problems_addressed_array}}
      }
    </step>

    <step n="4" file="{gapResolutionFile}" condition="step.closes_gaps">
      For each gap closed by this step, add/update:
      | {{gap.ref}} | Control/CX | {{gap.description}} | Resolved by {{step.tobe_ref}} | Resolved | {{now}} |
    </step>
  </persist>

  <!-- 🔴 MANDATORY VALIDATION - DO NOT SKIP -->
  <validate critical="true">
    <check n="1">Read {targetStateFile} section 3.4, confirm {{step.tobe_ref}} block exists</check>
    <check n="2">Read {targetStateFile} section 2.1, confirm reconciliation row exists</check>
    <check n="3">Read {transformationDataFile}, confirm step_reviews[{{step.tobe_ref}}].persisted == true</check>
    <on_failure>
      HALT - Do not proceed to next step
      Display error: "⚠️ PERSISTENCE FAILED for {{step.tobe_ref}} - Retrying write..."
      Retry persist steps
      If retry fails: Ask user to manually verify files
    </on_failure>
  </validate>

  <format>
  ✅ **{{step.tobe_ref}} Approved & Saved**

  📁 Written to:
  - target-state-documentation.md (Section 3.4 & 2.1)
  - transformation-data.json
  {{#if step.closes_gaps}}- gap-resolution-log.md ({{step.gaps_closed_count}} gap(s) marked resolved){{/if}}

  Moving to next step...
  </format>
</check>

<check if="response == 'E'">
  <ask response="step_{{loop.index}}_edit_details">
  What would you like to change about **{{step.tobe_ref}}**?

  You can modify:
  - Step name or description
  - Owner or systems
  - Automation level
  - Inputs/outputs
  - How it addresses problems
  - Rationale

  Please describe your changes:
  </ask>
  <action>
  1. Apply user's requested changes to step definition
  2. Update in-memory step object
  3. Regenerate the step display with updates
  4. Re-present step for approval (which will trigger persistence on [A])
  </action>
  <!-- Note: Persistence happens when user approves the edited version -->
</check>

<check if="response == 'B'">
  <format>
  Let's brainstorm alternatives for **{{step.tobe_ref}}**.

  **Current Approach:** {{step.tobe_summary}}

  I'll help explore other ways to achieve the same goals.
  </format>
  <action>
  Execute {advancedElicitationTask} focused on this specific step:
  - Present 2-3 alternative approaches
  - Compare trade-offs (complexity, cost, risk, benefit)
  - Get user selection
  - Update step definition based on selection
  - Re-present step for approval
  </action>
</check>

<check if="response == 'Q'">
  <ask response="step_{{loop.index}}_question">
  What questions do you have about **{{step.tobe_ref}}**?
  </ask>
  <action>
  Answer user's question thoroughly, drawing on:
  - AS-IS documentation
  - Transformation decisions (TD#)
  - Control analysis
  - CX analysis
  - Innovation ideas
  Then re-present the review options for this step.
  </action>
</check>

<check if="response == 'S'">
  <action>
  Mark {{step.tobe_ref}} as SKIPPED for later review.
  Record in transformation-data.json: step_reviews[{{step.tobe_ref}}] = { status: "skipped", timestamp: now }
  </action>
  <format>
  ⏭️ **{{step.tobe_ref}} Skipped** - We'll return to this step after reviewing the others.
  </format>
</check>

</for_each>
```

### 4. Review Skipped Steps

```
<check if="skipped_steps.count > 0">
<format>
---
## Returning to Skipped Steps

You skipped {{skipped_steps.count}} step(s) during the initial review. Let's revisit them now:

{{#each skipped_steps}}
{{loop.index}}. {{this.tobe_ref}} - {{this.tobe_name}}
{{/each}}
</format>

<for_each step in="skipped_steps">
  <action>Re-present step using the same format from Section 3</action>
  <action>User MUST select A, E, B, or Q (Skip not available on second pass)</action>
</for_each>
</check>

<check if="skipped_steps.count == 0">
<format>
All steps reviewed on first pass - no skipped steps to revisit.
</format>
</check>
```

### 5. Process Step Reconciliation Summary

```
<format>
---
## Process Step Design Complete

All {{total_steps}} steps have been reviewed:

| Status | Count |
|--------|-------|
| ✅ Approved | {{approved_count}} |
| ✏️ Edited | {{edited_count}} |
| 💡 Brainstormed | {{brainstormed_count}} |

### Change Type Summary

| Change Type | Count | % |
|-------------|-------|---|
| Unchanged | {{unchanged_count}} | {{unchanged_pct}}% |
| Modified | {{modified_count}} | {{modified_pct}}% |
| Automated | {{automated_count}} | {{automated_pct}}% |
| Consolidated | {{consolidated_count}} | {{consolidated_pct}}% |
| Eliminated | {{eliminated_count}} | {{eliminated_pct}}% |
| New | {{new_count}} | {{new_pct}}% |

### Final Reconciliation Table

| AS-IS Ref | AS-IS Step | → | TO-BE Ref | TO-BE Step | Change Type | Status |
|-----------|------------|---|-----------|------------|-------------|--------|
{{#each all_steps}}
| {{this.asis_ref}} | {{this.asis_name}} | → | {{this.tobe_ref}} | {{this.tobe_name}} | {{this.change_type}} | {{this.review_status}} |
{{/each}}

### Target Process Flow Diagram

```mermaid
{{tobe_process_diagram}}
```
</format>

<ask response="process_design_complete">
Process step design is complete. Ready to proceed?

- **[Y]** Yes - Continue to Control Design
- **[R]** Review - Go back to a specific step
</ask>

<check if="response == 'R'">
  <ask response="review_which_step">
  Which step would you like to review? Enter the TO-BE reference (e.g., TS-ONB-001):
  </ask>
  <action>Return to that specific step for re-review</action>
</check>
```

### 6. Interactive Control Design Review

```
<format>
## Control Design

{contributor_name}, now let's walk through each control in the target state.

For each control, I'll explain:
- **What changed** from AS-IS and why
- **Which gaps it closes** (if any)
- **Where it applies** in the new process

You'll approve, edit, or brainstorm alternatives for each control.

**Total Controls to Review:** {{total_controls}} ({{modified_count}} modified, {{new_count}} new, {{eliminated_count}} eliminated)
</format>

<action>
Prepare the control review queue:
1. Load all AS-IS controls (CP#) from as-is-process-documentation.md
2. Load all control gaps (CG#) from control analysis
3. Load transformation decisions (TD#) affecting controls
4. Map each AS-IS control to its TO-BE disposition
5. Include any NEW controls identified in elicitation
6. Order controls by process step sequence
</action>
```

### 7. Control-by-Control Design Walkthrough

```
<for_each control in="target_controls" order="sequential">

<format>
---
## Control {{loop.index}} of {{total_controls}}: {{control.tobe_name}}

| Reference | Disposition |
|-----------|-------------|
| **TO-BE:** {{control.tobe_ref}} | {{control.disposition}} |
| **AS-IS:** {{control.asis_ref}} | |

---

### 🛡️ What This Control Does (TO-BE)

{{control.tobe_description}}

**Control Type:** {{control.control_type}}
**Process Step:** {{control.process_step}} ({{control.ts_ref}})

---

### 🔄 How This Compares to AS-IS

{{#if control.is_new}}
**This is a NEW control** - no AS-IS equivalent exists.

**Why we need it:** {{control.new_rationale}}
{{else}}
**Before (AS-IS):**
{{control.asis_description}}

**After (TO-BE):**
{{control.tobe_summary}}

**Key Changes:**
{{control.verbal_differences}}
{{/if}}

---

### 🎯 Why We're Making This Change

**Driving Decision(s):** {{control.td_refs}}

{{control.rationale_explanation}}

---

### ✅ Gaps This Control Closes

{{#if control.closes_gaps}}
| Gap Reference | Gap Description | How This Control Addresses It |
|---------------|-----------------|-------------------------------|
{{#each control.gaps_closed}}
| {{this.ref}} | {{this.description}} | {{this.resolution}} |
{{/each}}
{{else}}
This control maintains existing coverage without closing specific documented gaps.
{{/if}}

---

### 📊 Control Attributes

| Attribute | AS-IS | TO-BE |
|-----------|-------|-------|
| **Control Type** | {{control.asis_type}} | {{control.tobe_type}} |
| **Frequency** | {{control.asis_frequency}} | {{control.tobe_frequency}} |
| **Owner** | {{control.asis_owner}} | {{control.tobe_owner}} |
| **Automation** | {{control.asis_automation}} | {{control.tobe_automation}} |
| **Evidence** | {{control.asis_evidence}} | {{control.tobe_evidence}} |

---

### ⚠️ SOD Considerations

{{#if control.sod_relevant}}
**Segregation of Duties Impact:**
{{control.sod_analysis}}
{{else}}
No SOD considerations for this control.
{{/if}}
</format>

<ask response="control_{{loop.index}}_review">
**Your input on {{control.tobe_ref}} - {{control.tobe_name}}:**

- **[A]** Approve - This control is correct as designed
- **[E]** Edit - I want to modify this control
- **[B]** Brainstorm - Let's explore alternative control designs
- **[Q]** Question - I have questions before deciding
- **[S]** Skip - Come back to this control later
</ask>

<check if="response == 'A'">
  <action>
  Mark {{control.tobe_ref}} as APPROVED.
  </action>

  <!-- 🔴 MANDATORY PERSISTENCE - DO NOT SKIP -->
  <persist critical="true">
    <step n="1" file="{targetStateFile}" section="4.2">
      Add/update control reconciliation row:
      | {{control.asis_ref}} | {{control.asis_name}} | {{control.disposition}} | {{control.tobe_ref}} | {{control.tobe_name}} | {{control.rationale_brief}} |
    </step>

    <step n="2" file="{targetStateFile}" section="4.3" condition="control.closes_gaps">
      Add gap closure row(s):
      {{#each control.gaps_closed}}
      | {{this.gap_id}} | {{this.description}} | {{this.resolution}} | {{control.tobe_ref}} | {{this.verification_method}} |
      {{/each}}
    </step>

    <step n="3" file="{targetStateFile}" section="4.4" condition="control.is_new">
      Add new control row:
      | {{control.tobe_ref}} | {{control.tobe_name}} | {{control.regulation}} | {{control.process_step}} | {{control.control_type}} | {{control.rationale}} |
    </step>

    <step n="4" file="{transformationDataFile}">
      Update JSON:
      control_reviews[{{control.tobe_ref}}] = {
        status: "approved",
        timestamp: "{{now}}",
        persisted: true,
        asis_ref: "{{control.asis_ref}}",
        disposition: "{{control.disposition}}",
        gaps_closed: {{control.gaps_closed_array}},
        sod_relevant: {{control.sod_relevant}}
      }
    </step>

    <step n="5" file="{gapResolutionFile}" condition="control.closes_gaps">
      For each gap closed by this control:
      {{#each control.gaps_closed}}
      Update/add row:
      | {{this.gap_id}} | Control Analyst | {{this.description}} | Resolved by {{control.tobe_ref}}: {{this.resolution}} | Resolved | {{now}} |
      {{/each}}
    </step>

    <step n="6" file="{transformationDecisionsFile}" condition="control.has_td">
      Update TD# entry with control implementation:
      TD#{{control.td_ref}} - Control Implementation: {{control.tobe_ref}}
    </step>
  </persist>

  <!-- 🔴 MANDATORY VALIDATION - DO NOT SKIP -->
  <validate critical="true">
    <check n="1">Read {targetStateFile} section 4.2, confirm {{control.tobe_ref}} reconciliation row exists</check>
    <check n="2" condition="control.closes_gaps">Read {gapResolutionFile}, confirm gaps marked resolved</check>
    <check n="3">Read {transformationDataFile}, confirm control_reviews[{{control.tobe_ref}}].persisted == true</check>
    <on_failure>
      HALT - Do not proceed to next control
      Display error: "⚠️ PERSISTENCE FAILED for {{control.tobe_ref}} - Retrying write..."
      Retry persist steps
      If retry fails: Ask user to manually verify files
    </on_failure>
  </validate>

  <format>
  ✅ **{{control.tobe_ref}} Approved & Saved**

  📁 Written to:
  - target-state-documentation.md (Section 4.2{{#if control.closes_gaps}}, 4.3{{/if}}{{#if control.is_new}}, 4.4{{/if}})
  - transformation-data.json
  {{#if control.closes_gaps}}- gap-resolution-log.md ({{control.gaps_closed_count}} gap(s) marked resolved){{/if}}

  Moving to next control...
  </format>
</check>

<check if="response == 'E'">
  <ask response="control_{{loop.index}}_edit_details">
  What would you like to change about **{{control.tobe_ref}}**?

  You can modify:
  - Control name or description
  - Control type or frequency
  - Owner or automation level
  - Evidence requirements
  - Gap closure approach

  Please describe your changes:
  </ask>
  <action>
  1. Apply user's requested changes to control definition
  2. Update in-memory control object
  3. Regenerate the control display with updates
  4. Re-present control for approval (which will trigger persistence on [A])
  </action>
  <!-- Note: Persistence happens when user approves the edited version -->
</check>

<check if="response == 'B'">
  <format>
  Let's brainstorm alternatives for **{{control.tobe_ref}}**.

  **Current Approach:** {{control.tobe_summary}}

  I'll help explore other ways to achieve the same control objectives.
  </format>
  <action>
  Execute {advancedElicitationTask} focused on this specific control:
  - Present 2-3 alternative control designs
  - Compare trade-offs (coverage, cost, auditability, automation potential)
  - Get user selection
  - Update control definition based on selection
  - Re-present control for approval
  </action>
</check>

<check if="response == 'Q'">
  <ask response="control_{{loop.index}}_question">
  What questions do you have about **{{control.tobe_ref}}**?
  </ask>
  <action>
  Answer user's question thoroughly, drawing on:
  - AS-IS control documentation
  - Control gap analysis
  - Transformation decisions (TD#)
  - Compliance requirements
  Then re-present the review options for this control.
  </action>
</check>

<check if="response == 'S'">
  <action>
  Mark {{control.tobe_ref}} as SKIPPED for later review.
  Record in transformation-data.json: control_reviews[{{control.tobe_ref}}] = { status: "skipped", timestamp: now }
  </action>
  <format>
  ⏭️ **{{control.tobe_ref}} Skipped** - We'll return to this control after reviewing the others.
  </format>
</check>

</for_each>
```

### 8. Review Skipped Controls

```
<check if="skipped_controls.count > 0">
<format>
---
## Returning to Skipped Controls

You skipped {{skipped_controls.count}} control(s) during the initial review. Let's revisit them now:

{{#each skipped_controls}}
{{loop.index}}. {{this.tobe_ref}} - {{this.tobe_name}}
{{/each}}
</format>

<for_each control in="skipped_controls">
  <action>Re-present control using the same format from Section 7</action>
  <action>User MUST select A, E, B, or Q (Skip not available on second pass)</action>
</for_each>
</check>

<check if="skipped_controls.count == 0">
<format>
All controls reviewed on first pass - no skipped controls to revisit.
</format>
</check>
```

### 9. Control Design Summary

```
<format>
---
## Control Design Complete

All {{total_controls}} controls have been reviewed:

| Status | Count |
|--------|-------|
| ✅ Approved | {{approved_count}} |
| ✏️ Edited | {{edited_count}} |
| 💡 Brainstormed | {{brainstormed_count}} |

### Control Disposition Summary

| Disposition | Count | % |
|-------------|-------|---|
| Unchanged | {{unchanged_count}} | {{unchanged_pct}}% |
| Modified | {{modified_count}} | {{modified_pct}}% |
| Eliminated | {{eliminated_count}} | {{eliminated_pct}}% |
| New | {{new_count}} | {{new_pct}}% |

### Gap Closure Summary

| Status | Count |
|--------|-------|
| Gaps Identified (AS-IS) | {{total_gaps}} |
| Gaps Closed (TO-BE) | {{gaps_closed}} |
| Gaps Remaining | {{gaps_remaining}} |
| Closure Rate | {{closure_pct}}% |

{{#if gaps_remaining > 0}}
⚠️ **Outstanding Gaps:**
{{#each outstanding_gaps}}
- {{this.ref}}: {{this.description}} - {{this.mitigation_plan}}
{{/each}}
{{/if}}

### Final Control Reconciliation Table

| AS-IS Ref | AS-IS Control | → | TO-BE Ref | TO-BE Control | Disposition | Gaps Closed | Status |
|-----------|---------------|---|-----------|---------------|-------------|-------------|--------|
{{#each all_controls}}
| {{this.asis_ref}} | {{this.asis_name}} | → | {{this.tobe_ref}} | {{this.tobe_name}} | {{this.disposition}} | {{this.gaps_closed}} | {{this.review_status}} |
{{/each}}

### SOD Verification Matrix

| SOD Requirement | AS-IS Compliance | TO-BE Compliance | Preserved |
|-----------------|------------------|------------------|-----------|
{{#each sod_requirements}}
| {{this.requirement}} | {{this.asis_status}} | {{this.tobe_status}} | {{this.preserved}} |
{{/each}}
</format>

<ask response="control_design_complete">
Control design is complete. Ready to proceed?

- **[Y]** Yes - Continue to CX Design
- **[R]** Review - Go back to a specific control
</ask>

<check if="response == 'R'">
  <ask response="review_which_control">
  Which control would you like to review? Enter the TO-BE reference (e.g., TC-ONB-001):
  </ask>
  <action>Return to that specific control for re-review</action>
</check>
```

### 10. Interactive CX Design Review

```
<format>
## Client Experience Design

{contributor_name}, now let's walk through each client touchpoint in the target state.

For each touchpoint, I'll explain:
- **What changed** from AS-IS and why
- **Which friction points it resolves** (if any)
- **Impact on CES score**
- **Which "Moments That Matter" it affects**

You'll approve, edit, or brainstorm alternatives for each touchpoint.

**Total Touchpoints to Review:** {{total_touchpoints}} ({{modified_count}} modified, {{new_count}} new, {{eliminated_count}} eliminated)
**Projected CES Improvement:** {{asis_ces}} → {{tobe_ces}} ({{ces_reduction}} reduction)
</format>

<action>
Prepare the touchpoint review queue:
1. Load all AS-IS touchpoints (JT#) from as-is-process-documentation.md
2. Load all friction points (FP#) from CX analysis
3. Load "Moments That Matter" from CX analysis
4. Load transformation decisions (TD#) affecting CX
5. Map each AS-IS touchpoint to its TO-BE disposition
6. Include any NEW touchpoints identified in elicitation
7. Order touchpoints by client journey sequence
</action>
```

### 11. Touchpoint-by-Touchpoint Design Walkthrough

```
<for_each touchpoint in="target_touchpoints" order="sequential">

<format>
---
## Touchpoint {{loop.index}} of {{total_touchpoints}}: {{touchpoint.tobe_name}}

| Reference | Disposition |
|-----------|-------------|
| **TO-BE:** {{touchpoint.tobe_ref}} | {{touchpoint.disposition}} |
| **AS-IS:** {{touchpoint.asis_ref}} | |

---

### 👤 What This Touchpoint Does (TO-BE)

{{touchpoint.tobe_description}}

**Channel:** {{touchpoint.channel}}
**Process Step:** {{touchpoint.process_step}} ({{touchpoint.ts_ref}})
**Client Effort Required:** {{touchpoint.client_effort}}

---

### 🔄 How This Compares to AS-IS

{{#if touchpoint.is_new}}
**This is a NEW touchpoint** - no AS-IS equivalent exists.

**Why we're adding it:** {{touchpoint.new_rationale}}
{{else if touchpoint.is_eliminated}}
**This touchpoint is being ELIMINATED.**

**AS-IS Experience:**
{{touchpoint.asis_description}}

**Why we're removing it:** {{touchpoint.elimination_rationale}}
{{else}}
**Before (AS-IS):**
{{touchpoint.asis_description}}

**After (TO-BE):**
{{touchpoint.tobe_summary}}

**Key Changes:**
{{touchpoint.verbal_differences}}
{{/if}}

---

### 🎯 Why We're Making This Change

**Driving Decision(s):** {{touchpoint.td_refs}}

{{touchpoint.rationale_explanation}}

---

### 😤 Friction Points This Resolves

{{#if touchpoint.resolves_friction}}
| Friction Ref | Friction Description | How This Touchpoint Resolves It | CES Impact |
|--------------|----------------------|--------------------------------|------------|
{{#each touchpoint.friction_resolved}}
| {{this.ref}} | {{this.description}} | {{this.resolution}} | -{{this.ces_reduction}} |
{{/each}}
{{else}}
This touchpoint maintains existing client experience without resolving specific documented friction.
{{/if}}

---

### ⭐ Moments That Matter

{{#if touchpoint.moments_that_matter}}
This touchpoint impacts the following critical moments:

| Moment | Importance | Enhancement |
|--------|------------|-------------|
{{#each touchpoint.moments_that_matter}}
| {{this.moment}} | {{this.importance}} | {{this.enhancement}} |
{{/each}}
{{else}}
This touchpoint doesn't directly impact documented "Moments That Matter."
{{/if}}

---

### 📊 Touchpoint Attributes

| Attribute | AS-IS | TO-BE |
|-----------|-------|-------|
| **Channel** | {{touchpoint.asis_channel}} | {{touchpoint.tobe_channel}} |
| **Trigger** | {{touchpoint.asis_trigger}} | {{touchpoint.tobe_trigger}} |
| **Client Effort** | {{touchpoint.asis_effort}} | {{touchpoint.tobe_effort}} |
| **Wait Time** | {{touchpoint.asis_wait}} | {{touchpoint.tobe_wait}} |
| **Personalization** | {{touchpoint.asis_personalization}} | {{touchpoint.tobe_personalization}} |
| **Self-Service** | {{touchpoint.asis_selfservice}} | {{touchpoint.tobe_selfservice}} |

---

### 📈 CES Impact Analysis

| Metric | Value |
|--------|-------|
| **AS-IS Effort Score** | {{touchpoint.asis_ces_contribution}} |
| **TO-BE Effort Score** | {{touchpoint.tobe_ces_contribution}} |
| **Net CES Improvement** | {{touchpoint.ces_improvement}} |
</format>

<ask response="touchpoint_{{loop.index}}_review">
**Your input on {{touchpoint.tobe_ref}} - {{touchpoint.tobe_name}}:**

- **[A]** Approve - This touchpoint is correct as designed
- **[E]** Edit - I want to modify this touchpoint
- **[B]** Brainstorm - Let's explore alternative approaches
- **[Q]** Question - I have questions before deciding
- **[S]** Skip - Come back to this touchpoint later
</ask>

<check if="response == 'A'">
  <action>
  Mark {{touchpoint.tobe_ref}} as APPROVED.
  </action>

  <!-- 🔴 MANDATORY PERSISTENCE - DO NOT SKIP -->
  <persist critical="true">
    <step n="1" file="{targetStateFile}" section="5.3">
      Add/update touchpoint reconciliation row:
      | {{touchpoint.asis_ref}} | {{touchpoint.asis_name}} | {{touchpoint.disposition}} | {{touchpoint.tobe_ref}} | {{touchpoint.tobe_name}} | {{touchpoint.ces_impact}} |
    </step>

    <step n="2" file="{targetStateFile}" section="5.4" condition="touchpoint.resolves_friction">
      Add friction resolution row(s):
      {{#each touchpoint.friction_resolved}}
      | {{this.friction_ref}} | {{this.description}} | {{this.severity}} | {{this.resolution}} | {{touchpoint.tobe_ref}} | -{{this.ces_reduction}} |
      {{/each}}
    </step>

    <step n="3" file="{targetStateFile}" section="5.5" condition="touchpoint.affects_moments">
      Add/update moments that matter row:
      | {{touchpoint.moment}} | {{touchpoint.tobe_ref}} | {{touchpoint.enhancement}} | {{touchpoint.expected_impact}} |
    </step>

    <step n="4" file="{targetStateFile}" section="5.2">
      Update CES comparison metrics (recalculate totals based on all approved touchpoints)
    </step>

    <step n="5" file="{transformationDataFile}">
      Update JSON:
      touchpoint_reviews[{{touchpoint.tobe_ref}}] = {
        status: "approved",
        timestamp: "{{now}}",
        persisted: true,
        asis_ref: "{{touchpoint.asis_ref}}",
        disposition: "{{touchpoint.disposition}}",
        friction_resolved: {{touchpoint.friction_resolved_array}},
        ces_contribution: {{touchpoint.ces_contribution}},
        ces_improvement: {{touchpoint.ces_improvement}}
      }
    </step>

    <step n="6" file="{gapResolutionFile}" condition="touchpoint.resolves_friction">
      For each friction point resolved by this touchpoint:
      {{#each touchpoint.friction_resolved}}
      Update/add row:
      | {{this.friction_ref}} | CX Analyst | {{this.description}} | Resolved by {{touchpoint.tobe_ref}}: {{this.resolution}} | Resolved | {{now}} |
      {{/each}}
    </step>

    <step n="7" file="{transformationDecisionsFile}" condition="touchpoint.has_td">
      Update TD# entry with touchpoint implementation:
      TD#{{touchpoint.td_ref}} - CX Implementation: {{touchpoint.tobe_ref}}
    </step>
  </persist>

  <!-- 🔴 MANDATORY VALIDATION - DO NOT SKIP -->
  <validate critical="true">
    <check n="1">Read {targetStateFile} section 5.3, confirm {{touchpoint.tobe_ref}} reconciliation row exists</check>
    <check n="2" condition="touchpoint.resolves_friction">Read {targetStateFile} section 5.4, confirm friction resolution rows exist</check>
    <check n="3">Read {transformationDataFile}, confirm touchpoint_reviews[{{touchpoint.tobe_ref}}].persisted == true</check>
    <check n="4" condition="touchpoint.resolves_friction">Read {gapResolutionFile}, confirm friction points marked resolved</check>
    <on_failure>
      HALT - Do not proceed to next touchpoint
      Display error: "⚠️ PERSISTENCE FAILED for {{touchpoint.tobe_ref}} - Retrying write..."
      Retry persist steps
      If retry fails: Ask user to manually verify files
    </on_failure>
  </validate>

  <format>
  ✅ **{{touchpoint.tobe_ref}} Approved & Saved**

  📁 Written to:
  - target-state-documentation.md (Section 5.2, 5.3{{#if touchpoint.resolves_friction}}, 5.4{{/if}}{{#if touchpoint.affects_moments}}, 5.5{{/if}})
  - transformation-data.json
  {{#if touchpoint.resolves_friction}}- gap-resolution-log.md ({{touchpoint.friction_resolved_count}} friction point(s) marked resolved){{/if}}

  **Running CES Total:** {{running_ces_total}} (target: {{target_ces}})

  Moving to next touchpoint...
  </format>
</check>

<check if="response == 'E'">
  <ask response="touchpoint_{{loop.index}}_edit_details">
  What would you like to change about **{{touchpoint.tobe_ref}}**?

  You can modify:
  - Touchpoint name or description
  - Channel or trigger
  - Client effort expectations
  - Personalization approach
  - How it resolves friction

  Please describe your changes:
  </ask>
  <action>
  1. Apply user's requested changes to touchpoint definition
  2. Recalculate CES impact
  3. Update in-memory touchpoint object
  4. Regenerate the touchpoint display with updates
  5. Re-present touchpoint for approval (which will trigger persistence on [A])
  </action>
  <!-- Note: Persistence happens when user approves the edited version -->
</check>

<check if="response == 'B'">
  <format>
  Let's brainstorm alternatives for **{{touchpoint.tobe_ref}}**.

  **Current Approach:** {{touchpoint.tobe_summary}}

  I'll help explore other ways to achieve the same client experience goals.
  </format>
  <action>
  Execute {advancedElicitationTask} focused on this specific touchpoint:
  - Present 2-3 alternative touchpoint designs
  - Compare trade-offs (client effort, implementation cost, personalization, channel preferences)
  - Get user selection
  - Update touchpoint definition based on selection
  - Re-present touchpoint for approval
  </action>
</check>

<check if="response == 'Q'">
  <ask response="touchpoint_{{loop.index}}_question">
  What questions do you have about **{{touchpoint.tobe_ref}}**?
  </ask>
  <action>
  Answer user's question thoroughly, drawing on:
  - AS-IS touchpoint documentation
  - CX analysis and friction points
  - Client journey mapping
  - Transformation decisions (TD#)
  Then re-present the review options for this touchpoint.
  </action>
</check>

<check if="response == 'S'">
  <action>
  Mark {{touchpoint.tobe_ref}} as SKIPPED for later review.
  Record in transformation-data.json: touchpoint_reviews[{{touchpoint.tobe_ref}}] = { status: "skipped", timestamp: now }
  </action>
  <format>
  ⏭️ **{{touchpoint.tobe_ref}} Skipped** - We'll return to this touchpoint after reviewing the others.
  </format>
</check>

</for_each>
```

### 12. Review Skipped Touchpoints

```
<check if="skipped_touchpoints.count > 0">
<format>
---
## Returning to Skipped Touchpoints

You skipped {{skipped_touchpoints.count}} touchpoint(s) during the initial review. Let's revisit them now:

{{#each skipped_touchpoints}}
{{loop.index}}. {{this.tobe_ref}} - {{this.tobe_name}}
{{/each}}
</format>

<for_each touchpoint in="skipped_touchpoints">
  <action>Re-present touchpoint using the same format from Section 11</action>
  <action>User MUST select A, E, B, or Q (Skip not available on second pass)</action>
</for_each>
</check>

<check if="skipped_touchpoints.count == 0">
<format>
All touchpoints reviewed on first pass - no skipped touchpoints to revisit.
</format>
</check>
```

### 13. CX Design Summary

```
<format>
---
## Client Experience Design Complete

All {{total_touchpoints}} touchpoints have been reviewed:

| Status | Count |
|--------|-------|
| ✅ Approved | {{approved_count}} |
| ✏️ Edited | {{edited_count}} |
| 💡 Brainstormed | {{brainstormed_count}} |

### Touchpoint Disposition Summary

| Disposition | Count | % |
|-------------|-------|---|
| Unchanged | {{unchanged_count}} | {{unchanged_pct}}% |
| Modified | {{modified_count}} | {{modified_pct}}% |
| Eliminated | {{eliminated_count}} | {{eliminated_pct}}% |
| New | {{new_count}} | {{new_pct}}% |

### CES Improvement Summary

| Metric | AS-IS | TO-BE | Improvement |
|--------|-------|-------|-------------|
| **Total CES Score** | {{asis_ces}} | {{tobe_ces}} | {{ces_improvement}} ({{ces_pct}}%) |
| **Friction Points** | {{asis_friction_count}} | {{tobe_friction_count}} | {{friction_resolved}} resolved |
| **Self-Service Touchpoints** | {{asis_selfservice_count}} | {{tobe_selfservice_count}} | +{{selfservice_added}} |
| **Avg Client Effort** | {{asis_avg_effort}} | {{tobe_avg_effort}} | {{effort_reduction}} reduction |

### Friction Resolution Summary

| Status | Count |
|--------|-------|
| Friction Points Identified (AS-IS) | {{total_friction}} |
| Friction Points Resolved (TO-BE) | {{friction_resolved}} |
| Friction Points Remaining | {{friction_remaining}} |
| Resolution Rate | {{friction_resolution_pct}}% |

{{#if friction_remaining > 0}}
⚠️ **Outstanding Friction Points:**
{{#each outstanding_friction}}
- {{this.ref}}: {{this.description}} - {{this.mitigation_plan}}
{{/each}}
{{/if}}

### Final Touchpoint Reconciliation Table

| AS-IS Ref | AS-IS Touchpoint | → | TO-BE Ref | TO-BE Touchpoint | Disposition | Friction Resolved | Status |
|-----------|------------------|---|-----------|------------------|-------------|-------------------|--------|
{{#each all_touchpoints}}
| {{this.asis_ref}} | {{this.asis_name}} | → | {{this.tobe_ref}} | {{this.tobe_name}} | {{this.disposition}} | {{this.friction_resolved}} | {{this.review_status}} |
{{/each}}

### Moments That Matter Enhancement

| Moment | AS-IS Experience | TO-BE Experience | Enhancement |
|--------|------------------|------------------|-------------|
{{#each moments_that_matter}}
| {{this.moment}} | {{this.asis_experience}} | {{this.tobe_experience}} | {{this.enhancement}} |
{{/each}}
</format>

<ask response="cx_design_complete">
CX design is complete. Ready to proceed?

- **[Y]** Yes - Continue to Innovation Integration
- **[R]** Review - Go back to a specific touchpoint
</ask>

<check if="response == 'R'">
  <ask response="review_which_touchpoint">
  Which touchpoint would you like to review? Enter the TO-BE reference (e.g., TJ-ONB-001):
  </ask>
  <action>Return to that specific touchpoint for re-review</action>
</check>
```

### 14. Document Innovation Integration

```
<format>
## Innovation Integration Summary

{contributor_name}, here's how the innovations from our brainstorming integrate into the target state.
</format>

<action>
Compile innovation integration from step reviews:
1. List all innovations (II#) from transformation-data.json
2. Map each to its integration points (TS#, TC#, TJ#)
3. Identify which were already reviewed inline with steps/controls/touchpoints
4. Present summary for confirmation
</action>

<format>
### Integrated Innovations

These innovations have been incorporated into the target state design:

| II# | Innovation | Priority | Integration Points | Status |
|-----|------------|----------|--------------------|--------|
{{#each integrated_innovations}}
| {{this.ref}} | {{this.name}} | {{this.priority}} | {{this.integration_points}} | Reviewed in {{this.review_context}} |
{{/each}}

### MUST HAVE Verification

All MUST HAVE innovations should be included. Let's verify:

| II# | Innovation | Included | Integration Evidence |
|-----|------------|----------|---------------------|
{{#each must_have_innovations}}
| {{this.ref}} | {{this.name}} | {{this.included}} | {{this.evidence}} |
{{/each}}

{{#if missing_must_haves}}
⚠️ **Warning:** The following MUST HAVE innovations are NOT integrated:
{{#each missing_must_haves}}
- {{this.ref}}: {{this.name}} - {{this.reason}}
{{/each}}
{{/if}}

### Deferred Innovations

These innovations were discussed but deferred for future phases:

| II# | Innovation | Reason for Deferral | Future Consideration |
|-----|------------|---------------------|----------------------|
{{#each deferred_innovations}}
| {{this.ref}} | {{this.name}} | {{this.deferral_reason}} | {{this.future_notes}} |
{{/each}}
</format>

<ask response="innovation_review">
Is the innovation integration accurate?

- **[Y]** Yes - Continue
- **[A]** Add - Include an additional innovation
- **[R]** Remove - Remove an innovation from scope
</ask>

<check if="response == 'A'">
  <ask response="add_innovation">
  Which innovation would you like to add? Provide:
  - Innovation name
  - Integration point (which TS#, TC#, or TJ#)
  - Priority (MUST HAVE, SHOULD HAVE, COULD HAVE)
  </ask>
  <action>Add innovation, update transformation-data.json, redisplay summary</action>
</check>

<check if="response == 'R'">
  <ask response="remove_innovation">
  Which innovation (II#) would you like to remove or defer?
  </ask>
  <action>Move to deferred list with reason, update transformation-data.json, redisplay summary</action>
</check>
```

### 15. Compile Transformation Metrics

```
<format>
## Transformation Metrics Dashboard

{contributor_name}, here's the consolidated view of what this transformation achieves.
</format>

<action>
Calculate all metrics from the reviewed designs:
1. Count steps by change type
2. Calculate control gap closure rate
3. Calculate CES improvement
4. Sum automation improvements
5. Compile innovation count
</action>

<format>
### Transformation Metrics at a Glance

| Metric | AS-IS | TO-BE | Change | Improvement |
|--------|-------|-------|--------|-------------|
| **Process Steps** | {{asis_steps}} | {{tobe_steps}} | {{steps_delta}} | {{steps_pct}}% |
| **Control Gaps** | {{asis_gaps}} | {{tobe_gaps}} | -{{gaps_closed}} | {{gaps_pct}}% closed |
| **Pain Points Addressed** | {{asis_pain}} | {{tobe_pain}} | -{{pain_resolved}} | {{pain_pct}}% resolved |
| **CES Score** | {{asis_ces}} | {{tobe_ces}} | -{{ces_delta}} | {{ces_pct}}% reduction |
| **Automation Level** | {{asis_auto}}% | {{tobe_auto}}% | +{{auto_delta}}% | - |
| **Innovations Integrated** | 0 | {{innovations_count}} | +{{innovations_count}} | - |

### Design Review Summary

| Domain | Items Reviewed | Approved | Edited | Brainstormed |
|--------|----------------|----------|--------|--------------|
| Process Steps | {{ts_count}} | {{ts_approved}} | {{ts_edited}} | {{ts_brainstormed}} |
| Controls | {{tc_count}} | {{tc_approved}} | {{tc_edited}} | {{tc_brainstormed}} |
| Touchpoints | {{tj_count}} | {{tj_approved}} | {{tj_edited}} | {{tj_brainstormed}} |

### Outstanding Items

{{#if any_outstanding}}
⚠️ **Items requiring attention:**
{{#each outstanding_items}}
- {{this.type}}: {{this.ref}} - {{this.description}}
{{/each}}
{{else}}
✅ All items reviewed and approved - no outstanding issues.
{{/if}}
</format>
```

### 16. Review Complete Documentation

```
<format>
## Documentation Summary

I've captured the following in target-state-documentation.md:

| Section | Content | References |
|---------|---------|------------|
| Executive Summary | Metrics comparison, validation status | - |
| Transformation Overview | Scope, objectives | TD# |
| AS-IS to TO-BE Reconciliation | Full mapping tables | PS#→TS# |
| TO-BE Process Design | {{ts_count}} target steps | TS# |
| Control Design | {{tc_count}} target controls | TC# |
| CX Design | {{tj_count}} target touchpoints | TJ# |
| Innovation Integration | {{innovations_count}} innovations | II# |
| Transformation Decisions | {{td_count}} decisions | TD# |

**Reference Summary:**
- TS# (Target Steps): {{ts_count}}
- TC# (Target Controls): {{tc_count}}
- TJ# (Target Touchpoints): {{tj_count}}
- TD# (Transformation Decisions): {{td_count}}
- II# (Integrated Innovations): {{ii_count}}
</format>

<ask response="documentation_review">
Would you like to review any section before moving to validation?

- **[1]** Review Process Design ({{ts_count}} steps)
- **[2]** Review Control Design ({{tc_count}} controls)
- **[3]** Review CX Design ({{tj_count}} touchpoints)
- **[4]** Review Innovation Integration ({{ii_count}} innovations)
- **[5]** Review Full Document
- **[C]** Continue to Validation
</ask>

<check if="documentation_review == '1'">
  <action>Navigate back to Section 5 (Process Step Reconciliation Summary)</action>
  <action>Allow user to select specific step to re-review</action>
</check>

<check if="documentation_review == '2'">
  <action>Navigate back to Section 9 (Control Design Summary)</action>
  <action>Allow user to select specific control to re-review</action>
</check>

<check if="documentation_review == '3'">
  <action>Navigate back to Section 13 (CX Design Summary)</action>
  <action>Allow user to select specific touchpoint to re-review</action>
</check>

<check if="documentation_review == '4'">
  <action>Navigate back to Section 14 (Innovation Integration)</action>
</check>

<check if="documentation_review == '5'">
  <action>Display full target-state-documentation.md for review</action>
  <ask response="full_doc_feedback">
  Any changes needed?
  - **[Y]** Yes - Tell me what to change
  - **[N]** No - Continue
  </ask>
</check>
```

### 17. Present Menu Options

```
<format>
---
## Progress: Step 4 of 7 - TO-BE Documentation Complete

✅ Process steps designed and reviewed ({{ts_count}} TS#)
✅ Controls designed and reviewed ({{tc_count}} TC#)
✅ Client touchpoints designed and reviewed ({{tj_count}} TJ#)
✅ Innovations integrated ({{ii_count}} II#)
✅ Transformation metrics compiled

**Ready for Validation**

Next, specialist agents will validate this target state against their original AS-IS analyses to ensure nothing was missed.

---

**Select an Option:**
- **[A]** Advanced Elicitation - Deep dive on specific sections
- **[P]** Party Mode - Preview what specialists will check
- **[C]** Continue - Proceed to sub-agent validation
</format>
```

#### Menu Handling Logic:

- IF A: Execute {advancedElicitationTask}
- IF P: Execute {partyModeWorkflow}
- IF C: Update {transformationDataFile}, then load, read entire file, then execute {nextStepFile}
- IF other: Address query, then redisplay menu

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'
- After other menu items execution completes, redisplay the menu
- User can chat or ask questions - always respond, then redisplay the menu

---

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN [C continue option] is selected and [TO-BE documentation is complete], will you then load and read fully `{nextStepFile}` to execute and begin sub-agent validation.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:
- **Interactive Review Completed:**
  - Each process step (TS#) presented individually with verbal explanation
  - Each control (TC#) presented individually with gap closure context
  - Each touchpoint (TJ#) presented individually with friction/CES context
  - User approved, edited, or brainstormed each element
- **Traceability Maintained:**
  - Every TO-BE element traces to AS-IS source (or marked NEW)
  - Change types applied consistently
  - Problems addressed (gaps, pain points, friction) documented per element
  - Innovations mapped to integration points
- **User Engagement:**
  - User had opportunity to approve/edit/brainstorm/question/skip each element
  - Skipped items were revisited before completion
  - Questions answered thoroughly before proceeding
- **🔴 PERSISTENCE EXECUTED (CRITICAL):**
  - After EVERY approved element, data written to output files
  - target-state-documentation.md updated with element details
  - transformation-data.json updated with persisted: true flag
  - gap-resolution-log.md updated when gaps/friction resolved
  - transformation-decisions-detail.md updated when TD# involved
  - Write validation performed after each persist operation
  - User shown confirmation of what was saved and where
- **Documentation Generated:**
  - target-state-documentation.md fully populated
  - transformation-data.json updated with review status
  - gap-resolution-log.md tracks all resolved gaps
  - transformation-decisions-detail.md tracks all TD# implementations
  - Reconciliation summaries compiled
  - Metrics dashboard calculated

### ❌ SYSTEM FAILURE:
- **🔴 PERSISTENCE FAILURES (CRITICAL):**
  - Approving an element WITHOUT immediately writing to output files
  - Batching writes (waiting until end to persist)
  - Not validating that writes succeeded
  - Proceeding to next element when persistence failed
  - Output files missing approved element data
  - transformation-data.json missing persisted: true flag
  - Session could not be recovered from output files if interrupted
- **Interactive Review Failures:**
  - Presenting bulk tables without interactive per-element review
  - Skipping verbal explanation of changes and rationale
  - Not showing which problems (gaps/pain points/friction) each element addresses
  - Auto-approving elements without user input
  - Proceeding past elements without user selection (A/E/B/Q/S)
  - Not revisiting skipped elements
- **Traceability Failures:**
  - TO-BE elements without AS-IS traceability
  - Missing change type classifications
  - Inconsistent reference numbering
  - New decisions made without SME confirmation

**Master Rule #1:** Each element MUST be presented individually with context and require user input before proceeding. Bulk presentations or auto-advancing is FORBIDDEN and constitutes SYSTEM FAILURE.

**Master Rule #2:** After EVERY approved/edited element, you MUST persist to output files AND validate the write succeeded BEFORE proceeding to the next element. Batching writes or skipping persistence is FORBIDDEN and constitutes SYSTEM FAILURE. If persistence fails, HALT and retry - never proceed with unpersisted data.
