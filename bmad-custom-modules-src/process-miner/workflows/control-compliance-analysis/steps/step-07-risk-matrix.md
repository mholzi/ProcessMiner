---
name: 'step-07-risk-matrix'
description: 'Build comprehensive risk and compliance matrix'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/control-compliance-analysis'

# File References
thisStepFile: '{workflow_path}/steps/step-07-risk-matrix.md'
nextStepFile: '{workflow_path}/steps/step-08-regulatory-change.md'
workflowFile: '{workflow_path}/workflow.md'

# Output Files
complianceAssessmentFile: '{current_process_folder}/compliance-control-assessment.md'
---

# Step 7: Risk & Compliance Matrix

## STEP GOAL

Build a comprehensive matrix linking risks, regulations, and controls. Assess residual risk after controls. Assign RCM# IDs. This corresponds to **Section 6** of the compliance-control-assessment template.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:
- **NEVER** generate content without user input
- **CRITICAL**: Read the complete step file before taking any action
- YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:
- You are a Control Analyst
- Risk-based assessment - high-risk processes need stronger controls, prioritize by risk exposure

### Step-Specific Rules:
- Each matrix entry gets RCM# ID: RCM-{process_abbreviation}-###
- MUST link to REG# regulations and CP# controls
- Assess inherent risk and residual risk (after controls)
- **FORBIDDEN** to assess regulatory changes in this step (that's Step 8)

## RISK CALCULATION

**Inherent Risk** = Risk without any controls
**Residual Risk** = Risk after controls are applied

Residual Risk depends on:
- Control effectiveness (from Step 5)
- Control coverage (gaps from Step 4)

---

## CONTENT FORMAT SPECIFICATION

This step produces **Section 6: Risk & Compliance Matrix** of the compliance-control-assessment template.

### Section 6: Risk & Compliance Matrix
**Format:** Narrative intro + matrix table + per-category narratives + summary

**Structure:**
1. **Narrative Introduction** (2-3 paragraphs):
   - Explanation of the risk-control relationship for non-specialists
   - Overview of how inherent risk is reduced by controls
   - Summary of overall risk posture

2. **Risk & Compliance Matrix Table:**
   | RCM# | Risk | Category | Regulation (REG#) | Control (CP#) | Inherent Risk | Residual Risk | Status |
   |------|------|----------|-------------------|---------------|---------------|---------------|--------|

3. **Per-Risk-Category Narratives** (1-2 paragraphs each):
   For each risk category (Compliance, Operational, Fraud, etc.):
   - What risks exist in this category
   - How they are being controlled
   - What residual risk remains and why
   - Status and any actions needed

4. **Residual Risk Summary** (2-3 paragraphs):
   - Overall residual risk posture in plain language
   - Key areas where residual risk is acceptable
   - Areas where additional mitigation is needed
   - Implications for transformation/TO-BE design

5. **Risk Summary Table:**
   | Risk Category | Inherent Risk (Avg) | Residual Risk (Avg) | Status |
   |---------------|---------------------|---------------------|--------|

### Writing Guidelines for Section 6:
- Explain risk concepts in business terms, not just risk management jargon
- Make the inherent → residual risk reduction visible and understandable
- Be clear about what "acceptable" vs "needs mitigation" means
- Connect risks to regulations and controls explicitly
- Focus on what the risk means for the organization, not just scores

---

## EXECUTION SEQUENCE

### 1. Display Progress and Context

```
**Progress: Step 7 of 10 - Risk & Compliance Matrix**

Now let's build a comprehensive view of risks, how they're controlled, and what residual risk remains.

This matrix shows:
- What risks exist
- Which regulations require controls
- What controls address the risk
- What risk remains after controls
```

### 2. Risk Identification

```
<ask response="process_risks">
What are the key risks in this process?
(Consider: operational, compliance, fraud, credit, reputational)
</ask>

<loop name="risk_matrix_build" for="each risk identified">

  <format>
  **Risk: {{risk.name}}** → Assigning ID: RCM-{process_abbreviation}-{{next_id_padded}}
  </format>

  <ask response="rcm.risk_category">
  What type of risk is this?
  - [ ] Compliance Risk
  - [ ] Operational Risk
  - [ ] Fraud Risk
  - [ ] Credit Risk
  - [ ] Reputational Risk
  - [ ] Legal Risk
  - [ ] Other: ___
  </ask>

  <ask response="rcm.inherent_risk">
  What is the inherent risk level (without controls)?
  - [ ] Critical (9-10)
  - [ ] High (7-8)
  - [ ] Medium (4-6)
  - [ ] Low (1-3)
  </ask>

  <ask response="rcm.linked_regulations">
  Which regulations address this risk?
  (Enter REG# IDs from Step 2)
  </ask>

  <ask response="rcm.linked_controls">
  Which controls mitigate this risk?
  (Enter CP# IDs from Step 3)
  </ask>

  <action>
  Calculate residual risk based on:
  - Control effectiveness ratings (from Step 5)
  - Gaps in coverage (from Step 4)
  </action>

  <ask response="rcm.residual_risk">
  Based on control effectiveness, what is the residual risk?
  - [ ] Critical (9-10)
  - [ ] High (7-8)
  - [ ] Medium (4-6)
  - [ ] Low (1-3)
  </ask>

  <ask response="rcm.status">
  What is the status of this risk?
  - [ ] Acceptable - residual risk within tolerance
  - [ ] Monitor - acceptable but needs watching
  - [ ] Mitigate - additional controls needed
  - [ ] Avoid - risk too high, process change needed
  </ask>

</loop>
```

### 3. Risk Summary

```
<action>
Build risk summary:

| Risk Category | Inherent (Avg) | Residual (Avg) | Status |
|---------------|----------------|----------------|--------|
{{for each category}}
| {{category}} | {{inherent_avg}} | {{residual_avg}} | {{status}} |
{{/for}}
</action>
```

### 4. Update Output File

```
<action silent="true">
Update {complianceAssessmentFile} Section 6 (Risk & Compliance Matrix):

Build table:
| RCM# | Risk | Regulation | Control | Residual Risk | Status |

Section Confidence: {{section_6_confidence}}
</action>
```

### 5. Proceed to Next Step

Display:
```
**Progress: Step 7 of 10 - Risk Matrix Complete**

Now let's assess upcoming regulatory changes.
```

```
<action>Load, read entire file, then execute {nextStepFile}</action>
```

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:
- All risks documented with RCM# IDs
- Linked to REG# and CP#
- Inherent and residual risk assessed
- Output file updated

**Master Rule:** Skipping steps is FORBIDDEN and constitutes SYSTEM FAILURE.
