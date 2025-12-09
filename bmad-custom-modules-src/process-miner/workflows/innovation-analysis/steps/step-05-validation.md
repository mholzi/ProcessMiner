---
name: 'step-05-validation'
description: 'Final quality assurance, 20-point validation checklist, and executive summary'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/innovation-analysis'

# File References
thisStepFile: '{workflow_path}/steps/step-05-validation.md'
workflowFile: '{workflow_path}/workflow.md'

# Shared Protocols
protocolsFile: '{module_root}/workflows/shared/protocols/protocols.md'

# Scoring Configuration
scoringConfig: '{workflow_path}/config/scoring.yaml'

# Output Files
innovationAnalysisFile: '{current_process_folder}/innovation-analysis.md'
innovationIdeasDetailFile: '{current_process_folder}/innovation-ideas-detail.md'
innovationExportFile: '{current_process_folder}/innovation-analysis.json'

# Source Files
structuredDataFile: '{current_process_folder}/structured-data.json'
asIsDocumentFile: '{current_process_folder}/as-is-process-documentation.md'
painPointsDetailFile: '{current_process_folder}/pain-points-detail.md'

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
---

# Step 5: Validation & Document Completion

## STEP GOAL

Final quality assurance and approval including 20-point validation checklist with pass/fail, executive summary generation, readability check for stakeholders, and version history tracking.

**Progress: Step 5 of 5** | Validation & Finalization | Est. time: 20-30 min

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:
- **NEVER** skip validation checklist items
- **CRITICAL**: Read the complete step file before taking any action
- **CRITICAL**: This is the final step - ensure complete workflow validation
- YOU ARE A FACILITATOR - all checklist items MUST pass before sign-off

### Role Reinforcement:
- You are a Quality Assurance Specialist validating the complete innovation analysis
- Continue using your established name, communication_style, and persona
- We engage in collaborative dialogue, not command-response
- You bring validation expertise and attention to detail, user brings final approval authority

### Step-Specific Rules:
- Run complete 20-point validation checklist
- **FORBIDDEN** to approve with failing checklist items
- Readability check is MANDATORY for non-technical stakeholders

---

## VALIDATION CHECKLIST (20 Points)

### Structural Checks (4 items)

| ID | Check | Criteria |
|----|-------|----------|
| S1 | ID Format | All IDs follow TR-/II-/COMP-/FIN- patterns |
| S2 | ID Consistency | Same IDs used across all sections |
| S3 | Section Complete | All required sections present |
| S4 | No Orphans | No IDs mentioned but not defined |

### Completeness Checks (8 items)

| ID | Check | Criteria |
|----|-------|----------|
| C1 | Market Research | All 6 research categories complete |
| C2 | Backlog Feasibility | All innovations have 6 feasibility dimensions |
| C3 | Backlog Dependencies | All innovations have dependencies captured |
| C4 | Priorities Handoffs | All MUST HAVEs have transformation handoffs |
| C5 | Priorities Metrics | All MUST HAVEs have SMART success metrics |
| C6 | Priorities Risks | All MUST HAVEs have risk mitigation |
| C7 | DEFER Phases | All DEFERs have phase assignment |
| C8 | Pain Point Links | Innovations linked to pain points |

### Quality Checks (4 items)

| ID | Check | Criteria |
|----|-------|----------|
| Q1 | No TBD | No TBD, TODO, or placeholder text |
| Q2 | No Ambiguity | No vague terms without specifics |
| Q3 | SMART Metrics | All metrics are Specific, Measurable, with Timeline |
| Q4 | Actionable | Transformation Agent can act without clarifying questions |

### Actionability Checks (4 items)

| ID | Check | Criteria |
|----|-------|----------|
| A1 | Clear Boundaries | MUST vs SHOULD clearly distinguished |
| A2 | Dependencies Clear | All dependencies explicitly stated |
| A3 | Constraints Clear | All constraints explicitly stated |
| A4 | Integration Points | All integration requirements defined |

---

## PHASE A: ANALYZE [AUTO - NO USER INTERRUPTION]

### A.1 Load Complete Document

Read `{innovationAnalysisFile}` completely - all sections from Steps 1-4.

### A.2 Run Validation Checklist

Execute each of the 20 validation checks:

**Structural:**
- Scan for TR-/II-/COMP-/FIN- pattern compliance
- Cross-reference IDs across sections
- Verify all required sections exist
- Check for orphaned ID references

**Completeness:**
- Count market research categories (need 6)
- Verify 6 dimensions per innovation in backlog
- Check dependencies captured for each
- Verify MUST HAVEs have handoffs, metrics, risks
- Verify DEFERs have phase assignments
- Check pain point linkage

**Quality:**
- Search for TBD, TODO, placeholder text
- Flag vague terms ("soon", "later", "some")
- Validate SMART metric structure
- Assess if Transformation Agent could proceed

**Actionability:**
- Review MUST/SHOULD boundary clarity
- Check dependency documentation
- Review constraint documentation
- Verify integration requirements

### A.3 Output: Validation Results

Create results summary:
- Pass count: [X]/20
- Fail count: [Y]/20
- Failing items: [List with details]

**[Proceed directly to Phase C - No external research for finalization]**

---

## PHASE C: ELICIT [INTERACTIVE - ONE TOPIC AT A TIME]

---

### TOPIC 1: Validation Checklist Results

Present 20-point checklist results:

```
**Validation Results: {{pass_count}}/20 Passing**

**Structural (S1-S4):**
| ID | Check | Result | Issue |
|----|-------|--------|-------|
| S1 | ID Format | {{result}} | {{issue_if_any}} |
| S2 | ID Consistency | {{result}} | {{issue_if_any}} |
| S3 | Section Complete | {{result}} | {{issue_if_any}} |
| S4 | No Orphans | {{result}} | {{issue_if_any}} |

**Completeness (C1-C8):**
| ID | Check | Result | Issue |
|----|-------|--------|-------|
| C1 | Market Research | {{result}} | {{issue_if_any}} |
| C2 | Backlog Feasibility | {{result}} | {{issue_if_any}} |
| C3 | Backlog Dependencies | {{result}} | {{issue_if_any}} |
| C4 | Priorities Handoffs | {{result}} | {{issue_if_any}} |
| C5 | Priorities Metrics | {{result}} | {{issue_if_any}} |
| C6 | Priorities Risks | {{result}} | {{issue_if_any}} |
| C7 | DEFER Phases | {{result}} | {{issue_if_any}} |
| C8 | Pain Point Links | {{result}} | {{issue_if_any}} |

**Quality (Q1-Q4):**
| ID | Check | Result | Issue |
|----|-------|--------|-------|
| Q1 | No TBD | {{result}} | {{issue_if_any}} |
| Q2 | No Ambiguity | {{result}} | {{issue_if_any}} |
| Q3 | SMART Metrics | {{result}} | {{issue_if_any}} |
| Q4 | Actionable | {{result}} | {{issue_if_any}} |

**Actionability (A1-A4):**
| ID | Check | Result | Issue |
|----|-------|--------|-------|
| A1 | Clear Boundaries | {{result}} | {{issue_if_any}} |
| A2 | Dependencies Clear | {{result}} | {{issue_if_any}} |
| A3 | Constraints Clear | {{result}} | {{issue_if_any}} |
| A4 | Integration Points | {{result}} | {{issue_if_any}} |
```

**IF failures exist:**

```
**Items Requiring Attention:**

{{for each failing_item}}
- **{{item.id}}**: {{item.check}}
  Issue: {{item.issue}}
  Fix: {{item.suggested_fix}}
{{/for}}
```

**Ask:** "Would you like to fix these issues now?"
- IF yes: Work through each failing item
- IF no: "Which issues should we prioritize?"

**Require all 20 to pass before sign-off.**

---

### TOPIC 2: Readability Check

Present readability assessment:

```
**Readability Assessment**

**Potential Issues for Non-Technical Reviewers:**
- Jargon terms: {{jargon_list}}
- Undefined acronyms: {{acronym_list}}
- Complex sentences: {{complex_sentence_count}}
```

**Ask:** "Will non-technical reviewers (executives, business stakeholders) read this document? Should we add a glossary or simplify any sections?"

---

### TOPIC 3: Transformation Readiness

Simulate Transformation Agent consuming document:

```
**Transformation Agent Readiness Check**

**Can the Transformation Agent proceed with:**

| Question | Answer |
|----------|--------|
| MUST HAVEs clearly defined? | {{yes_no}} |
| Success metrics verifiable? | {{yes_no}} |
| Constraints explicit? | {{yes_no}} |
| Dependencies mapped? | {{yes_no}} |
| Blocking questions? | {{questions_if_any}} |
```

**Ask:** "Is this clear enough for the Transformation Agent to proceed without clarifying questions? Any additional context needed?"

---

### TOPIC 4: Executive Summary

Present draft Executive Summary:

```
**EXECUTIVE SUMMARY**

**Process:** {current_process_name}
**Bank:** {bank_name}
**Analysis Date:** {{date}}
**Analyst:** {contributor_name}

**Key Findings:**
- Total Innovations Identified: {{total_innovations}}
- MUST HAVE (immediate): {{must_count}}
- SHOULD HAVE (next phase): {{should_count}}
- COULD HAVE (if capacity): {{could_count}}
- DEFER (future phases): {{defer_count}}

**Top 3 MUST HAVE Innovations:**
1. **II-{{seq}}**: {{name}} - {{one_line_description}}
2. **II-{{seq}}**: {{name}} - {{one_line_description}}
3. **II-{{seq}}**: {{name}} - {{one_line_description}}

**Key Metrics:**
| Metric | Target | Timeline |
|--------|--------|----------|
| {{metric_1}} | {{target}} | {{timeline}} |
| {{metric_2}} | {{target}} | {{timeline}} |
| {{metric_3}} | {{target}} | {{timeline}} |

**Investment Estimate:** {{total_investment_range}}
**Expected Value:** {{total_value_estimate}}

**Key Risks:**
1. {{risk_1}}
2. {{risk_2}}
3. {{risk_3}}

**Recommendation:**
{{recommendation_summary}}
```

**Ask:** "Does this Executive Summary capture the key messages? Any changes needed?"

---

### TOPIC 5: Final Document Update

Confirm finalization:

```
**Document Finalization**

The following updates will be applied:

1. Insert Executive Summary at document start
2. Add Sign-Off section at document end
3. Update Status: "draft" → "complete"
4. Set Version: "1.0"
5. Add Version History entry
6. Generate JSON export (if requested)
```

**Ask:** "Ready to finalize the document? [Y] Yes | [N] No - need more changes"

---

## FINALIZATION ACTIONS

**On Final Approval:**

1. **Update Document Status:**
   - Change frontmatter status: "draft" → "complete"
   - Set version: "1.0"

2. **Insert Executive Summary:**
   - Add as Section 1 of the document
   - Include key metrics and recommendations

3. **Append Final Sections:**
   - Section 9: Investment Analysis (cost estimates, ROI projections)
   - Section 10: Risk & Mitigation (consolidated risk table)
   - Section 11: Success Metrics (KPI framework, measurement plan)
   - Section 12: Appendices (research sources, glossary, change log)

4. **Add Version History:**
   ```
   | Version | Date | Author | Changes |
   |---------|------|--------|---------|
   | 1.0 | {{date}} | {contributor_name} | Initial release |
   ```

5. **Update frontmatter:**
   - Add "step-05" to stepsCompleted array
   - Mark workflow as complete

6. **Finalize Innovation Ideas Detail File:**
   - Update `{innovationIdeasDetailFile}` with any fixes made during validation:
     - Apply checklist item fixes to individual innovation entries
     - Update executive summary section in detail file
     - Finalize statistics with accurate counts
     - Update change log with final entry
   - Change status: "draft" → "complete"
   - Set version: "1.0"

---

## COMPLETION MESSAGE

Display:

```
**Innovation Analysis Complete!**

Your innovation analysis has been saved:

**Output Documents:**
- {current_process_folder}/innovation-analysis.md (Main document)
- {current_process_folder}/innovation-ideas-detail.md (Detailed innovation log)

**Summary:**
| Element | Count |
|---------|-------|
| Market Trends Identified | {{trend_count}} |
| Competitors Analyzed | {{competitor_count}} |
| Fintechs Assessed | {{fintech_count}} |
| Innovation Ideas Generated | {{innovation_count}} |
| MUST HAVE Priorities | {{must_count}} |
| SHOULD HAVE Priorities | {{should_count}} |
| Deferred to Future | {{defer_count}} |

**Validation:**
- Checklist: {{pass_count}}/20 passing
- Status: Complete
- Version: 1.0
- Date: {{date}}

**Cross-References:**
- All innovations linked to pain points (PP#)
- Market trends (TR#) linked to innovations (II#)
- Competitors (COMP#) and fintechs (FIN#) assessed
- MUST HAVEs have full transformation handoffs

**Next Steps:**
1. Review the complete innovation analysis document
2. Share with stakeholders for validation
3. Use as input for TO-BE transformation design
4. Monitor deferred items for future consideration

**Companion Documents:**
- [AS-IS Process Documentation](./as-is-process-documentation.md)
- [Pain Points Detail](./pain-points-detail.md)
- [Innovation Ideas Detail](./innovation-ideas-detail.md)
- [Structured Data](./structured-data.json)
```

---

## WORKFLOW COMPLETE

The Innovation Analysis workflow is now complete. The document is ready for:
- Transformation Agent consumption
- Stakeholder review
- Executive presentation
- Strategic planning input

**No further steps in this workflow.**

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:
- All 20 validation checklist items pass (Structural, Completeness, Quality, Actionability)
- No TBD, TODO, or placeholder text remains in document
- Readability check completed for non-technical stakeholders
- Transformation Agent simulation confirms document is actionable
- Executive Summary approved with key findings and recommendations
- Document status updated to "complete" with version 1.0
- Version history added to document
- All sections finalized (including Investment, Risk, Metrics, Appendices)
- Innovation Ideas Detail file (innovation-ideas-detail.md) finalized and marked complete

### SYSTEM FAILURE:
- Approving document with failing validation checklist items
- Skipping readability check when non-technical reviewers expected
- Generating incomplete or inaccurate executive summary
- Leaving document status as "draft"
- Missing required sections
- Not finalizing innovation-ideas-detail.md alongside main document

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
