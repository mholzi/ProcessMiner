---
name: 'step-03-load-context'
description: 'Load process documentation context and return control to invoking agent'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/shared/select-existing-process'

# File References
thisStepFile: '{workflow_path}/steps/step-03-load-context.md'
workflowFile: '{workflow_path}/workflow.md'

# Process documentation files (relative to current_process_folder)
structured_data: '{current_process_folder}/structured-data.json'
main_document: '{current_process_folder}/as-is-process-documentation.md'
exceptions_detail: '{current_process_folder}/exceptions-detail.md'
pain_points_detail: '{current_process_folder}/pain-points-detail.md'
control_points_detail: '{current_process_folder}/control-points-detail.md'
---

# Step 3: Load Process Context

## STEP GOAL:

Load the selected process's documentation into context and return control to the invoking agent for analysis.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- NEVER start analysis in this step
- CRITICAL: Read the complete step file before taking any action
- YOU ARE A FACILITATOR, preparing context for the agent

### Role Reinforcement:

- You are maintaining your agent persona
- After loading context, the agent resumes control with full process knowledge
- The agent will guide the user through their specific analysis

### Step-Specific Rules:

- Focus ONLY on loading documentation files
- FORBIDDEN to analyze or summarize content
- Load files silently (don't dump raw content to user)
- Return control to agent with summary of what was loaded

## EXECUTION PROTOCOLS:

- Load all available process documentation files
- Report what was loaded
- Set session ready for agent analysis
- Return control to invoking agent

## Sequence of Instructions

### 1. Load Process Documentation Files

Load the following files from `{current_process_folder}` (if they exist):

**Required:**
- `structured-data.json` - Core process data (steps, systems, etc.)
- `as-is-process-documentation.md` - Main AS-IS documentation

**Optional (may not exist yet):**
- `exceptions-detail.md` - Exception handling details
- `pain-points-detail.md` - Pain point analysis
- `control-points-detail.md` - Control point details

**For each file:**
- Check if file exists
- If exists, load and read fully (keep in context, don't display)
- Track which files were loaded vs missing

### 2. Report Loading Summary

Display:
```
**Process Context Loaded**

Process: {current_process_name} ({current_process_id})
Contributor: {contributor_name} ({contributor_role})

Documentation loaded:
- [x] Main AS-IS documentation
- [x] Structured data (JSON)
- [{check}] Exceptions detail
- [{check}] Pain points detail
- [{check}] Control points detail

Ready for analysis.
```

(Use `x` for loaded files, `-` for missing files)

### 3. Extract Key Process Metadata

From `structured-data.json`, extract and display:
```
**Process Overview:**
- Purpose: {metadata.purpose}
- Trigger: {metadata.trigger}
- Client Segments: {session.client_groups}
- Steps documented: {process_steps.length}
- Exceptions: {process_exceptions.length}
- Pain Points: {pain_points.length}
```

### 4. Return Control to Agent

Display:
```
---

Context loaded. I'm ready to begin {agent_specific_analysis_type}.

What would you like to focus on first?
```

**WORKFLOW COMPLETE** - Control returns to the invoking agent.

The agent now has:
- Process context in memory
- Contributor information
- Full documentation loaded
- Ready to guide their specific analysis workflow

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- All available documentation files loaded
- Clear summary of what was loaded
- Key metadata extracted and displayed
- Control returned to agent cleanly

### SYSTEM FAILURE:

- Starting analysis before returning control
- Dumping raw file contents to user
- Not reporting which files were loaded
- Not extracting process overview

**Master Rule:** Load context silently, summarize clearly, then return control to agent.
