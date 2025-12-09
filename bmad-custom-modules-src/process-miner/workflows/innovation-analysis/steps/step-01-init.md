---
name: 'step-01-init'
description: 'Process selection, prerequisite validation, and session initialization'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/innovation-analysis'
processes_folder: '{project-root}/docs/processes'

# File References
thisStepFile: '{workflow_path}/steps/step-01-init.md'
nextStepFile: '{workflow_path}/steps/step-02-market-research.md'
workflowFile: '{workflow_path}/workflow.md'

# Process abbreviation (derived from process name, used for ID generation)
# Examples: "Onboarding" → "ONB", "Credit Origination" → "CRO"
process_abbreviation: session-variable

# Shared Protocols
protocolsFile: '{module_root}/workflows/shared/protocols/protocols.md'

# Registry File
processRegistryFile: '{processes_folder}/process-registry.md'

# Prerequisite Files (must exist)
structuredDataFile: '{current_process_folder}/structured-data.json'
asIsDocumentFile: '{current_process_folder}/as-is-process-documentation.md'
painPointsDetailFile: '{current_process_folder}/pain-points-detail.md'

# Output Files
innovationAnalysisFile: '{current_process_folder}/innovation-analysis.md'
innovationIdeasDetailFile: '{current_process_folder}/innovation-ideas-detail.md'

# Template References
innovationAnalysisTemplate: '{module_root}/templates/innovation-analysis-template.md'
innovationIdeasDetailTemplate: '{module_root}/templates/innovation-ideas-detail.md'

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
---

# Step 1: Process Selection & Prerequisite Validation

## STEP GOAL

Select an existing process with AS-IS documentation, validate prerequisites exist, gather organizational context, initialize the innovation analysis session, and prepare output file.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:
- **NEVER** generate content without user input
- **CRITICAL**: Read the complete step file before taking any action
- **CRITICAL**: When loading next step, ensure entire file is read
- YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:
- You are an Innovation Analyst
- Continue using your established name, communication_style, and persona
- We engage in collaborative dialogue with the SME
- You bring innovation methodology expertise, SME brings process and organizational knowledge
- Maintain forward-looking, trend-aware communication style

### Step-Specific Rules:
- `{contributor_name}` and `{contributor_role}` were already captured during agent activation
- **DO NOT** ask for name or role again — use session variables directly
- **MUST** validate prerequisites before proceeding
- **FORBIDDEN** to proceed without existing AS-IS documentation
- **MUST** capture bank name and region for web research

## EXECUTION PROTOCOLS

- Read process registry to list available processes
- User selects process to analyze
- Validate prerequisite files exist
- Load AS-IS documentation into context
- Capture organizational context (bank name, region)
- Initialize innovation output file

## CONTEXT BOUNDARIES

- Variables from workflow.md are available in memory
- Prerequisites MUST be validated before proceeding
- Session state will be created in this step

---

## EXECUTION SEQUENCE

### 1. Greet SME and Set Expectations

Display:
```
Hey {contributor_name}, let's explore innovation opportunities for one of your documented processes.

I'll guide you through:
- Market research (competitors, fintech, trends)
- Innovation idea generation with feasibility scoring
- Strategic prioritization using MoSCoW
- Transformation handoffs for MUST HAVEs

By the end, you'll have a **comprehensive innovation analysis** ready to feed into transformation planning.

First, let's select which process to analyze.
```

### 2. Load Process Registry

```
<action>
Read {processRegistryFile} to get list of documented processes.

Parse the Active Processes table to extract:
- Process ID (###)
- Process Name
- Status (only show COMPLETE or DRAFT processes)

IF registry does not exist or is empty:
  <abort>
  **No processes found**

  There are no documented processes available for innovation analysis.
  Please run the **Process Documentation Analyst** first to document a process.

  To do this:
  1. Dismiss this workflow
  2. Call the Process Documentation Analyst agent
  3. Use "Start New Process Documentation"
  4. Return here once AS-IS documentation is complete
  </abort>
</action>
```

### 3. Display Process Selection

```
<format>
**Available Processes for Innovation Analysis:**

| # | Process ID | Process Name | Status |
|---|------------|--------------|--------|
{{for each process in registry}}
| {{index}} | {{process.id}} | {{process.name}} | {{process.status}} |
{{/for}}

</format>

<ask response="selected_process">
Which process would you like to analyze for innovation opportunities? (Enter number or process name)
</ask>
```

### 4. Validate Prerequisites (CRITICAL)

```
<action name="validate_prerequisites">
Set {current_process_folder} based on selected process.
Set {current_process_id} from registry.
Set {current_process_name} from registry.

CHECK 1: Does {structuredDataFile} exist?
CHECK 2: Does {asIsDocumentFile} exist?

IF BOTH files exist:
  - Load {structuredDataFile} into context
  - Load {asIsDocumentFile} into context
  - Extract process overview, steps, pain points, exceptions, systems
  - Continue to Section 5

IF structured-data.json does NOT exist:
  <abort>
  **Missing Prerequisite: structured-data.json**

  The selected process "{current_process_name}" does not have the required
  structured data file. Innovation analysis requires this data as input.

  Please run the **Process Documentation Analyst** first to complete
  the AS-IS documentation for this process.
  </abort>

IF as-is-process-documentation.md does NOT exist:
  <abort>
  **Missing Prerequisite: as-is-process-documentation.md**

  The selected process "{current_process_name}" does not have the required
  AS-IS documentation. Innovation analysis requires this documentation as input.

  Please run the **Process Documentation Analyst** first to complete
  the AS-IS documentation for this process.
  </abort>
</action>
```

### 5. Display Loaded Context

```
<format>
**Process Loaded Successfully**

Process: {current_process_id} - {current_process_name}

**From AS-IS Documentation:**
- {{count_process_steps}} Process Steps (PS#)
- {{count_pain_points}} Pain Points (PP#)
- {{count_exceptions}} Exceptions (EX#)
- {{count_controls}} Controls (CP#)
- {{count_systems}} Systems (SYS#)

We'll use this as our foundation for innovation analysis. Pain points are especially important - they're where innovation opportunities often emerge.
</format>
```

### 6. Capture Organizational Context

```
<format>
**Organizational Context**

To make the market research relevant, I need to understand your organization's context.
</format>

<ask response="bank_name">
What is the name of your bank/organization?
(This will be used for targeted web research)
</ask>

<ask response="region">
Which region/market does this process primarily operate in?
(This determines which competitors and regulations to research)

- [ ] EU (European Union)
- [ ] UK (United Kingdom)
- [ ] US (United States)
- [ ] APAC (Asia-Pacific)
- [ ] DACH (Germany, Austria, Switzerland)
- [ ] Nordics (Sweden, Norway, Denmark, Finland)
- [ ] Multiple regions
- [ ] Other: ___
</ask>

<ask response="innovation_appetite">
How would you describe your organization's innovation appetite?

- [ ] Conservative - proven solutions only, risk-averse
- [ ] Moderate - open to innovation with clear ROI
- [ ] Aggressive - willing to experiment, early adopter
</ask>

<ask response="strategic_themes">
What are the key strategic themes or priorities for your organization this year?
(e.g., digital transformation, cost reduction, client experience, sustainability)
</ask>
```

### 7. Generate Process Abbreviation

```
<action>
Derive process abbreviation from {current_process_name} for structured ID generation:

Rules:
1. If single word: Take first 3 letters uppercase (e.g., "Onboarding" → "ONB")
2. If multiple words: Take first letter of each word uppercase (e.g., "Credit Origination" → "CRO")
3. If abbreviation < 2 chars: Pad with first letters of first word
4. If abbreviation > 4 chars: Truncate to first 4

Set {process_abbreviation} = derived abbreviation

This will be used for all structured IDs:
- TR-{process_abbreviation}-### (Market Trends)
- II-{process_abbreviation}-### (Innovation Ideas)
- COMP-{process_abbreviation}-### (Competitors)
- FIN-{process_abbreviation}-### (Fintechs)
</action>

<format>
Process abbreviation for IDs: **{process_abbreviation}**
(e.g., innovations will be II-{process_abbreviation}-001, II-{process_abbreviation}-002, etc.)
</format>
```

### 8. Initialize Session State

**Create Session:**
- Generate unique `session_id` (timestamp-based)
- Create session tracking for innovation analysis
- Store {process_abbreviation} for ID generation
- Store {bank_name} for web research
- Store {region} for targeted research
- Store {innovation_appetite} for prioritization context
- Store {strategic_themes} for alignment assessment

### 9. Initialize Output Files (Silent)

```
<action silent="true">
Create {innovationAnalysisFile} from {innovationAnalysisTemplate}:
- Replace {{process_name}} with {current_process_name}
- Replace {{analysis_id}} with generated session_id
- Replace {{date}} with current date
- Replace {{contributor_name}} with {contributor_name}
- Set status to "draft"
- Initialize stepsCompleted array as empty

Create {innovationIdeasDetailFile} from {innovationIdeasDetailTemplate}:
- Replace {{process_name}} with {current_process_name}
- Replace {{process_id}} with {current_process_id}
- Replace {{date}} with current date
- Replace {{contributor_name}} with {contributor_name}
- Replace {{contributor_role}} with {contributor_role}
- Set document_id to generated session_id + "-innovations"
</action>
```

### 10. Summary and Transition

Display:
```
**Innovation Analysis Context Set**

| Setting | Value |
|---------|-------|
| Process | {current_process_name} |
| Bank | {bank_name} |
| Region | {region} |
| Innovation Appetite | {innovation_appetite} |
| Strategic Themes | {strategic_themes} |
| ID Prefix | {process_abbreviation} |

**Pain Points Available for Innovation Focus:**
{{top_5_pain_points_summary}}

Next, I'll conduct comprehensive market research to identify:
- What competitors are doing
- Fintech disruptors to watch
- Industry best practices
- Technology trends
- Regulatory horizon
```

### 11. Proceed to Next Step

Display:
```
**Progress: Step 1 of 5 - Initialization Complete**

Now let's research the market landscape for innovation opportunities.
```

```
<action>Load, read entire file, then execute {nextStepFile}</action>
```

---

## CRITICAL STEP COMPLETION NOTE

This is an auto-proceed step. IMMEDIATELY after [prerequisites validated] and [organizational context captured] and [output file initialized], load and read fully `{nextStepFile}` to execute and begin market research.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:
- Process registry loaded
- User selected a process
- Prerequisites validated (both files exist)
- AS-IS data loaded into context
- Bank name and region captured
- Innovation appetite and strategic themes captured
- Process abbreviation derived
- Output files initialized (innovation-analysis.md AND innovation-ideas-detail.md)
- Session state created
- Ready to proceed to Step 2

### SYSTEM FAILURE:
- Proceeded without validating prerequisites
- Did not load AS-IS documentation into context
- Asked for contributor name/role again
- Did not capture bank name or region
- Started innovation elicitation before completing initialization
- Did not initialize output files
- Skipped to later steps

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
