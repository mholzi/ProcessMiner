---
name: 'step-07-handoff'
description: 'Prepare data for downstream workflows and complete import process'

# Workflow Parameters (passed from calling workflow)
# return_mode: 'continue_elicitation' | 'standalone' (default)
#   - continue_elicitation: Auto-return to calling workflow (e.g., start-new-process)
#   - standalone: Show [M]/[E] menu for user choice

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/shared/import-existing-docs'
config_source: '{module_root}/config.yaml'

# File References
thisStepFile: '{workflow_path}/steps/step-07-handoff.md'
previousStepFile: '{workflow_path}/steps/step-06-validate.md'
workflowFile: '{workflow_path}/workflow.md'

# Related Workflows
startNewProcessWorkflow: '{module_root}/workflows/start-new-process/workflow.md'

# Output Configuration
source_documents_folder: '{current_process_folder}/source-documentation'
output_file: '{current_process_folder}/imported-data.json'
gap_analysis_file: '{current_process_folder}/gap-analysis.md'

# Documentation Templates
templates_folder: '{module_root}/templates'
as_is_template: '{templates_folder}/as-is-process-documentation.md'
pain_points_template: '{templates_folder}/pain-points-detail.md'
exceptions_template: '{templates_folder}/exceptions-detail.md'
control_points_template: '{templates_folder}/control-points-detail.md'

# Output Documentation Files
as_is_output: '{current_process_folder}/as-is-process-documentation.md'
pain_points_output: '{current_process_folder}/pain-points-detail.md'
exceptions_output: '{current_process_folder}/exceptions-detail.md'
control_points_output: '{current_process_folder}/control-points-detail.md'

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
partyModeWorkflow: '{project-root}/.bmad/core/workflows/party-mode/workflow.md'
---

# Step 7: Integration & Handoff

## STEP GOAL:

To prepare imported data for use in downstream workflows and provide clear guidance on next steps based on SME's gap resolution choice.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 **NEVER** generate content without user input
- 📖 **CRITICAL**: Read the complete step file before taking any action
- 🔄 **CRITICAL**: This is the final step - provide clear closure and options
- 📋 **YOU ARE A FACILITATOR**, not a content generator

### Role Reinforcement:

- ✅ You are a documentation analyst completing the import process
- ✅ Provide clear summary of what was accomplished
- ✅ Guide user to appropriate next workflow based on their choice
- ✅ Ensure smooth handoff to downstream processes

### Step-Specific Rules:

- 🎯 Focus ONLY on handoff and closure
- 💬 Provide clear options based on gap_choice from step 6
- 🚫 Do not start new processes - just prepare for handoff
- 📋 Ensure all files are saved and accessible

## EXECUTION PROTOCOLS:

- 🎯 Review gap_choice from validation step
- 💾 Prepare appropriate handoff based on choice
- 📖 Provide clear summary and next steps
- ⏸️ This is the FINAL step of this workflow

## CONTEXT BOUNDARIES:

- Validated data from step 6 is available
- gap_choice determines the handoff path
- Output files should be finalized
- User may exit or continue to another workflow

---

## HANDOFF SEQUENCE:

### 1. Populate Documentation Templates

Before handling the gap choice, generate the human-readable documentation from extracted data.

#### 1.1 Load Templates

Load the four documentation templates:
- `{as_is_template}` - Main process documentation
- `{pain_points_template}` - Pain point detail analysis
- `{exceptions_template}` - Exception detail analysis
- `{control_points_template}` - Control point detail analysis

#### 1.2 Populate Templates with Extracted Data

For each template, fill in placeholders using validated data from `{output_file}`:

**Confidence Indicators:**
- Data with HIGH confidence -> Display value normally
- Data with MEDIUM confidence -> Display value with `[MEDIUM]` marker
- Data with LOW confidence -> Display value with `[LOW - Needs Verification]` marker
- Missing data -> Display `[REQUIRES SME INPUT]` placeholder

**Population Rules:**
- Process metadata -> Fill in as-is-process-documentation.md header and Section 1
- Process steps -> Fill in Section 2 (steps summary table and details)
- Controls -> Fill in Section 4 summary AND control-points-detail.md full entries
- Systems -> Fill in Section 5 (systems summary table)
- Pain points -> Fill in Section 9 summary AND pain-points-detail.md full entries
- Exceptions -> Fill in Section 3 summary AND exceptions-detail.md full entries
- Gaps -> Fill in Section 8 (identified gaps, missing documentation)

**For each detailed companion document:**
- Fill sections with extracted items
- Include all source references
- Include confidence scores
- Mark incomplete fields as `[REQUIRES SME INPUT]`

#### 1.3 Save Documentation Files

Save populated templates to the process folder:
- `{as_is_output}`
- `{pain_points_output}`
- `{exceptions_output}`
- `{control_points_output}`

These files are now ready for:
- Immediate review by the user
- Completion via start-new-process workflow
- Downstream agent consumption

---

### 2. Review Gap Choice

From step 6 validation, the SME chose one of:
- **[F] Fill gaps now** - Transition to start-new-process workflow
- **[L] Fill gaps later** - Save state for future continuation
- **[U] Use as-is** - Accept incomplete data

### 3. Handle Each Choice

#### IF SME chose "Fill gaps now" [F]:

Prepare for transition to start-new-process workflow:

**Actions:**
- Set workflow to "gap-filling mode" - only ask about missing/unclear items
- Pre-populate session_state with extracted data
- Pass extracted_data to start-new-process workflow

**Display:**
"Transitioning to knowledge elicitation workflow...

I'll only ask about the {gap_count} missing or unclear items.
This should take about {estimated_time} minutes.

**Items to discuss:**
{list_gap_items}

Ready to begin gap-filling?"

**Options:**
- [Y] Yes, begin gap-filling now
- [N] No, save for later instead

**If Y**: Provide instructions to invoke start-new-process workflow
**If N**: Treat as "Fill gaps later" choice

#### IF SME chose "Fill gaps later" [L]:

Save current state with gap analysis:

**Actions:**
- Ensure all files are saved
- Create resume token/notes for easy continuation
- Document what was completed and what remains

**Display:**
"Data saved successfully.

**To resume gap-filling later:**
- Use menu: 'Continue Existing Session'
- Provide process name: {process_name}
- Or run start-new-process workflow with this process folder

**Current Status:**
- {extracted_count} elements captured
- {gap_count} gaps remain
- Completeness: {completeness_score}%

**Files saved:**
- Extracted data: `{output_file}`
- Gap analysis: `{gap_analysis_file}`
- Source documents: `{source_documents_folder}/`
- Documentation: `{as_is_output}` (+ companion detail docs)"

#### IF SME chose "Use as-is" [U]:

Accept incomplete data with warnings:

**Actions:**
- Mark extracted_data as "review required" status
- Update output file with incomplete flag
- Provide clear documentation of gaps and limitations

**Display:**
"Data accepted as-is.

**Note:** Documentation is incomplete.
Completeness score: {completeness_score}%

**Missing elements may affect downstream analysis quality:**
{list_missing_elements}

Downstream agents will flag missing data when referenced.

**Files saved:**
- Extracted data: `{output_file}` (marked as incomplete)
- Gap analysis: `{gap_analysis_file}`
- Source documents: `{source_documents_folder}/`
- Documentation: `{as_is_output}` (+ companion detail docs, marked incomplete)"

### 4. Final Summary

Display comprehensive import completion summary:

**Import Workflow Complete!**

**Process:** {process_name}
**Date:** {date}
**Processed by:** {user_name}

**Source Documents:**
- {source_doc_count} document(s) imported
- Stored in: `{source_documents_folder}/`

**Extraction Results:**
- Process steps: {step_count}
- Pain points: {pain_count}
- Controls: {control_count}
- Systems: {system_count}
- Completeness: {completeness_score}%

**Output Files:**
- `{output_file}` (structured data)
- `{gap_analysis_file}` (gap report)
- `{as_is_output}` (main documentation)
- `{pain_points_output}` (pain point details)
- `{exceptions_output}` (exception details)
- `{control_points_output}` (control point details)

**Status:** {final_status}

**Next Steps:**
{recommended_next_steps_based_on_choice}

---

## WORKFLOW COMPLETION

### Check for Calling Workflow

**IF `return_mode` parameter exists (workflow was invoked from another workflow):**

Handle based on return_mode value:

#### IF return_mode == 'continue_elicitation':

The import workflow was called from start-new-process workflow. Return control automatically:

Display:
```
---
**Documentation Import Complete**

Extracted data and gap analysis have been loaded.
We'll now continue with the process documentation.
---
```

**Action:** Return control to the calling workflow. The calling workflow will:
- Load extracted data from `{output_file}`
- Load gap analysis from `{gap_analysis_file}`
- Set `documents_uploaded = true`
- Continue to its next step

**Do NOT display menu options.** Auto-return to calling workflow.

#### IF return_mode == 'standalone' OR return_mode is not set:

Display: "**Import Complete.** [M] Return to Main Menu [E] Exit Workflow"

### EXECUTION RULES (standalone mode only):

- ALWAYS halt and wait for user input after presenting menu
- This is the final step - workflow ends here
- User chooses to return to agent menu or exit

### Menu Handling Logic (standalone mode only):

- **IF M**: Return control to the calling agent's main menu
- **IF E**: End the workflow session
- **IF Any other comments or queries**: Help user respond then redisplay menu

## CRITICAL STEP COMPLETION NOTE

- **If called from another workflow (return_mode set):** Return control automatically after displaying completion message
- **If standalone:** When user selects [M] or [E], the workflow is complete

All files have been saved and are accessible for downstream workflows.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Documentation templates populated with extracted data
- Confidence indicators applied correctly
- Missing data marked as `[REQUIRES SME INPUT]`
- All four documentation files saved to process folder
- All files saved and accessible
- Clear summary provided
- **If return_mode set:** Auto-return to calling workflow without menu
- **If standalone:** Present [M]/[E] menu and handle user choice
- Smooth handoff to calling workflow (if applicable)

### ❌ FAILURE:

- Not populating documentation templates
- Missing confidence indicators on uncertain data
- Not marking missing fields appropriately
- Not saving documentation files
- Files not saved properly
- Unclear or missing summary
- **Showing [M]/[E] menu when return_mode is set** (should auto-return)
- **Not returning to calling workflow when return_mode == 'continue_elicitation'**

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
