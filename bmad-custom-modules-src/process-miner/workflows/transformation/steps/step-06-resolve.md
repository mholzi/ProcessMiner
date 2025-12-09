---
name: 'step-06-resolve'
description: 'Work through validation gaps with SME until resolved'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/transformation'

# File References
thisStepFile: '{workflow_path}/steps/step-06-resolve.md'
nextStepFile: '{workflow_path}/steps/step-07-finalize.md'
revalidateStepFile: '{workflow_path}/steps/step-05-validate.md'
workflowFile: '{workflow_path}/workflow.md'

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
partyModeWorkflow: '{project-root}/.bmad/core/workflows/party-mode/workflow.md'

# Output Files
transformationDataFile: '{current_process_folder}/transformation-data.json'
targetStateFile: '{current_process_folder}/target-state-documentation.md'
gapResolutionLogFile: '{current_process_folder}/gap-resolution-log.md'
transformationDecisionsFile: '{current_process_folder}/transformation-decisions-detail.md'

# Template References
# (Resolution uses gap-resolution-log structure, no external templates)
---

# Step 6: Gap Resolution

## STEP GOAL

Work through validation gaps (VG#) with the SME, resolving each through design changes, documentation updates, or justified deferral. Iterate until all critical/high gaps are resolved.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:
- 🛑 **NEVER** generate content without user input
- 📖 **CRITICAL**: Read the complete step file before taking any action
- 🔄 **CRITICAL**: When loading next step, ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:
- ✅ You are a Process Transformation Orchestrator
- ✅ **GAPS ARE DESIGN INPUTS** - Not failures, but requirements
- ✅ Work collaboratively with SME to resolve each gap
- ✅ Every resolution updates the target state

### Step-Specific Rules:
- Focus on RESOLVING gaps, one at a time
- **FORBIDDEN** to dismiss gaps without resolution or justification
- Critical gaps MUST be resolved (cannot be deferred)
- High gaps SHOULD be resolved (deferral requires justification)
- Medium/Low gaps CAN be deferred with justification

## EXECUTION PROTOCOLS

- Present gaps by severity (Critical first)
- Work through each gap with SME
- Apply resolution: Design Change | Documentation Update | Deferral
- Update target state documentation accordingly
- Track resolution in gap-resolution-log.md

## CONTEXT BOUNDARIES

- Validation gaps collected from Step 5
- This is iteration {{iteration_number}}
- Max iterations: 3
- Must resolve Critical and High before proceeding

---

## EXECUTION SEQUENCE

### 1. Set Resolution Context

Display:
```
{contributor_name}, let's work through the validation gaps.

**Current Status:**
- Validation Iteration: {{iteration_number}} of 3
- Total Gaps: {{total_gaps}}
- Critical: {{critical_count}} (must resolve)
- High: {{high_count}} (should resolve)
- Medium: {{medium_count}} (can defer)
- Low: {{low_count}} (can defer)

**Resolution Types:**
1. **Design Change** - Modify the target state
2. **Documentation Update** - Clarify or add detail
3. **Risk Acceptance** - Defer with justification (not for Critical)

We'll start with Critical gaps, then work down by severity.
```

### 2. Resolve Critical Gaps

```
<check if="critical_count > 0">
  <format>
  ## Critical Gaps (MUST RESOLVE)

  These gaps block transformation approval. Each must be addressed.
  </format>

  <for_each gap in="critical_gaps">
    <format>
    ### VG#{{gap.id}}: {{gap.title}}

    | Attribute | Value |
    |-----------|-------|
    | **Source** | {{gap.source_agent}} |
    | **Severity** | CRITICAL |
    | **TO-BE Reference** | {{gap.tobe_reference}} |
    | **AS-IS Reference** | {{gap.asis_reference}} |

    **Gap Description:**
    {{gap.description}}

    **Resolution Required:**
    {{gap.resolution_required}}
    </format>

    <ask response="critical_resolution_{{gap.id}}">
    How should we resolve this critical gap?

    **Option A: Design Change**
    Modify the target state to address the concern.
    → Describe the change needed:

    **Option B: Documentation Update**
    The concern is addressed but not clearly documented.
    → Describe what clarification is needed:

    (Note: Critical gaps cannot be deferred)

    Your choice [A/B] and description:
    </ask>

    <action>
    Based on SME response:

    1. Record resolution in {gapResolutionLogFile}:
       - VG#{{gap.id}}: Status = "Resolved"
       - Resolution Type: {{resolution_type}}
       - Resolution Description: {{resolution_description}}
       - Resolved Date: {{date}}

    2. Update {targetStateFile}:
       - Apply design change OR documentation update
       - Update affected section

    3. If design change, create TD# decision:
       - TD#{{next_td}}: Gap Resolution - {{gap.title}}
       - Category: Gap Resolution
       - Append to {transformationDecisionsFile}

    Display: "✓ VG#{{gap.id}} resolved - {{resolution_summary}}"
    </action>
  </for_each>

  <format>
  **Critical Gaps: All Resolved**
  Moving to High severity gaps...
  </format>
</check>
```

### 3. Resolve High Gaps

```
<check if="high_count > 0">
  <format>
  ## High Gaps (SHOULD RESOLVE)

  These are significant issues. Resolution is strongly recommended.
  </format>

  <for_each gap in="high_gaps">
    <format>
    ### VG#{{gap.id}}: {{gap.title}}

    | Attribute | Value |
    |-----------|-------|
    | **Source** | {{gap.source_agent}} |
    | **Severity** | HIGH |
    | **TO-BE Reference** | {{gap.tobe_reference}} |

    **Gap Description:**
    {{gap.description}}

    **Resolution Required:**
    {{gap.resolution_required}}
    </format>

    <ask response="high_resolution_{{gap.id}}">
    How should we address this high-severity gap?

    **Option A: Design Change**
    → Describe the change:

    **Option B: Documentation Update**
    → Describe the clarification:

    **Option C: Defer (requires justification)**
    → Why defer? What's the risk acceptance?

    Your choice [A/B/C] and description:
    </ask>

    <check if="high_resolution == 'C'">
      <ask response="high_deferral_justification">
      To defer a High gap, please provide:
      1. Business justification for deferral
      2. Who accepts the risk?
      3. When should this be revisited?
      </ask>

      <action>
      Record deferral:
      - VG#{{gap.id}}: Status = "Deferred"
      - Reason: {{deferral_justification}}
      - Risk Owner: {{risk_owner}}
      - Review Date: {{review_date}}
      </action>
    </check>

    <check if="high_resolution in ['A', 'B']">
      <action>
      Apply resolution (same as Critical flow).
      </action>
    </check>
  </for_each>
</check>
```

### 4. Address Medium/Low Gaps

```
<check if="medium_count + low_count > 0">
  <format>
  ## Medium/Low Gaps

  {{medium_count}} Medium and {{low_count}} Low severity gaps remain.

  These can be:
  - Resolved now
  - Batch deferred with justification
  - Addressed individually
  </format>

  <ask response="medium_low_approach">
  How would you like to handle the remaining gaps?

  **[R]** Review and resolve each individually
  **[B]** Batch defer all with single justification
  **[S]** Selective - I'll choose which to resolve vs defer

  Your choice:
  </ask>

  <check if="medium_low_approach == 'R'">
    <for_each gap in="medium_low_gaps">
      [Same resolution flow as High gaps]
    </for_each>
  </check>

  <check if="medium_low_approach == 'B'">
    <ask response="batch_justification">
    Please provide justification for deferring all Medium/Low gaps:
    </ask>

    <action>
    For each Medium/Low gap:
    - Set Status = "Deferred"
    - Set Reason = {{batch_justification}}
    - Set Review Date = Post-implementation
    </action>
  </check>

  <check if="medium_low_approach == 'S'">
    <format>
    Mark which gaps to resolve now vs defer:

    | VG# | Description | Severity | Resolve? |
    |-----|-------------|----------|----------|
    {{medium_low_selection_table}}
    </format>

    <ask response="selective_resolution">
    Enter VG# numbers to resolve (comma-separated), or 'all' or 'none':
    </ask>

    [Resolve selected, defer remainder]
  </check>
</check>
```

### 5. Resolution Summary

```
<format>
## Gap Resolution Summary - Iteration {{iteration_number}}

### Resolution Statistics

| Status | Count |
|--------|-------|
| Resolved | {{resolved_count}} |
| Deferred | {{deferred_count}} |
| Remaining Open | {{open_count}} |

### Resolution Details

| VG# | Severity | Resolution | Action Taken |
|-----|----------|------------|--------------|
{{resolution_summary_table}}

### Deferred Gaps (Risk Register)

| VG# | Reason | Risk Owner | Review Date |
|-----|--------|------------|-------------|
{{deferred_summary_table}}
</format>
```

### 6. Check Revalidation Need

```
<check if="design_changes_made > 0 AND iteration_number < 3">
  <format>
  **Design Changes Made**

  {{design_changes_made}} design change(s) were applied to resolve gaps.

  **Recommendation:** Run another validation iteration to ensure changes don't introduce new issues.
  </format>

  <ask response="revalidation_choice">
  Would you like to:

  **[V]** Run validation again (iteration {{next_iteration}})
  **[S]** Skip revalidation and proceed to finalization
  **[R]** Review changes before deciding

  Your choice:
  </ask>

  <check if="revalidation_choice == 'V'">
    <action>
    Update iteration number.
    Load and execute {revalidateStepFile}.
    </action>
  </check>

  <check if="revalidation_choice == 'R'">
    Display changes made.
    Return to revalidation choice.
  </check>
</check>

<check if="iteration_number >= 3">
  <format>
  **Maximum Iterations Reached**

  We've completed 3 validation iterations. Proceeding to finalization with current state.

  Note: Any remaining open gaps will be documented for post-implementation review.
  </format>
</check>
```

### 7. Update Documentation

```
<action>
Update all documentation with resolution results:

1. {gapResolutionLogFile}:
   - Update all VG# statuses
   - Add resolution history for each
   - Calculate metrics

2. {targetStateFile}:
   - Update Section 13 (Gap Resolution Log)
   - Update Section 8 (Validation Summary)
   - Apply any design changes to relevant sections

3. {transformationDecisionsFile}:
   - Add any new TD# from gap resolutions

4. {transformationDataFile}:
   - Update validation.gaps array
   - Set checkpoint
</action>
```

### 8. Present Menu Options

```
<format>
**Progress: Step 6 of 7 - Gap Resolution Complete**

✓ {{resolved_count}} gap(s) resolved
✓ {{deferred_count}} gap(s) deferred with justification
✓ Target state updated
✓ Resolution log documented

{{#if open_count > 0}}
⚠️ {{open_count}} gap(s) remain open - will be documented for post-implementation
{{/if}}

**Select an Option:**
- **[A]** Advanced Elicitation - Review specific resolutions
- **[P]** Party Mode - Discuss outcomes with specialists
- **[V]** Validate Again - Run another validation iteration
- **[C]** Continue - Proceed to finalization
</format>
```

#### Menu Handling Logic:

- IF A: Execute {advancedElicitationTask}
- IF P: Execute {partyModeWorkflow}
- IF V: Load, read entire file, then execute {revalidateStepFile}
- IF C: Update state, then load, read entire file, then execute {nextStepFile}
- IF other: Address query, then redisplay menu

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C' or 'V'
- After other menu items execution completes, redisplay the menu
- User can chat or ask questions - always respond, then redisplay the menu

---

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN [C continue option] is selected and [Critical/High gaps resolved or justified], will you then load and read fully `{nextStepFile}` to execute and begin finalization.

If user chooses V, load step-05-validate.md for revalidation.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:
- All Critical gaps resolved (not deferred)
- All High gaps resolved or deferred with justification
- Medium/Low gaps addressed (resolved or deferred)
- Design changes applied to target state
- Resolution history documented in gap-resolution-log.md
- New TD# decisions recorded for significant changes
- transformation-data.json updated
- Revalidation offered after design changes
- Menu presented and user input handled correctly

### ❌ SYSTEM FAILURE:
- Deferring Critical gaps
- Deferring without justification
- Not applying design changes to documentation
- Missing resolution history
- Exceeding 3 iterations without resolution
- Proceeding with unaddressed Critical gaps

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
