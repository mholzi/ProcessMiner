---
name: 'step-03-route'
description: 'Analyze process progress and route to appropriate step in the target workflow based on calling agent'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/shared/continue-session'

# File References
thisStepFile: '{workflow_path}/steps/step-03-route.md'
workflowFile: '{workflow_path}/workflow.md'

# Target Workflows (resolved based on calling_agent_id)
workflows:
  process-documentation-analyst:
    workflow: '{module_root}/workflows/start-new-process/workflow.md'
    output_file: 'structured-data.json'
    total_steps: 9
    type: 'process-documentation'
    display_name: 'Process Documentation (start-new-process)'
  innovation-analyst:
    workflow: '{module_root}/workflows/innovation-analysis/workflow.md'
    output_file: 'innovation-analysis.md'
    total_steps: 5
    type: 'innovation-analysis'
    display_name: 'Innovation Analysis'
  client-journey-analyst:
    workflow: '{module_root}/workflows/cx-journey-analysis/workflow.md'
    output_file: 'cx-journey-documentation.md'
    total_steps: 8
    type: 'cx-journey'
    display_name: 'CX Journey Analysis'
  control-analyst:
    workflow: '{module_root}/workflows/control-compliance-analysis/workflow.md'
    output_file: 'compliance-control-assessment.md'
    total_steps: 10
    type: 'control-compliance'
    display_name: 'Control & Compliance Analysis'
---

# Step 3: Progress Analysis and Routing

## STEP GOAL:

Analyze the selected process's documentation to determine which step to resume at, then route the user to the appropriate step in the **target workflow based on calling_agent_id**.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- NEVER guess completion status - analyze actual files
- CRITICAL: Read the complete step file before taking any action
- YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:

- You are a session continuity specialist
- If you already have been given communication or persona patterns, continue to use those
- We engage in collaborative dialogue, not command-response
- You bring systematic analysis, user brings process knowledge

### Step-Specific Rules:

- Focus on accurate progress analysis
- FORBIDDEN to assume completion without file verification
- Show clear progress summary before routing
- WAIT for user confirmation before routing
- **Use calling_agent_id to determine which workflow and checklist to use**

## EXECUTION PROTOCOLS:

- Identify target workflow from calling_agent_id
- Load and analyze process files appropriate for that workflow
- Determine accurate completion status for each step
- Calculate correct start_at_step value
- Do NOT route without showing progress summary

## CONTEXT BOUNDARIES:

- Session variables set: `{current_process_id}`, `{current_process_name}`, `{current_process_folder}`, `{calling_agent_id}`
- **Folder naming convention**: `{output_folder}/processes/{ID} - {Name}` (e.g., `output/processes/P001 - Onboarding`)
- This step determines which workflow step to resume from

---

## Sequence of Instructions

### 0. Validate Calling Agent

**Check calling_agent_id is set:**

If `{calling_agent_id}` is NOT set or empty:
```
Error: Unable to determine which workflow to resume.

The calling agent was not identified. This may indicate a configuration issue.
Please return to the agent menu and try again.
```
**Exit this workflow.**

**Resolve target workflow configuration:**

Based on `{calling_agent_id}`, set:
- `{target_workflow}` = workflow path
- `{target_output_file}` = primary output file to check
- `{total_steps}` = number of steps in target workflow
- `{workflow_display_name}` = human-readable workflow name

### 1. Load Process Files

Load files from `{current_process_folder}` based on workflow type:

**For process-documentation-analyst:**
1. `structured-data.json` - Primary source for completion indicators
2. `as-is-process-documentation.md` - Secondary verification

**For innovation-analyst:**
1. `innovation-analysis.md` - Primary output document (check frontmatter for stepsCompleted)
2. `structured-data.json` - Prerequisite verification

**For client-journey-analyst:**
1. `cx-journey-documentation.md` - Primary output document (check frontmatter for stepsCompleted)
2. `structured-data.json` - Prerequisite verification

**For control-analyst:**
1. `compliance-control-assessment.md` - Primary output document (check frontmatter for stepsCompleted)
2. `structured-data.json` - Prerequisite verification

**If process folder does not exist:**
```
Error: Process folder not found for {current_process_id}

The process may have been moved or deleted.
Please check the registry or use the appropriate menu option to start a new session.
```
**Exit this workflow.**

**If primary output file does not exist (for secondary agents):**
```
No existing {workflow_display_name} session found for {current_process_name}.

This process does not have a {target_output_file} file yet.
Would you like to start a new {workflow_display_name} session instead? [Y/N]
```
Wait for user input. If Y, set `{start_at_step}` = 1.

**If files are corrupted or unreadable:**
```
Warning: Unable to read data files for {current_process_id}

Defaulting to Step 1 to ensure no data is lost.
Would you like to continue from Step 1? [Y/N]
```
Wait for user input. If Y, set `{start_at_step}` = 1.

### 2. Analyze Completion Status

Use the appropriate checklist based on `{calling_agent_id}`:

---

#### CHECKLIST: process-documentation-analyst (9 Steps)

Examine `structured-data.json`:

| Step | Check For | Completion Indicator |
|------|-----------|---------------------|
| 1 | Session initialized | `metadata.contributor_name` and `metadata.contributor_role` populated |
| 2 | Documents checked | `metadata.documents_uploaded` flag present (true or false) |
| 3 | Overview complete | `metadata.purpose`, `metadata.trigger`, `metadata.frequency`, `metadata.volume` all populated |
| 4 | Steps complete | `process_steps[]` array has entries with PS# IDs |
| 5 | Exceptions complete | `exceptions[]` array populated with EX# IDs (or `exceptions_na: true`) |
| 6 | Pain points complete | `pain_points[]` array populated with PP# IDs (or `pain_points_na: true`) |
| 7 | Controls complete | `controls[]` array populated with CP# IDs |
| 8 | Systems complete | `systems[]` array populated with SYS# IDs |
| 9 | Review complete | `completion_timestamp` present in structured-data.json |

**Step Names for Display:**
1. Session Setup
2. Document Review
3. Process Overview
4. Process Steps
5. Exceptions
6. Pain Points
7. Control Points
8. Systems
9. Final Review

---

#### CHECKLIST: innovation-analyst (5 Steps)

Examine `innovation-analysis.md` frontmatter for `stepsCompleted` array:

| Step | Check For | Completion Indicator |
|------|-----------|---------------------|
| 1 | Initialization | `stepsCompleted` contains "step-01-init" or section 1 populated |
| 2 | Market Research | `stepsCompleted` contains "step-02-market-research" or Sections 2-3 populated |
| 3 | Innovation Backlog | `stepsCompleted` contains "step-03-innovation-backlog" or Section 4 populated |
| 4 | Priorities | `stepsCompleted` contains "step-04-priorities" or Sections 5-8 populated |
| 5 | Validation | `stepsCompleted` contains "step-05-validation" or completion_timestamp present |

**Step Names for Display:**
1. Initialization & Context
2. Market Research
3. Innovation Backlog
4. Priorities & Roadmap
5. Validation & Sign-off

---

#### CHECKLIST: client-journey-analyst (8 Steps)

Examine `cx-journey-documentation.md` frontmatter for `stepsCompleted` array:

| Step | Check For | Completion Indicator |
|------|-----------|---------------------|
| 1 | Initialization | `stepsCompleted` contains "step-01-init" or section 1 populated |
| 2 | Journey Overview | `stepsCompleted` contains "step-02-journey-overview" or Section 1 populated |
| 3 | Touchpoints | `stepsCompleted` contains "step-03-touchpoints" or Section 2 populated (JT# IDs) |
| 4 | Friction | `stepsCompleted` contains "step-04-friction" or Sections 4 & 7 populated (FP# IDs) |
| 5 | Moments | `stepsCompleted` contains "step-05-moments" or Sections 3 & 5 populated |
| 6 | Channels | `stepsCompleted` contains "step-06-channels" or Section 6 populated (CH# IDs) |
| 7 | Research | `stepsCompleted` contains "step-07-research" or Section 8 populated |
| 8 | Validation | `stepsCompleted` contains "step-08-validation" or completion_timestamp present |

**Step Names for Display:**
1. Initialization & Context
2. Journey Overview
3. Client Touchpoints
4. Friction Points
5. Moments That Matter
6. Channel Analysis
7. Industry Research
8. Validation & Sign-off

---

#### CHECKLIST: control-analyst (10 Steps)

Examine `compliance-control-assessment.md` frontmatter for `stepsCompleted` array:

| Step | Check For | Completion Indicator |
|------|-----------|---------------------|
| 1 | Initialization | `stepsCompleted` contains "step-01-init" or section 1 populated |
| 2 | Regulatory Framework | `stepsCompleted` contains "step-02-regulatory-framework" or Section 1 populated (REG# IDs) |
| 3 | Control Inventory | `stepsCompleted` contains "step-03-control-inventory" or Section 2 populated (CP# IDs) |
| 4 | Compliance Gaps | `stepsCompleted` contains "step-04-compliance-gaps" or Section 3 populated (GAP# IDs) |
| 5 | Effectiveness | `stepsCompleted` contains "step-05-effectiveness" or Section 4 populated (CEA# IDs) |
| 6 | Audit Trail | `stepsCompleted` contains "step-06-audit-trail" or Section 5 populated (ATR# IDs) |
| 7 | Risk Matrix | `stepsCompleted` contains "step-07-risk-matrix" or Section 6 populated (RCM# IDs) |
| 8 | Regulatory Change | `stepsCompleted` contains "step-08-regulatory-change" or Section 7 populated (RCI# IDs) |
| 9 | Recommendations | `stepsCompleted` contains "step-09-recommendations" or Section 8 populated (CIR# IDs) |
| 10 | Validation | `stepsCompleted` contains "step-10-validation" or completion_timestamp present |

**Step Names for Display:**
1. Initialization & Context
2. Regulatory Framework
3. Control Inventory
4. Compliance Gaps
5. Control Effectiveness
6. Audit Trail Requirements
7. Risk & Compliance Matrix
8. Regulatory Change Impact
9. Recommendations
10. Validation & Sign-off

---

### 3. Determine Start Step

Find the **FIRST incomplete step** (1 to {total_steps}):
- Set `{start_at_step}` = that step number
- If all steps complete, set `{start_at_step}` = {total_steps} + 1 (indicates completion)

### 4. Display Progress Summary

**Build a visual progress summary:**

```
Process: {current_process_name} ({current_process_id})
Workflow: {workflow_display_name}
Agent: {calling_agent_id}

Progress Status:
[x] Step 1: {step_1_name}
[x] Step 2: {step_2_name}
[x] Step 3: {step_3_name}
[ ] Step 4: {step_4_name}        <-- Resume here
[ ] Step 5: {step_5_name}
... (continue for all steps)

Progress: X of {total_steps} steps complete
```

Use `[x]` for completed steps, `[ ]` for incomplete steps.
Mark the resume point with `<-- Resume here`.

### 5. Route Based on Progress

**Scenario 1: All Steps Complete (start_at_step > total_steps)**

Display:
```
Process: {current_process_name} ({current_process_id})
Workflow: {workflow_display_name}

Status: All {total_steps} steps complete!

Summary:
{workflow-specific summary of captured items}

---

Ready to finalize? Options:
- Use *review-draft to validate and finalize the documentation
- Use *generate-outputs to create the executive summary
- Return to menu for other options

What would you like to do?
```

**WAIT for user input** before proceeding.
**Exit this workflow** after user makes their choice.

**Scenario 2: Steps Remaining (start_at_step <= total_steps)**

Display:
```
Ready to continue from Step {start_at_step}?

[C] Continue from Step {start_at_step}
[R] Restart from Step 1
[M] Return to menu

Enter your choice:
```

**WAIT for user input.**

**If user selects C (Continue):**
```
Continuing {workflow_display_name} from Step {start_at_step}...
```

**Invoke the target workflow:**

Execute `{target_workflow}` with these parameters:
- `start_at_step` = {start_at_step}
- `current_process_folder` = {current_process_folder}
- `current_process_id` = {current_process_id}
- `current_process_name` = {current_process_name}
- `calling_agent_id` = {calling_agent_id}

**Exit this workflow** - control transfers to target workflow.

**If user selects R (Restart):**
```
Restarting {workflow_display_name} from Step 1...
```
Set `{start_at_step}` = 1 and invoke the workflow as above.

**If user selects M (Menu):**
```
Returning to menu...
```
**Exit this workflow** without invoking the target workflow.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- calling_agent_id validated and target workflow resolved
- Correct checklist used for the workflow type
- All relevant files loaded and analyzed
- Completion status accurately determined for each step
- `{start_at_step}` correctly calculated
- Clear progress summary displayed with workflow name
- Correct routing action taken to correct target workflow
- All required parameters passed to target workflow

### SYSTEM FAILURE:

- Using wrong checklist for the workflow type
- Incorrect completion detection
- Wrong start_at_step calculation
- Routing without showing progress
- Routing to wrong workflow
- Not passing all required parameters to target workflow
- Invoking workflow without user confirmation

**Master Rule:** Always use calling_agent_id to determine which workflow and checklist to use. Always analyze actual file contents to determine completion status. Never assume or guess based on file existence alone. Always get user confirmation before routing.
