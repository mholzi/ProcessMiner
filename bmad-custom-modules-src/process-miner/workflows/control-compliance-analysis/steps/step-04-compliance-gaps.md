---
name: 'step-04-compliance-gaps'
description: 'Analyze compliance gaps between requirements and controls'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/control-compliance-analysis'

# File References
thisStepFile: '{workflow_path}/steps/step-04-compliance-gaps.md'
nextStepFile: '{workflow_path}/steps/step-05-effectiveness.md'
workflowFile: '{workflow_path}/workflow.md'

# Shared Protocols
protocolsFile: '{module_root}/workflows/shared/protocols/protocols.md'

# Output Files
complianceAssessmentFile: '{current_process_folder}/compliance-control-assessment.md'

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
---

# Step 4: Compliance Gap Analysis

## STEP GOAL

Identify gaps between regulatory requirements and existing controls. Assess risk exposure for each gap and determine remediation priority. Assign GAP# IDs. This corresponds to **Section 3** of the compliance-control-assessment template.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:
- **NEVER** generate content without user input
- **CRITICAL**: Read the complete step file before taking any action
- **CRITICAL**: When loading next step, ensure entire file is read
- YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:
- You are a Control Analyst (Compliance & Control Specialist)
- Continue using your established name, communication_style, and persona
- Direct about gaps and risks - no sugar-coating, no diplomatic hedging
- Risk-based assessment - high-risk processes need stronger controls

### Step-Specific Rules:
- Each gap gets a unique GAP# ID using format: GAP-{process_abbreviation}-### (e.g., GAP-ONB-001)
- MUST link gaps to REG# requirements
- MUST link gaps to affected CP# controls (or note absence)
- Assess risk exposure for each gap
- **FORBIDDEN** to assess control effectiveness in this step (that's Step 5)

## RISK LEVEL REFERENCE

| Risk Level | Score | Response Time | Examples |
|------------|-------|---------------|----------|
| Critical | 9-10 | Immediate | Regulatory sanction risk, material breach |
| High | 7-8 | 30 days | Significant compliance exposure |
| Medium | 4-6 | 90 days | Non-critical but requires attention |
| Low | 1-3 | Next review cycle | Minor, best-practice improvement |

## EXECUTION PROTOCOLS

- Load protocols from `{protocolsFile}` for elicitation techniques
- Reference regulations (REG#) and controls (CP#) from previous steps
- Systematically compare requirements to controls
- Use advanced-elicitation-task for root cause analysis

## CONTEXT BOUNDARIES

- Session initialized in Step 1
- Regulations mapped in Step 2 with REG# IDs
- Controls cataloged in Step 3 with CP# IDs
- This step identifies where controls are missing or insufficient

---

## CONTENT FORMAT SPECIFICATION

This step produces **Section 3: Compliance Gap Analysis** of the compliance-control-assessment template.

### Section 3.1: Current vs Required
**Format:** Narrative overview + table + per-gap detail blocks

**Structure:**
1. **Narrative Overview** (2-3 paragraphs):
   - Summary of the gap analysis findings
   - Overall compliance posture assessment
   - Key areas of concern for non-specialist readers

2. **Gap Summary Table:**
   | GAP# | Requirement (REG#) | Current State | Gap Description | Risk Level | Priority |
   |------|-------------------|---------------|-----------------|------------|----------|

3. **Per-Gap Detail Blocks** (for Critical and High risk gaps):
   Each block includes 1-2 paragraphs covering:
   - What the requirement demands
   - What is currently in place (or missing)
   - Why this gap matters (risk implications)
   - Recommended remediation approach

### Section 3.2: Risk Exposure
**Format:** Narrative summary + table

**Structure:**
1. **Narrative Summary** (2-3 paragraphs):
   - Overall risk exposure assessment in plain language
   - Explanation of what the risk levels mean for the organization
   - Key risk areas that need attention

2. **Risk Exposure Table:**
   | Risk Level | Gap Count | Key Areas Affected | Remediation Urgency |
   |------------|-----------|-------------------|---------------------|
   | Critical   | X         | ...               | Immediate           |
   | High       | X         | ...               | 30 days             |
   | Medium     | X         | ...               | 90 days             |
   | Low        | X         | ...               | Next review cycle   |

### Section 3.3: Remediation Needs
**Format:** Narrative intro + prioritized table

**Structure:**
1. **Narrative Introduction** (1-2 paragraphs):
   - Overview of remediation approach
   - Key themes in remediation needs

2. **Remediation Table:**
   | GAP# | Remediation Action | Owner | Priority | Target Completion |
   |------|-------------------|-------|----------|-------------------|

### Writing Guidelines for Section 3:
- Be direct about gaps - no sugar-coating or diplomatic hedging
- Explain risk implications in business terms, not just compliance terms
- Make it clear WHY each gap matters to someone unfamiliar with the details
- Prioritize clarity over comprehensiveness in narratives
- Ensure remediation actions are specific and actionable

---

## EXECUTION SEQUENCE

### 1. Display Progress and Context

```
**Progress: Step 4 of 10 - Compliance Gap Analysis**

Now let's identify where requirements lack adequate controls.

A gap exists when:
- A regulatory requirement has NO control
- A control exists but doesn't FULLY address the requirement
- A control exists but is INEFFECTIVE (we'll assess this in Step 5)

**Regulatory Requirements Summary:**
| REG# | Regulation | Requirements | Controls Mapped |
|------|------------|--------------|-----------------|
{{for each regulation}}
| {{reg.id}} | {{reg.name}} | {{req_count}} | {{control_count}} |
{{/for}}
```

### 2. Automated Gap Detection

```
<action>
Analyze regulatory requirements vs control coverage:

For each REG# regulation:
1. List specific requirements from that regulation
2. Check which CP# controls are linked
3. Identify requirements with:
   - NO control linked
   - PARTIAL control coverage
   - MULTIPLE controls (potential overlap)

Generate preliminary gap list.
</action>

<format>
**Preliminary Gap Analysis:**

| Requirement | Status | Controls | Potential Gap |
|-------------|--------|----------|---------------|
{{for each requirement}}
| {{reg_id}}: {{requirement}} | {{status}} | {{linked_controls}} | {{gap_indicator}} |
{{/for}}

Let's review each potential gap.
</format>
```

### 3. Gap Confirmation and Details

```
<loop name="gap_review" for="each potential gap identified">

  <format>
  ---
  **Potential Gap: {{requirement.text}}**
  Regulation: {{requirement.reg_id}}
  Current Controls: {{requirement.linked_controls OR 'None'}}
  </format>

  <ask response="is_actual_gap">
  Is this an actual compliance gap?

  - [ ] Yes - this is a gap
  - [ ] No - requirement is adequately addressed
  - [ ] Partial - control exists but doesn't fully address
  </ask>

  <check if="is_actual_gap == 'Yes' OR is_actual_gap == 'Partial'">

    <format>
    **Gap Confirmed** → Assigning ID: GAP-{process_abbreviation}-{{next_id_padded}}
    </format>

    <ask response="gap.description">
    Describe the gap:
    - What is required?
    - What is missing or insufficient?
    </ask>

    <ask response="gap.current_state">
    What is the current state? How is this handled today (if at all)?
    </ask>

    <ask response="gap.risk_level">
    What is the risk level of this gap?

    - [ ] Critical (9-10) - Regulatory sanction risk, material breach
    - [ ] High (7-8) - Significant compliance exposure
    - [ ] Medium (4-6) - Non-critical but requires attention
    - [ ] Low (1-3) - Minor, best-practice improvement
    </ask>

    <ask response="gap.risk_description">
    What specific risk does this gap create?
    (e.g., regulatory finding, financial loss, reputational damage)
    </ask>

    <ask response="gap.remediation_priority">
    What is the remediation priority?

    - [ ] Immediate - must fix now
    - [ ] High - within 30 days
    - [ ] Medium - within 90 days
    - [ ] Low - next review cycle
    </ask>

    <ask response="gap.remediation_approach">
    What remediation is needed?
    (e.g., new control, strengthen existing control, automate)
    </ask>

    <ask response="gap.owner">
    Who should own the remediation?
    </ask>

  </check>

</loop>
```

### 4. Additional Gaps

```
<ask response="additional_gaps">
Are there any other compliance gaps not identified above?
(e.g., gaps you're aware of from audits, self-assessments)

- [ ] Yes - I'll add more
- [ ] No - we've covered them all
</ask>

<check if="additional_gaps == 'Yes'">
  <loop name="additional_gap_capture" until="user says done">
    <!-- Capture full gap details as in Section 3 -->
    <ask response="gap.requirement">What requirement is not being met?</ask>
    <ask response="gap.regulation">Which regulation (REG#) requires this?</ask>
    <!-- Continue with all gap fields -->
  </loop>
</check>
```

### 5. Risk Exposure Summary

```
<action>
Calculate overall risk exposure:

| Risk Level | Gap Count | Remediation Needed |
|------------|-----------|-------------------|
| Critical | {{critical_count}} | Immediate |
| High | {{high_count}} | 30 days |
| Medium | {{medium_count}} | 90 days |
| Low | {{low_count}} | Next cycle |

Total Gaps: {{total_gaps}}
Highest Risk: {{highest_risk_level}}
</action>

<format>
**Risk Exposure Summary:**

{{risk_exposure_narrative}}

Top 3 Risk Areas:
1. {{top_risk_1}}
2. {{top_risk_2}}
3. {{top_risk_3}}
</format>
```

### 6. Capture Confidence

```
<ask response="section_3_confidence">
How confident are you in the gap analysis?

- [ ] High - comprehensive, validated by audit/legal
- [ ] Medium - good coverage, may have missed some
- [ ] Low - preliminary, needs validation
</ask>

<ask response="section_3_confidence_basis">
What's the basis for this confidence? (e.g., recent audit, self-assessment, assumption)
</ask>
```

### 7. Update Output File

```
<action silent="true">
Update {complianceAssessmentFile} Section 3 (Compliance Gap Analysis):

3.1 Current vs Required:
Build gap table:
| GAP# | Requirement | Current State | Gap Description | Risk Level | Remediation Priority |

3.2 Risk Exposure:
Risk exposure narrative and summary table

3.3 Remediation Needs:
Prioritized list of remediation actions with owners

Section Confidence: {{section_3_confidence}}
Confidence Basis: {{section_3_confidence_basis}}
</action>
```

### 8. Summary and Transition

Display:
```
**Compliance Gap Analysis Complete**

| Metric | Value |
|--------|-------|
| Total Gaps Identified | {{total_gaps}} |
| Critical Risk Gaps | {{critical_count}} |
| High Risk Gaps | {{high_count}} |
| Medium Risk Gaps | {{medium_count}} |
| Low Risk Gaps | {{low_count}} |
| Immediate Remediation Needed | {{immediate_count}} |
| Confidence | {{section_3_confidence}} |

**Priority Gaps:**
{{#each priority_gaps}}
- GAP-{process_abbreviation}-{{id}}: {{description}} ({{risk_level}})
{{/each}}

Next, we'll assess the effectiveness of existing controls.
```

### 9. Proceed to Next Step

Display:
```
**Progress: Step 4 of 10 - Gap Analysis Complete**

Now let's assess how effective your existing controls are.
```

```
<action>Load, read entire file, then execute {nextStepFile}</action>
```

---

## CRITICAL STEP COMPLETION NOTE

This is an auto-proceed step. IMMEDIATELY after [gaps identified] and [output file updated], load and read fully `{nextStepFile}` to execute and begin control effectiveness assessment.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:
- All gaps identified with GAP# IDs in correct format
- Each gap linked to REG# requirement
- Risk level and priority assessed for each gap
- Remediation approach captured
- Risk exposure summarized
- Confidence assessment captured
- Output file updated
- Ready to proceed to Step 5

### SYSTEM FAILURE:
- Did not assign GAP# IDs
- Did not link to REG# requirements
- Did not assess risk levels
- Started assessing control effectiveness
- Did not update output file
- Skipped to later steps

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
