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

## CONTENT FORMAT SPECIFICATION

This section defines the exact formatting requirements for Section 1 (Executive Summary), Section 10 (Risk & Mitigation), Section 11 (Success Metrics), and Section 12 (Appendices). The AI MUST follow these specifications when generating content.

**NOTE:** Section 9 (Investment Analysis) has been removed from this workflow — no cost estimates or ROI projections are included.

### Section 1: Executive Summary

**Format:**
- **Structure**: Narrative paragraphs + embedded key metrics table
- **Content**: 3-4 paragraphs summarizing key findings and recommendations with metrics table

**Paragraph Structure:**
1. **Context & Scope**: What was analyzed and why
2. **Key Findings**: Major discoveries from market research and innovation identification
3. **Priorities**: MUST HAVE innovations and their strategic importance
4. **Recommendation**: Clear call to action

**Key Metrics Table:**
| Metric | Value |
|--------|-------|
| Innovations Identified | [count] |
| MUST HAVE | [count] |
| SHOULD HAVE | [count] |
| COULD HAVE | [count] |
| DEFER | [count] |
| Market Trends Analyzed | [count] |
| Competitors Assessed | [count] |

**Example - Executive Summary:**
```
## 1. Executive Summary

This innovation analysis examined the SME Onboarding process at Example Bank, identifying opportunities to transform the client experience and operational efficiency. The analysis encompassed market research across 5 competitors and 7 fintech disruptors, assessment of 12 technology trends, and generation of 15 innovation ideas with feasibility scoring.

| Metric | Value |
|--------|-------|
| Innovations Identified | 15 |
| MUST HAVE | 3 |
| SHOULD HAVE | 4 |
| COULD HAVE | 5 |
| DEFER | 3 |
| Market Trends Analyzed | 12 |
| Competitors Assessed | 12 |

The analysis reveals that Example Bank has significant opportunity to improve competitive positioning through three MUST HAVE innovations: AI-powered document extraction (II-ONB-001), automated decisioning for simple structures (II-ONB-004), and real-time status notifications (II-ONB-005). Together, these innovations address the top client pain points and enable same-day processing for 60% of applications — matching the best-in-class fintech experience.

The recommendation is to proceed with transformation planning incorporating all three MUST HAVE innovations as core requirements. The SHOULD HAVE innovations (video verification, mobile application) should be included if feasible, with regulatory engagement initiated immediately for video verification. Deferred items should be monitored against their trigger conditions for future inclusion.
```

### Section 10: Risk & Mitigation

#### 10.1 Innovation Risks Table

| Column | Content | Formatting Rules |
|--------|---------|------------------|
| **Risk ID** | Risk identifier | Format: RISK-### |
| **Risk Description** | What could go wrong | 1-2 sentences |
| **Likelihood** | Probability of occurrence | High / Medium / Low |
| **Impact** | Severity if occurs | High / Medium / Low |
| **Mitigation Strategy** | How to prevent or reduce | 1-2 sentences |

**Example - Innovation Risks Table:**
```
| Risk ID | Risk Description | Likelihood | Impact | Mitigation Strategy |
|---------|------------------|------------|--------|---------------------|
| RISK-001 | AI document extraction accuracy below 95% threshold | Medium | High | Extensive testing with diverse document samples; parallel running before cutover |
| RISK-002 | Regulatory rejection of automated decisioning | Low | High | Early engagement with compliance; document audit trail requirements |
| RISK-003 | Client adoption of video verification lower than expected | Medium | Medium | A/B testing with client segments; maintain branch option as fallback |
| RISK-004 | Integration complexity exceeds estimates | Medium | Medium | Proof of concept phase before commitment; vendor technical assessment |
| RISK-005 | Resource constraints delay implementation | High | Medium | Prioritize MUST HAVEs; phase implementations to match capacity |
```

#### 10.2 Risk Mitigation Plan

**Format:**
- **Structure**: Overall narrative + per-risk detail blocks + grouped by risk category
- **Overall Narrative**: 1-2 paragraphs on risk management approach
- **Per-Risk Blocks**: Key risks get detailed mitigation sections
- **Category Grouping**: Risks grouped by type (Technical, Regulatory, Adoption, Resource, etc.)

**Example - Risk Mitigation Plan:**
```
### 10.2 Risk Mitigation Plan

The risk mitigation strategy focuses on early validation and phased deployment. Rather than big-bang implementations, each MUST HAVE innovation will follow a proof-of-concept approach, validating key assumptions before full commitment. This approach reduces the impact of risks materializing by catching issues early when course correction is cheaper.

For high-impact risks, specific mitigation actions are assigned with clear ownership. The compliance team is engaged from project initiation for regulatory risks, while technical risks are addressed through vendor assessments and proof-of-concept phases.

#### Technical Risks

**RISK-001: AI document extraction accuracy below 95% threshold**

This is the highest-impact technical risk as it directly affects the value proposition of same-day processing. Mitigation approach:
- **Pre-commitment validation**: Test with 500+ historical documents across all document types before vendor selection
- **Accuracy monitoring**: Implement real-time accuracy dashboards with alerts below threshold
- **Fallback process**: Maintain manual review capability for documents below confidence threshold
- **Contingency**: If no vendor achieves 95%, adjust threshold with compensating controls (human review for lower-confidence extractions)

**RISK-004: Integration complexity exceeds estimates**

Integration risk is inherent in any transformation involving legacy systems. Mitigation approach:
- **Technical discovery**: Conduct API assessment for all integration points before design
- **Proof of concept**: Build end-to-end integration prototype before commitment
- **Vendor support**: Include integration support in vendor contracts
- **Contingency**: If integration proves infeasible, consider middleware or data replication approaches

#### Regulatory Risks

**RISK-002: Regulatory rejection of automated decisioning**

Automated decisioning without human oversight could face regulatory challenge. Mitigation approach:
- **Early engagement**: Brief compliance team in week 1; request formal opinion before design
- **Audit trail**: Design comprehensive audit trail exceeding current requirements
- **Human oversight**: Include human review for edge cases and random sampling
- **Contingency**: If full automation rejected, implement "human-in-the-loop" with staff approval for automated recommendations

#### Adoption Risks

**RISK-003: Client adoption of video verification lower than expected**

Client adoption is critical for realizing the benefit of removing branch visits. Mitigation approach:
- **Client research**: Validate client appetite through survey before build
- **A/B testing**: Pilot with early adopter segment before broad rollout
- **Client communication**: Clear messaging on benefits and security
- **Contingency**: Maintain branch verification option; monitor adoption and adjust messaging
```

### Section 11: Success Metrics

#### 11.1 KPI Framework

**Format:**
- **Structure**: Introductory narrative paragraph + KPI table
- **Narrative**: 1-2 paragraphs explaining the measurement framework
- **Table Columns**: KPI | Definition | Target | Measurement Method

**Example - KPI Framework:**
```
### 11.1 KPI Framework

Success will be measured across four dimensions: client experience, operational efficiency, competitive positioning, and innovation adoption. Each MUST HAVE innovation has specific KPIs that define success, with targets set based on current baseline performance and industry benchmarks.

The KPI framework is designed to be measurable from day one of implementation, using data sources that already exist or can be readily created. Leading indicators (like processing time) will be monitored continuously, while lagging indicators (like client satisfaction) will be measured quarterly.

| KPI | Definition | Target | Measurement Method |
|-----|------------|--------|-------------------|
| Document Processing Time | Average time from document upload to data extraction complete | < 5 minutes (from 45 mins) | System timestamp logs |
| Same-Day Decision Rate | % of applications receiving decision within 24 hours | > 60% (from 15%) | Application status tracking |
| Client Effort Score (CES) | Survey-based effort score for onboarding journey | 30% reduction | Post-onboarding survey |
| Application Abandonment | % of applications started but not completed | < 15% (from 25%) | Application funnel analytics |
| Digital Completion Rate | % of onboardings completed without branch visit | > 70% (from 30%) | Channel tracking |
| Status Inquiry Calls | Inbound calls asking about application status | 50% reduction | Call center categorization |
```

#### 11.2 Measurement Plan

**Format:**
- **Structure**: Narrative overview + measurement table
- **Narrative**: 1-2 paragraphs on how and when metrics will be measured
- **Table Columns**: KPI | Data Source | Frequency | Owner | Baseline

**Example - Measurement Plan:**
```
### 11.2 Measurement Plan

Metrics will be captured through a combination of system logs, analytics, and surveys. System-based metrics (processing time, completion rates) will be automated and available in real-time dashboards. Survey-based metrics (CES, satisfaction) will be collected through post-onboarding surveys sent 7 days after account activation.

A baseline measurement will be established in the first month of the project, capturing current performance across all KPIs. This baseline will serve as the comparison point for measuring improvement. Monthly reviews will track progress, with quarterly deep-dives examining trends and identifying improvement opportunities.

| KPI | Data Source | Frequency | Owner | Baseline |
|-----|-------------|-----------|-------|----------|
| Document Processing Time | Document management system logs | Real-time | Operations | 45 minutes avg |
| Same-Day Decision Rate | Application workflow system | Daily | Operations | 15% |
| Client Effort Score | Post-onboarding survey | Quarterly | Client Experience | TBD (survey to establish) |
| Application Abandonment | Web/mobile analytics | Weekly | Digital | 25% |
| Digital Completion Rate | Channel tracking | Weekly | Digital | 30% |
| Status Inquiry Calls | Call center system | Weekly | Customer Service | 450 calls/week |
```

#### 11.3 Target Outcomes

**Format:**
- **Structure**: Table + narrative explanation
- **Table Columns**: Outcome | Success Criteria | Linked II#
- **Narrative**: 1-2 paragraphs explaining how outcomes link to innovations

**Example - Target Outcomes:**
```
### 11.3 Target Outcomes

| Outcome | Success Criteria | Linked II# |
|---------|------------------|------------|
| Same-day processing capability | 60%+ applications decided within 24 hours | II-ONB-001, II-ONB-004 |
| Reduced client effort | CES reduction of 30%+ | II-ONB-005, II-ONB-001 |
| Digital-first journey | 70%+ onboardings without branch visit | II-ONB-002, II-ONB-006 |
| Competitive parity | Feature match with top 3 competitors | II-ONB-001, II-ONB-002 |
| Operational efficiency | 50% reduction in processing staff time | II-ONB-001, II-ONB-004 |

The target outcomes represent the strategic objectives of the transformation, with each outcome enabled by one or more innovations. Same-day processing requires both AI document extraction (II-ONB-001) to accelerate data capture AND automated decisioning (II-ONB-004) to remove the decision bottleneck. Neither innovation alone achieves the outcome.

Similarly, the digital-first journey outcome depends on video verification (II-ONB-002) to eliminate the branch requirement. If video verification is not implemented (SHOULD HAVE), this outcome will not be achieved, and the 70% target should be adjusted downward.
```

### Section 12: Appendices

#### 12.1 Research Sources

**Format:**
- **Structure**: Table listing all sources used in the analysis
- **Table Columns**: Source | Type | Date | Relevance

**Source Types:**
- Industry Report
- Competitor Analysis
- Regulatory Document
- Internal Document
- Web Research
- SME Interview

**Example - Research Sources:**
```
### 12.1 Research Sources

| Source | Type | Date | Relevance |
|--------|------|------|-----------|
| Forrester Banking Digital Transformation Report | Industry Report | Q3 2024 | Market trends, best practices |
| McKinsey Banking Operations Benchmarks | Industry Report | 2024 | Efficiency benchmarks |
| Bank A Annual Report | Competitor Analysis | 2024 | Competitor strategy |
| Fintech X Product Demo | Competitor Analysis | Nov 2024 | Feature comparison |
| PSD3 Draft Regulation | Regulatory Document | 2024 | Regulatory horizon |
| Example Bank Digital Strategy | Internal Document | 2024 | Strategic alignment |
| SME Onboarding Pain Points Analysis | Internal Document | 2024 | Pain point input |
| Industry onboarding trends search | Web Research | Dec 2024 | Current trends |
```

#### 12.2 Market Data

**Format:**
- **Structure**: Table with key market data points
- **Table Columns**: Data Point | Value | Source | Relevance

**Example - Market Data:**
```
### 12.2 Market Data

| Data Point | Value | Source | Relevance |
|------------|-------|--------|-----------|
| Average SME onboarding time (industry) | 5-7 days | Forrester 2024 | Benchmark |
| Best-in-class onboarding time | < 1 day | Fintech analysis | Target benchmark |
| SME digital banking adoption | 78% | Industry survey | Digital priority justification |
| Mobile banking preference (SME) | 62% | Internal survey | Mobile innovation priority |
| Video verification adoption (early movers) | 45% | Competitor analysis | Adoption expectation |
| AI document processing accuracy (leaders) | 95%+ | Vendor assessments | Technical threshold |
```

#### 12.3 Technical Specifications

**Format:**
- **Structure**: Table with technical requirements per innovation
- **Table Columns**: Innovation | Technology | Integration Points | Technical Requirements

**Example - Technical Specifications:**
```
### 12.3 Technical Specifications

| Innovation | Technology | Integration Points | Technical Requirements |
|------------|------------|-------------------|----------------------|
| II-ONB-001 | AI/ML Document Processing | DMS, Core Banking, Workflow | Cloud deployment, 95% accuracy, < 30s processing |
| II-ONB-002 | Video Verification | Mobile SDK, Web SDK, ID Database | Real-time streaming, liveness detection, secure storage |
| II-ONB-004 | Rules Engine | Core Banking, Risk System | Decision audit trail, policy version control |
| II-ONB-005 | Notification Service | Workflow, CRM, Mobile Push | Real-time triggers, multi-channel delivery |
```

#### 12.4 Change Log

**Format:**
- **Structure**: Table tracking document versions
- **Table Columns**: Version | Date | Author | Changes

**Example - Change Log:**
```
### 12.4 Change Log

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 0.1 | 2024-12-01 | J. Smith | Initial draft - market research |
| 0.2 | 2024-12-05 | J. Smith | Added innovation backlog |
| 0.3 | 2024-12-08 | J. Smith | Added priorities and recommendations |
| 1.0 | 2024-12-10 | J. Smith | Final version after SME validation |
```

#### 12.5 Glossary

**Format:**
- **Structure**: Simple list with Term: Definition format

**Example - Glossary:**
```
### 12.5 Glossary

- **CES (Client Effort Score)**: A metric measuring how much effort a client must expend to complete a process. Lower is better.
- **COMP#**: Identifier for competitors analyzed in this document (e.g., COMP-ONB-001).
- **FIN#**: Identifier for fintech disruptors analyzed in this document (e.g., FIN-ONB-001).
- **II#**: Identifier for innovation ideas captured in this document (e.g., II-ONB-001).
- **MoSCoW**: Prioritization method categorizing items as Must Have, Should Have, Could Have, or Won't Have (Defer).
- **PP#**: Identifier for pain points from AS-IS documentation (e.g., PP-ONB-001).
- **TR#**: Identifier for market trends analyzed in this document (e.g., TR-ONB-001).
- **Same-day decisioning**: Providing an application decision within 24 hours of submission.
- **Straight-through processing**: Automated processing without human intervention.
```

### Section Confidence Statement

**Format:**
```
> **Section Confidence:** {{percentage}}% | **Basis:** {{ai_inferred_basis}}
```

**Example:**
```
> **Section Confidence:** 90% | **Basis:** All 20 validation checklist items passed. Executive summary validated by SME. Risk and metrics sections based on SME input.
```

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
