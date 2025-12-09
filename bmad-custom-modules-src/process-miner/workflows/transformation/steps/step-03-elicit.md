---
name: 'step-03-elicit'
description: 'Derive target state through collaborative SME elicitation'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/transformation'

# File References
thisStepFile: '{workflow_path}/steps/step-03-elicit.md'
nextStepFile: '{workflow_path}/steps/step-04-design.md'
workflowFile: '{workflow_path}/workflow.md'

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
partyModeWorkflow: '{project-root}/.bmad/core/workflows/party-mode/workflow.md'

# Output Files
transformationDataFile: '{current_process_folder}/transformation-data.json'
transformationDecisionsFile: '{current_process_folder}/transformation-decisions-detail.md'

# Template References
# (Elicitation uses collaborative dialogue, no external templates)
---

# Step 3: Elicit Target State

## STEP GOAL

Collaboratively derive the target state with the SME through structured elicitation. The business owns the future state - we facilitate, not dictate.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:
- 🛑 **NEVER** generate content without user input
- 📖 **CRITICAL**: Read the complete step file before taking any action
- 🔄 **CRITICAL**: When loading next step, ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:
- ✅ You are a Process Transformation Orchestrator
- ✅ **ELICIT, DON'T DICTATE** - Target state emerges through SME collaboration
- ✅ Present options with trade-offs, let SME decide
- ✅ Document decisions with rationale as TD# references

### Step-Specific Rules:
- Focus on ELICITING target state, not PRESCRIBING it
- **FORBIDDEN** to make transformation decisions without SME input
- Every significant decision becomes a TD# record
- Balance competing demands - make trade-offs explicit

## EXECUTION PROTOCOLS

- Walk through each priority area from synthesis
- Present options with trade-offs for each
- Capture SME decisions as TD# records
- Build target state progressively through dialogue

## CONTEXT BOUNDARIES

- Synthesis complete from Step 2
- This step builds the conceptual target state
- Documentation happens in Step 4

---

## EXECUTION SEQUENCE

### 1. Set Elicitation Context

Display:
```
{contributor_name}, now we design the target state together.

**My approach:**
- I'll present options based on the AS-IS analysis
- You decide what the TO-BE should look like
- We'll document each decision with rationale
- Trade-offs will be explicit - no hidden compromises

**Remember:** You own this process. I bring transformation expertise, but you know what will work for your business.

Let's start with the critical priorities.
```

### 2. Elicit Process Flow Transformation

```
<format>
## Process Flow Transformation

Looking at the current {{total_steps}} steps, let's discuss the target flow.
</format>

<for_each priority in="critical_process_priorities">
  <format>
  ### Priority: {{priority.title}}

  **Current State (AS-IS):**
  {{priority.current_state}}

  **References:** {{priority.references}}

  **Options for TO-BE:**
  </format>

  <ask response="process_decision_{{priority.id}}">
  Consider these approaches:

  **Option A: {{option_a_title}}**
  - Change: {{option_a_description}}
  - Pros: {{option_a_pros}}
  - Cons: {{option_a_cons}}
  - Effort: {{option_a_effort}}

  **Option B: {{option_b_title}}**
  - Change: {{option_b_description}}
  - Pros: {{option_b_pros}}
  - Cons: {{option_b_cons}}
  - Effort: {{option_b_effort}}

  **Option C: Keep As-Is**
  - No change to current approach
  - Risk: {{keep_risk}}

  Which approach do you prefer? [A/B/C] Or describe your own approach:
  </ask>

  <action>
  Record decision as TD#:
  - TD#{{next_td_id}}: {{priority.title}}
  - Category: Process
  - Decision: {{selected_option}}
  - Rationale: {{sme_rationale}}
  - AS-IS Reference: {{priority.references}}
  - Append to {transformationDecisionsFile}
  </action>
</for_each>
```

### 3. Elicit Control Transformation

```
<format>
## Control Transformation

We have {{control_gaps}} control gaps to address. Let's work through each.
</format>

<for_each gap in="control_gaps">
  <format>
  ### Control Gap: {{gap.title}}

  **Gap Description:** {{gap.description}}
  **Regulation:** {{gap.regulation}}
  **Current Control:** {{gap.current_control}}
  **Risk if Unaddressed:** {{gap.risk}}
  </format>

  <ask response="control_decision_{{gap.id}}">
  How should we address this gap in the target state?

  **Option A: Strengthen Existing Control**
  - Enhance {{gap.current_control}}
  - Implementation: {{option_a_impl}}

  **Option B: Add New Control**
  - Introduce {{option_b_control}}
  - Implementation: {{option_b_impl}}

  **Option C: Automate Control**
  - Replace manual with automated
  - Implementation: {{option_c_impl}}

  **Option D: Accept Risk (requires justification)**
  - Document risk acceptance
  - Requires approval from: {{approval_authority}}

  Which approach? [A/B/C/D]:
  </ask>

  <check if="control_decision == 'D'">
    <ask response="risk_justification">
    Please provide justification for accepting this risk:
    </ask>
  </check>

  <action>
  Record decision as TD#:
  - TD#{{next_td_id}}: Control - {{gap.title}}
  - Category: Control
  - Decision: {{selected_option}}
  - Rationale: {{sme_rationale}}
  - Gap Reference: {{gap.id}}
  </action>
</for_each>

<format>
### SOD Verification

Segregation of Duties requirements must be preserved. Current SOD patterns:
{{sod_patterns}}

**Confirm:** Will the target state maintain these SOD requirements? [Y/N]
</format>

<check if="sod_confirmation == 'N'">
  <ask response="sod_exception">
  Which SOD requirement needs modification and why?
  </ask>
  Record as TD# with regulatory justification required.
</check>
```

### 4. Elicit CX Transformation

```
<format>
## Client Experience Transformation

Current CES: {{ces_score}} | Target: {{ces_target}} (30% reduction)
</format>

<for_each friction in="top_friction_points">
  <format>
  ### Friction Point: {{friction.title}}

  **Current Experience:**
  - Touchpoint: {{friction.touchpoint}}
  - Client Emotion: {{friction.emotion}}
  - CES Impact: +{{friction.ces_contribution}}

  **Enhancement Ideas from CX Analyst:**
  {{friction.enhancement_ideas}}
  </format>

  <ask response="cx_decision_{{friction.id}}">
  How should we address this friction in the target state?

  **Option A: Eliminate Touchpoint**
  - Remove this interaction entirely
  - CES Reduction: {{option_a_reduction}}
  - Trade-off: {{option_a_tradeoff}}

  **Option B: Streamline Touchpoint**
  - Reduce effort while keeping interaction
  - CES Reduction: {{option_b_reduction}}
  - Trade-off: {{option_b_tradeoff}}

  **Option C: Digitize/Automate**
  - Move to self-service
  - CES Reduction: {{option_c_reduction}}
  - Trade-off: {{option_c_tradeoff}}

  **Option D: Keep but Enhance**
  - Improve experience without structural change
  - CES Reduction: {{option_d_reduction}}

  Which approach? [A/B/C/D]:
  </ask>

  <action>
  Record decision as TD#.
  </action>
</for_each>

<format>
### Moments That Matter

These critical touchpoints must be protected or enhanced:
{{moments_that_matter}}

**Confirm:** Are there any moments we should NOT change? [List or 'None']
</format>
```

### 5. Elicit Innovation Integration

```
<format>
## Innovation Integration

The Innovation Analyst identified {{total_innovations}} ideas. Let's prioritize for the target state.
</format>

<format>
### MUST HAVE Innovations (Required for Target State)

| II# | Innovation | Feasibility | Your Decision |
|-----|------------|-------------|---------------|
{{must_have_table}}

**These are flagged as MUST HAVE. Confirm inclusion or provide justification for exclusion.**
</format>

<for_each innovation in="must_have_innovations">
  <ask response="innovation_decision_{{innovation.id}}">
  **{{innovation.title}}** (Feasibility: {{innovation.feasibility}}/5)

  - Include in target state? [Y/N]
  - If N, provide justification:
  </ask>

  <check if="innovation_decision == 'N'">
    <action>
    Record exclusion as TD# with justification.
    Flag for Innovation Analyst validation.
    </action>
  </check>
</for_each>

<format>
### SHOULD HAVE Innovations (Recommended)

{{should_have_list}}

Which of these would you like to include in the target state?
</format>

<ask response="should_have_selections" multiselect="true">
Select SHOULD HAVE innovations to include:
{{should_have_options}}
</ask>
```

### 6. Capture Trade-offs

```
<format>
## Trade-off Summary

Based on our elicitation, here are the key trade-offs in this transformation:
</format>

<for_each tradeoff in="identified_tradeoffs">
  <format>
  ### Trade-off: {{tradeoff.title}}

  **Competing Demands:**
  - {{tradeoff.demand_a}}
  - {{tradeoff.demand_b}}

  **Your Decision:** {{tradeoff.decision}}
  **Accepted Compromise:** {{tradeoff.compromise}}
  </format>
</for_each>

<ask response="additional_tradeoffs">
Are there any other trade-offs we should document? [Describe or 'None']
</ask>
```

### 7. Summarize Target State Vision

```
<format>
## Target State Vision Summary

Based on our elicitation, here's the emerging target state:

### Process Changes
{{process_changes_summary}}

### Control Changes
{{control_changes_summary}}

### CX Improvements
{{cx_improvements_summary}}

### Innovations Included
{{innovations_summary}}

### Key Decisions Made
| TD# | Decision | Category |
|-----|----------|----------|
{{decisions_table}}

### Expected Outcomes
| Metric | AS-IS | TO-BE Target |
|--------|-------|--------------|
{{expected_outcomes_table}}
</format>

<ask response="vision_confirmation">
Does this capture your vision for the target state?

- **[Y]** Yes - Proceed to documentation
- **[N]** No - Let's revise
- **[P]** Partial - Some areas need adjustment
</ask>

<check if="vision_confirmation == 'N' or vision_confirmation == 'P'">
  <ask response="revision_areas">
  Which areas need revision?
  </ask>
  Return to relevant section for re-elicitation.
</check>
```

### 8. Present Menu Options

```
<format>
**Progress: Step 3 of 7 - Target State Elicitation Complete**

✓ Process flow decisions captured
✓ Control gap resolutions defined
✓ CX improvements decided
✓ Innovations selected
✓ Trade-offs documented
✓ {{total_decisions}} transformation decisions (TD#) recorded

**Select an Option:**
- **[A]** Advanced Elicitation - Deep dive on specific decisions
- **[P]** Party Mode - Get specialist perspectives on decisions
- **[C]** Continue - Proceed to document the TO-BE state
</format>
```

#### Menu Handling Logic:

- IF A: Execute {advancedElicitationTask}
- IF P: Execute {partyModeWorkflow}
- IF C: Update {transformationDataFile}, then load, read entire file, then execute {nextStepFile}
- IF other: Address query, then redisplay menu

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'
- After other menu items execution completes, redisplay the menu
- User can chat or ask questions - always respond, then redisplay the menu

---

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN [C continue option] is selected and [SME confirms target state vision], will you then load and read fully `{nextStepFile}` to execute and begin TO-BE documentation.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:
- Target state elicited through SME collaboration
- All critical priorities addressed with decisions
- Control gaps have resolution paths
- CX improvements selected with trade-offs
- MUST HAVE innovations confirmed or justified
- All decisions recorded as TD# with rationale
- Trade-offs explicitly documented
- SME confirms target state vision
- Menu presented and user input handled correctly

### ❌ SYSTEM FAILURE:
- Dictating target state without SME input
- Making decisions for the SME
- Skipping any priority areas
- Not documenting decision rationale
- Proceeding without vision confirmation
- Hidden trade-offs (not made explicit)

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
