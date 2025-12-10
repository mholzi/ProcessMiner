---
name: 'step-10-recommendations'
description: 'Consolidate control improvement recommendations'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/control-compliance-analysis'

# File References
thisStepFile: '{workflow_path}/steps/step-10-recommendations.md'
nextStepFile: '{workflow_path}/steps/step-11-validation.md'
workflowFile: '{workflow_path}/workflow.md'

# Output Files
complianceAssessmentFile: '{current_process_folder}/compliance-control-assessment.md'
controlPointsDetailFile: '{current_process_folder}/control-points-detail.md'
---

# Step 10: Control Improvement Recommendations

## STEP GOAL

Consolidate all improvement recommendations from previous steps, prioritize them, and document actionable recommendations. Assign CIR# IDs. This corresponds to **Section 9** of the compliance-control-assessment template.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:
- **NEVER** generate content without user input
- **CRITICAL**: Read the complete step file before taking any action
- YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:
- You are a Control Analyst
- Control optimization maintains protection - optimize HOW without compromising WHAT
- Practical, actionable recommendations

### Step-Specific Rules:
- Each recommendation gets CIR# ID: CIR-{process_abbreviation}-###
- MUST link to CP# controls being improved
- Prioritize by risk reduction and effort
- **FORBIDDEN** to start validation in this step (that's Step 11)

---

## CONTENT FORMAT SPECIFICATION

This step produces **Section 9: Control Improvement Recommendations** of the compliance-control-assessment template.

### Section 9: Control Improvement Recommendations
**Format:** Narrative intro + table + grouped recommendations with narratives

**Structure:**
1. **Narrative Introduction** (2-3 paragraphs):
   - Overview of improvement themes identified across the analysis
   - Summary of recommendation priorities
   - How recommendations connect to gaps, weaknesses, and regulatory changes

2. **Recommendations Summary Table:**
   | CIR# | Control (CP#) | Recommendation | Priority | Effort | Expected Benefit |
   |------|---------------|----------------|----------|--------|------------------|

3. **Grouped Recommendations by Priority:**

   **Critical Priority** (if any):
   - Narrative intro (1 paragraph) explaining why these are critical
   - Per-recommendation detail (1-2 paragraphs each):
     - What needs to change
     - Why it's critical (compliance risk, etc.)
     - Expected outcome

   **High Priority:**
   - Narrative intro (1 paragraph)
   - Per-recommendation detail (1-2 paragraphs each)

   **Medium Priority:**
   - Narrative intro (1 paragraph)
   - Brief descriptions for each recommendation

   **Low Priority:**
   - Brief list with one-line descriptions

4. **Transformation Considerations** (1-2 paragraphs):
   - How these recommendations should inform TO-BE design
   - Key themes for the transformation agent to consider

### Writing Guidelines for Section 9:
- Make recommendations specific and actionable
- Explain the "why" behind each recommendation
- Connect recommendations back to gaps, weaknesses, or regulatory changes
- Prioritize clarity and actionability over comprehensiveness
- Focus on practical improvements, not theoretical best practices

---

## EXECUTION SEQUENCE

### 1. Display Progress and Context

```
**Progress: Step 10 of 11 - Control Improvement Recommendations**

Let's consolidate all improvement opportunities identified throughout this analysis.

Sources of recommendations:
- Compliance gaps (Step 4)
- Effectiveness weaknesses (Step 5)
- Audit trail gaps (Step 6)
- Risk mitigation needs (Step 7)
- Regulatory changes (Step 8)
- Open audit findings (Step 9)
```

### 2. Consolidate Recommendations

```
<action>
Gather all improvement opportunities from previous steps:

**From Compliance Gaps (Step 4):**
{{for each gap}}
- {{gap.id}}: {{gap.remediation_approach}}
{{/for}}

**From Effectiveness Assessment (Step 5):**
{{for each weakness}}
- {{control.id}}: {{improvement_needed}}
{{/for}}

**From Audit Trail Gaps (Step 6):**
{{for each atr_gap}}
- {{atr.id}}: {{gap_description}}
{{/for}}

**From Risk Matrix (Step 7):**
{{for each risk_needing_mitigation}}
- {{rcm.id}}: {{additional_controls_needed}}
{{/for}}

**From Regulatory Changes (Step 8):**
{{for each change_requiring_action}}
- {{rci.id}}: {{action_required}}
{{/for}}

**From Open Audit Findings (Step 9):**
{{for each open_finding}}
- {{oaf.id}}: {{oaf.remediation_plan}}
{{/for}}
</action>
```

### 3. Recommendation Capture

```
<loop name="recommendation_capture" for="each improvement opportunity">

  <format>
  **Recommendation** → Assigning ID: CIR-{process_abbreviation}-{{next_id_padded}}
  </format>

  <ask response="cir.control">
  Which control (CP#) does this improve?
  </ask>

  <ask response="cir.recommendation">
  What is the specific recommendation?
  </ask>

  <ask response="cir.priority">
  What is the priority?
  - [ ] Critical - Immediate compliance risk
  - [ ] High - Significant improvement needed
  - [ ] Medium - Should address
  - [ ] Low - Nice to have
  </ask>

  <ask response="cir.effort">
  What is the implementation effort?
  - [ ] Low - Quick fix
  - [ ] Medium - Moderate effort
  - [ ] High - Significant project
  </ask>

  <ask response="cir.expected_benefit">
  What is the expected benefit?
  </ask>

</loop>
```

### 4. Additional Recommendations

```
<ask response="additional_recommendations">
Are there any other recommendations you'd like to add?
(e.g., automation opportunities, process changes, training needs)
</ask>
```

### 5. Prioritized Summary

```
<action>
Build prioritized recommendation list:

| Priority | CIR# | Control | Recommendation | Effort | Benefit |
|----------|------|---------|----------------|--------|---------|
{{sorted by priority then effort}}
</action>
```

### 6. Update Output Files

```
<action silent="true">
Update {complianceAssessmentFile} Section 9 (Control Improvement Recommendations):

Build table:
| CIR# | Control | Recommendation | Priority | Effort | Expected Benefit |

Section Confidence: {{section_9_confidence}}
</action>

<action silent="true">
Update {controlPointsDetailFile} for each control:
- improvement_recommendations section
- transformation_considerations section
</action>
```

### 7. Proceed to Next Step

Display:
```
**Progress: Step 10 of 11 - Recommendations Complete**

Now let's do a final review and complete the documentation.
```

```
<action>Load, read entire file, then execute {nextStepFile}</action>
```

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:
- All recommendations documented with CIR# IDs
- Linked to CP# controls
- Priority and effort assessed
- Output files updated

**Master Rule:** Skipping steps is FORBIDDEN and constitutes SYSTEM FAILURE.
