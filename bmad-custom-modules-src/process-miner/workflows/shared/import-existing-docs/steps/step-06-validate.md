---
name: 'step-06-validate'
description: 'Present extracted data to SME for review and validation'

# Path Definitions
workflow_path: '{module_root}/workflows/shared/import-existing-docs'
module_path: '{module_root}'
config_source: '{module_root}/config.yaml'

# File References
thisStepFile: '{workflow_path}/steps/step-06-validate.md'
nextStepFile: '{workflow_path}/steps/step-07-handoff.md'
previousStepFile: '{workflow_path}/steps/step-05-output.md'
workflowFile: '{workflow_path}/workflow.md'

# Output Configuration
output_file: '{current_process_folder}/imported-data.json'
gap_analysis_file: '{current_process_folder}/gap-analysis.md'

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
partyModeWorkflow: '{project-root}/.bmad/core/workflows/party-mode/workflow.md'
---

# Step 6: SME Review & Validation

## STEP GOAL:

To present extracted data to the Subject Matter Expert (SME) for validation, collect feedback, and apply corrections.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 **NEVER** generate content without user input
- 📖 **CRITICAL**: Read the complete step file before taking any action
- 🔄 **CRITICAL**: When loading next step with 'C', ensure entire file is read
- 📋 **YOU ARE A FACILITATOR**, not a content generator

### Role Reinforcement:

- ✅ You are a documentation analyst facilitating SME review
- ✅ Present data clearly and allow SME to validate/correct
- ✅ Update confidence scores based on SME feedback
- ✅ Apply corrections to the output file

### Step-Specific Rules:

- 🎯 Focus ONLY on validation and correction
- 🚫 **FORBIDDEN** to perform handoff in this step (that's step 7)
- 💬 Be patient and thorough during review
- 📋 Track all changes made during validation

## EXECUTION PROTOCOLS:

- 🎯 Present extracted data section by section
- 💾 Collect SME feedback on accuracy
- 📖 Apply corrections and update confidence scores
- 💾 Update output_file with validated data
- 🚫 **FORBIDDEN** to load next step until validation is complete

## CONTEXT BOUNDARIES:

- JSON output from step 5 is available
- Gap analysis from step 4 is available
- SME is the authority on accuracy
- Changes should be tracked for audit

---

## VALIDATION SEQUENCE:

### 1. Introduction to Validation

Present to SME:

"I've extracted structured data from your documentation. Let's review the key findings to ensure accuracy.

This review will cover:
1. Process Steps ({step_count} identified)
2. Pain Points ({pain_count} identified)
3. Controls ({control_count} identified)
4. Systems ({system_count} identified)
5. Gaps and Conflicts

For each section, you can approve, request adjustments, or flag issues."

### 2. Validate Process Steps

Display process steps with confidence scores:

**Process Steps ({step_count} identified):**

| ID | Name | Confidence | Source |
|----|------|------------|--------|
{display_steps_table}

Ask: "Are these process steps accurate?
- [Y] Yes, all correct
- [A] Adjustments needed (let's review together)
- [N] Major issues (needs significant revision)"

#### Handle Responses:

**If Y**: Mark all steps as SME-validated, update confidence to "validated"

**If A**:
- Ask which specific steps need adjustment
- For each flagged step, ask what the correction should be
- Apply corrections to the data
- Update confidence scores

**If N**:
- Review each step individually with SME
- Apply corrections as directed
- Consider if fresh elicitation would be more efficient

### 3. Validate Pain Points

Display pain points:

**Pain Points ({pain_count} identified):**
{display_pain_points}

**If pain_count = 0:**
Ask: "No pain points were found in the source documentation.
- [Y] Confirm none identified (will be captured as part of the detailed process review later)"

**If pain_count > 0:**
Ask: "Are these pain points accurate?
- [Y] Yes, accurate
- [R] Remove incorrect items
- [E] Edit existing items"

Handle removals and edits as directed.

### 4. Validate Controls

Display controls:

**Controls ({control_count} identified):**
{display_controls}

**If control_count = 0:**
Ask: "No controls were found in the source documentation.
- [Y] Confirm none identified (will be captured as part of the detailed process review later)"

**If control_count > 0:**
Ask: "Are these controls accurate?
- [Y] Yes, accurate
- [R] Remove incorrect items
- [E] Edit existing items"

Handle removals and edits as directed.

### 5. Validate Systems

Display systems:

**Systems ({system_count} identified):**
{display_systems}

**If system_count = 0:**
Ask: "No systems were found in the source documentation.
- [Y] Confirm none identified (will be captured as part of the detailed process review later)"

**If system_count > 0:**
Ask: "Are these systems accurate?
- [Y] Yes, accurate
- [R] Remove incorrect items
- [E] Edit existing items"

Handle removals and edits as directed.

### 6. Review Gap Analysis

Display gap summary:

**Gap Analysis - What's Missing:**
{display_gap_summary}

**Key Areas for Refinement:**
{display_gap_clarification_items}

Inform user: "These gaps will be addressed through the further development of the As-Is process documentation."

Proceed to next section.

### 7. Update Output File

After all validation:
- Apply all corrections to the JSON data
- Update confidence scores for validated items
- Add validation metadata (validator, date, changes made)
- Save updated file to `{output_file}`

### 8. Display Validation Summary

Show:

**Validation Complete!**

**Changes Made:**
- Steps validated: {validated_steps}/{total_steps}
- Steps corrected: {corrected_steps}
- Pain points validated: {validated_pains}
- Controls validated: {validated_controls}
- Systems validated: {validated_systems}

**Updated Data saved to:**
`{output_file}`

---

## STEP COMPLETION

After displaying the Validation Summary, automatically proceed to load, read entire file, then execute `{nextStepFile}` for handoff.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- All data sections presented to SME
- SME feedback collected and applied
- Corrections made accurately
- Confidence scores updated
- Output file updated with validated data

### ❌ FAILURE:

- Skipping validation sections
- Not applying SME corrections
- Not updating confidence scores
- Not saving validated data
- Making assumptions instead of asking SME

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
