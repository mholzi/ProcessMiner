---
name: 'step-05-validate'
description: 'Orchestrate parallel sub-agent validation of target state'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/transformation'

# File References
thisStepFile: '{workflow_path}/steps/step-05-validate.md'
nextStepFile: '{workflow_path}/steps/step-06-resolve.md'
workflowFile: '{workflow_path}/workflow.md'

# Output Files
transformationDataFile: '{current_process_folder}/transformation-data.json'
targetStateFile: '{current_process_folder}/target-state-documentation.md'
gapResolutionLogFile: '{current_process_folder}/gap-resolution-log.md'

# Sub-Agent References
controlAnalystAgent: '{module_root}/agents/control-analyst.agent.yaml'
cxAnalystAgent: '{module_root}/agents/client-journey-analyst.agent.yaml'
innovationAnalystAgent: '{module_root}/agents/innovation-analyst.agent.yaml'
processAnalystAgent: '{module_root}/agents/process-documentation-analyst.agent.yaml'

# Source Documents for Validation
asIsProcessDoc: '{current_process_folder}/as-is-process-documentation.md'
cxJourneyDoc: '{current_process_folder}/cx-journey-documentation.md'
controlComplianceDoc: '{current_process_folder}/compliance-control-assessment.md'
innovationAnalysisDoc: '{current_process_folder}/innovation-analysis.md'

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
partyModeWorkflow: '{project-root}/.bmad/core/workflows/party-mode/workflow.md'

# Template References
# (Validation uses sub-agent invocation, no external templates)
---

# Step 5: Sub-Agent Validation

## STEP GOAL

Orchestrate parallel validation of the target state by invoking all four specialist agents. Each agent validates against their original AS-IS analysis, raising validation gaps (VG#) for any concerns.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:
- 🛑 **NEVER** generate content without user input
- 📖 **CRITICAL**: Read the complete step file before taking any action
- 🔄 **CRITICAL**: When loading next step, ensure entire file is read
- 📋 YOU ARE A FACILITATOR AND ORCHESTRATOR

### Role Reinforcement:
- ✅ You are a Process Transformation Orchestrator
- ✅ **VALIDATE WITH SPECIALISTS** - Each perspective matters
- ✅ Invoke all 4 agents in parallel for efficiency
- ✅ Collect and consolidate validation feedback

### Step-Specific Rules:
- Focus on ORCHESTRATING validation, not doing validation yourself
- **FORBIDDEN** to skip any specialist agent
- All gaps become VG# records in gap-resolution-log.md
- Track validation iteration number

## EXECUTION PROTOCOLS

- Invoke all 4 specialist agents with validation context
- Collect validation results from each
- Consolidate gaps into gap-resolution-log.md
- Determine if iteration is needed

## CONTEXT BOUNDARIES

- TO-BE documentation complete from Step 4
- Each agent has their original AS-IS analysis
- This is validation iteration {{iteration_number}}
- Max iterations: 3

---

## EXECUTION SEQUENCE

### 1. Set Validation Context

Display:
```
{contributor_name}, the target state is documented. Now we validate.

**Validation Approach:**
I'll invoke all four specialists simultaneously. Each will review the target state against their original AS-IS analysis:

| Specialist | Focus Area |
|------------|------------|
| **Control Analyst** | Control gaps closed? SOD preserved? Regulatory compliance? |
| **CX Analyst** | CES improved? Friction resolved? Moments protected? |
| **Innovation Analyst** | MUST HAVEs included? Feasibility aligned? |
| **Process Analyst** | Full traceability? Reference consistency? Completeness? |

Any concerns become **Validation Gaps (VG#)** that we'll resolve together.

**Validation Iteration:** {{iteration_number}} of 3 max
```

### 2. Prepare Validation Context

```
<action>
Prepare validation context for each agent:

**For Control Analyst:**
- Load: {controlComplianceDoc} (original AS-IS)
- Load: {targetStateFile} Section 4 (Control Design)
- Validation focus:
  - Are all CG# gaps addressed with TC# resolutions?
  - Is SOD preserved in TO-BE?
  - Do new controls have regulatory justification?
  - Are audit trails maintained?

**For CX Analyst:**
- Load: {cxJourneyDoc} (original AS-IS)
- Load: {targetStateFile} Section 5 (CX Design)
- Validation focus:
  - Does TO-BE CES meet target reduction?
  - Are all high-severity friction points resolved?
  - Are moments that matter protected or enhanced?
  - Is exception handling improved?

**For Innovation Analyst:**
- Load: {innovationAnalysisDoc} (original AS-IS)
- Load: {targetStateFile} Section 6 (Innovation Integration)
- Validation focus:
  - Are all MUST HAVE innovations included?
  - Are included innovations feasibility-aligned?
  - Is TO-BE future-proofed against emerging trends?
  - Are deferred innovations justified?

**For Process Analyst:**
- Load: {asIsProcessDoc} (original AS-IS)
- Load: {targetStateFile} Sections 2-3 (Reconciliation & Process)
- Validation focus:
  - Does every PS# have a TO-BE disposition?
  - Are all TS# properly traced to AS-IS?
  - Is reference numbering consistent?
  - Are pain points and exceptions addressed?
</action>
```

### 3. Invoke Specialist Agents (Parallel)

```
<action parallel="true">
Invoke all four specialists simultaneously for validation:

**Invocation Template for Each Agent:**

"You are being invoked as a validation sub-agent by the Transformation Agent.

**Your Task:** Review the target state design against your original AS-IS analysis.

**Context:**
- Process: {current_process_name}
- Validation Iteration: {{iteration_number}}
- Your Original Analysis: [attached]
- Target State Design: [attached - relevant section]

**Validation Checklist:**
[Agent-specific checklist from Section 2]

**Output Required:**
For each concern, provide:
1. VG# ID (I'll assign the number)
2. Description of the gap
3. Severity: Critical | High | Medium | Low
4. Specific TO-BE reference affected
5. What resolution is needed

If no concerns: Respond with 'VALIDATED - No gaps identified'

Begin validation now."
</action>
```

### 4. Display Validation Progress

```
<format>
**Validation In Progress...**

| Specialist | Status | Gaps Found |
|------------|--------|------------|
| Control Analyst | {{control_status}} | {{control_gaps}} |
| CX Analyst | {{cx_status}} | {{cx_gaps}} |
| Innovation Analyst | {{innovation_status}} | {{innovation_gaps}} |
| Process Analyst | {{process_status}} | {{process_gaps}} |

Waiting for all specialists to complete...
</format>
```

### 5. Collect and Consolidate Results

```
<action>
As each specialist returns:

1. Parse validation response
2. Extract gaps (if any)
3. Assign VG# to each gap: VG-{PROCESS}-{SEQ}
4. Categorize by severity
5. Add to gap-resolution-log.md

**Gap Consolidation:**
</action>

<format>
**Validation Complete**

### Control Analyst Results
**Status:** {{control_validation_status}}
{{control_feedback}}

**Gaps Raised:**
{{control_gaps_list}}

---

### CX Analyst Results
**Status:** {{cx_validation_status}}
{{cx_feedback}}

**Gaps Raised:**
{{cx_gaps_list}}

---

### Innovation Analyst Results
**Status:** {{innovation_validation_status}}
{{innovation_feedback}}

**Gaps Raised:**
{{innovation_gaps_list}}

---

### Process Analyst Results
**Status:** {{process_validation_status}}
{{process_feedback}}

**Gaps Raised:**
{{process_gaps_list}}
</format>
```

### 6. Present Validation Summary

```
<format>
## Validation Summary - Iteration {{iteration_number}}

### Overall Status

| Metric | Value |
|--------|-------|
| Total Gaps Raised | {{total_gaps}} |
| Critical Gaps | {{critical_gaps}} |
| High Gaps | {{high_gaps}} |
| Medium Gaps | {{medium_gaps}} |
| Low Gaps | {{low_gaps}} |

### Gaps by Specialist

| Specialist | Gaps | Critical | Status |
|------------|------|----------|--------|
| Control Analyst | {{control_gap_count}} | {{control_critical}} | {{control_status}} |
| CX Analyst | {{cx_gap_count}} | {{cx_critical}} | {{cx_status}} |
| Innovation Analyst | {{innovation_gap_count}} | {{innovation_critical}} | {{innovation_status}} |
| Process Analyst | {{process_gap_count}} | {{process_critical}} | {{process_status}} |

### Gap Summary Table

| VG# | Source | Description | Severity | Resolution Required |
|-----|--------|-------------|----------|---------------------|
{{gap_summary_table}}
</format>
```

### 7. Determine Next Action

```
<check if="total_gaps == 0">
  <format>
  🎉 **All Specialists Validated!**

  No validation gaps were raised. The target state design meets all specialist requirements.

  - Control compliance: ✅ Verified
  - Client experience: ✅ Verified
  - Innovation alignment: ✅ Verified
  - Process completeness: ✅ Verified

  Ready to proceed to finalization.
  </format>

  <action>
  Update {targetStateFile} Section 8 (Validation Summary):
  - Set all specialist statuses to PASSED
  - Record validation date
  - Note: "Validated in {{iteration_number}} iteration(s)"
  </action>

  Skip to Section 9 (Menu Options) with Continue to Step 7.
</check>

<check if="total_gaps > 0 AND critical_gaps > 0">
  <format>
  ⚠️ **Critical Gaps Identified**

  {{critical_gaps}} critical gap(s) must be resolved before proceeding.

  Critical gaps block transformation approval. We'll address these with you in the next step.
  </format>
</check>

<check if="total_gaps > 0 AND critical_gaps == 0">
  <format>
  📋 **Gaps Identified (Non-Critical)**

  {{total_gaps}} gap(s) were identified, but none are critical blockers.

  We should still review and resolve these before finalizing.
  </format>
</check>
```

### 8. Update Documentation

```
<action>
Update {targetStateFile} Sections 9-12 with validation detail:

**Section 9 - Control Validation:**
{{control_validation_detail}}

**Section 10 - CX Validation:**
{{cx_validation_detail}}

**Section 11 - Innovation Validation:**
{{innovation_validation_detail}}

**Section 12 - Process Validation:**
{{process_validation_detail}}

Update {gapResolutionLogFile}:
- Add all VG# records
- Set status to "Open"
- Record source agent
- Record severity
- Add to iteration {{iteration_number}}

Update {transformationDataFile}:
- Set validation.iteration = {{iteration_number}}
- Set validation.status = "{{validation_status}}"
- Update validation.gaps array
- Update specialist results
</action>
```

### 9. Present Menu Options

```
<check if="total_gaps == 0">
  <format>
  **Progress: Step 5 of 7 - Validation Complete (PASSED)**

  ✓ All specialists validated the target state
  ✓ No gaps identified
  ✓ Ready for finalization

  **Select an Option:**
  - **[A]** Advanced Elicitation - Explore validation details
  - **[P]** Party Mode - Celebrate with the team
  - **[C]** Continue - Proceed to finalization (skip gap resolution)
  </format>

  IF C selected: Load and execute step-07-finalize.md (skip Step 6)
</check>

<check if="total_gaps > 0">
  <format>
  **Progress: Step 5 of 7 - Validation Complete (GAPS FOUND)**

  ✓ All specialists completed validation
  ✗ {{total_gaps}} gap(s) identified
  → Gap resolution required

  **Select an Option:**
  - **[A]** Advanced Elicitation - Deep dive on specific gaps
  - **[P]** Party Mode - Discuss gaps with specialists
  - **[C]** Continue - Proceed to gap resolution
  </format>

  IF C selected: Load and execute {nextStepFile}
</check>
```

#### Menu Handling Logic:

- IF A: Execute {advancedElicitationTask}
- IF P: Execute {partyModeWorkflow}
- IF C (no gaps): Load, read entire file, then execute step-07-finalize.md
- IF C (with gaps): Load, read entire file, then execute {nextStepFile}
- IF other: Address query, then redisplay menu

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'
- After other menu items execution completes, redisplay the menu
- User can chat or ask questions - always respond, then redisplay the menu

---

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN [C continue option] is selected and [validation results documented], will you then load the appropriate next step:
- If no gaps: Load step-07-finalize.md
- If gaps exist: Load step-06-resolve.md

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:
- All 4 specialist agents invoked for validation
- Validation context properly prepared for each
- All validation responses collected
- Gaps assigned VG# references
- Gap severity properly classified
- target-state-documentation.md updated with validation results
- gap-resolution-log.md populated with all gaps
- transformation-data.json updated with validation state
- Appropriate next step determined
- Menu presented and user input handled correctly

### ❌ SYSTEM FAILURE:
- Skipping any specialist agent
- Doing validation yourself instead of invoking specialists
- Not assigning VG# to gaps
- Missing severity classification
- Proceeding without documenting results
- Wrong next step selected based on gap status

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
