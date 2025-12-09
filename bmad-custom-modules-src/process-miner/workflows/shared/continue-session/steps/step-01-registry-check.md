---
name: 'step-01-registry-check'
description: 'Verify active processes exist in the registry before proceeding'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/shared/continue-session'

# File References
thisStepFile: '{workflow_path}/steps/step-01-registry-check.md'
nextStepFile: '{workflow_path}/steps/step-02-process-selection.md'
workflowFile: '{workflow_path}/workflow.md'

# Registry Location
process_registry: '{output_folder}/process-registry.md'

# Dependencies
start_new_workflow: '{module_root}/workflows/start-new-process/workflow.md'
---

# Step 1: Registry Check

## STEP GOAL:

Verify that active processes exist in the registry before proceeding with process selection. Handle empty registry by routing to start-new workflow.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- NEVER skip registry verification
- CRITICAL: Read the complete step file before taking any action
- CRITICAL: When loading next step, ensure entire file is read
- YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:

- You are a session continuity specialist
- If you already have been given communication or persona patterns, continue to use those
- We engage in collaborative dialogue, not command-response
- You bring systematic analysis, user brings process knowledge

### Step-Specific Rules:

- Focus ONLY on loading and parsing the registry
- FORBIDDEN to proceed to selection if no active processes exist
- Provide clear feedback on registry status
- Handle missing registry gracefully

## EXECUTION PROTOCOLS:

- Load registry file from {process_registry}
- Parse the Active Processes table correctly
- Count only processes in the Active Processes section
- Do NOT count processes in the Discontinued Processes section

## CONTEXT BOUNDARIES:

- User wants to continue an existing process
- Registry file may or may not exist
- Registry may have zero or more active processes
- This step determines if continuation is possible

## Sequence of Instructions

### 1. Load Process Registry

Load the process registry from `{output_folder}/process-registry.md`

**If file does not exist:**
```
No process registry found at {output_folder}/process-registry.md

You haven't started any processes yet. Use *start-new to create your first process.
```
**Exit this workflow** - do not proceed further.

### 2. Parse Registry for Active Processes

**CRITICAL PARSING INSTRUCTIONS:**

The registry has two sections:
- `## Active Processes` - Contains processes that can be continued
- `## Discontinued Processes` - Contains archived processes (IGNORE these)

**To correctly parse active processes:**

1. Find the section starting with `## Active Processes`
2. Look for the markdown table AFTER this heading
3. The table has format: `| ID | Process Name | Status | Created | Last Updated | Contributor |`
4. Skip the header row and separator row (`|----|----|...`)
5. Each subsequent row until the next `##` heading is an active process
6. Extract the ID (e.g., P001, P004) and Process Name from each row

**Example parsing:**
```markdown
## Active Processes

| ID | Process Name | Status | Created | Last Updated | Contributor |
|----|--------------|--------|---------|--------------|-------------|
| P004 | Onboarding of Corporate Clients | Active | 2025-12-04 | 2025-12-04 | Markus (CEO) |
```
This means: **1 active process** - P004 "Onboarding of Corporate Clients"

**IMPORTANT:** Do NOT count processes listed under `## Discontinued Processes` - these are archived and cannot be continued.

### 3. Determine Action Based on Count

**If ZERO active processes found:**

Display to user:
```
No active processes found in the registry.

Let's create your first process!
```

Then automatically invoke the `*start-new` command to begin the start-new-process workflow.

**Exit this workflow** - do not proceed to Step 2.

**If ONE OR MORE active processes found:**

Store the list of active processes (ID and Name pairs) for the next step.

Proceed to load the next step file.

### 4. Load Next Step

**ONLY when active processes exist:**

Load, read entire file, then execute `{nextStepFile}` (step-02-process-selection.md)

Pass the following session context:
- List of active processes (ID, Name pairs)
- Total count of active processes

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- Registry file loaded successfully
- Active Processes section correctly identified and parsed
- Correct count of active processes determined
- Appropriate routing (empty -> start-new, has processes -> step 2)

### SYSTEM FAILURE:

- Counting discontinued processes as active
- Failing to parse the markdown table correctly
- Not finding active processes when they exist in the table
- Proceeding to step 2 when no active processes exist

**Master Rule:** The parsing logic MUST correctly identify the `## Active Processes` section and parse the markdown table within it. Do NOT look at the entire file - focus on the specific section.
