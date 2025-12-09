---
name: 'step-01-init'
description: 'Load and verify AS-IS context from all specialist agents'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/transformation'
processes_folder: '{project-root}/docs/processes'

# File References
thisStepFile: '{workflow_path}/steps/step-01-init.md'
nextStepFile: '{workflow_path}/steps/step-02-synthesize.md'
workflowFile: '{workflow_path}/workflow.md'

# Registry File
processRegistryFile: '{processes_folder}/process-registry.md'

# Select Process Workflow
selectProcessWorkflow: '{module_root}/workflows/shared/select-existing-process/workflow.md'

# Source Documents (AS-IS) - REQUIRED (all 4 must exist)
asIsProcessDoc: '{current_process_folder}/as-is-process-documentation.md'
cxJourneyDoc: '{current_process_folder}/cx-journey-documentation.md'
controlComplianceDoc: '{current_process_folder}/compliance-control-assessment.md'
innovationAnalysisDoc: '{current_process_folder}/innovation-analysis.md'
structuredDataFile: '{current_process_folder}/structured-data.json'

# Specialist Agent References (for missing document guidance)
agentsFolder: '{module_root}/agents'
processAnalystAgent: '{agentsFolder}/process-documentation-analyst.agent.yaml'
cxAnalystAgent: '{agentsFolder}/client-journey-analyst.agent.yaml'
controlAnalystAgent: '{agentsFolder}/control-analyst.agent.yaml'
innovationAnalystAgent: '{agentsFolder}/innovation-analyst.agent.yaml'

# Detail Documents (AS-IS) - Optional but valuable
exceptionsDetailDoc: '{current_process_folder}/exceptions-detail.md'
painPointsDetailDoc: '{current_process_folder}/pain-points-detail.md'
controlPointsDetailDoc: '{current_process_folder}/control-points-detail.md'
touchpointsDetailDoc: '{current_process_folder}/client-touchpoints-detail.md'
frictionPointsDetailDoc: '{current_process_folder}/friction-points-detail.md'
innovationIdeasDetailDoc: '{current_process_folder}/innovation-ideas-detail.md'

# Output Files (TO-BE)
targetStateFile: '{current_process_folder}/target-state-documentation.md'
transformationDecisionsFile: '{current_process_folder}/transformation-decisions-detail.md'
gapResolutionLogFile: '{current_process_folder}/gap-resolution-log.md'
transformationDataFile: '{current_process_folder}/transformation-data.json'

# Templates
targetStateTemplate: '{module_root}/templates/target-state-documentation.md'
transformationDecisionsTemplate: '{module_root}/templates/transformation-decisions-detail.md'
gapResolutionLogTemplate: '{module_root}/templates/gap-resolution-log.md'
---

# Step 1: Initialize & Load AS-IS Context

## STEP GOAL

Select a process with complete AS-IS documentation, load all source documents into context, and initialize transformation output files.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:
- 🛑 **NEVER** generate content without user input
- 📖 **CRITICAL**: Read the complete step file before taking any action
- 🔄 **CRITICAL**: When loading next step, ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:
- ✅ You are a Process Transformation Orchestrator
- ✅ Continue using your established name, communication_style, and persona
- ✅ We engage in collaborative dialogue with SMEs
- ✅ You bring transformation expertise, SME brings domain knowledge

### Step-Specific Rules:
- Focus ONLY on loading and verifying AS-IS context
- **FORBIDDEN** to start eliciting target state in this step
- **FORBIDDEN** to proceed without ALL required AS-IS documents
- All 4 specialist documents MUST exist before transformation can begin

## EXECUTION PROTOCOLS

- Verify contributor context from agent activation
- Select process with complete AS-IS analysis
- Validate all required documents exist
- Load AS-IS context into memory
- Initialize transformation output files

## CONTEXT BOUNDARIES

- `{contributor_name}` and `{contributor_role}` from agent activation
- Process selection required - transformation works on existing AS-IS
- All 4 specialist documents must be present

---

## EXECUTION SEQUENCE

### 1. Greet SME and Set Expectations

Display:
```
Welcome, {contributor_name}!

I'm ready to guide you through the **transformation process** - designing the TO-BE target state based on the AS-IS analysis from our specialist agents.

Here's what we'll do together:
1. **Load** all AS-IS context (process, controls, CX, innovation)
2. **Synthesize** the current state and improvement opportunities
3. **Design** the target state through collaborative elicitation
4. **Validate** with all specialists in parallel
5. **Resolve** any gaps through iteration
6. **Document** the final transformation for IT handover

Let's start by selecting the process to transform.
```

### 2. Select Process

```
<action>
Read {processRegistryFile} to get list of existing processes.

Display available processes:
| # | Process ID | Process Name | Status | Last Updated |
|---|------------|--------------|--------|--------------|
{{process_list}}

<ask response="selected_process">
Which process would you like to transform?
Enter the process number or ID:
</ask>

Set session variables:
- {current_process_folder} = "{processes_folder}/{{selected_folder}}"
- {current_process_id} = "{{selected_id}}"
- {current_process_name} = "{{selected_name}}"
</action>
```

### 3. Verify AS-IS Documentation Completeness

```
<action critical="true">
🛑 **MANDATORY PREREQUISITE CHECK - CANNOT PROCEED WITHOUT ALL DOCUMENTS**

Verify that ALL 4 required AS-IS documents exist for the selected process:

| # | Document | Required File | Check |
|---|----------|---------------|-------|
| 1 | AS-IS Process Documentation | {current_process_folder}/as-is-process-documentation.md | {{exists_1}} |
| 2 | CX Journey Documentation | {current_process_folder}/cx-journey-documentation.md | {{exists_2}} |
| 3 | Compliance Control Assessment | {current_process_folder}/compliance-control-assessment.md | {{exists_3}} |
| 4 | Innovation Analysis | {current_process_folder}/innovation-analysis.md | {{exists_4}} |

<check if="ANY of the 4 documents does NOT exist">
  <abort critical="true">

  🚫 **TRANSFORMATION BLOCKED - Missing Required Documents**

  I cannot proceed with the transformation workflow because the following AS-IS documentation is missing:

  {{#each missing_documents}}
  ❌ **{{this.name}}** - File not found: `{{this.path}}`
  {{/each}}

  ---

  ## Required Action

  Before transformation can begin, you MUST complete AS-IS analysis with the appropriate specialist agent(s).

  **Available Specialist Agents:**
  (Located in: `{module_root}/agents/`)

  | Missing Document | Required Agent | Agent File |
  |------------------|----------------|------------|
  {{#if missing_process}}| as-is-process-documentation.md | **Process Documentation Analyst** | `process-documentation-analyst.agent.yaml` |{{/if}}
  {{#if missing_cx}}| cx-journey-documentation.md | **Client Journey Analyst** | `client-journey-analyst.agent.yaml` |{{/if}}
  {{#if missing_control}}| compliance-control-assessment.md | **Control Analyst** | `control-analyst.agent.yaml` |{{/if}}
  {{#if missing_innovation}}| innovation-analysis.md | **Innovation Analyst** | `innovation-analyst.agent.yaml` |{{/if}}

  ---

  ## How to Proceed

  1. **Dismiss this agent** using menu option [D] or command
  2. **Load the appropriate specialist agent** from:
     `{module_root}/agents/`
  3. **Complete the AS-IS analysis** for the missing document(s)
  4. **Return to this transformation workflow** once all 4 documents exist

  ---

  ⚠️ **This workflow will now terminate.** Please complete the missing AS-IS documentation first.

  </abort>
</check>

<check if="ALL 4 documents exist">
  Display:

  ✅ **All AS-IS Documentation Verified**

  | Document | Status | Path |
  |----------|--------|------|
  | AS-IS Process Documentation | ✓ Found | `{current_process_folder}/as-is-process-documentation.md` |
  | CX Journey Documentation | ✓ Found | `{current_process_folder}/cx-journey-documentation.md` |
  | Compliance Control Assessment | ✓ Found | `{current_process_folder}/compliance-control-assessment.md` |
  | Innovation Analysis | ✓ Found | `{current_process_folder}/innovation-analysis.md` |

  All prerequisites met. Proceeding to load context...
</check>
</action>
```

### 4. Load AS-IS Context

```
<action silent="false">
Loading AS-IS context from all specialist documents...

**Loading Process Documentation...**
- Read {asIsProcessDoc}
- Extract: Process steps (PS#), exceptions (EX#), pain points (PP#), systems (SYS#)
- Store key metrics: {{total_steps}}, {{total_exceptions}}, {{total_pain_points}}

**Loading CX Journey Documentation...**
- Read {cxJourneyDoc}
- Extract: Touchpoints (JT#), friction points (FP#), CES baseline
- Store key metrics: {{total_touchpoints}}, {{total_friction}}, {{ces_score}}

**Loading Control Compliance Assessment...**
- Read {controlComplianceDoc}
- Extract: Control points (CP#), gaps, regulatory mappings
- Store key metrics: {{total_controls}}, {{control_gaps}}, {{regulatory_coverage}}

**Loading Innovation Analysis...**
- Read {innovationAnalysisDoc}
- Extract: Innovation ideas (II#), MUST HAVEs, feasibility scores
- Store key metrics: {{total_innovations}}, {{must_haves}}, {{feasibility_avg}}

<optional>
Also load detail documents if they exist:
- {exceptionsDetailDoc}
- {painPointsDetailDoc}
- {controlPointsDetailDoc}
- {touchpointsDetailDoc}
- {frictionPointsDetailDoc}
- {innovationIdeasDetailDoc}
</optional>
</action>
```

### 5. Display Context Summary

```
<format>
**AS-IS Context Loaded Successfully**

### Process Overview
- **Process:** {current_process_id} - {current_process_name}
- **Total Steps:** {{total_steps}}
- **Exceptions:** {{total_exceptions}}
- **Pain Points:** {{total_pain_points}}

### Client Experience
- **Touchpoints:** {{total_touchpoints}}
- **Friction Points:** {{total_friction}}
- **CES Baseline:** {{ces_score}}

### Controls & Compliance
- **Control Points:** {{total_controls}}
- **Open Gaps:** {{control_gaps}}
- **Regulatory Coverage:** {{regulatory_coverage}}%

### Innovation
- **Innovation Ideas:** {{total_innovations}}
- **MUST HAVEs:** {{must_haves}}
- **Avg Feasibility:** {{feasibility_avg}}/5

---

This is what we're working with. In the next step, I'll present a synthesized view of the AS-IS state and improvement opportunities.
</format>
```

### 6. Initialize Transformation Output Files

```
<action silent="true">
Initialize {transformationDataFile} with:
{
  "$schema": "transformation-data-v1",
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
    }
  },

  "asis_context": {
    "process_steps": {{total_steps}},
    "exceptions": {{total_exceptions}},
    "pain_points": {{total_pain_points}},
    "controls": {{total_controls}},
    "control_gaps": {{control_gaps}},
    "touchpoints": {{total_touchpoints}},
    "friction_points": {{total_friction}},
    "ces_score": {{ces_score}},
    "innovation_ideas": {{total_innovations}},
    "must_haves": {{must_haves}}
  },

  "tobe_design": {
    "target_steps": [],
    "target_controls": [],
    "target_touchpoints": [],
    "innovations_included": [],
    "decisions": []
  },

  "validation": {
    "iteration": 0,
    "status": "NOT_STARTED",
    "gaps": [],
    "results": {
      "control": null,
      "cx": null,
      "innovation": null,
      "process": null
    }
  },

  "checkpoint": {
    "step": 1,
    "last_action": "context_loaded"
  }
}
</action>

<action silent="true">
Create output documents from templates:
- Create {targetStateFile} from {targetStateTemplate}
- Create {transformationDecisionsFile} from {transformationDecisionsTemplate}
- Create {gapResolutionLogFile} from {gapResolutionLogTemplate}

Initialize header information in each with:
- Process name: {current_process_name}
- Process ID: {current_process_id}
- Contributor: {contributor_name}
- Date: {{date}}
</action>
```

### 7. Proceed to Next Step

```
<format>
**Progress: Step 1 of 7 - Initialization Complete**

✓ Process selected
✓ All AS-IS documentation verified
✓ Context loaded into memory
✓ Transformation files initialized

Next: I'll synthesize the AS-IS state into a consolidated view for your review.
</format>

<action>Load, read entire file, then execute {nextStepFile}</action>
```

---

## CRITICAL STEP COMPLETION NOTE

This is an auto-proceed step. IMMEDIATELY after [AS-IS context loaded] and [output files initialized], load and read fully `{nextStepFile}` to execute and begin AS-IS synthesis.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:
- Contributor confirmed from session variables
- Process selected from registry
- ALL 4 required AS-IS documents verified
- AS-IS context loaded into memory
- Key metrics extracted and stored
- Transformation output files initialized
- Ready to proceed to Step 2

### ❌ SYSTEM FAILURE:
- Proceeding without all 4 AS-IS documents
- Starting target state elicitation in this step
- Failing to load AS-IS context
- Not initializing output files
- Skipping to later steps

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
