---
name: 'step-04-priorities'
description: 'Generate innovation priorities with MoSCoW categorization, transformation handoffs, SMART metrics, and risk mitigation'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/innovation-analysis'

# File References
thisStepFile: '{workflow_path}/steps/step-04-priorities.md'
nextStepFile: '{workflow_path}/steps/step-05-validation.md'
workflowFile: '{workflow_path}/workflow.md'

# Shared Protocols
protocolsFile: '{module_root}/workflows/shared/protocols/protocols.md'

# Scoring Configuration
scoringConfig: '{workflow_path}/config/scoring.yaml'

# Output Files
innovationAnalysisFile: '{current_process_folder}/innovation-analysis.md'
innovationIdeasDetailFile: '{current_process_folder}/innovation-ideas-detail.md'

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
---

# Step 4: Generate Innovation Priorities

## STEP GOAL

Prioritize innovations using MoSCoW categorization with explicit criteria, create structured transformation handoffs for MUST HAVEs, define SMART success metrics, develop risk mitigation strategies, and phase DEFER items.

**Progress: Step 4 of 5** | Innovation Priorities | Est. time: 40-50 min

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:
- **NEVER** generate final content without user validation
- **CRITICAL**: Read the complete step file before taking any action
- **CRITICAL**: When loading next step, ensure entire file is read
- YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:
- You are an Innovation Strategist prioritizing innovations and creating transformation handoffs
- Continue using your established name, communication_style, and persona
- We engage in collaborative dialogue, not command-response
- You bring prioritization methodology and strategic thinking, user brings organizational context and constraints

### Step-Specific Rules:
- Apply EXPLICIT priority criteria with thresholds
- **FORBIDDEN** to skip transformation handoff for MUST HAVEs
- SMART metrics MUST be defined for all MUST HAVEs
- Risk mitigation MUST be captured for all MUST HAVEs
- DEFER items MUST have phase assignment (Phase 2/3/Future)

---

## PRIORITY CRITERIA CONFIGURATION

### MUST HAVE Criteria:
- Feasibility Score: ≥ 3.0
- Impact: High
- Strategic Alignment: Yes
- **Special Conditions (any qualifies):**
  - Addresses critical pain point
  - Required for regulatory compliance
  - First mover competitive advantage
  - Foundation for other innovations

### SHOULD HAVE Criteria:
- Feasibility Score: ≥ 2.5
- Impact: High or Medium
- Strategic Alignment: Yes or Partial

### COULD HAVE Criteria:
- Feasibility Score: ≥ 2.0
- Impact: Medium or Low
- Strategic Alignment: Partial or TBD

### DEFER Criteria (any condition):
- Feasibility Score: < 2.0
- Dependencies not met
- Beyond transformation scope
- Requires proof of concept
- Regulatory not yet in place

### DEFER Phases:
- **Phase 2:** 0-12 months post TO-BE
- **Phase 3:** 12-24 months
- **Future:** 24+ months

---

## CONTENT FORMAT SPECIFICATION

This section defines the exact formatting requirements for Section 6 (Innovation Deep Dives), Section 7 (MoSCoW Prioritization), and Section 8 (Strategic Recommendations). The AI MUST follow these specifications when generating content.

**NOTE:** This workflow does NOT include time estimates or cost projections. Focus on feasibility, strategic value, and complexity without specific timelines or budgets.

### Section 6: Innovation Deep Dives

#### 6.1 Top Priority Innovations

**Format:**
- **Structure**: Summary table + abbreviated detail blocks (2+ paragraphs per innovation)
- **Coverage**: MUST HAVE, SHOULD HAVE, and COULD HAVE innovations all get detail blocks
- **Summary Table**: Quick reference for all prioritized innovations
- **Detail Blocks**: Per-innovation sections with transformation handoff information

**Summary Table Columns:**
| Column | Content | Formatting Rules |
|--------|---------|------------------|
| **II#** | Innovation identifier | Format: II-{ABBREV}-### |
| **Innovation** | Short name | 5-10 words |
| **Priority** | MoSCoW category | MUST / SHOULD / COULD |
| **Feasibility Score** | Total score | Number |
| **Key Justification** | Why this priority | 1 sentence |

**Per-Innovation Detail Block Structure:**
```
### II-XXX-###: [Innovation Name] (MUST HAVE / SHOULD HAVE / COULD HAVE)

#### Overview

| Attribute | Value |
|-----------|-------|
| **Priority** | [MUST HAVE / SHOULD HAVE / COULD HAVE] |
| **Feasibility Score** | [Score] |
| **Why This Priority** | [1-2 sentence justification] |

#### Description & Business Case

[2+ paragraphs covering:
- What this innovation does
- What problem it solves
- Why it matters strategically
- Expected benefits and outcomes]

#### Transformation Handoff (MUST HAVEs only)

**What TO-BE Must Include:**
[Bullet list of requirements for transformation design]

**Integration Requirements:**
[Bullet list of integration points and dependencies]

**Constraints:**
[Bullet list of technical, regulatory, or organizational constraints]
```

**Example - Top Priority Innovation:**
```
### II-ONB-001: AI-powered document extraction (MUST HAVE)

#### Overview

| Attribute | Value |
|-----------|-------|
| **Priority** | MUST HAVE |
| **Feasibility Score** | 25 |
| **Why This Priority** | Addresses critical pain point (PP-ONB-003), enables same-day decisioning, competitive necessity |

#### Description & Business Case

This innovation replaces manual document review with AI-powered extraction and validation. Machine learning models will automatically extract data from business registration documents, financial statements, and identity documents, validating against external sources. The system flags exceptions for human review while enabling straight-through processing for standard applications.

The business case is compelling: current document processing requires 45 minutes of staff time per application, creating a bottleneck that prevents same-day decisioning. AI extraction reduces this to under 5 minutes of exception handling, enabling 60% of applications to receive same-day decisions. This directly addresses the top client complaint (status uncertainty during processing delays) and matches competitor capabilities that are now table stakes in the market.

#### Transformation Handoff

**What TO-BE Must Include:**
- AI document extraction service integrated with application intake
- Confidence scoring for extracted data with threshold for human review
- Audit trail capturing extraction results and any manual corrections
- Fallback process for documents that fail extraction

**Integration Requirements:**
- Integration with document management system for ingestion
- Integration with core banking for data validation
- Integration with workflow system for exception routing

**Constraints:**
- Model accuracy must exceed 95% for production deployment
- Extracted data must be auditable for regulatory compliance
- Must support document formats: PDF, JPG, PNG, TIFF
```

#### 6.2 Technical Architecture

**Format:**
- **Structure**: Per-innovation architecture notes for MUST HAVEs
- **Content**: 1-2 paragraphs per innovation describing key technical considerations

**Example - Technical Architecture:**
```
#### II-ONB-001: AI-powered document extraction

The technical architecture centers on a document processing pipeline with three components: ingestion, extraction, and validation. The ingestion layer receives documents from multiple channels (portal upload, email, branch scan) and normalizes formats. The extraction layer uses pre-trained ML models fine-tuned on banking documents, with separate models for each document type (registration, financials, identity). The validation layer cross-references extracted data against external sources (companies registry, credit bureaus) and flags discrepancies for review.

Key technical decisions include: (1) cloud vs on-premise deployment — cloud is recommended for scalability and model updates, subject to data residency requirements; (2) build vs buy — vendor solutions are mature and recommended over custom build; (3) integration pattern — async processing with webhook callbacks is recommended to avoid blocking the application flow.

#### II-ONB-002: Video identity verification

The video verification architecture requires a real-time streaming component for the verification session, integration with government ID databases for validation, and secure storage for verification recordings. The recommended approach is a vendor-provided SDK embedded in the mobile and web applications, with the vendor handling the verification logic and returning a confidence score and audit trail.

Key considerations include: liveness detection to prevent spoofing, accessibility requirements for clients who cannot use video, and fallback to branch verification for edge cases.
```

#### 6.3 Implementation Approach

**Format:**
- **Structure**: Per-innovation implementation approach for MUST HAVEs
- **Content**: 1-2 paragraphs per innovation describing how to implement

**Example - Implementation Approach:**
```
#### II-ONB-001: AI-powered document extraction

Implementation should follow a phased approach starting with a proof of concept on a single document type (business registration) before expanding to other document types. Phase 1 focuses on validating model accuracy with a sample of historical applications — the target is 95% extraction accuracy with less than 5% false positive rate on exception flagging. Phase 2 expands to additional document types and integrates with the production workflow. Phase 3 implements continuous learning to improve model performance based on correction feedback.

Key success factors include: early engagement with compliance to validate the audit approach, parallel running with manual processing during initial deployment, and clear escalation paths for extraction failures.

#### II-ONB-002: Video identity verification

Implementation begins with vendor selection — three vendors should be evaluated against criteria including accuracy, accessibility, regulatory compliance, and integration complexity. Following vendor selection, implementation involves SDK integration with mobile and web applications, integration with the identity verification workflow, and staff training on exception handling. A pilot with a subset of applications is recommended before full rollout.

Success factors include: clear client communication about the new verification option, accessibility alternatives for clients who cannot use video, and monitoring of verification success rates and abandonment.
```

### Section 7: MoSCoW Prioritization

**NOTE:** Section 7 replaces the original "Prioritized Roadmap" with MoSCoW categories. No Gantt charts or timeline-based phases.

**Format:**
- **Structure**: Four subsections, one per MoSCoW category
- **Per Category**: Table of innovations + brief narrative explaining the category criteria

#### 7.1 MUST HAVE

**Format:**
- **Table Columns**: II# | Innovation | Feasibility | Justification
- **Narrative**: 1-2 paragraphs on what makes these MUST HAVE

**Example:**
```
### 7.1 MUST HAVE

These innovations are essential for the transformation to succeed. They address critical pain points, enable competitive parity, or are required foundations for other improvements.

| II# | Innovation | Feasibility | Justification |
|-----|-----------|-------------|---------------|
| II-ONB-001 | AI document extraction | 25 | Addresses critical bottleneck, competitive necessity |
| II-ONB-004 | Automated decisioning | 26 | Enables same-day decisions, high business value |
| II-ONB-005 | Status notifications | 28 | Top client complaint, low risk implementation |

These three innovations form the core of the transformation. Without AI document extraction (II-ONB-001), processing times cannot be reduced sufficiently to enable same-day decisioning. Without automated decisioning (II-ONB-004), the benefits of faster document processing cannot be realized. Status notifications (II-ONB-005) address the most frequent client complaint and can be implemented independently as a quick win.
```

#### 7.2 SHOULD HAVE

**Format:**
- **Table Columns**: II# | Innovation | Feasibility | Justification
- **Narrative**: 1-2 paragraphs on what makes these SHOULD HAVE

**Example:**
```
### 7.2 SHOULD HAVE

These innovations add significant value and should be included if feasible. They are important but the transformation could proceed without them in the initial scope.

| II# | Innovation | Feasibility | Justification |
|-----|-----------|-------------|---------------|
| II-ONB-002 | Video identity verification | 25 | Competitive differentiator, removes branch dependency |
| II-ONB-006 | Mobile application completion | 22 | Client preference, extends digital reach |

Video verification (II-ONB-002) would eliminate the branch visit requirement for 70% of applications, significantly improving the digital-first experience. However, regulatory approval for video verification is still in progress, making this a SHOULD HAVE rather than MUST HAVE. Mobile application (II-ONB-006) addresses client preference for mobile-first journeys but is not essential if web application is optimized for mobile browsers.
```

#### 7.3 COULD HAVE

**Format:**
- **Table Columns**: II# | Innovation | Feasibility | Justification
- **Narrative**: 1-2 paragraphs on what makes these COULD HAVE

#### 7.4 DEFER

**Format:**
- **Table Columns**: II# | Innovation | Feasibility | Why Deferred | Reconsider When
- **Narrative**: 1-2 paragraphs on deferral rationale

**Example:**
```
### 7.4 DEFER

These innovations are not recommended for the current transformation scope. They may be valuable in future phases when conditions change.

| II# | Innovation | Feasibility | Why Deferred | Reconsider When |
|-----|-----------|-------------|--------------|-----------------|
| II-ONB-009 | Embedded banking partnerships | 18 | Market not ready, requires API platform | API platform deployed |
| II-ONB-010 | Blockchain KYC sharing | 15 | Technology immature, regulatory unclear | Industry consortium forms |

Embedded banking (II-ONB-009) is an attractive long-term opportunity but requires an API platform that doesn't yet exist. This should be reconsidered once the core banking API modernization project completes. Blockchain KYC (II-ONB-010) shows promise but no banking consortium has achieved production scale, and regulatory treatment remains unclear.
```

### Section 8: Strategic Recommendations

#### 8.1 Low Complexity / High Value

**Format:**
- **Structure**: Bullet list of innovations with brief rationale
- **Content**: Innovations that deliver high value with minimal complexity

**Example:**
```
### 8.1 Low Complexity / High Value

These innovations should be prioritized for immediate attention due to their favorable value-to-complexity ratio:

- **II-ONB-005: Real-time status notifications** — Leverages existing notification infrastructure, addresses top client complaint, can be deployed rapidly with minimal risk.

- **II-ONB-004: Automated decisioning for simple structures** — Policy logic already documented, implementation is primarily configuration, enables same-day decisions for majority of applications.

- **II-ONB-007: Pre-filled application fields** — Integration with existing data sources, reduces client effort significantly, proven pattern from other products.
```

#### 8.2 Strategic Bets

**Format:**
- **Structure**: Bullet list of innovations with brief rationale
- **Content**: Innovations requiring significant investment but delivering transformative value

**Example:**
```
### 8.2 Strategic Bets

These innovations require more significant investment but deliver transformative value:

- **II-ONB-001: AI document extraction** — Requires vendor selection and integration, but enables same-day processing which is a market differentiator. Investment is justified by operational savings and competitive positioning.

- **II-ONB-002: Video identity verification** — Dependent on regulatory approval, but eliminates the primary friction point (branch visits) for digital-native clients. Worth investing in regulatory engagement to accelerate approval.
```

#### 8.3 Future Consideration

**Format:**
- **Structure**: Bullet list of innovations with monitoring triggers
- **Content**: Innovations not ready now but worth watching

**Example:**
```
### 8.3 Future Consideration

These innovations should be monitored for future inclusion:

- **II-ONB-009: Embedded banking partnerships** — Monitor API platform project progress; revisit when platform is production-ready.

- **II-ONB-010: Blockchain KYC sharing** — Monitor industry consortium developments; revisit if major banks achieve production deployment.

- **II-ONB-011: Voice-activated applications** — Monitor voice assistant adoption in banking; revisit when client demand signals emerge.
```

### Section Confidence Statement

**Format:**
```
> **Section Confidence:** {{percentage}}% | **Basis:** {{ai_inferred_basis}}
```

**Example:**
```
> **Section Confidence:** 80% | **Basis:** Prioritization based on feasibility scores and SME judgment. Transformation handoffs validated with SME. Technical architecture requires IT review for final validation.
```

---

## PHASE A: ANALYZE [AUTO - NO USER INTERRUPTION]

### A.1 Load Inputs

Read and analyze:
- Step 2 output (Market Research) from `{innovationAnalysisFile}`
- Step 3 output (Innovation Backlog with feasibility scores) from `{innovationAnalysisFile}`

### A.2 Apply Priority Criteria

For each innovation in backlog:
1. Check against MUST HAVE criteria
2. If not MUST, check SHOULD HAVE criteria
3. If not SHOULD, check COULD HAVE criteria
4. Otherwise, assign to DEFER

### A.3 Generate for MUST HAVEs

For each MUST HAVE, prepare:

**Transformation Handoff:**
- What TO-BE must include
- Integration requirements
- Technical constraints
- User experience requirements

**SMART Success Metrics:**
- **S**pecific: What exactly will be measured?
- **M**easurable: How will it be measured?
- **A**chievable: Is target realistic?
- **R**elevant: Why does this metric matter?
- **T**ime-bound: When will it be measured?

**Risk Mitigation Strategy:**
- Key risks identified
- Mitigation actions
- Contingency plans

### A.4 Generate for DEFERs

For each DEFER, prepare:
- Phase assignment (Phase 2/3/Future)
- Why deferred
- Unblock conditions
- Trigger to reconsider

### A.5 Output: Draft Priorities

Create preliminary prioritization with:
- MUST HAVE list with handoffs
- SHOULD HAVE list
- COULD HAVE list
- DEFER list by phase

**[Proceed directly to Phase B - NO user interaction yet]**

---

## PHASE B: RESEARCH [AUTO - NO USER INTERRUPTION]

### B.1 For MUST HAVEs

Research:
- Implementation patterns and best practices
- Case studies (success AND failure)
- Common pitfalls
- Success factors
- Integration considerations
- Risk mitigation examples from industry

### B.2 For DEFERs

Research:
- Unblock condition timelines
- Technology maturation forecasts
- Regulatory timeline estimates

### B.3 Output: Research Findings

Compile per MUST HAVE:
- Implementation guidance
- Case study insights
- Pitfall warnings

**[Proceed directly to Phase C with combined A+B findings]**

---

## PHASE C: ELICIT [INTERACTIVE - ONE TOPIC AT A TIME]

**Standard Pattern:** Present → Ask → WAIT → **Decision** → WAIT → Next topic

---

### TOPIC 1: Priority Overview

Present prioritization summary:

| Priority | Count | Criteria |
|----------|-------|----------|
| MUST HAVE | {{must_count}} | Feasibility ≥3.0, High Impact, Strategic |
| SHOULD HAVE | {{should_count}} | Feasibility ≥2.5, High/Medium Impact |
| COULD HAVE | {{could_count}} | Feasibility ≥2.0, Medium/Low Impact |
| DEFER | {{defer_count}} | Feasibility <2.0 or blocked |

**Ask:** "Does this prioritization approach make sense for your context? Any criteria to adjust?"

**Decision:** [A] Approve criteria | [B] Adjust criteria | [E] Elicit more

---

### TOPIC 2: MUST HAVE Review (Per Item)

**For EACH MUST HAVE:**

```
<loop name="must_have_review" for="each MUST HAVE innovation">

  <format>
  ---
  **MUST HAVE: II-{abbrev}-{{seq}}**

  **Name:** {{innovation.name}}
  **Feasibility Score:** {{innovation.score}}
  **Why MUST HAVE:** {{innovation.must_have_justification}}
  </format>

  <format>
  **Transformation Handoff:**

  **What TO-BE Must Include:**
  {{to_be_requirements}}

  **Integration Requirements:**
  {{integration_requirements}}

  **Technical Constraints:**
  {{technical_constraints}}

  **UX Requirements:**
  {{ux_requirements}}
  </format>

  <format>
  **SMART Success Metrics:**

  | Metric | Specific | Measurable | Target | Timeline |
  |--------|----------|------------|--------|----------|
  | {{metric_1}} | {{specific}} | {{how_measured}} | {{target}} | {{when}} |
  | {{metric_2}} | {{specific}} | {{how_measured}} | {{target}} | {{when}} |
  </format>

  <format>
  **Risk Mitigation:**

  | Risk | Likelihood | Impact | Mitigation | Contingency |
  |------|------------|--------|------------|-------------|
  | {{risk_1}} | {{likelihood}} | {{impact}} | {{mitigation}} | {{contingency}} |
  | {{risk_2}} | {{likelihood}} | {{impact}} | {{mitigation}} | {{contingency}} |
  </format>

  <format>
  **Research Insights:**
  {{case_study_insights}}
  {{common_pitfalls}}
  </format>

  <ask response="must_have_decision">
  **Decision for II-{abbrev}-{{seq}}:**

  - [A] Confirm as MUST HAVE - handoff complete
  - [S] Downgrade to SHOULD HAVE
  - [C] Downgrade to COULD HAVE
  - [D] Move to DEFER
  </ask>

  <check if="must_have_decision != 'A'">
    <ask response="downgrade_reason">Why should this be downgraded?</ask>
  </check>

  <check if="must_have_decision == 'A'">
    <ask response="handoff_complete">
    Is the transformation handoff complete? Does the Transformation Agent have everything needed?

    - [ ] Yes - handoff is complete
    - [ ] No - needs additions
    </ask>

    <check if="handoff_complete == 'No'">
      <ask response="handoff_additions">What needs to be added to the handoff?</ask>
    </check>
  </check>

</loop>
```

---

### TOPIC 3: SHOULD HAVE Review (Per Item)

For each SHOULD HAVE, present summary:

| II# | Innovation | Feasibility | Impact | Why Not MUST |
|-----|-----------|-------------|--------|--------------|
| II-{abbrev}-XXX | {{name}} | {{score}} | {{impact}} | {{reason}} |

**Ask:** "For each SHOULD HAVE - should it be upgraded, kept, downgraded, or deferred?"

**Per item decision:**
- [U] Upgrade to MUST (requires full handoff template)
- [K] Keep as SHOULD HAVE
- [C] Downgrade to COULD HAVE
- [D] Move to DEFER

---

### TOPIC 4: COULD HAVE Quick Review

Present COULD HAVE table:

| II# | Innovation | Feasibility | Impact | Why COULD |
|-----|-----------|-------------|--------|-----------|
| II-{abbrev}-XXX | {{name}} | {{score}} | {{impact}} | {{reason}} |

**Ask:** "Any COULD HAVEs to upgrade or remove entirely?"

**Decision:** [A] Approve as-is | [B] Adjust items

---

### TOPIC 5: DEFER - Phase 2 (0-12 months post TO-BE)

Present Phase 2 deferred items:

| II# | Innovation | Feasibility | Why Deferred | Unblock Condition |
|-----|-----------|-------------|--------------|-------------------|
| II-{abbrev}-XXX | {{name}} | {{score}} | {{reason}} | {{unblock}} |

For each, capture:
- Unblock condition (what needs to happen)
- Dependencies to monitor
- Trigger for reconsideration

**Ask:** "Are Phase 2 assignments correct? Any unblock conditions to adjust?"

---

### TOPIC 6: DEFER - Phase 3 (12-24 months)

Present Phase 3 deferred items:

| II# | Innovation | Feasibility | Why Deferred | Watch For |
|-----|-----------|-------------|--------------|-----------|
| II-{abbrev}-XXX | {{name}} | {{score}} | {{reason}} | {{watch}} |

**Ask:** "Phase 3 assignments correct? Any triggers for earlier consideration?"

---

### TOPIC 7: DEFER - Future (24+ months)

Present Future watch list:

| II# | Innovation | Feasibility | Why Future | Monitor |
|-----|-----------|-------------|------------|---------|
| II-{abbrev}-XXX | {{name}} | {{score}} | {{reason}} | {{monitor}} |

**Ask:** "Future assignments correct? What should we monitor for these?"

---

### TOPIC 8: Final Validation

Present final priority summary:

```
**Final Priority Distribution**

| Priority | Count | Est. Investment | Est. Value |
|----------|-------|-----------------|------------|
| MUST HAVE | {{must}} | {{must_investment}} | {{must_value}} |
| SHOULD HAVE | {{should}} | {{should_investment}} | {{should_value}} |
| COULD HAVE | {{could}} | {{could_investment}} | {{could_value}} |
| DEFER Phase 2 | {{defer_2}} | - | - |
| DEFER Phase 3 | {{defer_3}} | - | - |
| DEFER Future | {{defer_f}} | - | - |

**MUST HAVE Summary:**
{{for each must_have}}
- II-{{seq}}: {{name}} (Score: {{score}})
  Metrics: {{key_metric}}
  Key Risk: {{key_risk}}
{{/for}}
```

**Ask:** "Final validation questions:"
- Are the MUST HAVEs achievable in your transformation timeline?
- Are the success metrics realistic and measurable?
- Are the risk mitigations adequate?
- Any additional constraints the Transformation Agent should know?

---

## OUTPUT APPROVAL

Present complete priorities with handoffs:

```
**Innovation Priorities Complete**

**For Transformation Agent:**
- {{must_count}} MUST HAVE innovations with full handoffs
- {{should_count}} SHOULD HAVE innovations for consideration
- {{could_count}} COULD HAVE innovations if capacity allows

**Deferred for Future Phases:**
- Phase 2: {{defer_2_count}} innovations
- Phase 3: {{defer_3_count}} innovations
- Future: {{defer_f_count}} innovations

**Key Guidance:**
{{transformation_guidance_summary}}
```

**Ask:** "Do you approve the Innovation Priorities? [Y] Yes | [N] No - needs changes"

- IF N: "What needs to change?" → iterate on specific section
- IF Y: Proceed to append and continue

---

## APPEND TO DOCUMENT

**On Approval:**

1. APPEND the approved Innovation Priorities section to `{innovationAnalysisFile}`:
   - Section 6: Innovation Deep Dives (top priority details, architecture, approach)
   - Section 7: Prioritized Roadmap (Gantt, phases)
   - Section 8: Strategic Recommendations (quick wins, strategic initiatives, future exploration)

2. APPEND the Guidance for Transformation Agent section

3. UPDATE `{innovationIdeasDetailFile}` with priority changes:
   - For each innovation with priority changes (upgraded/downgraded):
     - Update the `priority` field in the detailed entry
     - Update the `recommended_action` based on MoSCoW category
   - For MUST HAVEs:
     - Add transformation handoff details to each entry
     - Add SMART success metrics to each entry
     - Add risk mitigation strategy to each entry
   - For DEFERs:
     - Add phase assignment (Phase 2/3/Future)
     - Add unblock conditions
     - Add monitoring triggers
   - Update priority matrix section (Quick Wins, Strategic Bets, Fill-Ins, Reconsider)
   - Update recommendations sections (immediate, short-term, long-term)

4. Update frontmatter: add "step-04" to stepsCompleted array in both files

5. Display: "Step 4 Complete: Innovation Priorities added to Innovation Analysis document and Innovation Ideas Detail log updated"

---

## MENU OPTIONS

**Select an Option:** [A] Advanced Elicitation | [P] Party Mode | [C] Continue to Step 5

### Menu Handling Logic:

- IF A: Execute `{advancedElicitationTask}`, then return to this menu
- IF P: Execute Party Mode workflow, then capture outputs and return to this menu
- IF C: Save content to `{innovationAnalysisFile}`, then load, read entire file, then execute `{nextStepFile}`
- IF other: Respond to query, then redisplay menu

### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'
- After other menu items execution, return to this menu
- User can chat or ask questions - always respond and then redisplay menu options

---

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN [C continue option] is selected and [priorities approved and appended to document], will you then load and read fully `{nextStepFile}` to execute review and finalization.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:
- Priority criteria applied consistently (MUST/SHOULD/COULD/DEFER thresholds)
- Each MUST HAVE has complete transformation handoff with integration requirements
- Each MUST HAVE has SMART success metrics defined
- Each MUST HAVE has risk mitigation strategy documented
- Each DEFER has phase assignment (Phase 2/3/Future) with unblock conditions
- User validated each priority category with upgrade/downgrade decisions
- Final validation confirms achievability of MUST HAVE list
- Innovation Priorities and Transformation Agent Guidance sections appended to innovation-analysis.md
- Innovation Ideas Detail file (innovation-ideas-detail.md) updated with priorities, handoffs, metrics, risks
- Menu presented and user input handled correctly

### SYSTEM FAILURE:
- Skipping transformation handoff for any MUST HAVE
- Not defining SMART metrics for MUST HAVEs
- Not capturing risk mitigation for MUST HAVEs
- DEFER items without phase assignment
- Proceeding without user validation per priority category
- Generating priority content without user approval
- Not updating innovation-ideas-detail.md with priority changes
- Proceeding to next step without user selecting 'C'

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
