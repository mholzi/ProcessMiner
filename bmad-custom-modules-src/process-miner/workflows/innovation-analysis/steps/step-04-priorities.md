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
