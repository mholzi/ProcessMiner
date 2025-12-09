---
name: 'step-02-synthesize'
description: 'Present consolidated AS-IS summary topic-by-topic for SME approval'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/transformation'

# File References
thisStepFile: '{workflow_path}/steps/step-02-synthesize.md'
nextStepFile: '{workflow_path}/steps/step-03-elicit.md'
workflowFile: '{workflow_path}/workflow.md'

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
partyModeWorkflow: '{project-root}/.bmad/core/workflows/party-mode/workflow.md'
brainstormingWorkflow: '{project-root}/.bmad/core/workflows/brainstorming-session/workflow.md'

# Output Files
transformationDataFile: '{current_process_folder}/transformation-data.json'
targetStateFile: '{current_process_folder}/target-state-documentation.md'
---

# Step 2: Synthesize AS-IS State

## STEP GOAL

Present a consolidated view of the AS-IS state from all four specialist perspectives, **topic by topic**, with SME approval at each stage before proceeding.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:
- 🛑 **NEVER** generate content without user input
- 📖 **CRITICAL**: Read the complete step file before taking any action
- 🔄 **CRITICAL**: When loading next step, ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:
- ✅ You are a Process Transformation Orchestrator
- ✅ Present information as a strategic consultant
- ✅ Use scenarios and trade-offs in your framing
- ✅ Help SME see the full picture before designing solutions

### Step-Specific Rules:
- Focus ONLY on synthesizing and presenting AS-IS state
- **FORBIDDEN** to propose TO-BE solutions in this step
- Present ONE topic at a time, get approval, then proceed
- Let SME digest before moving to next topic

### 🚨 MANDATORY MENU RULE (NO EXCEPTIONS)
**EVERY approval menu MUST include ALL THREE options:**
```
- [Y] Yes, Accept
- [E] Edit
- [R] Rewrite
```
**FORBIDDEN:** Showing only [Y]/[E] without [R]. The [R] Rewrite option opens the AI-assisted sub-menu (Advanced Elicitation, Party Mode, Brainstorming, Quick Questions).

## EXECUTION PROTOCOLS

- Synthesize insights from all 4 specialist analyses
- Present **one topic at a time** for SME review
- Use consistent Y/E/R approval menu for each topic
- All 6 topics must be approved before proceeding

## CONTEXT BOUNDARIES

- All AS-IS context loaded in memory from Step 1
- This step is about UNDERSTANDING, not DESIGNING
- SME approval required for each topic before proceeding

---

## SYNTHESIS TOPICS

| # | Topic | Content |
|---|-------|---------|
| 1 | Process Health Summary | Overall metrics + heat map |
| 2 | Critical Priorities | 🔴 Red flags that must be addressed |
| 3 | Important Priorities | 🟡 Yellow flags that should be addressed |
| 4 | Cross-Cutting Themes | Synthesized themes across all analyses |
| 5 | Transformation Targets | KPI targets + innovation inclusion |
| 6 | Constraints | Non-negotiables, regulatory, technical |

---

## EXECUTION SEQUENCE

### 1. Present Synthesis Introduction

Display:
```
{contributor_name}, I've analyzed the inputs from all four specialist agents. Let me present a consolidated view of where this process stands today.

This synthesis brings together:
- **Process Documentation** - The step-by-step flow, exceptions, and pain points
- **Control Compliance** - Regulatory requirements and control gaps
- **Client Experience** - Journey touchpoints and friction analysis
- **Innovation** - Market trends and improvement opportunities

We'll walk through 6 topics, one at a time. Each needs your approval before we move on.
```

### 2. Iterate Through Each Topic

For each topic (1-6), present content and get approval:

```
<iterate for="each topic">
  <format>
  ---
  **Topic {{topic_number}} of 6: {{topic_name}}**
  </format>

  <!-- Generate topic-specific content based on AS-IS analysis -->
  <action>Generate {{topic_name}} content from loaded AS-IS context</action>

  <!-- Present with approval menu -->
  <approval-menu topic="{{topic_name}}">
    <display>
    ---
    **{{topic_name}} - Draft:**

    {{topic_content}}

    ---
    How would you like to proceed?
    - **[Y] Yes, Accept** — This accurately captures {{topic_name}}
    - **[E] Edit** — I have corrections to make
    - **[R] Rewrite** — Let's redraft this together using AI-assisted techniques
    </display>

    <handle option="Y">
      Mark {{topic_name}} as approved
      Display: "✓ {{topic_name}} approved."
      Proceed to next topic
    </handle>

    <handle option="E">
      Ask: "Please provide your corrections:"
      Incorporate corrections into content
      Present updated content
      Ask: "Does this now accurately reflect {{topic_name}}? [Y/N]"
      If Y: Mark approved, proceed to next topic
      If N: Loop until approved
    </handle>

    <handle option="R">
      <display>
      ---
      ## Rewrite: {{topic_name}}

      You've selected Rewrite. How would you like to approach this?

      - **[A] Advanced Elicitation** — Structured techniques (Five Whys, Socratic questioning)
      - **[P] Party Mode** — Multiple AI perspectives discuss
      - **[B] Brainstorming** — Creative exploration and idea generation
      - **[Q] Quick Questions** — 3-5 targeted questions
      - **[X] Back** — Return to approval menu
      </display>

      <handle option="A">
        Invoke {advancedElicitationTask} with context about {{topic_name}}
        After elicitation: Generate new draft, return to approval menu
      </handle>

      <handle option="P">
        Invoke {partyModeWorkflow} with context about {{topic_name}}
        After party mode: Generate new draft, return to approval menu
      </handle>

      <handle option="B">
        Invoke {brainstormingWorkflow} with context about {{topic_name}}
        After brainstorming: Generate new draft, return to approval menu
      </handle>

      <handle option="Q">
        Ask 3-5 targeted questions about {{topic_name}}
        After user answers: Synthesize into new draft, return to approval menu
      </handle>

      <handle option="X">
        Return to approval menu
      </handle>
    </handle>
  </approval-menu>
</iterate>
```

---

## TOPIC CONTENT TEMPLATES

### Topic 1: Process Health Summary

```
<format>
## Process Health Summary: {current_process_name}

### Overall Metrics

| Dimension | Current State | Assessment |
|-----------|---------------|------------|
| **Complexity** | {{total_steps}} steps, {{total_exceptions}} exceptions | {{complexity_assessment}} |
| **Pain Points** | {{total_pain_points}} identified | {{pain_assessment}} |
| **Control Gaps** | {{control_gaps}} open | {{control_assessment}} |
| **Client Effort** | CES {{ces_score}} | {{ces_assessment}} |
| **Innovation Gap** | {{must_haves}} MUST HAVEs pending | {{innovation_assessment}} |

### Heat Map

| Area | 🔴 Red | 🟡 Yellow | 🟢 Green |
|------|--------|-----------|----------|
| Process Flow | {{process_red}} | {{process_yellow}} | {{process_green}} |
| Controls | {{control_red}} | {{control_yellow}} | {{control_green}} |
| Client Experience | {{cx_red}} | {{cx_yellow}} | {{cx_green}} |
| Innovation | {{innovation_red}} | {{innovation_yellow}} | {{innovation_green}} |
</format>
```

### Topic 2: Critical Priorities

```
<format>
## 🔴 Critical Priorities (Must Address)

Based on the specialist analyses, these are RED FLAG areas requiring immediate attention:

{{#each critical_priorities}}
**{{@index}}. {{this.title}}**
- **Source:** {{this.source_agent}}
- **Issue:** {{this.description}}
- **Impact:** {{this.impact}}
- **References:** {{this.references}}

{{/each}}

{{If no critical priorities: "No critical priorities identified - the process has a solid foundation."}}
</format>
```

### Topic 3: Important Priorities

```
<format>
## 🟡 Important Priorities (Should Address)

These YELLOW FLAG areas should be addressed but are not blocking:

{{#each important_priorities}}
**{{@index}}. {{this.title}}**
- **Source:** {{this.source_agent}}
- **Issue:** {{this.description}}
- **References:** {{this.references}}

{{/each}}

### 🟢 Opportunities (Could Address)

{{#each opportunity_priorities}}
**{{@index}}. {{this.title}}**
- **Source:** {{this.source_agent}}
- **Opportunity:** {{this.description}}

{{/each}}
</format>
```

### Topic 4: Cross-Cutting Themes

```
<format>
## Cross-Cutting Themes

Looking across all four specialist analyses, I see these recurring themes:

### Theme 1: {{theme_1_title}}
{{theme_1_description}}

**Evidence:**
- Process: {{theme_1_process_evidence}}
- Controls: {{theme_1_control_evidence}}
- CX: {{theme_1_cx_evidence}}
- Innovation: {{theme_1_innovation_evidence}}

### Theme 2: {{theme_2_title}}
{{theme_2_description}}

**Evidence:**
- Process: {{theme_2_process_evidence}}
- Controls: {{theme_2_control_evidence}}
- CX: {{theme_2_cx_evidence}}
- Innovation: {{theme_2_innovation_evidence}}

### Theme 3: {{theme_3_title}}
{{theme_3_description}}

**Evidence:**
- Process: {{theme_3_process_evidence}}
- Controls: {{theme_3_control_evidence}}
- CX: {{theme_3_cx_evidence}}
- Innovation: {{theme_3_innovation_evidence}}
</format>
```

### Topic 5: Transformation Targets

```
<format>
## Potential Transformation Targets

Based on the analysis, here's what success could look like:

| Metric | AS-IS | Target (30% Improvement) | Stretch Goal |
|--------|-------|--------------------------|--------------|
| {{metric_1}} | {{asis_1}} | {{target_1}} | {{stretch_1}} |
| {{metric_2}} | {{asis_2}} | {{target_2}} | {{stretch_2}} |
| {{metric_3}} | {{asis_3}} | {{target_3}} | {{stretch_3}} |
| {{metric_4}} | {{asis_4}} | {{target_4}} | {{stretch_4}} |

### Innovation Inclusion Targets

| Priority | Count | Target Inclusion |
|----------|-------|------------------|
| MUST HAVE | {{must_have_count}} | 100% |
| SHOULD HAVE | {{should_have_count}} | 70%+ |
| COULD HAVE | {{could_have_count}} | As feasible |
| DEFER | {{defer_count}} | Future phase |
</format>
```

### Topic 6: Constraints

```
<format>
## Constraints to Consider

As we design the target state, keep these constraints in mind:

### Non-Negotiables
{{#each non_negotiables}}
- **{{this.constraint}}:** {{this.reason}} (Source: {{this.source}})
{{/each}}

### Regulatory Requirements
{{#each regulatory_requirements}}
- **{{this.regulation}}:** {{this.requirement}}
{{/each}}

### Technical Dependencies
{{#each technical_dependencies}}
- **{{this.system}}:** {{this.constraint}}
{{/each}}

### Resource Considerations
{{resource_considerations}}
</format>
```

---

### 3. Verify All Topics Approved

```
<action>Verify all 6 topics approved: Process Health, Critical Priorities, Important Priorities, Cross-Cutting Themes, Transformation Targets, Constraints</action>
```

### 4. Present Summary and Key Takeaways

Display:
```
---
**Synthesis Complete**

All 6 topics reviewed and approved:
✓ Process Health Summary
✓ Critical Priorities
✓ Important Priorities
✓ Cross-Cutting Themes
✓ Transformation Targets
✓ Constraints

**Key Takeaways:**
1. {{key_takeaway_1}}
2. {{key_takeaway_2}}
3. {{key_takeaway_3}}
```

### 5. Update Output Files (Silent)

```
<action silent="true">Update {transformationDataFile}:
  - synthesis section with all 6 approved topics
  - session.checkpoint.step = 2
  - session.last_updated = {{timestamp}}
</action>
```

### 6. Present Menu Options

```
<format>
**Progress: Step 2 of 7 - Synthesis Complete**

**Select an Option:**
- **[A]** Advanced Elicitation - Deep dive on specific areas
- **[P]** Party Mode - Get all agents' perspective on priorities
- **[C]** Continue - Proceed to target state elicitation
</format>
```

#### Menu Handling Logic:

- IF A: Execute {advancedElicitationTask}
- IF P: Execute {partyModeWorkflow}
- IF C: Load, read entire file, then execute {nextStepFile}
- IF other: Address query, then redisplay menu

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'
- After other menu items execution completes, redisplay the menu
- User can chat or ask questions - always respond, then redisplay the menu

---

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN [all 6 topics approved] and [user selects C], will you then load and read fully `{nextStepFile}` to execute and begin target state elicitation.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:
- All 6 topics presented one at a time
- Each topic approved using Y/E/R menu
- Cross-cutting themes extracted from all 4 specialist views
- Transformation targets established
- Constraints documented
- SME approves each topic before proceeding
- Menu presented and user input handled correctly

### ❌ SYSTEM FAILURE:
- Presenting all topics at once (information overload)
- Missing the [R] Rewrite option on any approval menu
- Proposing TO-BE solutions in this step
- Skipping topic approval
- Missing any of the 4 specialist perspectives
- Proceeding without user selecting Continue

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
