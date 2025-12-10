---
name: 'step-02-journey-overview'
description: 'Capture journey identification, client persona, and journey context using AI-first analysis'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/cx-journey-analysis'

# File References
thisStepFile: '{workflow_path}/steps/step-02-journey-overview.md'
nextStepFile: '{workflow_path}/steps/step-03-touchpoints.md'
workflowFile: '{workflow_path}/workflow.md'

# Shared Protocols
protocolsFile: '{module_root}/workflows/shared/protocols/protocols.md'

# Output Files
cxJourneyFile: '{current_process_folder}/cx-journey-documentation.md'

# Source Files
asIsDocFile: '{current_process_folder}/as-is-process-documentation.md'
structuredDataFile: '{current_process_folder}/structured-data.json'

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
---

# Step 2: Journey Overview

## STEP GOAL

Capture the client journey perspective: what the client is trying to achieve, who they are, and the context of their journey. This reframes the operational process from the client's point of view.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:
- **AI ANALYZES FIRST** — Examine existing documentation before asking questions
- **PROPOSE, DON'T ASK** — Present structured proposals for SME validation
- **CRITICAL**: Read the complete step file before taking any action
- **CRITICAL**: When loading next step, ensure entire file is read

### Role Reinforcement:
- You are a Client Journey Analyst
- Continue using your established name, communication_style, and persona
- You bring CX analysis expertise AND proactive documentation analysis
- SME validates your proposals, not builds from scratch
- Maintain professional, supportive tone throughout

### AI-First Analysis Pattern:
1. **Analyze** existing AS-IS documentation and structured data
2. **Propose** structured answers based on what you find
3. **Present** with confidence score and source references
4. **SME Validates**: Accept / Edit / Deep Dive

### Step-Specific Rules:
- Reference loaded AS-IS documentation to ground proposals
- Focus on CLIENT perspective, not operational details
- Infer client intent from process purpose and triggers
- **FORBIDDEN** to start identifying touchpoints in this step

## EXECUTION PROTOCOLS

- Load protocols from `{protocolsFile}` — especially `ai_first_analysis`
- Use advanced-elicitation-task ONLY when SME requests Deep Dive
- Focus on the "why" from the client's perspective

## CONTEXT BOUNDARIES

- Session initialized in Step 1
- AS-IS documentation loaded and available
- `{current_process_folder}`, `{current_process_id}`, `{current_process_name}` are set
- Client segment identified

---

## CONTENT FORMAT SPECIFICATION

This section defines the exact formatting requirements for Section 1: Journey Overview. The AI MUST follow these specifications when generating content.

### 1.1 Journey Identification (Table)

| Attribute | Value | Formatting Rules |
|-----------|-------|------------------|
| **Journey Name** | {{journey_name}} | Client perspective phrase (e.g., "Getting my business account set up") |
| **Process ID** | {{process_id}} | As captured in Step 1 |
| **Client Goal** | {{client_goal}} | Both goal + outcome in one statement |
| **Journey Trigger** | {{journey_trigger}} | Always include the actor (e.g., "Client submits application...") |
| **Success Outcome** | {{success_outcome}} | Narrative + measurable criteria |
| **Typical Duration** | {{typical_duration}} | Either range or target (e.g., "3-5 business days" or "Within 5 business days") |

**Example - Journey Identification:**
```
| Attribute | Value |
|-----------|-------|
| **Journey Name** | Getting my business account set up |
| **Process ID** | PROC-ONB-001 |
| **Client Goal** | Open a fully operational business account that allows me to manage payments, receive funds, and access digital banking services |
| **Journey Trigger** | Business owner submits application through the online portal or via Relationship Manager |
| **Success Outcome** | Account active with cards issued, online banking access enabled, and first transaction completed. Measurable: account operational within SLA, client can transact |
| **Typical Duration** | 3-5 business days |
```

### 1.2 Client Persona (Table)

| Attribute | Value | Formatting Rules |
|-----------|-------|------------------|
| **Segment** | {{client_segment}} | From config/structured data |
| **Typical Profile** | {{client_profile}} | Both demographics + behavioral characteristics |
| **Key Motivations** | {{client_motivations}} | Prioritized list (most important first) |
| **Expected Experience** | {{expected_experience}} | Industry expectations + competitor benchmarks |

**Example - Client Persona:**
```
| Attribute | Value |
|-----------|-------|
| **Segment** | BizBanking (SME) |
| **Typical Profile** | SME owner, 5-20 employees, €1-5M revenue. Time-poor, digital-first, expects quick responses. Often managing finances personally alongside running the business |
| **Key Motivations** | 1. Speed — need account operational quickly to not miss business opportunities. 2. Simplicity — minimal paperwork and clear requirements. 3. Reliability — confidence the bank will deliver on promises |
| **Expected Experience** | Industry: Same-day decisions, digital-first applications. Competitors: Fintech banks offering 10-minute onboarding. Expectation of real-time status visibility and proactive communication |
```

### 1.3 Journey Context

**Format:**
- **Structure**: 2-3 paragraphs minimum, covering different aspects
- **Plus**: Bullet points when required for specific details

**Content MUST cover:**
1. Client's emotional state entering the journey
2. Time pressure / urgency factors
3. Competitive alternatives available
4. Relationship context (new vs existing client)

**Example - Journey Context:**
```
Clients entering this journey are typically experiencing a mix of anticipation and anxiety. For new business owners, this may be their first banking relationship for the company, creating uncertainty about requirements and timelines. Existing clients expanding operations may feel frustrated if the process doesn't reflect their established relationship with the bank.

Time pressure is a significant factor for most clients. New businesses often have immediate operational needs — suppliers to pay, customer payments to receive, or payroll deadlines. A delay in account opening can directly impact their ability to operate. This urgency is heightened for seasonal businesses or those with time-sensitive opportunities.

The competitive landscape offers clients multiple alternatives:
- Traditional banks with established business banking propositions
- Fintech challengers offering rapid digital onboarding (some claiming 10-minute account opening)
- Existing banking relationships that could be expanded instead

Clients are increasingly aware of these alternatives and benchmark their experience accordingly. First-time business owners may have consumer banking expectations shaped by mobile-first experiences, while experienced business owners compare against previous corporate banking relationships.
```

### Section Confidence Statement

**Format:**
```
> **Section Confidence:** {{percentage}}% | **Basis:** {{ai_inferred_basis}}
```

- **Confidence**: AI-inferred percentage (0-100%)
- **Basis**: AI-inferred assessment explaining the confidence level

**Example:**
```
> **Section Confidence:** 85% | **Basis:** Journey identification derived from AS-IS documentation. Client persona based on segment data with SME behavioral assumptions. Journey context inferred from pain points and industry knowledge.
```

---

## EXECUTION SEQUENCE

### 1. Display Progress

```
**Progress: Step 2 of 8 - Journey Overview**

Let me analyze your existing documentation and propose the journey overview.
```

### 2. AI Analysis: Journey Identification

```
<action name="analyze_journey_identification">
Analyze {asIsDocFile} and {structuredDataFile} to extract:
- Process name, purpose, trigger from documentation
- Infer client's perspective name for this journey
- Infer client goal from process purpose
- Infer journey trigger from client's viewpoint
- Infer success outcome from process completion criteria
- Note typical duration if mentioned

Calculate confidence based on:
- Explicit mentions = high confidence
- Reasonable inferences = medium confidence
- Gaps requiring SME input = low confidence
</action>

<format>
**AI Analysis: Journey Identification** (Confidence: {{confidence}}%)

Based on your AS-IS documentation, here's my understanding:

| Attribute | Proposed Value | Source |
|-----------|---------------|--------|
| **Journey Name** (client's view) | {{proposed_journey_name}} | Inferred from: {{source}} |
| **Client Goal** | {{proposed_client_goal}} | Inferred from: {{source}} |
| **Journey Trigger** | {{proposed_journey_trigger}} | Inferred from: {{source}} |
| **Success Outcome** | {{proposed_success_outcome}} | Inferred from: {{source}} |
| **Typical Duration** | {{proposed_duration}} | {{source_or_gap}} |

**Key Insight:** {{any_notable_gap_between_bank_view_and_client_view}}

---
How would you like to proceed?
- **[A] Accept** — This accurately captures the journey
- **[E] Edit** — I have corrections or additions
- **[D] Deep Dive** — Let's explore this further
</format>

<handle option="A">
  <action>Save journey identification as accepted</action>
  <action>Proceed to Section 3 (Client Persona)</action>
</handle>

<handle option="E">
  <ask>What would you like to change or add?</ask>
  <action>Apply edits and re-present for confirmation</action>
</handle>

<handle option="D">
  <display>
  **Deep Dive Options:**
  - **[A] Advanced Elicitation** — Structured techniques (5 Whys, SIPOC, etc.)
  - **[Q] Quick Questions** — Targeted clarifying questions
  - **[X] Back** — Return to proposal
  </display>
  <action>Execute selected technique, integrate results, re-present</action>
</handle>
```

### 3. AI Analysis: Client Persona

```
<action name="analyze_client_persona">
Analyze {asIsDocFile} and {structuredDataFile} to extract:
- Client segment (already captured in Step 1)
- Business type indicators from process context
- Decision-maker role from process actors
- Infer motivations from process purpose and pain points
- Infer expectations from industry context (banking/financial services)

Calculate confidence based on available data.
</action>

<format>
**AI Analysis: Client Persona** (Confidence: {{confidence}}%)

Based on your documentation and the {{client_segment}} segment:

| Attribute | Proposed Value | Source |
|-----------|---------------|--------|
| **Typical Profile** | {{proposed_profile}} | Inferred from: {{source}} |
| **Key Motivations** | {{proposed_motivations}} | Inferred from: {{source}} |
| **Expected Experience** | {{proposed_expectations}} | Industry knowledge + {{source}} |

{{#if low_confidence_areas}}
**Areas needing your input:**
{{list_low_confidence_areas}}
{{/if}}

---
How would you like to proceed?
- **[A] Accept** — This captures our typical client
- **[E] Edit** — I have corrections or additions
- **[D] Deep Dive** — Let's explore this further
</format>

<handle option="A">
  <action>Save client persona as accepted</action>
  <action>Proceed to Section 4 (Journey Context)</action>
</handle>

<handle option="E">
  <ask>What would you like to change or add?</ask>
  <action>Apply edits and re-present for confirmation</action>
</handle>

<handle option="D">
  <action>Execute selected deep dive technique</action>
</handle>
```

### 4. AI Analysis: Journey Context

```
<action name="analyze_journey_context">
Analyze {asIsDocFile} and {structuredDataFile} to extract:
- First interaction vs existing client (from process trigger)
- Time pressures (from SLAs, urgency indicators)
- Emotional stakes (from pain points, exception handling)
- Alternatives (industry knowledge)
</action>

<format>
**AI Analysis: Journey Context** (Confidence: {{confidence}}%)

| Context Factor | Proposed Understanding | Source |
|---------------|----------------------|--------|
| **Client Type** | {{new_vs_existing}} | {{source}} |
| **Time Pressure** | {{urgency_level}} | {{source}} |
| **Emotional Stakes** | {{emotional_context}} | {{source}} |
| **Alternatives** | {{competitive_context}} | Industry knowledge |

---
How would you like to proceed?
- **[A] Accept** — This captures the context
- **[E] Edit** — I have corrections or additions
- **[D] Deep Dive** — Let's explore this further
</format>

<handle_responses_as_above>
```

### 5. AI Assessment: Overall Confidence

```
<action name="assess_overall_confidence">
Based on the information captured in this step, the AI MUST:

1. Calculate section confidence:
   - Count "Accept" responses vs "Edit" responses
   - Assess source quality (explicit documentation vs inference)
   - Note any gaps flagged during analysis

2. Determine confidence level:
   - HIGH: All proposals accepted, strong documentation sources, no major gaps
   - MEDIUM: Some edits needed, mixed sources, minor gaps (DEFAULT if uncertain)
   - LOW: Significant edits, mostly inference-based, notable gaps

3. Generate confidence basis automatically:
   - "Based on AS-IS documentation analysis" (if most data from docs)
   - "Based on SME validation of AI proposals" (if edits were minimal)
   - "Based on limited source data with SME supplementation" (if many edits)

CRITICAL: Do NOT ask the user for confidence level or basis.
The AI makes this judgment call based on what was captured.
</action>

<set>
section_confidence: {{calculated_confidence_level}}
confidence_basis: {{generated_confidence_basis}}
</set>
```

### 6. Update Output File

```
<action name="write_cx_journey_file" CRITICAL="MANDATORY">
WRITE to {cxJourneyFile} - Section 1 (Journey Overview):

IMPORTANT: You MUST write actual content to the file, not placeholders.
Use the accepted values from the previous sections.

---

## 1. Journey Overview

> **About this section:** What is this journey from the client's perspective? What outcome are they trying to achieve?

### 1.1 Journey Identification

| Attribute | Value |
|-----------|-------|
| **Journey Name** | {{accepted_journey_name}} |
| **Process ID** | {current_process_id} |
| **Client Goal** | {{accepted_client_goal}} |
| **Journey Trigger** | {{accepted_journey_trigger}} |
| **Success Outcome** | {{accepted_success_outcome}} |
| **Typical Duration** | {{accepted_duration}} |

### 1.2 Client Persona

| Attribute | Value |
|-----------|-------|
| **Segment** | {client_segment} |
| **Typical Profile** | {{accepted_client_profile}} |
| **Key Motivations** | {{accepted_client_motivations}} |
| **Expected Experience** | {{accepted_expected_experience}} |

### 1.3 Journey Context

{{#Write a narrative paragraph combining:}}
- Client type: {{accepted_client_type}}
- Time pressure: {{accepted_time_pressure}}
- Emotional stakes: {{accepted_emotional_stakes}}
- Alternatives available: {{accepted_alternatives}}
{{/Write narrative paragraph}}

> **Section Confidence:** {{section_confidence}} | **Basis:** {{confidence_basis}}

---

</action>

<verification>
AFTER WRITING: Confirm the file now contains:
- [ ] Journey Identification table with all 6 attributes filled
- [ ] Client Persona table with all 4 attributes filled
- [ ] Journey Context narrative paragraph
- [ ] Section Confidence and Basis line
</verification>
```

### 7. Summary and Transition

Display:
```
**Journey Overview Captured**

| Attribute | Value |
|-----------|-------|
| Journey Name | {{accepted_journey_name}} |
| Client Goal | {{accepted_client_goal}} |
| Trigger | {{accepted_journey_trigger}} |
| Success Outcome | {{accepted_success_outcome}} |
| Client Profile | {{accepted_client_profile}} |
| Confidence | {{section_confidence}} |

{{#if key_insights}}
**Key Insights:**
{{list_key_insights}}
{{/if}}

Next: I'll analyze your process steps to identify client touchpoints.
```

### 8. Proceed to Next Step

```
**Progress: Step 2 of 8 - Journey Overview Complete**
```

```
<action>Load, read entire file, then execute {nextStepFile}</action>
```

---

## CRITICAL STEP COMPLETION NOTE

This is an auto-proceed step. IMMEDIATELY after [journey overview captured] and [output file updated], load and read fully `{nextStepFile}` to execute and begin touchpoint identification.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:
- AI analyzed documentation BEFORE asking questions
- Proposals presented with confidence scores and sources
- SME validated (Accept/Edit/Deep Dive) — not asked to build from scratch
- Journey name captured (client perspective)
- Client goal and trigger identified
- Success outcome defined
- Client persona built
- Journey context understood
- Confidence assessment captured
- Output file updated
- Ready to proceed to Step 3

### SYSTEM FAILURE:
- Asked open-ended questions without proposing answers first
- Made SME build content from scratch
- Used operational terminology instead of client perspective
- Started identifying touchpoints
- Did not capture confidence assessment
- Did not update output file
- Skipped to later steps

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
