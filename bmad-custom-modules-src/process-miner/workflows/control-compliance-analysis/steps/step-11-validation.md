---
name: 'step-11-validation'
description: 'Final review, AI-driven gap analysis, and document generation'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/control-compliance-analysis'

# File References
thisStepFile: '{workflow_path}/steps/step-11-validation.md'
workflowFile: '{workflow_path}/workflow.md'

# Shared Protocols
protocolsFile: '{module_root}/workflows/shared/protocols/protocols.md'

# Output Files
complianceAssessmentFile: '{current_process_folder}/compliance-control-assessment.md'
controlPointsDetailFile: '{current_process_folder}/control-points-detail.md'

# Source Files
structuredDataFile: '{current_process_folder}/structured-data.json'
asIsDocumentFile: '{current_process_folder}/as-is-process-documentation.md'

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
---

# Step 11: Validation & Document Completion

## STEP GOAL

Perform final review of all captured compliance content. AI analyzes for gaps, ambiguities, and inconsistencies. Finalize documentation with executive summary and complete traceability.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:
- **NEVER** generate content without user input
- **CRITICAL**: Read the complete step file before taking any action
- YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:
- You are a Control Analyst
- Maintain precision and regulatory accuracy
- Ensure complete traceability from requirements to controls to evidence

### AI-Driven Assessment:
- AI MUST actively analyze captured content
- Surface gaps, ambiguities, inconsistencies
- Ask clarification questions before declaring complete

### Step-Specific Rules
- This is the FINAL step — no step-12 exists
- Both output files must be finalized
- SME must confirm completeness
- All cross-references must be validated

---

## CONTENT FORMAT SPECIFICATION

This step produces the **Executive Summary** and finalizes both output documents.

### Executive Summary
**Format:** Narrative paragraphs + key metrics table

**Structure:**
1. **Narrative Summary** (3-4 paragraphs):
   - **Paragraph 1 - Scope & Context**: What process was analyzed, why this compliance assessment was conducted, and the regulatory context
   - **Paragraph 2 - Key Findings**: Summary of the most important findings (control strengths, gaps, risk areas) written for a non-specialist executive audience
   - **Paragraph 3 - Risk Posture**: Overall compliance and risk posture, what it means for the organization, and any urgent concerns
   - **Paragraph 4 - Recommended Actions**: High-level summary of priority actions and next steps

2. **Key Metrics Table:**
   | Metric | Value |
   |--------|-------|
   | Total Regulations Mapped | X |
   | Total Control Points | X |
   | Compliance Gaps Identified | X |
   | Critical/High Risk Gaps | X |
   | Open Audit Findings | X |
   | Average Control Effectiveness | X/5 |
   | Controls Needing Improvement | X |
   | Improvement Recommendations | X |

3. **Confidence Summary Table:**
   | Section | Confidence Level |
   |---------|-----------------|
   | Regulatory Framework | High/Medium/Low |
   | Control Inventory | High/Medium/Low |
   | ... | ... |
   | **Overall** | **X** |

### Document Finalization Checklist
Before completing, ensure:
- [ ] All sections have narrative introductions
- [ ] All tables are properly formatted
- [ ] All cross-references are valid (REG# → CP# → PS#)
- [ ] Traceability is complete and verifiable
- [ ] Executive summary accurately reflects content
- [ ] Writing is accessible to non-specialists
- [ ] Change log is updated

### Writing Guidelines for Executive Summary:
- Write for executives who need the key points quickly
- Avoid jargon - use plain business language
- Lead with the most important findings
- Be direct about risks and gaps
- End with clear, actionable next steps
- Keep it concise but comprehensive enough to stand alone

---

## EXECUTION SEQUENCE

### 1. Display Progress and Summary

```
**Progress: Step 11 of 11 - Final Review**

Excellent work! Let me summarize what we've captured:

**Compliance Assessment Summary:**

| Category | Count |
|----------|-------|
| Regulations (REG#) | {{reg_count}} |
| Control Points (CP#) | {{cp_count}} |
| Compliance Gaps (GAP#) | {{gap_count}} |
| Effectiveness Assessments (CEA#) | {{cea_count}} |
| Audit Trail Requirements (ATR#) | {{atr_count}} |
| Risk Matrix Entries (RCM#) | {{rcm_count}} |
| Regulatory Changes (RCI#) | {{rci_count}} |
| Open Audit Findings (OAF#) | {{oaf_count}} |
| Improvement Recommendations (CIR#) | {{cir_count}} |

**Risk Summary:**
| Risk Level | Count | Residual Risk |
|------------|-------|---------------|
| Critical | {{critical_count}} | {{critical_residual}} |
| High | {{high_count}} | {{high_residual}} |
| Medium | {{medium_count}} | {{medium_residual}} |
| Low | {{low_count}} | {{low_residual}} |

**Control Effectiveness:**
- Average Effectiveness: {{avg_effectiveness}}/5
- Controls Needing Improvement: {{needs_improvement_count}}

**Compliance Gaps:**
- Total Gaps: {{gap_count}}
- Immediate Remediation: {{immediate_remediation_count}}
```

### 2. AI-Driven Gap Analysis

```
<critical name="AI_ASSESSMENT">
Before asking the user if they're done, the AI MUST actively analyze the captured content
and identify any gaps, ambiguities, or inconsistencies that need clarification.
</critical>

<action>Analyze all captured compliance content and identify:
  1. **Coverage Gaps** - Requirements without controls, risks without mitigation
  2. **Traceability Gaps** - Items not properly cross-referenced
  3. **Ambiguities** - Vague requirements, unclear control activities
  4. **Inconsistencies** - Conflicting effectiveness ratings, mismatched risk levels
  5. **Missing Elements** - Incomplete control entries, missing evidence specifications
</action>

<action>Generate list of clarification questions (0 to N items)</action>
```

### 3. Handle Clarification Questions

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
  </loop>
</check>

<check if="clarification_questions.length == 0">
  <format>
  ---
  **Review Assessment**

  I've reviewed everything we captured — no gaps or inconsistencies found.
  The compliance documentation looks complete and internally consistent.
  </format>
</check>
```

### 4. Traceability Validation

```
<action>
Validate complete traceability:

**Requirement → Control Traceability:**
| REG# | Requirements | CP# Linked | Coverage |
{{for each regulation}}
| {{reg.id}} | {{req_count}} | {{cp_count}} | {{coverage_pct}}% |
{{/for}}

**Control → Evidence Traceability:**
| CP# | Control | ATR# Linked | Evidence Complete |
{{for each control}}
| {{cp.id}} | {{cp.name}} | {{atr_id}} | {{evidence_status}} |
{{/for}}
</action>

<ask response="traceability_confirmed">
Does this traceability look correct?
- [ ] Yes - traceability is complete
- [ ] No - some gaps need addressing
</ask>
```

### 5. User Final Confirmation

```
<ask response="user_additions">
Anything else you'd like to add or correct before we finalize?

- [ ] Yes, I have additions
- [ ] No, looks good — finalize it
</ask>
```

### 6. Calculate Overall Confidence

```
<action>
Calculate overall document confidence:

| Section | Confidence |
|---------|------------|
| 1. Regulatory Framework | {{section_1_confidence}} |
| 2. Control Inventory | {{section_2_confidence}} |
| 3. Compliance Gaps | {{section_3_confidence}} |
| 4. Control Effectiveness | {{section_4_confidence}} |
| 5. Audit Trail | {{section_5_confidence}} |
| 6. Risk Matrix | {{section_6_confidence}} |
| 7. Regulatory Change | {{section_7_confidence}} |
| 8. Open Audit Findings | {{section_8_confidence}} |
| 9. Recommendations | {{section_9_confidence}} |

Overall Confidence: {{calculate_overall_confidence}}
</action>
```

### 7. Finalize All Output Files

```
<action silent="true">Finalize {complianceAssessmentFile} with:
- Executive Summary (auto-generate from captured data)
- All sections complete with cross-references
- Traceability matrices
- Document Metadata (contributors, dates, method)
- Overall Document Confidence table
- Change Log entry
</action>

<action silent="true">Finalize {controlPointsDetailFile} with:
- Executive Summary
- Control Point Summary Table
- Control Statistics
- Regulatory Coverage Matrix
- Control Type Breakdown
- All CP# entries complete
- Control Framework Analysis
- Segregation of Duties Matrix
- Audit Readiness Assessment
- Recommendations
- Input for Downstream Agents
- Regulatory Quick Reference
- Change Log entry
</action>
```

### 8. Completion Message

Display:
```
**Compliance & Control Analysis Complete!**

Your compliance documentation has been saved:

**Main Assessment Document:**
- {current_process_folder}/compliance-control-assessment.md

**Detail Document:**
- {current_process_folder}/control-points-detail.md

**Summary:**
| Category | Count |
|----------|-------|
| Regulations Mapped | {{reg_count}} |
| Controls Documented | {{cp_count}} |
| Compliance Gaps | {{gap_count}} |
| Open Audit Findings | {{oaf_count}} |
| Improvement Recommendations | {{cir_count}} |

**Risk Profile:**
| Metric | Value |
|--------|-------|
| Highest Risk Level | {{highest_risk}} |
| Gaps Requiring Immediate Action | {{immediate_gaps}} |
| Average Control Effectiveness | {{avg_effectiveness}}/5 |

**Traceability:**
- All regulations linked to controls (REG# → CP#)
- All controls linked to process steps (CP# → PS#)
- All controls linked to audit evidence (CP# → ATR#)
- All gaps linked to remediation (GAP# → CIR#)
- All audit findings linked to controls (OAF# → CP#)

**Overall Confidence:** {{overall_confidence}}

**Next Steps:**
1. Review the complete compliance documentation
2. Address critical and high-priority gaps
3. Implement control improvement recommendations
4. Use as input for TO-BE transformation design

**Companion Documents:**
- [AS-IS Process Documentation](./as-is-process-documentation.md)
- [Pain Points Detail](./pain-points-detail.md)
- [Exceptions Detail](./exceptions-detail.md)
```

---

## CRITICAL STEP COMPLETION NOTE

This is the FINAL step. ONLY WHEN [AI gap analysis complete] and [clarifications addressed] and [all output files finalized], will the workflow be complete.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:
- AI performed gap analysis
- Clarification questions addressed
- Traceability validated
- User confirmed completeness
- Both output files finalized
- Executive summary generated
- Completion message displayed
- Next steps communicated

### SYSTEM FAILURE:
- Skipped AI gap analysis
- Did not validate traceability
- Did not address clarification questions
- Did not finalize output files
- Did not display completion summary

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
