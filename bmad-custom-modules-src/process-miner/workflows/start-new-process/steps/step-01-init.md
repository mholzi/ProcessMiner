---
name: 'step-01-init'
description: 'Session initialization, contributor confirmation, and context gathering'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/start-new-process'
processes_folder: '{project-root}/docs/processes'

# File References
thisStepFile: '{workflow_path}/steps/step-01-init.md'
nextStepFile: '{workflow_path}/steps/step-02-import.md'
workflowFile: '{workflow_path}/workflow.md'

# Shared Protocols
protocolsFile: '{module_root}/workflows/shared/protocols/protocols.md'

# Registry File
processRegistryFile: '{processes_folder}/process-registry.md'
processRegistryTemplate: '{module_root}/templates/process-registry.md'

# Output Files (resolved after folder creation)
structuredDataFile: '{current_process_folder}/structured-data.json'
mainDocumentFile: '{current_process_folder}/as-is-process-documentation.md'
exceptionsDetailFile: '{current_process_folder}/exceptions-detail.md'
painPointsDetailFile: '{current_process_folder}/pain-points-detail.md'
controlPointsDetailFile: '{current_process_folder}/control-points-detail.md'

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
partyModeWorkflow: '{project-root}/.bmad/core/workflows/party-mode/workflow.md'

# Template References (can be overridden by agent_template)
processTemplate: '{module_root}/templates/as-is-process-documentation.md'
exceptionsTemplate: '{module_root}/templates/exceptions-detail.md'
painPointsTemplate: '{module_root}/templates/pain-points-detail.md'
controlPointsTemplate: '{module_root}/templates/control-points-detail.md'

# Agent override variables (from menu item parameters)
calling_agent_id: session-variable
agent_template: session-variable
agent_output_file: session-variable

# Process selection workflow (for non-PDA agents)
selectProcessWorkflow: '{module_root}/workflows/shared/select-existing-process/workflow.md'
---

# Step 1: Session Initialization & Context Gathering

## STEP GOAL

Initialize the elicitation session by confirming contributor details, setting expectations, and gathering initial context about the process being documented.

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

### Step-Specific Rules:
- `{contributor_name}` and `{contributor_role}` were already captured during agent activation
- **DO NOT** ask for name or role again — use session variables directly
- Focus ONLY on initialization and context gathering
- **FORBIDDEN** to start eliciting process details in this step

## EXECUTION PROTOCOLS

- Greet SME professionally
- Set clear expectations for the session
- Capture client segment context
- Initialize all output files

## CONTEXT BOUNDARIES

- Variables from workflow.md are available in memory
- `{current_process_id}` and `{current_process_name}` set by `*start-new` command
- Session state will be created in this step

---

## EXECUTION SEQUENCE

### 0. Agent Permission Check (CRITICAL - EXECUTE FIRST)

```
<check if="calling_agent_id is NOT 'process-documentation-analyst'">

  **NON-PDA AGENT DETECTED** - This workflow was called by: {calling_agent_id}

  Secondary agents (Client Journey Analyst, etc.) CANNOT create new processes.
  They must work with EXISTING processes that have AS-IS documentation.

  <action>
  1. Read {processRegistryFile} to get list of existing processes
  2. Display available processes to user for selection
  3. User selects a process
  4. Verify {processes_folder}/{selected_process}/as-is-process-documentation.md EXISTS

  IF as-is-process-documentation.md does NOT exist:
    <abort>
    ⚠️ **Cannot proceed** - The selected process does not have AS-IS documentation yet.

    Please run the **Process Documentation Analyst** first to create the initial
    AS-IS process documentation, then return to this agent.

    To do this:
    1. Dismiss this agent
    2. Call the Process Documentation Analyst agent
    3. Use "Start New Process Documentation" to document the process
    4. Return to {calling_agent_id} once AS-IS documentation is complete
    </abort>

  IF as-is-process-documentation.md EXISTS:
    - Set {current_process_folder} to selected process folder
    - Set {current_process_id} from registry
    - Set {current_process_name} from registry
    - Load as-is-process-documentation.md into context
    - Load structured-data.json into context (if exists)
    - SKIP to Section 3 (Gather Client Segment Context) - folder already exists
  </action>

</check>

<check if="calling_agent_id IS 'process-documentation-analyst' OR calling_agent_id is NOT set">
  **PDA AGENT** - Proceeding with new process creation flow.
  Continue to Section 1.
</check>
```

### 1. Greet SME and Set Expectations

Display:
```
Hey {contributor_name}, let's document your process together.

I'll walk you through this step by step — you share what you know, I'll organize it. By the end, you'll have a **first draft of a detailed As-Is process view** ready for review.

Let's get started.
```

### 2. Confirm Process Context

Check if process was created via `*start-new` command:

```
<check if="current_process_name already set from *start-new">
  <format>
  We already have:
  - Process: {current_process_id} - {current_process_name}
  - Contributor: {contributor_name} ({contributor_role})
  </format>
</check>

<check if="current_process_name NOT set">
  <ask response="process_name">What is the name of the process we're documenting today?</ask>
</check>
```

### 3. Gather Client Segment Context

```
<ask response="client_groups" multiselect="true">
Which business segment(s) does this process apply to?
(This helps us highlight if it's segment-specific or applies across the board)

- [ ] BizBanking
- [ ] MidCap
- [ ] LargeCap
- [ ] All segments
</ask>
```

### 4. Check/Create Process Registry

```
<action silent="true">
Check if {processRegistryFile} exists in {processes_folder}:

IF registry does NOT exist:
  1. Create {processes_folder} directory if needed
  2. Copy {processRegistryTemplate} to {processRegistryFile}
  3. Log: "Process registry initialized"

IF registry exists:
  1. Read {processRegistryFile}
  2. Parse "Next Number" from Registry Notes section
  3. Store as {{next_process_number}}
</action>
```

### 5. Create Numbered Process Folder

```
<action silent="true">
Create process folder with sequential numbering:

1. Get {{next_process_number}} from registry (default: 1 if new registry)
2. Format number with leading zeros: {{process_number_formatted}} = pad({{next_process_number}}, 3) → "001", "002", etc.
3. Convert process name to kebab-case: {{process_name_kebab}} = kebab({current_process_name})
4. Create folder name: {{folder_name}} = "{{process_number_formatted}}-{{process_name_kebab}}"
5. Set {current_process_folder} = "{processes_folder}/{{folder_name}}"
6. Create directory: {current_process_folder}
7. Create sessions subdirectory: {current_process_folder}/sessions

Update registry:
1. Add new row to Active Processes table:
   | {{process_number_formatted}} | {current_process_id} | {current_process_name} | DRAFT | {{date}} | {{date}} |
2. Increment "Next Number" in Registry Notes section
3. Save {processRegistryFile}
</action>
```

### 6. Initialize Session State

**Create Session:**
- Generate unique `session_id` (timestamp-based)
- Create session file at `{current_process_folder}/sessions/{{process_name}}-session-{{session_id}}.json`

### 7. Initialize Output Files (Silent)

```
<action silent="true">Initialize {structuredDataFile} with schema v1.0.0:
{
  "$schema": "process-miner-structured-data-v1",
  "schema_version": "1.0.0",

  "session": {
    "id": "{{session_id}}",
    "started": "{{timestamp}}",
    "last_updated": "{{timestamp}}",
    "contributor": {
      "name": "{contributor_name}",
      "role": "{contributor_role}"
    },
    "process": {
      "id": "{current_process_id}",
      "name": "{current_process_name}"
    },
    "client_groups": {{client_groups}},
    "checkpoint": {
      "step": 1,
      "last_item_id": null
    }
  },

  "metadata": {
    "purpose": null,
    "trigger": null,
    "frequency": null,
    "volume": null,
    "confidence": null
  },

  "process_steps": [],
  "process_exceptions": [],
  "pain_points": [],
  "controls": [],
  "systems": [],

  "validation": {
    "status": "DRAFT",
    "completed_at": null,
    "unknowns": [],
    "overrides": []
  }
}
</action>

<action silent="true">
Create main document from template:
- IF {agent_template} is set (from calling agent menu item):
    - Use {agent_template} as the template source
    - Use {agent_output_file} as the output filename
    - Create at: {current_process_folder}/{agent_output_file}
- ELSE (default PDA behavior):
    - Use {processTemplate} (as-is-process-documentation.md)
    - Create at: {mainDocumentFile}
</action>
<action silent="true">Create {exceptionsDetailFile} from {exceptionsTemplate} with header info</action>
<action silent="true">Create {painPointsDetailFile} from {painPointsTemplate} with header info</action>
<action silent="true">Create {controlPointsDetailFile} from {controlPointsTemplate} with header info</action>
```

### 8. Proceed to Next Step

Display:
```
**Progress: Step 1 of 9 - Initialization Complete**

Session initialized. Now let's check if you have any existing documentation we can build on.
```

```
<action>Load, read entire file, then execute {nextStepFile}</action>
```

---

## CRITICAL STEP COMPLETION NOTE

This is an auto-proceed step. IMMEDIATELY after [session initialized] and [output files created], load and read fully `{nextStepFile}` to execute and begin checking for existing documentation.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:
- Contributor confirmed (using existing session variables)
- Process context captured
- Client segments identified
- Process registry checked/created from template
- Numbered process folder created (e.g., `001-process-name`)
- Registry updated with new process entry
- All 5 output files initialized with schema v1.0.0
- Session state created
- Ready to proceed to Step 2

### ❌ SYSTEM FAILURE:

- Asked for contributor name/role again
- Started eliciting process details
- Failed to check/create process registry
- Created folder without numbered prefix
- Failed to update registry with new process
- Failed to initialize output files
- Did not confirm process context
- Skipped to later steps

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
