---
name: 'step-05-moments'
description: 'Identify moments that matter and consolidate CES analysis'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/cx-journey-analysis'

# File References
thisStepFile: '{workflow_path}/steps/step-05-moments.md'
nextStepFile: '{workflow_path}/steps/step-06-channels.md'
workflowFile: '{workflow_path}/workflow.md'

# Shared Protocols
protocolsFile: '{module_root}/workflows/shared/protocols/protocols.md'

# Output Files
cxJourneyFile: '{current_process_folder}/cx-journey-documentation.md'
clientTouchpointsFile: '{current_process_folder}/client-touchpoints-detail.md'

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
---

# Step 5: Moments That Matter & CES Analysis

## STEP GOAL

Identify the critical touchpoints that disproportionately define client perception ("moments that matter"). Consolidate the Client Effort Score (CES) analysis across the entire journey.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:
- **NEVER** generate content without user input
- **CRITICAL**: Read the complete step file before taking any action
- **CRITICAL**: When loading next step, ensure entire file is read
- YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:
- You are a Client Journey Analyst
- Continue using your established name, communication_style, and persona
- We engage in collaborative dialogue with the SME
- You bring CX analysis expertise, SME brings process experience
- Maintain professional, supportive tone throughout

### Step-Specific Rules:
- Moments that matter are subset of touchpoints (JT#)
- Not every touchpoint is a moment that matters
- CES consolidation uses data from Steps 3 and 4
- **FORBIDDEN** to discuss channel analysis in this step

## MOMENTS THAT MATTER CRITERIA

A touchpoint is a "moment that matter" if it meets ANY of these criteria:

| Criteria | Description |
|----------|-------------|
| First Impression | First client interaction - sets expectations |
| Decision Point | Where client decides to proceed or abandon |
| Problem Resolution | How we handle issues or exceptions |
| High Emotional Stakes | Critical moments with significant anxiety/hope |
| Peak/End Moments | Highest intensity or final impression |

## CES WEIGHTS REFERENCE

| Component | Weight | Description |
|-----------|--------|-------------|
| Client Actions | 1.0 | Distinct actions client must take |
| Documents Required | 1.5 | Documents/info client must provide |
| Information Requests | 1.0 | Questions client must ask/answer |
| Follow-ups Required | 2.0 | Client follow-ups needed |
| Channel Switches | 1.5 | Forced channel changes |
| Active Time (min) | 0.5 | Active minutes (not waiting) |

## EXECUTION PROTOCOLS

- Review all captured touchpoints (JT#)
- Evaluate each against moments that matter criteria
- Consolidate CES from touchpoints and friction
- Calculate journey-level CES baseline

## CONTEXT BOUNDARIES

- Touchpoints captured in Step 3 with CES per touchpoint
- Friction points captured in Step 4 with CES impact
- This step creates the CES baseline for TO-BE comparison

---

## EXECUTION SEQUENCE

### 1. Display Progress and Context

```
**Progress: Step 5 of 7 - Moments That Matter & CES Analysis**

Now let's identify which touchpoints truly define how clients perceive this journey, and consolidate the effort analysis.

"Moments that matter" are the touchpoints that:
- Create lasting impressions
- Determine if clients continue or abandon
- Drive word-of-mouth and NPS
- Must be protected in any transformation
```

### 2. Display Touchpoint Summary

```
<format>
**Captured Touchpoints:**

| JT# | Touchpoint | Stage | CES | Friction? |
|-----|------------|-------|-----|-----------|
{{for each touchpoint in captured_touchpoints}}
| {{touchpoint.id}} | {{touchpoint.name}} | {{touchpoint.stage}} | {{touchpoint.ces}} | {{touchpoint.has_friction}} |
{{/for}}

Let's evaluate which of these are "moments that matter".
</format>
```

### 3. Moments That Matter Identification

```
<loop name="mtm_evaluation" for="each touchpoint in captured_touchpoints">

  <format>
  ---
  **Evaluating: {{touchpoint.id}} - {{touchpoint.name}}**
  </format>

  <ask response="mtm.is_first_impression">
  Is this the first client interaction (sets expectations)?
  - [ ] Yes
  - [ ] No
  </ask>

  <ask response="mtm.is_decision_point">
  Is this a decision point where clients might abandon?
  - [ ] Yes
  - [ ] No
  </ask>

  <ask response="mtm.is_problem_resolution">
  Is this where we handle problems or exceptions?
  - [ ] Yes
  - [ ] No
  </ask>

  <ask response="mtm.is_high_emotion">
  Are there high emotional stakes at this point?
  - [ ] Yes
  - [ ] No
  </ask>

  <ask response="mtm.is_peak_or_end">
  Is this a peak intensity moment or the final impression?
  - [ ] Yes
  - [ ] No
  </ask>

  <action>
  Calculate MTM score = count of "Yes" responses (0-5)
  IF MTM score >= 2: Mark as Moment That Matters
  </action>

  <check if="MTM score >= 2">
    <format>
    **{{touchpoint.id}} is a MOMENT THAT MATTERS** (Score: {{mtm_score}}/5)
    </format>

    <ask response="mtm.why_critical">
    Why is this moment critical for client perception?
    </ask>

    <ask response="mtm.current_state">
    How would you rate the current experience at this moment?
    - [ ] Excellent - Delight clients
    - [ ] Good - Meets expectations
    - [ ] Acceptable - Gets the job done
    - [ ] Poor - Causes frustration
    - [ ] Critical - Major issues
    </ask>

    <ask response="mtm.degradation_risk">
    If this moment were degraded in a transformation, what would be the risk?
    </ask>

    <ask response="mtm.protection_priority">
    How would you prioritize protecting/enhancing this moment?
    - [ ] Must Protect - Non-negotiable
    - [ ] Should Enhance - Opportunity to delight
    - [ ] Can Optimize - Improve without risk
    </ask>
  </check>

</loop>
```

### 4. CES Consolidation

```
<format>
**Client Effort Score (CES) Consolidation**

Now let's calculate the total client effort for this journey.
</format>

<action>
Calculate from Step 3 touchpoint data:

| Metric | Count | Weight | Weighted Score |
|--------|-------|--------|----------------|
| Client Actions | {{sum_actions}} | 1.0 | {{sum_actions_weighted}} |
| Documents Required | {{sum_documents}} | 1.5 | {{sum_documents_weighted}} |
| Information Requests | {{sum_info_requests}} | 1.0 | {{sum_info_requests_weighted}} |
| Follow-ups Required | {{sum_follow_ups}} | 2.0 | {{sum_follow_ups_weighted}} |
| Channel Switches | {{sum_channel_switches}} | 1.5 | {{sum_channel_switches_weighted}} |
| Active Time (min) | {{sum_active_time}} | 0.5 | {{sum_time_weighted}} |
| **BASE CES** | | | **{{base_ces}}** |

Add friction-caused CES impact from Step 4:
| Friction CES Impact | | | +{{friction_ces_total}} |
| **TOTAL CES** | | | **{{total_ces}}** |
</action>

<format>
**Journey CES Summary**

| Component | Value |
|-----------|-------|
| Base CES (from touchpoints) | {{base_ces}} |
| Friction CES (additional effort) | {{friction_ces_total}} |
| **Total Journey CES** | **{{total_ces}}** |

**CES Interpretation:**
- Low CES (< 20): Excellent client experience, minimal effort
- Medium CES (20-40): Acceptable experience, improvement opportunities exist
- High CES (> 40): Poor experience, significant transformation required
</format>
```

### 5. CES by Journey Stage

```
<action>
Calculate CES breakdown by journey stage:

| Stage | Base CES | Friction CES | Total Stage CES | % of Journey |
|-------|----------|--------------|-----------------|--------------|
{{for each stage}}
| {{stage.name}} | {{stage.base_ces}} | {{stage.friction_ces}} | {{stage.total_ces}} | {{stage.percentage}} |
{{/for}}
</action>

<ask response="ces_highest_stage">
Looking at the CES by stage, does the distribution make sense to you?
Which stage would you prioritize for CES reduction?
</ask>
```

### 6. CES Benchmark Comparison

```
<ask response="industry_average_ces">
Do you have any sense of industry average CES for this type of journey?
(If not, we can estimate or leave as TBD)
</ask>

<ask response="internal_target_ces">
What would be a reasonable CES target for this journey?
(Industry standard is 30-40% CES reduction in transformation)
</ask>
```

### 7. AI Assessment: Section Confidence

```
<action name="assess_moments_and_ces_confidence">
Based on the moments/CES information captured in this step, the AI MUST:

1. Calculate Section 3 (Moments That Matter) confidence:
   - Count "Accept" responses vs "Edit" responses for MTM identification
   - Assess MTM scoring consistency
   - Note whether MTMs are clearly differentiated from regular touchpoints

2. Calculate Section 5 (CES Analysis) confidence:
   - Assess effort score data completeness across touchpoints
   - Check if duration estimates are well-supported
   - Verify benchmark comparisons are reasonable

3. Determine confidence levels:
   - HIGH: Clear MTM criteria met, consistent scoring, solid effort data
   - MEDIUM: Some subjective MTM selection, estimated effort values (DEFAULT if uncertain)
   - LOW: Disputed MTMs, significant effort estimation gaps

4. Generate confidence basis automatically:
   - "Based on touchpoint analysis and friction correlation" (if MTMs align with high-friction/high-impact)
   - "Based on SME validation of critical moments" (if edits were minimal)
   - "Based on estimations requiring future measurement" (if significant uncertainty)

CRITICAL: Do NOT ask the user for confidence level or basis.
The AI makes this judgment call based on what was captured.
</action>

<set>
section_3_confidence: {{calculated_mtm_confidence_level}}
section_5_confidence: {{calculated_ces_confidence_level}}
</set>
```

### 8. Update Output Files

```
<action name="write_cx_journey_section_3" CRITICAL="MANDATORY">
APPEND to {cxJourneyFile} - Section 3 (Moments That Matter):

IMPORTANT: You MUST write actual content, not placeholders.

---

## 3. Moments That Matter

> **About this section:** Critical touchpoints that disproportionately define client perception. These must be protected or enhanced in any transformation.

### 3.1 Identified Moments

{{#for each moment_that_matters}}
**{{index}}. {{mtm.name}}** ({{mtm.touchpoint_id}})

| Attribute | Value |
|-----------|-------|
| **Stage** | {{mtm.stage}} |
| **Why Critical** | {{mtm.reason}} |
| **Current Experience** | {{mtm.current_state}} |
| **Emotional Impact** | {{mtm.emotional_impact}} |
| **Risk if Degraded** | {{mtm.degradation_risk}} |

{{/for}}

### 3.2 Moments Summary

| Moment | Touchpoint | Current State | Enhancement Priority |
|--------|-----------|---------------|---------------------|
{{#for each moment_that_matters}}
| {{mtm.name}} | {{mtm.touchpoint_id}} | {{mtm.current_state}} | {{mtm.priority}} |
{{/for}}

> **Section Confidence:** {{section_3_confidence}} | **Basis:** Based on touchpoint analysis and friction correlation

---

</action>

<action name="write_cx_journey_section_5" CRITICAL="MANDATORY">
APPEND to {cxJourneyFile} - Section 5 (Client Effort Score Analysis):

---

## 5. Client Effort Score (CES) Analysis

> **About this section:** Quantified measurement of client effort across the journey. This is the baseline for transformation target comparison.

### 5.1 CES Breakdown by Stage

| Journey Stage | Actions | Documents | Info Requests | Follow-ups | Channel Switches | Wait Time | Stage CES |
|---------------|---------|-----------|---------------|------------|------------------|-----------|-----------|
{{#for each stage}}
| {{stage.name}} | {{stage.actions}} | {{stage.documents}} | {{stage.info_requests}} | {{stage.follow_ups}} | {{stage.channel_switches}} | {{stage.wait_time}} | {{stage.ces}} |
{{/for}}
| **TOTAL** | {{total.actions}} | {{total.documents}} | {{total.info_requests}} | {{total.follow_ups}} | {{total.channel_switches}} | {{total.wait_time}} | **{{total_ces}}** |

### 5.2 CES Breakdown by Touchpoint

| Touchpoint | CES Contribution | % of Total | Reduction Priority |
|------------|------------------|------------|-------------------|
{{#for each touchpoint sorted by ces descending}}
| {{tp.name}} ({{tp.id}}) | {{tp.ces}} | {{tp.percentage}}% | {{tp.priority}} |
{{/for}}

### 5.3 Benchmark Comparison

| Benchmark | Score | Our Gap |
|-----------|-------|---------|
| Industry Average | {{benchmark_industry_avg}} | {{gap_industry}} |
| Best-in-Class | {{benchmark_best_in_class}} | {{gap_best}} |
| Internal Target | {{internal_target_ces}} | {{gap_target}} |

### 5.4 CES Baseline Statement

> **CES BASELINE FOR TO-BE COMPARISON**
>
> This AS-IS CES score (**{{total_ces}}**) establishes the baseline for transformation.
> During TO-BE design, this score will be compared against the target state to measure
> improvement. Industry standard for transformation projects is **30-40% CES reduction**.
>
> **Target CES:** {{target_ces}} (30% reduction from {{total_ces}})

> **Section Confidence:** {{section_5_confidence}} | **Basis:** Based on touchpoint CES calculations and friction impact analysis

---

</action>

<action name="update_executive_summary_metrics" CRITICAL="MANDATORY">
UPDATE {cxJourneyFile} - Executive Summary Key Metrics:

Update the "Key Metrics at a Glance" table with actual values:

| Metric | Value |
|--------|-------|
| Journey Touchpoints | {{total_touchpoints}} |
| Friction Points Identified | {{total_friction_points}} |
| Enhancement Ideas Captured | {{total_enhancement_ideas}} |
| Client Effort Score (CES) | {{total_ces}} |
| Moments That Matter | {{count_mtm}} |
| Channels Used | {{total_channels}} |
| Overall Confidence | TBD (Step 8) |

Update the "CES Baseline Summary" table with actual values.
</action>

<action name="update_touchpoints_with_mtm" CRITICAL="MANDATORY">
UPDATE {clientTouchpointsFile} - For each MTM touchpoint:

Find each touchpoint identified as a Moment That Matter and update:

#### Moment That Matters Assessment

| Criteria | Assessment |
|----------|------------|
| **First Impression?** | {{mtm.is_first_impression}} |
| **Decision Point?** | {{mtm.is_decision_point}} |
| **Problem Resolution?** | {{mtm.is_problem_resolution}} |
| **High Emotional Stakes?** | {{mtm.is_high_emotion}} |
| **Moment That Matters Score** | {{mtm.score}} / 5 |

**Why This Matters:**
{{mtm.why_moment_matters}}

**Protection Priority:**
{{mtm.protection_priority}}
</action>

<verification>
AFTER WRITING: Confirm files contain:

{cxJourneyFile} Section 3:
- [ ] Each Moment That Matter with full details table
- [ ] Moments Summary Table
- [ ] Section Confidence

{cxJourneyFile} Section 5:
- [ ] CES Breakdown by Stage table with all columns filled
- [ ] CES Breakdown by Touchpoint table sorted by CES
- [ ] Benchmark Comparison table
- [ ] CES Baseline Statement with target calculation
- [ ] Section Confidence

{cxJourneyFile} Executive Summary:
- [ ] Key Metrics at a Glance table updated with actual numbers
- [ ] CES Baseline Summary table updated

{clientTouchpointsFile}:
- [ ] Each MTM touchpoint has full "Moment That Matters Assessment" section
- [ ] is_moment_that_matters: true for each MTM
</verification>
```

### 9. Summary and Transition

Display:
```
**Moments That Matter & CES Analysis Complete**

**Moments That Matter:**
| JT# | Touchpoint | MTM Score | Current State | Priority |
|-----|------------|-----------|---------------|----------|
{{for each mtm}}
| {{mtm.id}} | {{mtm.name}} | {{mtm.score}}/5 | {{mtm.current_state}} | {{mtm.priority}} |
{{/for}}

**CES Baseline:**
| Metric | Value |
|--------|-------|
| Total Journey CES | {{total_ces}} |
| Base CES | {{base_ces}} |
| Friction CES | {{friction_ces_total}} |
| Target CES (30% reduction) | {{target_ces}} |
| Highest CES Stage | {{highest_ces_stage}} |

Next, we'll analyze channel usage across the journey.
```

### 10. Proceed to Next Step

Display:
```
**Progress: Step 5 of 8 - Moments & CES Complete**

Now let's analyze how channels are used across this journey.
```

```
<action>Load, read entire file, then execute {nextStepFile}</action>
```

---

## CRITICAL STEP COMPLETION NOTE

This is an auto-proceed step. IMMEDIATELY after [moments identified] and [CES consolidated] and [output files updated], load and read fully `{nextStepFile}` to execute and begin channel analysis.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:
- All touchpoints evaluated for MTM criteria
- Moments that matter identified with justification
- Current state and protection priority captured for each MTM
- CES consolidated from touchpoints and friction
- CES breakdown by stage calculated
- Benchmark comparison captured
- Confidence assessment captured
- Output files updated
- Ready to proceed to Step 6

### SYSTEM FAILURE:
- Did not evaluate all touchpoints
- Did not calculate consolidated CES
- Did not identify moments that matter
- Started discussing channels
- Did not update output files
- Skipped to later steps

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
