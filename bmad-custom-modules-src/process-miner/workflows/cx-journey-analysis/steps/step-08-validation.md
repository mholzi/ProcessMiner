---
name: 'step-08-validation'
description: 'Final review, AI-driven gap analysis, enhancement consolidation, and document generation'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/cx-journey-analysis'

# File References
thisStepFile: '{workflow_path}/steps/step-08-validation.md'
workflowFile: '{workflow_path}/workflow.md'

# Shared Protocols
protocolsFile: '{module_root}/workflows/shared/protocols/protocols.md'

# Output Files
cxJourneyFile: '{current_process_folder}/cx-journey-documentation.md'
frictionPointsFile: '{current_process_folder}/friction-points-detail.md'
clientTouchpointsFile: '{current_process_folder}/client-touchpoints-detail.md'

# Source Files
structuredDataFile: '{current_process_folder}/structured-data.json'
asIsDocumentFile: '{current_process_folder}/as-is-process-documentation.md'
painPointsDetailFile: '{current_process_folder}/pain-points-detail.md'

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
---

# Step 8: Validation & Document Completion

## STEP GOAL

Perform final review of all captured CX content. AI analyzes for gaps, ambiguities, and inconsistencies. Consolidate enhancement ideas. Generate final documentation with traceability to AS-IS.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:
- **NEVER** generate content without user input
- **CRITICAL**: Read the complete step file before taking any action
- YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:
- You are a Client Journey Analyst
- Continue using your established name, communication_style, and persona
- We engage in collaborative dialogue with the SME
- You bring CX analysis expertise, SME brings process experience
- Maintain professional, supportive tone throughout

### AI-Driven Assessment:
- AI MUST actively analyze captured content
- Surface gaps, ambiguities, inconsistencies
- Ask clarification questions before declaring complete

### Step-Specific Rules
- This is the FINAL step — no step-09 exists
- All 3 CX output files must be finalized
- SME must confirm completeness
- Cross-references to AS-IS must be validated

## EXECUTION PROTOCOLS

- Load protocols from `{protocolsFile}`
- AI analyzes all captured data
- Consolidate enhancement ideas with prioritization
- Generate transformation inputs summary
- Finalize all documents with completion metadata

## CONTEXT BOUNDARIES

- All previous steps (1-7) complete
- All structured IDs assigned (JT-{abbrev}-###, FP-{abbrev}-###, EI-{abbrev}-###, CH-{abbrev}-###)
- All cross-references to AS-IS (PS#, PP#, EX#, CP#) established

---

## EXECUTION SEQUENCE

### 1. Display Progress and Summary

```
**Progress: Step 8 of 8 - Final Review**

Excellent work! Let me summarize what we've captured:

**Journey Overview:**
- Journey Name: {{journey_name}}
- Client Segment: {client_segment}
- Client Goal: {{client_goal}}
- Typical Duration: {{typical_duration}}

**Captured Elements:**
| Element | Count |
|---------|-------|
| Touchpoints (JT#) | {{count_touchpoints}} |
| Friction Points (FP#) | {{count_friction_points}} |
| Enhancement Ideas (EI#) | {{count_enhancement_ideas}} |
| Moments That Matter | {{count_mtm}} |
| Channels (CH#) | {{count_channels}} |

**CES Summary:**
| Metric | Value |
|--------|-------|
| Total CES | {{total_ces}} |
| Target CES (30% reduction) | {{target_ces}} |
| Highest CES Stage | {{highest_ces_stage}} |

**Cross-References to AS-IS:**
- Process Steps (PS#) linked: {{count_ps_links}}
- Pain Points (PP#) linked: {{count_pp_links}}
- Exceptions (EX#) linked: {{count_ex_links}}
```

### 2. AI-Driven Gap Analysis

```
<critical name="AI_ASSESSMENT">
Before asking the user if they're done, the AI MUST actively analyze the captured content
and identify any gaps, ambiguities, or inconsistencies that need clarification.
</critical>

<action>Analyze all captured CX content and identify:
  1. **Gaps** - Touchpoints without CES, friction without severity, missing links
  2. **Ambiguities** - Vague descriptions, unclear impact assessments
  3. **Inconsistencies** - Conflicting information between touchpoints and friction
  4. **Missing Links** - Items not cross-referenced to AS-IS elements
  5. **Shallow Areas** - Sections with less depth compared to others
  6. **CES Anomalies** - Unexplained high CES or missing components
</action>

<action>Generate list of clarification questions (0 to N items)</action>
```

### 3. Handle Clarification Questions (if any)

```
<check if="clarification_questions.length > 0">
  <format>
  ---
  **Review Assessment**

  I've reviewed everything we captured. Before we finalize, I have {{clarification_questions.length}} question(s):
  </format>

  <loop name="clarification_loop" for="each question in clarification_questions">
    <format>
    **Question {{index}}:** {{question.text}}
    Related to: {{question.element_id}}
    </format>

    <ask response="clarification_response">
    - (a) **Answer directly** — I'll provide the answer
    - (b) **Explore deeper** — Let's discuss this more
    - (c) **Skip** — Not important / I don't know
    </ask>

    <check if="clarification_response == 'a'">
      <ask response="direct_answer">Please provide the answer:</ask>
      <action>Update relevant element with new information</action>
    </check>

    <check if="clarification_response == 'b'">
      <invoke task="{advancedElicitationTask}" mode="depth">
        <context>{{question.context}}</context>
      </invoke>
    </check>
  </loop>
</check>

<check if="clarification_questions.length == 0">
  <format>
  ---
  **Review Assessment**

  I've reviewed everything we captured — no gaps or inconsistencies found.
  The CX documentation looks complete and internally consistent.
  </format>
</check>
```

### 4. Enhancement Ideas Consolidation

```
<format>
**Enhancement Ideas Summary**

Let's consolidate and prioritize the enhancement ideas captured during friction analysis.
</format>

<action>
Build consolidated enhancement catalog:

| EI# | Target Friction (FP#) | Enhancement | Est. CES Reduction | Complexity | Quick Win? |
|-----|----------------------|-------------|-------------------|------------|------------|
{{for each enhancement in all_enhancements}}
| {{ei.id}} | {{ei.target_fp}} | {{ei.description}} | {{ei.ces_reduction}} | {{ei.complexity}} | {{ei.is_quick_win}} |
{{/for}}
</action>

<format>
**Enhancement Statistics:**

| Metric | Value |
|--------|-------|
| Total Enhancement Ideas | {{total_enhancements}} |
| Quick Wins | {{quick_win_count}} |
| Strategic Initiatives | {{strategic_count}} |
| Total Est. CES Reduction | {{total_ces_reduction_potential}} |
| Potential New CES | {{ces_after_all_enhancements}} |
</format>

<ask response="enhancement_priority_validation">
Does this prioritization look right to you?
Any adjustments needed?
</ask>
```

### 5. Transformation Inputs Summary

```
<format>
**Inputs for TO-BE Design**

This summary provides key inputs for the Transformation Agent:

**CES Baseline:**
| Metric | AS-IS Value | Target (30% Reduction) |
|--------|-------------|------------------------|
| Overall CES | {{total_ces}} | {{target_ces}} |
| Client Actions | {{total_actions}} | {{target_actions}} |
| Documents Required | {{total_documents}} | {{target_documents}} |
| Channel Switches | {{total_switches}} | {{target_switches}} |

**Critical Success Factors:**
{{success_factors}}

**Experience Degradation Risks:**
DO NOT make these changes in TO-BE (would worsen CX):
{{degradation_risks}}

**Moments That Matter to Protect:**
{{mtm_summary}}

**Top Enhancement Opportunities:**
{{top_enhancements}}
</format>

<ask response="transformation_notes">
Any additional notes or context for the Transformation Agent?
</ask>
```

### 6. Discovery Logging (New Items for AS-IS)

```
<ask response="new_discoveries">
During this CX analysis, did we discover any new:
- Pain points not in the AS-IS documentation?
- Exceptions not previously documented?
- Controls not previously identified?

These should be logged back to the AS-IS documentation.
</ask>

<check if="new_discoveries exist">
  <action>
  Log new discoveries to respective AS-IS detail files:
  - New pain points → {painPointsDetailFile}
  - Update {asIsDocumentFile} summary tables
  - Update {structuredDataFile} with new elements
  </action>

  <format>
  **New Items Logged to AS-IS Documentation:**
  | Type | Count | Files Updated |
  |------|-------|---------------|
  | Pain Points | {{new_pp_count}} | pain-points-detail.md, as-is-process-documentation.md |
  | Exceptions | {{new_ex_count}} | exceptions-detail.md, as-is-process-documentation.md |
  | Controls | {{new_cp_count}} | control-points-detail.md, as-is-process-documentation.md |
  </format>
</check>
```

### 7. User Final Confirmation

```
<ask response="user_additions">
Anything else you'd like to add or correct before we finalize?

- [ ] Yes, I have additions
- [ ] No, looks good — finalize it
</ask>

<check if="user_additions == 'Yes'">
  <ask response="additions_detail">What would you like to add or correct?</ask>
  <action>Apply additions to relevant sections and files</action>
</check>
```

### 8. Calculate Overall Confidence

```
<action>
Calculate overall document confidence:

| Section | Confidence |
|---------|------------|
| 1. Journey Overview | {{section_1_confidence}} |
| 2. Client Touchpoints | {{section_2_confidence}} |
| 3. Moments That Matter | {{section_3_confidence}} |
| 4. Friction Points | {{section_4_confidence}} |
| 5. CES Analysis | {{section_5_confidence}} |
| 6. Channel Analysis | {{section_6_confidence}} |
| 7. Enhancement Ideas | {{section_7_confidence}} |
| 8. Industry Research | {{section_8_confidence}} |

Overall Confidence: {{calculate_overall_confidence}}
</action>
```

### 9. Finalize All Output Files

```
<action name="finalize_cx_journey_file" CRITICAL="MANDATORY">
FINALIZE {cxJourneyFile}:

IMPORTANT: You MUST write actual content. Do not leave placeholders.

1. WRITE Executive Summary at the TOP of the document:

---

# Client Experience Journey: {{process_name}}

**Document Type:** Client Experience AS-IS Analysis
**Process ID:** {current_process_id}
**Business Unit:** {{business_unit}}
**Client Segment:** {client_segment}
**Analyst:** {contributor_name}
**Last Updated:** {{current_date}}
**Version:** 1.0

---

## Executive Summary

{{#Write 3 paragraphs:}}
Paragraph 1: Journey overview - what this journey is, client goal, key stages
Paragraph 2: Key findings - friction summary, CES score, moments that matter
Paragraph 3: Transformation potential - quick wins, strategic recommendations
{{/Write}}

### Key Metrics at a Glance

| Metric | Value |
|--------|-------|
| Journey Touchpoints | {{total_touchpoints}} |
| Friction Points Identified | {{total_friction_points}} |
| Enhancement Ideas Captured | {{total_enhancement_ideas}} |
| Client Effort Score (CES) | {{total_ces}} |
| Moments That Matter | {{count_mtm}} |
| Channels Used | {{total_channels}} |
| Overall Confidence | {{overall_confidence}} |

### CES Baseline Summary

| Metric | Count | Weight | Weighted Score |
|--------|-------|--------|----------------|
| Client Actions | {{metrics.client_actions}} | 1.0 | {{metrics.client_actions_weighted}} |
| Documents Required | {{metrics.documents}} | 1.5 | {{metrics.documents_weighted}} |
| Information Requests | {{metrics.info_requests}} | 1.0 | {{metrics.info_requests_weighted}} |
| Follow-ups Required | {{metrics.follow_ups}} | 2.0 | {{metrics.follow_ups_weighted}} |
| Channel Switches | {{metrics.channel_switches}} | 1.5 | {{metrics.channel_switches_weighted}} |
| Active Time (minutes) | {{metrics.active_time}} | 0.5 | {{metrics.active_time_weighted}} |
| **TOTAL CES** | | | **{{total_ces}}** |

---

2. WRITE Section 7 (Enhancement Ideas) - consolidate from friction:

## 7. Enhancement Ideas

> **About this section:** Captured enhancement ideas for TO-BE consideration.

### 7.1 Enhancement Catalog

| EI# | Target Friction | Enhancement Idea | Est. CES Reduction | Complexity | Priority |
|-----|-----------------|------------------|-------------------|------------|----------|
{{#for each enhancement}}
| {{ei.id}} | {{ei.target_fp}} | {{ei.description}} | {{ei.ces_reduction}} | {{ei.complexity}} | {{ei.priority}} |
{{/for}}

### 7.2 Enhancement Statistics

| Metric | Value |
|--------|-------|
| Total Enhancement Ideas | {{total_enhancement_ideas}} |
| Quick Wins (Low Effort) | {{quick_win_count}} |
| Strategic (High Effort) | {{strategic_count}} |
| Automation Opportunities | {{automation_count}} |
| Total Est. CES Reduction | {{total_ces_reduction_potential}} |

> **Section Confidence:** {{section_7_confidence}} | **Basis:** Based on friction analysis and SME validation

---

3. WRITE Section 9 (Inputs for TO-BE Design):

## 9. Inputs for TO-BE Design

> **About this section:** Consolidated inputs for the Transformation Agent.

### 9.1 CES Baseline Summary

| Metric | AS-IS Value | Target (30% Reduction) |
|--------|-------------|------------------------|
| Overall CES Score | {{total_ces}} | {{target_ces}} |
| Client Actions | {{total_actions}} | {{target_actions}} |
| Documents Required | {{total_documents}} | {{target_documents}} |
| Channel Switches | {{total_switches}} | {{target_switches}} |

### 9.2 Critical Success Factors

For a successful TO-BE from a CX perspective:

{{#for each success_factor}}
- **{{factor.name}}:** {{factor.description}}
{{/for}}

### 9.3 Experience Degradation Risks

**DO NOT** make these changes in TO-BE (would worsen CX):

{{#for each degradation_risk}}
- **{{risk.name}}:** {{risk.explanation}}
{{/for}}

### 9.4 Enhancement Ideas Available

The Transformation Agent has **{{total_enhancement_ideas}}** enhancement ideas to consider (see Section 7).

---

4. WRITE Section 10 (Discovery Logging Summary):

## 10. Discovery Logging Summary

| Type | Count | Files Updated |
|------|-------|---------------|
| Pain Points | {{new_pain_points_count}} | pain-points-detail.md |
| Exceptions | {{new_exceptions_count}} | exceptions-detail.md |
| Controls | {{new_controls_count}} | control-points-detail.md |

---

5. WRITE Document Metadata at END:

## Document Metadata

**SME Contributors:** {{sme_contributors}}
**Analysis Date(s):** {{analysis_dates}}
**Documentation Method:** Progressive Elicitation via CX Journey Analysis Workflow

### Overall Document Confidence

| Section | Confidence | Key Gaps |
|---------|------------|----------|
| 1. Journey Overview | {{section_1_confidence}} | {{section_1_gaps}} |
| 2. Client Touchpoints | {{section_2_confidence}} | {{section_2_gaps}} |
| 3. Moments That Matter | {{section_3_confidence}} | {{section_3_gaps}} |
| 4. Friction Points | {{section_4_confidence}} | {{section_4_gaps}} |
| 5. CES Analysis | {{section_5_confidence}} | {{section_5_gaps}} |
| 6. Channel Analysis | {{section_6_confidence}} | {{section_6_gaps}} |
| 7. Enhancement Ideas | {{section_7_confidence}} | {{section_7_gaps}} |
| 8. Industry Research | {{section_8_confidence}} | {{section_8_gaps}} |

**Overall Confidence:** {{overall_confidence}}

### Companion Documents

| Document | Purpose | Link |
|----------|---------|------|
| Client Touchpoints Detail | Full touchpoint analysis | [client-touchpoints-detail.md](./client-touchpoints-detail.md) |
| Friction Points Detail | Full friction analysis | [friction-points-detail.md](./friction-points-detail.md) |
| AS-IS Process Documentation | Operational view | [as-is-process-documentation.md](./as-is-process-documentation.md) |

---

## Change Log

| Date | Contributor | Role | Changes |
|------|-------------|------|---------|
| {{current_date}} | {contributor_name} | {contributor_role} | Initial CX analysis |

---

_Generated by ProcessMiner Client Journey Analyst_
_Document ID: CX-{current_process_id}_

</action>

<action name="finalize_friction_points_file" CRITICAL="MANDATORY">
FINALIZE {frictionPointsFile}:

1. Ensure Executive Summary is complete
2. Add Prioritized Recommendations sections:

## Prioritized Recommendations

### Priority 1: Critical (Address Immediately)

{{#for each p1_friction}}
- **{{fp.id}}: {{fp.name}}** — {{fp.recommendation}}
{{/for}}

### Priority 2: High (Address in First Phase)

{{#for each p2_friction}}
- **{{fp.id}}: {{fp.name}}** — {{fp.recommendation}}
{{/for}}

### Priority 3: Medium (Address in Second Phase)

{{#for each p3_friction}}
- **{{fp.id}}: {{fp.name}}** — {{fp.recommendation}}
{{/for}}

---

3. Add CES Reduction Roadmap:

## CES Reduction Roadmap

### Phase 1: Quick Wins

| Target | Current CES | Post-Phase CES | Reduction |
|--------|-------------|----------------|-----------|
| Total Journey | {{current_ces}} | {{post_phase1_ces}} | {{phase1_reduction}} |

**Friction Points Addressed:** {{phase1_fps}}

### Phase 2: Core Improvements

| Target | Post-Phase 1 CES | Post-Phase CES | Reduction |
|--------|------------------|----------------|-----------|
| Total Journey | {{post_phase1_ces}} | {{post_phase2_ces}} | {{phase2_reduction}} |

**Friction Points Addressed:** {{phase2_fps}}

---

4. Update Change Log entry

</action>

<action name="finalize_touchpoints_file" CRITICAL="MANDATORY">
FINALIZE {clientTouchpointsFile}:

1. Ensure Executive Summary is complete
2. Add CES Contribution Analysis:

## CES Contribution Analysis

### Top CES Contributors

| Rank | JT# | Touchpoint | CES Contribution | % of Total |
|------|-----|------------|------------------|------------|
{{#for top 5 touchpoints by CES}}
| {{rank}} | {{tp.id}} | {{tp.name}} | {{tp.ces}} | {{tp.percentage}}% |
{{/for}}

### CES Reduction Opportunities

| JT# | Touchpoint | Current CES | Potential Reduction | Method |
|-----|------------|-------------|---------------------|--------|
{{#for each reduction_opportunity}}
| {{tp.id}} | {{tp.name}} | {{tp.ces}} | {{tp.potential}} | {{tp.method}} |
{{/for}}

---

3. Add Input for Downstream Agents:

## Input for Downstream Agents

### For Transformation Agent

{{#Write summary of key touchpoints to redesign}}

### For Channel Optimization

{{#Write channel-specific insights}}

---

4. Update Change Log entry

</action>

<verification CRITICAL="MANDATORY">
FINAL VERIFICATION - ALL THREE FILES MUST BE COMPLETE:

{cxJourneyFile}:
- [ ] Executive Summary with 3 narrative paragraphs
- [ ] Key Metrics at a Glance table - ALL values filled
- [ ] CES Baseline Summary table - ALL values filled
- [ ] Section 1: Journey Overview - complete
- [ ] Section 2: Client Touchpoints - complete with diagram
- [ ] Section 3: Moments That Matter - all MTMs listed
- [ ] Section 4: Friction Point Analysis - summary table complete
- [ ] Section 5: CES Analysis - all breakdowns complete
- [ ] Section 6: Channel Analysis - all tables complete
- [ ] Section 7: Enhancement Ideas - catalog complete
- [ ] Section 8: Industry Research - benchmarks and trends
- [ ] Section 9: Inputs for TO-BE Design - all subsections
- [ ] Section 10: Discovery Logging - counts accurate
- [ ] Document Metadata - all confidence values
- [ ] Change Log entry

{frictionPointsFile}:
- [ ] Executive Summary paragraph
- [ ] ALL FP# entries with full detail sections
- [ ] Enhancement Ideas Catalog complete
- [ ] Prioritized Recommendations (P1, P2, P3)
- [ ] CES Reduction Roadmap with phases
- [ ] Traceability Matrix complete
- [ ] Change Log entry

{clientTouchpointsFile}:
- [ ] Executive Summary paragraph
- [ ] ALL JT# entries with full detail sections
- [ ] MTM Assessment for each moment that matters
- [ ] Channel Details for each touchpoint
- [ ] CES Contribution Analysis
- [ ] Channel Distribution and Self-Service tables
- [ ] Wait Point Analysis table
- [ ] Input for Downstream Agents
- [ ] Change Log entry

IF ANY ITEMS ARE INCOMPLETE: Go back and write the missing content before displaying completion message.
</verification>
```

### 10. Completion Message

Display:
```
**CX Journey Analysis Complete!**

Your client experience documentation has been saved:

**Main CX Document:**
- {current_process_folder}/cx-journey-documentation.md

**Detail Documents:**
- {current_process_folder}/friction-points-detail.md
- {current_process_folder}/client-touchpoints-detail.md

**Summary:**
| Element | Count |
|---------|-------|
| Touchpoints Documented | {{count_touchpoints}} |
| Friction Points Identified | {{count_friction_points}} |
| Enhancement Ideas Captured | {{count_enhancement_ideas}} |
| Moments That Matter | {{count_mtm}} |
| Channels Analyzed | {{count_channels}} |

**CES Baseline:**
| Metric | Value |
|--------|-------|
| Current CES | {{total_ces}} |
| Target CES | {{target_ces}} |
| Quick Win CES Reduction | {{quick_win_ces_reduction}} |

**Cross-References:**
- All touchpoints linked to process steps (PS#)
- All friction points linked to touchpoints (JT#)
- Pain points (PP#) cross-referenced where applicable
- Enhancement ideas linked to friction points (FP#)

**Overall Confidence:** {{overall_confidence}}

**Next Steps:**
1. Review the complete CX documentation
2. Share with stakeholders for validation
3. Use as input for TO-BE transformation design

**Companion Documents:**
- [AS-IS Process Documentation](./as-is-process-documentation.md)
- [Pain Points Detail](./pain-points-detail.md)
- [Exceptions Detail](./exceptions-detail.md)
- [Control Points Detail](./control-points-detail.md)
```

---

## CRITICAL STEP COMPLETION NOTE

This is the FINAL step. ONLY WHEN [AI gap analysis complete] and [clarifications addressed] and [all 3 output files finalized], will the workflow be complete.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:
- AI performed gap analysis
- Clarification questions addressed
- Enhancement ideas consolidated and prioritized
- Transformation inputs summarized
- New discoveries logged to AS-IS
- User confirmed completeness
- All 3 output files finalized
- Cross-references validated
- Completion message displayed
- Next steps communicated

### SYSTEM FAILURE:
- Skipped AI gap analysis
- Did not address clarification questions
- Did not consolidate enhancement ideas
- Did not finalize output files
- Did not display completion summary

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
