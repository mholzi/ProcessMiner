---
name: 'step-00-continuation'
description: 'Handle session resumption for Innovation Analysis workflow'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/innovation-analysis'

# File References
thisStepFile: '{workflow_path}/steps/step-00-continuation.md'
workflowFile: '{workflow_path}/workflow.md'

# Step Files for resumption
step1: '{workflow_path}/steps/step-01-init.md'
step2: '{workflow_path}/steps/step-02-market-research.md'
step3: '{workflow_path}/steps/step-03-innovation-backlog.md'
step4: '{workflow_path}/steps/step-04-priorities.md'
step5: '{workflow_path}/steps/step-05-validation.md'

# Output Files
innovationAnalysisFile: '{current_process_folder}/innovation-analysis.md'
---

# Step 0: Session Continuation

## STEP GOAL

Resume a previously started Innovation Analysis session. Load previous state and continue from where the user left off.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:
- **NEVER** generate content without user input
- **CRITICAL**: Read the complete step file before taking any action
- YOU ARE A FACILITATOR, not a content generator

### Step-Specific Rules:
- This step is ONLY executed when `start_at_step` session variable is set
- Must restore full context from previous session
- Must validate that prerequisite files still exist

---

## EXECUTION SEQUENCE

### 1. Display Continuation Message

```
**Resuming Innovation Analysis Session**

Welcome back, {contributor_name}! Let me restore your previous session.
```

### 2. Load Previous State

```
<action>
Load state from output files:
1. Read {innovationAnalysisFile} - extract completed sections
2. Parse frontmatter for `stepsCompleted` array
3. Extract captured data:
   - Market Trends (TR#)
   - Innovation Ideas (II#)
   - Competitors (COMP#)
   - Fintechs (FIN#)
   - Feasibility scores
   - Priority assignments
</action>
```

### 3. Display Session Summary

```
<format>
**Previous Session Summary:**

Process: {current_process_id} - {current_process_name}
Bank: {bank_name}
Region: {region}

**Progress:**
{{for each completed_step}}
- [x] Step {{step.number}}: {{step.name}}
{{/for}}

**Captured So Far:**
| Element | Count |
|---------|-------|
| Market Trends (TR#) | {{count_trends}} |
| Innovation Ideas (II#) | {{count_innovations}} |
| Competitors (COMP#) | {{count_competitors}} |
| Fintechs (FIN#) | {{count_fintechs}} |

**Last Checkpoint:** Step {{last_step_completed}}
</format>
```

### 4. Confirm Continuation Point

```
<ask response="continue_from">
Where would you like to continue from?

{{for each remaining_step}}
- [ ] Step {{step.number}}: {{step.name}}
{{/for}}
- [ ] Start over from beginning
</ask>
```

### 5. Load Appropriate Step

```
<check if="continue_from == 'Start over'">
  <action>Load, read entire file, then execute {step1}</action>
</check>

<check if="continue_from == 'Step 2'">
  <action>Load, read entire file, then execute {step2}</action>
</check>

<check if="continue_from == 'Step 3'">
  <action>Load, read entire file, then execute {step3}</action>
</check>

<check if="continue_from == 'Step 4'">
  <action>Load, read entire file, then execute {step4}</action>
</check>

<check if="continue_from == 'Step 5'">
  <action>Load, read entire file, then execute {step5}</action>
</check>
```

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:
- Previous state loaded from output files
- Session summary displayed accurately
- User selected continuation point
- Correct step file loaded and executed

### SYSTEM FAILURE:
- Failed to load previous state
- Did not display session summary
- Loaded wrong step file
- Lost previously captured data

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
