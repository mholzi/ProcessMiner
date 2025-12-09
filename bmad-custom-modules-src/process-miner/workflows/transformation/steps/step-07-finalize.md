---
name: 'step-07-finalize'
description: 'Generate final transformation documentation for IT handover'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/transformation'
processes_folder: '{project-root}/docs/processes'

# File References
thisStepFile: '{workflow_path}/steps/step-07-finalize.md'
workflowFile: '{workflow_path}/workflow.md'

# Registry
processRegistryFile: '{processes_folder}/process-registry.md'

# Output Files
transformationDataFile: '{current_process_folder}/transformation-data.json'
targetStateFile: '{current_process_folder}/target-state-documentation.md'
gapResolutionLogFile: '{current_process_folder}/gap-resolution-log.md'
transformationDecisionsFile: '{current_process_folder}/transformation-decisions-detail.md'

# Task References
partyModeWorkflow: '{project-root}/.bmad/core/workflows/party-mode/workflow.md'

# Template References
# (Finalization compiles existing content, no external templates)
---

# Step 7: Finalize Transformation

## STEP GOAL

Complete the transformation documentation, generate final outputs, and prepare for IT handover. Mark the transformation as complete.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:
- 🛑 **NEVER** generate content without user input
- 📖 **CRITICAL**: Read the complete step file before taking any action
- 📋 YOU ARE A FACILITATOR, celebrating completion

### Role Reinforcement:
- ✅ You are a Process Transformation Orchestrator
- ✅ **DOCUMENT FOR HANDOVER** - IT inherits context, not just diagrams
- ✅ Ensure all documentation is complete and consistent
- ✅ Celebrate the achievement with the SME

### Step-Specific Rules:
- Focus on COMPLETING and PACKAGING the transformation
- Ensure all documents are consistent and cross-referenced
- Generate summary outputs for different audiences
- Mark workflow as complete

## EXECUTION PROTOCOLS

- Compile final documentation
- Generate executive summary
- Prepare IT handover notes
- Update process registry
- Celebrate completion

## CONTEXT BOUNDARIES

- All validation complete (passed or gaps resolved/deferred)
- Target state documented
- This is the final step

---

## EXECUTION SEQUENCE

### 1. Final Documentation Review

Display:
```
{contributor_name}, we're at the finish line!

Let me compile and review all documentation before we finalize.
```

```
<action>
Review all output documents for completeness:

**target-state-documentation.md**
- [ ] Executive Summary complete
- [ ] Transformation Overview complete
- [ ] Reconciliation tables complete
- [ ] TO-BE Process Design complete
- [ ] Control Design complete
- [ ] CX Design complete
- [ ] Innovation Integration complete
- [ ] Transformation Decisions complete
- [ ] Validation Summary complete
- [ ] Gap Resolution complete
- [ ] Impact Analysis complete
- [ ] Implementation Considerations complete
- [ ] Metrics complete
- [ ] Document Metadata complete

**transformation-decisions-detail.md**
- [ ] All TD# documented
- [ ] Alternatives recorded
- [ ] Rationale captured

**gap-resolution-log.md**
- [ ] All VG# accounted for
- [ ] Resolutions documented
- [ ] Deferred gaps have justification

Check for:
- Missing sections
- Incomplete tables
- Unresolved {{placeholders}}
- Cross-reference consistency
</action>

<format>
**Documentation Review Complete**

| Document | Sections | Complete | Issues |
|----------|----------|----------|--------|
| Target State | 16 | {{target_complete}}/16 | {{target_issues}} |
| Decisions Detail | {{td_sections}} | {{decisions_complete}} | {{decisions_issues}} |
| Gap Resolution | {{vg_sections}} | {{gaps_complete}} | {{gaps_issues}} |

{{#if issues_found}}
**Issues to Address:**
{{issues_list}}
{{/if}}
</format>
```

### 2. Generate Executive Summary

```
<action>
Compile executive summary for {targetStateFile} Section 1:
</action>

<format>
## Executive Summary

### Transformation Overview

**Process:** {current_process_name} ({current_process_id})
**Transformation Lead:** {contributor_name}
**Completion Date:** {{date}}

### Key Outcomes

| Metric | AS-IS | TO-BE | Improvement |
|--------|-------|-------|-------------|
| Process Steps | {{asis_steps}} | {{tobe_steps}} | {{steps_improvement}} |
| Control Gaps | {{asis_gaps}} | 0 | 100% closed |
| Pain Points | {{asis_pain}} | {{tobe_pain}} | {{pain_improvement}} |
| CES Score | {{asis_ces}} | {{tobe_ces}} | {{ces_improvement}} |
| Automation | {{asis_auto}}% | {{tobe_auto}}% | +{{auto_improvement}}% |

### Validation Status

| Specialist | Status |
|------------|--------|
| Control Analyst | {{control_status}} |
| CX Analyst | {{cx_status}} |
| Innovation Analyst | {{innovation_status}} |
| Process Analyst | {{process_status}} |

**Overall Status:** {{overall_status}}

### Key Decisions

{{top_decisions_summary}}

### Deferred Items

{{deferred_items_summary}}
</format>

<ask response="summary_review">
Does this executive summary accurately represent the transformation?

- **[Y]** Yes - Proceed
- **[E]** Edit - I'd like to adjust
</ask>
```

### 3. Prepare Impact Analysis

```
<format>
## Impact Analysis Summary

### Role Changes

| Role | Change | Action Required |
|------|--------|-----------------|
{{role_impact_table}}

### System Changes

| System | Change | Technical Requirement |
|--------|--------|----------------------|
{{system_impact_table}}

### Training Needs

{{training_summary}}

### Timeline Considerations

{{timeline_considerations}}
</format>
```

### 4. Prepare IT Handover

```
<format>
## Implementation Considerations (IT Handover)

### Technical Dependencies

| Dependency | Type | Owner | Notes |
|------------|------|-------|-------|
{{dependencies_table}}

### Implementation Sequence

{{implementation_sequence}}

### Integration Requirements

{{integration_requirements}}

### Testing Requirements

{{testing_requirements}}

### Rollback Considerations

{{rollback_notes}}

### Open Questions for IT

{{open_questions}}
</format>

<ask response="handover_additions">
Any additional notes for the IT team?

(Enter notes or 'None')
</ask>

<check if="handover_additions != 'None'">
  <action>
  Append to Implementation Considerations section.
  </action>
</check>
```

### 5. Update Process Registry

```
<action>
Update {processRegistryFile}:

Find row for {current_process_id}:
- Update Status: "DRAFT" → "TRANSFORMATION COMPLETE"
- Update Last Updated: {{date}}
- Add note: "TO-BE designed, validated, ready for implementation"
</action>
```

### 6. Generate Final Outputs

```
<action>
Ensure all files are complete and saved:

1. {targetStateFile} - Main transformation document
2. {transformationDecisionsFile} - Decision log
3. {gapResolutionLogFile} - Gap tracking
4. {transformationDataFile} - Structured data

Update {transformationDataFile}:
{
  ...existing...,
  "completion": {
    "status": "COMPLETE",
    "completed_at": "{{timestamp}}",
    "completed_by": "{contributor_name}",
    "validation_iterations": {{total_iterations}},
    "gaps_resolved": {{gaps_resolved}},
    "gaps_deferred": {{gaps_deferred}},
    "decisions_made": {{decisions_count}}
  }
}
</action>
```

### 7. Present Completion Summary

```
<format>
---

# 🎉 Transformation Complete!

{contributor_name}, congratulations! The transformation for **{current_process_name}** is complete.

## What We Accomplished

| Milestone | Status |
|-----------|--------|
| AS-IS Context Loaded | ✅ |
| Synthesis Presented | ✅ |
| Target State Elicited | ✅ |
| TO-BE Documented | ✅ |
| Validation Complete | ✅ |
| Gaps Resolved | ✅ |
| Documentation Finalized | ✅ |

## Transformation Metrics

| Metric | Before | After | Change |
|--------|--------|-------|--------|
| Process Steps | {{asis_steps}} | {{tobe_steps}} | {{steps_delta}} |
| Control Gaps | {{asis_gaps}} | 0 | Closed |
| CES Score | {{asis_ces}} | {{tobe_ces}} | {{ces_delta}} |
| Pain Points | {{asis_pain}} | {{tobe_pain}} | {{pain_delta}} |
| Automation | {{asis_auto}}% | {{tobe_auto}}% | +{{auto_delta}}% |

## Decisions Made

{{decisions_count}} transformation decisions (TD#) documented with full rationale.

## Validation

{{validation_iterations}} iteration(s) with all specialists.
{{gaps_resolved}} gaps resolved, {{gaps_deferred}} deferred.

## Output Files

| File | Purpose | Location |
|------|---------|----------|
| Target State Documentation | Main TO-BE design | {targetStateFile} |
| Transformation Decisions | Decision log | {transformationDecisionsFile} |
| Gap Resolution Log | Validation tracking | {gapResolutionLogFile} |

## Next Steps

1. **Review** - Share documentation with stakeholders
2. **IT Handover** - Engage IT team with implementation considerations
3. **Planning** - Create implementation project plan
4. **Execute** - Implement the transformation

---

Thank you for collaborating on this transformation. The target state is documented, validated, and ready for implementation.

**Questions?** The documentation includes everything needed for the next phase.
</format>
```

### 8. Final Menu

```
<format>
**Transformation Workflow Complete**

**Select an Option:**
- **[R]** Review any section of the documentation
- **[E]** Export summary for stakeholders
- **[P]** Party Mode - Celebrate with the team!
- **[D]** Done - Exit workflow
</format>

<check if="selection == 'R'">
  <ask response="review_section">
  Which section would you like to review?
  1. Executive Summary
  2. Process Design
  3. Control Design
  4. CX Design
  5. Decisions Log
  6. Full Document
  </ask>
  Display requested section.
  Return to menu.
</check>

<check if="selection == 'E'">
  <action>
  Generate stakeholder summary:
  - 1-page executive summary
  - Key metrics
  - Next steps
  </action>
  Display summary.
  Return to menu.
</check>

<check if="selection == 'P'">
  Execute {partyModeWorkflow} for celebration.
  Return to menu.
</check>

<check if="selection == 'D'">
  <format>
  **Transformation Complete**

  All documentation saved to: {current_process_folder}/

  Files created:
  - target-state-documentation.md
  - transformation-decisions-detail.md
  - gap-resolution-log.md
  - transformation-data.json

  Process registry updated.

  Goodbye, {contributor_name}! Great work on this transformation.
  </format>

  End workflow.
</check>
```

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY end workflow when user selects 'D'
- After R, E, or P execution completes, redisplay the menu
- User can chat or ask questions - always respond, then redisplay the menu

---

## CRITICAL STEP COMPLETION NOTE

This is the FINAL step. When user selects 'D' (Done), the workflow ends gracefully. All documentation should be complete and saved.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:
- All documentation complete and consistent
- Executive summary generated
- Impact analysis documented
- IT handover notes prepared
- Process registry updated
- Completion metrics captured
- Celebration presented
- User can exit gracefully

### ❌ SYSTEM FAILURE:
- Incomplete documentation sections
- Missing cross-references
- Unresolved placeholders
- Process registry not updated
- No completion confirmation
- Abrupt workflow end without summary

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
