---
name: 'step-04-friction'
description: 'Capture friction points with FP# IDs, impact analysis, and enhancement ideas'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/cx-journey-analysis'

# File References
thisStepFile: '{workflow_path}/steps/step-04-friction.md'
nextStepFile: '{workflow_path}/steps/step-05-moments.md'
workflowFile: '{workflow_path}/workflow.md'

# Shared Protocols
protocolsFile: '{module_root}/workflows/shared/protocols/protocols.md'

# Output Files
cxJourneyFile: '{current_process_folder}/cx-journey-documentation.md'
frictionPointsFile: '{current_process_folder}/friction-points-detail.md'

# Source Files
structuredDataFile: '{current_process_folder}/structured-data.json'
painPointsDetailFile: '{current_process_folder}/pain-points-detail.md'

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
---

# Step 4: Friction Points

## STEP GOAL

Identify every point where clients experience friction — struggle, confusion, frustration, or unnecessary effort. Assign FP# IDs, analyze impact, link to touchpoints (JT#) and pain points (PP#), and capture enhancement ideas.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:
- **NEVER** generate content without user input
- **CRITICAL**: Read the complete step file before taking any action
- **CRITICAL**: When loading next step, ensure entire file is read
- YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:
- You are a Client Journey Analyst
- Continue using your established name, communication_style, and persona
- We engage in collaborative dialogue with the SME
- You bring CX analysis expertise, SME brings process experience
- Maintain professional, supportive tone throughout

### Step-Specific Rules:
- Each friction point gets a unique FP# ID using format: FP-{process_abbreviation}-### (e.g., FP-ONB-001)
- Each enhancement idea gets a unique EI# ID using format: EI-{process_abbreviation}-### (e.g., EI-ONB-001)
- MUST link friction points to JT# touchpoints
- MAY link to PP# pain points from AS-IS documentation
- Capture enhancement ideas as they emerge
- **FORBIDDEN** to discuss moments that matter or CES totals in this step

## FRICTION TYPE REFERENCE

| Friction Type | Description | Examples |
|---------------|-------------|----------|
| Effort Friction | Too much work required | Multiple forms, repeated info |
| Wait Friction | Delays and waiting | Processing time, response delays |
| Communication Friction | Unclear or missing communication | Jargon, no status updates |
| Channel Friction | Channel issues | Forced channel switches, no digital option |
| Exception Friction | When things go wrong | Error handling, edge cases |
| Information Friction | Missing or confusing info | Unclear requirements, hidden fees |

## EXECUTION PROTOCOLS

- Load protocols from `{protocolsFile}` for elicitation techniques
- Reference touchpoints (JT#) from Step 3
- Reference pain points (PP#) from AS-IS documentation
- Use advanced-elicitation-task for deep root cause analysis

## CONTEXT BOUNDARIES

- Touchpoints captured in Step 3 with JT# IDs
- AS-IS pain points (PP#) loaded and available for cross-reference
- Focus on CLIENT experience of friction, not operational issues

---

## CONTENT FORMAT SPECIFICATION

This section defines the exact formatting requirements for Section 4: Friction Point Analysis. The AI MUST follow these specifications when generating content.

### 4.1 Friction Summary (Narrative)

**Format:**
- **Structure**: 2+ paragraphs minimum
- **Paragraph 1**: Total friction points identified, severity distribution (P1/P2/P3/P4 counts)
- **Paragraph 2**: Key friction themes and patterns identified
- **Paragraph 3+**: Which stages/touchpoints have most friction, overall impact

**Example - Friction Summary:**
```
The client journey analysis identified 12 friction points across the account opening journey. The severity distribution shows 2 critical (P1), 4 high (P2), 5 medium (P3), and 1 low (P4) friction points. The total CES impact from friction is estimated at 34 points, with 4 opportunities identified as quick wins.

Three dominant friction themes emerged from the analysis. First, documentation requirements create significant effort friction, with clients required to provide the same information multiple times across different forms. Second, communication gaps during the review and approval stages leave clients uncertain about status and next steps. Third, channel switching between digital application and branch requirements disrupts the journey flow.

The Documentation stage accounts for 45% of total friction, with FP-ONB-003 (repeated data entry) and FP-ONB-004 (unclear document requirements) being the highest impact items. The Review & Approval stage contributes another 30% of friction, primarily from wait times and lack of proactive status updates. Quick win opportunities are concentrated in communication friction, where automated status notifications could address 3 friction points with minimal implementation effort.
```

### 4.2 Friction Point Summary Table

| Column | Content | Formatting Rules |
|--------|---------|------------------|
| **FP#** | Friction point ID | Format: FP-{abbrev}-### (e.g., FP-ONB-001) |
| **Friction Point** | Description | Client-perspective name, 5-10 words |
| **Stage** | Journey stage | Stage name from touchpoint mapping |
| **Touchpoint** | Linked JT# IDs | Multiple IDs if applicable (e.g., "JT-ONB-003, JT-ONB-004") |
| **Severity** | Priority level | Label with description: "P1 - Critical", "P2 - High", "P3 - Medium", "P4 - Low" |
| **CES Impact** | Effort score | Number with ranking: "8 (Rank #1)", "6 (Rank #2)" |
| **Client Emotion** | Emotional impact | Emotion with intensity: "Frustrated (High)", "Confused (Medium)" |

**Example - Friction Point Summary Table:**
```
| FP# | Friction Point | Stage | Touchpoint | Severity | CES Impact | Client Emotion |
|-----|----------------|-------|------------|----------|------------|----------------|
| FP-ONB-001 | Multiple form submissions with repeated data | Documentation | JT-ONB-003, JT-ONB-004 | P2 - High | 8 (Rank #1) | Frustrated (High) |
| FP-ONB-002 | No visibility into application status | Review | JT-ONB-005 | P1 - Critical | 7 (Rank #2) | Anxious (High) |
| FP-ONB-003 | Unclear document requirements | Documentation | JT-ONB-003 | P2 - High | 6 (Rank #3) | Confused (Medium) |
| FP-ONB-004 | Forced branch visit for verification | Verification | JT-ONB-006, JT-ONB-007 | P3 - Medium | 5 (Rank #4) | Annoyed (Medium) |
```

### 4.3 Friction by Type

**Format:**
- **Structure**: Summary table with Priority Items column, plus 1-2 sentence explanation per friction type that has significant friction

**Table Columns:**
| Column | Content |
|--------|---------|
| **Friction Type** | Type name from reference list |
| **Count** | Number of friction points of this type |
| **Combined CES Impact** | Sum of CES impact for this type |
| **Priority Items** | FP# with brief name (e.g., "FP-ONB-001 - Repeated data entry") |

**After Table**: Add 1-2 sentence explanation for each friction type with significant friction (count > 0 and CES impact > 5)

**Example - Friction by Type:**
```
| Friction Type | Count | Combined CES Impact | Priority Items |
|---------------|-------|---------------------|----------------|
| Effort Friction | 4 | 18 | FP-ONB-001 - Repeated data entry, FP-ONB-003 - Unclear requirements |
| Wait Friction | 3 | 12 | FP-ONB-002 - Status uncertainty, FP-ONB-008 - Processing delays |
| Communication Friction | 3 | 10 | FP-ONB-005 - No proactive updates, FP-ONB-009 - Jargon in notifications |
| Channel Friction | 2 | 8 | FP-ONB-004 - Forced branch visit, FP-ONB-010 - No mobile option |
| Exception Friction | 0 | 0 | — |
| Information Friction | 0 | 0 | — |

**Effort Friction** dominates this journey with 4 friction points totaling 18 CES impact. The repeated data entry requirement (FP-ONB-001) is the single highest-impact friction point, requiring clients to enter the same business details across 3 different forms.

**Wait Friction** creates significant anxiety during the review stage. Clients have no visibility into where their application is in the process, leading to unnecessary follow-up calls that create additional effort.

**Communication Friction** is concentrated in automated notifications that use banking jargon and fail to provide clear next steps or expected timelines.

**Channel Friction** forces digital-first clients to visit a branch for identity verification, disrupting the otherwise digital journey.
```

### 4.4 Friction Statistics

**Format**: Table with Metric | Value columns (keep as-is in template)

**Required Metrics:**
- Total Friction Points
- High-Severity (P1)
- Medium-Severity (P2)
- Low-Severity (P3)
- Quick Win Opportunities

**Example - Friction Statistics:**
```
| Metric | Value |
|--------|-------|
| Total Friction Points | 12 |
| High-Severity (P1) | 2 |
| Medium-Severity (P2) | 4 |
| Low-Severity (P3) | 5 |
| Low-Severity (P4) | 1 |
| Quick Win Opportunities | 4 |
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
> **Section Confidence:** 80% | **Basis:** Friction points derived from AS-IS pain point analysis with SME validation. Severity assessments based on SME expertise. CES impact estimates require further quantitative validation.
```

### Friction Points Detail Document Specification

The detail document (`friction-points-detail.md`) MUST include ALL of the following sections for each friction point:

#### Per Friction Point Structure

```markdown
### FP-XXX-###: [Friction Point Name]

#### Overview

| Attribute | Value |
|-----------|-------|
| **Friction Point ID** | FP-XXX-### |
| **Friction Point Name** | [Client-perspective name] |
| **Friction Type** | [Effort/Wait/Communication/Channel/Exception/Information] |
| **Journey Stage** | [Stage name] |
| **Linked Touchpoint(s)** | [JT# IDs, comma-separated] |
| **Severity** | [P1-Critical/P2-High/P3-Medium/P4-Low] |
| **CES Impact** | [0-10 score] |
| **Quick Win Potential** | [Yes/No] |

#### Client Experience Description

[2-3 sentences describing what the client actually experiences — what they see, feel, struggle with. Written from client perspective.]

#### Impact Analysis

**Emotional Impact:**
[1-2 sentences describing the emotional impact — frustration, confusion, anxiety, etc. Include intensity level.]

**Effort Impact:**
| Component | Additional Effort | CES Contribution |
|-----------|------------------|------------------|
| Additional Actions | [number] | [CES points] |
| Additional Documents | [number] | [CES points] |
| Additional Time (mins) | [minutes] | [CES points] |
| Channel Switches | [number] | [CES points] |
| Follow-ups Required | [number] | [CES points] |
| **Total CES Impact** | | **[total]** |

**Behavioral Impact:**
[1-2 sentences on behavioral consequences — complaints, abandonment risk, workarounds used]

**Business Impact:**
- Churn Risk: [Low/Medium/High]
- NPS Impact: [Estimated impact, e.g., "-5 to -10 points"]
- Complaint Likelihood: [Low/Medium/High]

#### Frequency & Scope

| Attribute | Value |
|-----------|-------|
| **Frequency** | [Always/Often/Sometimes/Rarely] |
| **% of Clients Affected** | [percentage] |
| **Client Segments Most Affected** | [segment names] |

#### Root Cause Analysis

**What the Client Sees/Experiences:**
[2-3 sentences describing the visible symptoms from the client perspective]

**Underlying Operational Cause:**
[2-3 sentences explaining the operational or process issue that creates this friction. Reference process steps or systems where relevant.]

**Linked Pain Points (PP#):**
| PP# | Pain Point | Connection |
|-----|------------|------------|
| [PP-XXX-###] | [Pain point name] | [How this PP causes or relates to this friction] |

#### Enhancement Ideas

**[EI-XXX-###]: [Enhancement Title]**

| Attribute | Value |
|-----------|-------|
| **Description** | [2-3 sentences describing the enhancement] |
| **Est. CES Reduction** | [0-10, how much CES this would reduce] |
| **Complexity** | [Low/Medium/High — without specific time/cost estimates] |
| **Quick Win?** | [Yes/No] |
```

**Example - Full Friction Point Detail:**
```markdown
### FP-ONB-001: Multiple form submissions with repeated data entry

#### Overview

| Attribute | Value |
|-----------|-------|
| **Friction Point ID** | FP-ONB-001 |
| **Friction Point Name** | Multiple form submissions with repeated data entry |
| **Friction Type** | Effort Friction |
| **Journey Stage** | Documentation |
| **Linked Touchpoint(s)** | JT-ONB-003, JT-ONB-004 |
| **Severity** | P2 - High |
| **CES Impact** | 8 |
| **Quick Win Potential** | No |

#### Client Experience Description

The client is asked to provide their business name, registration number, and address on the initial application form, then again on the KYC form, and a third time on the account preferences form. Each form looks different and has slightly different field labels, making the client question whether they should enter exactly the same information or something different. The repetition feels like a waste of time and signals that the bank's systems are not connected.

#### Impact Analysis

**Emotional Impact:**
Clients experience high frustration at having to re-enter the same information multiple times. This frustration intensifies with each subsequent form, often leading to verbal complaints to branch staff or negative feedback in post-onboarding surveys.

**Effort Impact:**
| Component | Additional Effort | CES Contribution |
|-----------|------------------|------------------|
| Additional Actions | 24 (8 fields × 3 forms) | 4 |
| Additional Documents | 0 | 0 |
| Additional Time (mins) | 15 | 2 |
| Channel Switches | 0 | 0 |
| Follow-ups Required | 2 | 2 |
| **Total CES Impact** | | **8** |

**Behavioral Impact:**
Some clients save partial forms and abandon the process to complete later, increasing drop-off rates. Others call customer service to ask if they "really need to fill this in again," creating unnecessary support volume.

**Business Impact:**
- Churn Risk: Medium
- NPS Impact: -5 to -8 points
- Complaint Likelihood: High

#### Frequency & Scope

| Attribute | Value |
|-----------|-------|
| **Frequency** | Always |
| **% of Clients Affected** | 100% |
| **Client Segments Most Affected** | All segments equally affected |

#### Root Cause Analysis

**What the Client Sees/Experiences:**
The client sees three separate forms that each request their business name, registration number, and registered address. The field labels are slightly different ("Business Name" vs "Company Name" vs "Legal Entity Name"), creating confusion about whether identical information should be entered. No explanation is provided for why the information is needed again.

**Underlying Operational Cause:**
The three forms are owned by different departments (Sales, Compliance, Operations) and feed into different backend systems that do not share data. Each system was implemented independently, and integration was deemed too expensive during initial implementation. The forms have never been consolidated because each department considers their specific field labels to be required for their downstream processing.

**Linked Pain Points (PP#):**
| PP# | Pain Point | Connection |
|-----|------------|------------|
| PP-ONB-012 | Disconnected departmental systems | Root cause — systems don't share customer data |
| PP-ONB-015 | Manual data reconciliation | Effect — staff must reconcile data across systems |

#### Enhancement Ideas

**EI-ONB-001: Pre-populate forms from initial application**

| Attribute | Value |
|-----------|-------|
| **Description** | Implement data pass-through so that business information entered on the initial application form is pre-populated on subsequent KYC and account preferences forms. Client can review and confirm rather than re-enter. |
| **Est. CES Reduction** | 6 |
| **Complexity** | High — requires integration between three departmental systems |
| **Quick Win?** | No |

**EI-ONB-002: Consolidate forms into single multi-section form**

| Attribute | Value |
|-----------|-------|
| **Description** | Redesign the three separate forms into a single multi-section form with clear progress indicator. Business information entered once at the top, then referenced throughout. |
| **Est. CES Reduction** | 7 |
| **Complexity** | Medium — requires form redesign and stakeholder alignment |
| **Quick Win?** | No |
```

---

## EXECUTION SEQUENCE

### 1. Display Progress and Context

```
**Progress: Step 4 of 7 - Friction Points**

Now let's identify where clients struggle, get frustrated, or experience unnecessary effort.

Friction is anything that:
- Makes the client work harder than necessary
- Causes confusion or frustration
- Leads to complaints or abandonment
- Creates anxiety or stress
```

### 2. Display Pain Points Reference

```
<format>
**Pain Points from AS-IS Documentation:**

These are the operational pain points already documented. Some may directly cause client friction:

| PP# | Pain Point | Severity |
|-----|------------|----------|
{{for each pp in loaded_pain_points}}
| {{pp.id}} | {{pp.name}} | {{pp.severity}} |
{{/for}}

We'll link friction points to these where relevant.
</format>
```

### 3. Friction Discovery by Touchpoint

```
<format>
Let's walk through each touchpoint and identify friction.
</format>

<loop name="friction_by_touchpoint" for="each touchpoint in captured_touchpoints">

  <format>
  ---
  **Touchpoint: {{touchpoint.id}} - {{touchpoint.name}}**
  Channel: {{touchpoint.channel}}
  What client does: {{touchpoint.what_client_does}}
  </format>

  <ask response="touchpoint_friction">
  Does the client experience any friction at this touchpoint?

  - [ ] Yes, there's friction here
  - [ ] No significant friction
  </ask>

  <check if="touchpoint_friction == 'Yes'">

    <ask response="friction.name">
    Describe the friction in one sentence from the client's perspective:
    </ask>

    <format>
    **Friction Point: {{friction.name}}** → Assigning ID: FP-{process_abbreviation}-{{next_id_padded}}
    </format>

    <ask response="friction.type">
    What type of friction is this?

    - [ ] Effort Friction - Too much work required
    - [ ] Wait Friction - Delays and waiting
    - [ ] Communication Friction - Unclear or missing communication
    - [ ] Channel Friction - Channel issues or forced switches
    - [ ] Exception Friction - When things go wrong
    - [ ] Information Friction - Missing or confusing information
    </ask>

    <ask response="friction.client_experience">
    Describe what the client actually experiences. What do they see, feel, or struggle with?
    </ask>

    <ask response="friction.emotional_impact">
    What emotional impact does this have on the client?
    (e.g., frustrated, confused, anxious, angry, disappointed)
    </ask>

    <ask response="friction.severity">
    How severe is this friction?

    - [ ] P1 - Critical: Causes abandonment or serious complaints
    - [ ] P2 - High: Significant frustration, may affect NPS
    - [ ] P3 - Medium: Noticeable inconvenience
    - [ ] P4 - Low: Minor annoyance
    </ask>

    <ask response="friction.ces_impact">
    How much additional effort does this friction cause? (estimate CES impact 0-10)
    </ask>

    <ask response="friction.frequency">
    How often does this friction occur?

    - [ ] Always - Every client experiences this
    - [ ] Often - Most clients experience this
    - [ ] Sometimes - Some clients experience this
    - [ ] Rarely - Edge cases only
    </ask>

    <ask response="friction.percentage_affected">
    What percentage of clients are affected by this friction? (estimate %)
    </ask>

    <ask response="friction.linked_pain_points">
    Does this friction link to any documented pain points (PP#)?
    (Enter PP# IDs if applicable, or "None")
    </ask>

    <format>
    **Root Cause Analysis for FP{{current_id}}**
    </format>

    <ask response="friction.client_visible_symptoms">
    What does the client see or experience as symptoms of this friction?
    </ask>

    <ask response="friction.operational_cause">
    What operational issue causes this friction?
    (Reference the process steps or systems involved)
    </ask>

    <ask response="friction.client_workarounds">
    Do clients have any workarounds for this friction?
    If so, what do they do to cope?
    </ask>

    <format>
    **Enhancement Ideas for FP-{process_abbreviation}-{{current_id_padded}}**
    </format>

    <ask response="friction.enhancement_ideas">
    What ideas do you have to eliminate or reduce this friction?
    (We'll capture each as an EI# enhancement idea)
    </ask>

    <loop name="enhancement_capture" for="each idea in friction.enhancement_ideas">
      <format>
      **Enhancement Idea: {{idea.title}}** → Assigning ID: EI-{process_abbreviation}-{{next_ei_id_padded}}
      </format>

      <ask response="idea.ces_reduction">
      How much CES reduction would this enhancement provide? (estimate 0-10)
      </ask>

      <ask response="idea.complexity">
      How complex would this enhancement be to implement?

      - [ ] Low - Quick win, minimal effort
      - [ ] Medium - Moderate effort, some dependencies
      - [ ] High - Significant effort, major changes needed
      </ask>

      <ask response="idea.is_quick_win">
      Would you consider this a "quick win"? (Low effort, high impact)

      - [ ] Yes - Quick win
      - [ ] No - Not a quick win
      </ask>
    </loop>

  </check>

</loop>
```

### 4. Additional Friction Discovery

```
<ask response="additional_friction">
Are there any other friction points that don't map directly to a specific touchpoint?
(e.g., overall journey complexity, lack of visibility, cross-channel issues)

- [ ] Yes, I have more friction points to add
- [ ] No, we've covered them all
</ask>

<check if="additional_friction == 'Yes'">
  <loop name="additional_friction_capture" until="user says done">
    <!-- Repeat friction capture questions from Section 3 -->
  </loop>
</check>
```

### 5. Friction Patterns

```
<ask response="friction_patterns">
Looking at all the friction points we've identified, do you see any patterns or themes?
(e.g., "Most friction is in the documentation phase", "Channel switching is a consistent issue")
</ask>

<ask response="systemic_issues">
Are any of these friction points caused by the same underlying systemic issue?
(If so, describe the systemic issue and which FP# items it affects)
</ask>
```

### 6. AI Assessment: Section Confidence

```
<action name="assess_friction_confidence">
Based on the friction point information captured in this step, the AI MUST:

1. Calculate section confidence:
   - Count "Accept" responses vs "Edit" responses
   - Assess source quality (PP# pain points from AS-IS vs new friction identified)
   - Note linkage completeness (FP# to JT# and PP# cross-references)

2. Determine confidence level:
   - HIGH: All friction validated, strong PP# linkage, clear severity assessments
   - MEDIUM: Some edits needed, partial PP# mapping, some severity estimates (DEFAULT if uncertain)
   - LOW: Significant new friction identified, weak cross-references, severity disputed

3. Generate confidence basis automatically:
   - "Based on AS-IS pain point analysis" (if most FP# derived from PP#)
   - "Based on SME validation with cross-reference mapping" (if edits were minimal)
   - "Based on SME expertise with limited documentation" (if many new friction points)

CRITICAL: Do NOT ask the user for confidence level or basis.
The AI makes this judgment call based on what was captured.
</action>

<set>
section_4_confidence: {{calculated_confidence_level}}
section_4_confidence_basis: {{generated_confidence_basis}}
</set>
```

### 7. Update Output Files

```
<action name="write_friction_points_file" CRITICAL="MANDATORY">
WRITE to {frictionPointsFile}:

IMPORTANT: You MUST write actual content, not placeholders.
Write the FULL document structure with all captured friction data.

---

# Friction Points Detail: {{process_name}}

**Process ID:** {current_process_id}
**Document Type:** Client Friction Analysis
**Last Updated:** {{current_date}}
**Related Document:** [CX Journey Documentation](./cx-journey-documentation.md)

---

## Executive Summary

{{#Write 2-3 sentences summarizing:}}
- Total friction points identified and severity distribution
- Key friction themes
- Total CES impact and quick win potential
{{/Write summary}}

---

## Friction Point Summary Table

| FP# | Friction Point | Stage | Touchpoint | Severity | CES Impact | Quick Win? |
|-----|----------------|-------|------------|----------|------------|------------|
{{#for each accepted_friction_point}}
| {{fp.id}} | {{fp.name}} | {{fp.stage}} | {{fp.linked_jt}} | {{fp.severity}} | {{fp.ces_impact}} | {{fp.quick_win}} |
{{/for}}

---

## Friction Statistics

| Metric | Value |
|--------|-------|
| Total Friction Points Identified | {{total_friction_points}} |
| High-Severity (P1) | {{high_severity_count}} |
| Medium-Severity (P2) | {{medium_severity_count}} |
| Low-Severity (P3) | {{low_severity_count}} |
| Total CES Impact | {{total_ces_impact}} |
| Quick Win Opportunities | {{quick_win_count}} |
| Systemic Issues | {{systemic_count}} |

---

## Friction Categories

| Friction Type | Count | Combined CES Impact | Top Priority |
|---------------|-------|---------------------|--------------|
| Effort Friction | {{effort_friction_count}} | {{effort_friction_ces}} | {{effort_top_priority}} |
| Wait Friction | {{wait_friction_count}} | {{wait_friction_ces}} | {{wait_top_priority}} |
| Communication Friction | {{comm_friction_count}} | {{comm_friction_ces}} | {{comm_top_priority}} |
| Channel Friction | {{channel_friction_count}} | {{channel_friction_ces}} | {{channel_top_priority}} |
| Exception Friction | {{exception_friction_count}} | {{exception_friction_ces}} | {{exception_top_priority}} |
| Information Friction | {{info_friction_count}} | {{info_friction_ces}} | {{info_top_priority}} |

---

## Detailed Friction Point Analysis

{{#for each accepted_friction_point}}

### {{fp.id}}: {{fp.name}}

#### Overview

| Attribute | Value |
|-----------|-------|
| **Friction Point ID** | {{fp.id}} |
| **Friction Point Name** | {{fp.name}} |
| **Friction Type** | {{fp.type}} |
| **Journey Stage** | {{fp.stage}} |
| **Linked Touchpoint(s)** | {{fp.linked_touchpoints}} |
| **Severity** | {{fp.severity}} |
| **CES Impact** | {{fp.ces_impact}} |
| **Quick Win Potential** | {{fp.quick_win}} |

#### Client Experience Description

{{fp.client_experience_description}}

#### Impact Analysis

**Emotional Impact:**
{{fp.emotional_impact}}

**Effort Impact:**
| Component | Additional Effort | CES Contribution |
|-----------|------------------|------------------|
| Additional Actions | {{fp.additional_actions}} | {{fp.actions_ces}} |
| Additional Documents | {{fp.additional_documents}} | {{fp.docs_ces}} |
| Additional Time (mins) | {{fp.additional_time}} | {{fp.time_ces}} |
| Channel Switches | {{fp.channel_switches}} | {{fp.switch_ces}} |
| Follow-ups Required | {{fp.follow_ups}} | {{fp.followup_ces}} |
| **Total CES Impact** | | **{{fp.ces_impact}}** |

**Behavioral Impact:**
{{fp.behavioral_impact}}

**Business Impact:**
- Churn Risk: {{fp.churn_risk}}
- NPS Impact: {{fp.nps_impact}}
- Complaint Likelihood: {{fp.complaint_likelihood}}

#### Frequency & Scope

| Attribute | Value |
|-----------|-------|
| **Frequency** | {{fp.frequency}} |
| **% of Clients Affected** | {{fp.percentage_affected}} |
| **Client Segments Most Affected** | {{fp.segments_affected}} |

#### Root Cause Analysis

**What the Client Sees/Experiences:**
{{fp.client_visible_symptoms}}

**Underlying Operational Cause:**
{{fp.operational_cause}}

**Linked Pain Points (PP#):**
| PP# | Pain Point | Connection |
|-----|------------|------------|
{{#for each linked_pp}}
| {{pp.id}} | {{pp.name}} | {{pp.connection}} |
{{/for}}

#### Enhancement Ideas

{{#for each enhancement in fp.enhancement_ideas}}
**{{ei.id}}: {{ei.title}}**

| Attribute | Value |
|-----------|-------|
| **Description** | {{ei.description}} |
| **Est. CES Reduction** | {{ei.ces_reduction}} |
| **Complexity** | {{ei.complexity}} |
| **Quick Win?** | {{ei.is_quick_win}} |

{{/for}}

---

{{/for each friction_point}}

## Enhancement Ideas Catalog

| EI# | Target Friction (FP#) | Enhancement | CES Reduction | Complexity | Priority |
|-----|----------------------|-------------|---------------|------------|----------|
{{#for each enhancement_idea}}
| {{ei.id}} | {{ei.target_fp}} | {{ei.description}} | {{ei.ces_reduction}} | {{ei.complexity}} | {{ei.priority}} |
{{/for}}

---

## Traceability Matrix

### Friction to Pain Points

| FP# | Related PP# | Connection Type |
|-----|-------------|-----------------|
{{#for each friction_to_pp}}
| {{fp.id}} | {{pp.id}} | {{connection}} |
{{/for}}

### Friction to Touchpoints

| FP# | Related JT# | Where in Touchpoint |
|-----|-------------|---------------------|
{{#for each friction_to_jt}}
| {{fp.id}} | {{jt.id}} | {{location}} |
{{/for}}

---

## Change Log

| Date | Contributor | Role | Changes |
|------|-------------|------|---------|
| {{current_date}} | {contributor_name} | {contributor_role} | Initial friction analysis |

---

_Generated by ProcessMiner Client Journey Analyst_

</action>

<action name="write_cx_journey_section_4" CRITICAL="MANDATORY">
APPEND to {cxJourneyFile} - Section 4 (Friction Point Analysis):

---

## 4. Friction Point Analysis

> **About this section:** Summary of friction points. For full details including root cause analysis and enhancement ideas, see [Friction Points Detail](./friction-points-detail.md).

### 4.1 Friction Summary

{{#Write a narrative paragraph summarizing:}}
- Total friction points and severity distribution
- Key friction themes/patterns
- Which stages/touchpoints have most friction
{{/Write narrative}}

### 4.2 Friction Point Summary Table

| FP# | Friction Point | Stage | Touchpoint | Severity | CES Impact | Client Emotion |
|-----|----------------|-------|------------|----------|------------|----------------|
{{#for each accepted_friction_point}}
| {{fp.id}} | {{fp.name}} | {{fp.stage}} | {{fp.linked_jt}} | {{fp.severity}} | {{fp.ces_impact}} | {{fp.emotion}} |
{{/for}}

### 4.3 Friction by Type

| Friction Type | Count | Combined CES Impact | Priority Items |
|---------------|-------|---------------------|----------------|
{{#for each friction_type}}
| {{type.name}} | {{type.count}} | {{type.ces}} | {{type.priority_fps}} |
{{/for}}

### 4.4 Friction Statistics

| Metric | Value |
|--------|-------|
| Total Friction Points | {{total_friction_points}} |
| High-Severity (P1) | {{high_severity_count}} |
| Medium-Severity (P2) | {{medium_severity_count}} |
| Low-Severity (P3) | {{low_severity_count}} |
| Quick Win Opportunities | {{quick_win_count}} |

> **Full Analysis:** [View Friction Points Detail](./friction-points-detail.md)
>
> **Section Confidence:** {{section_4_confidence}} | **Basis:** {{section_4_confidence_basis}}

---

</action>

<action name="update_touchpoints_with_friction" CRITICAL="MANDATORY">
UPDATE {clientTouchpointsFile} - Add friction links to each touchpoint:

For each touchpoint that has friction:
- Update the "Linked Friction Points" section
- Add table: | FP# | Friction Point | Severity | Status |
</action>

<verification>
AFTER WRITING: Confirm files contain:

{frictionPointsFile}:
- [ ] Executive summary paragraph
- [ ] Friction Point Summary Table with all FP# entries
- [ ] Friction Statistics table filled
- [ ] Friction Categories table filled
- [ ] Detailed analysis for EACH friction point (Overview, Client Experience, Impact Analysis, Frequency, Root Cause, Enhancement Ideas)
- [ ] Enhancement Ideas Catalog
- [ ] Traceability Matrix (FP to PP, FP to JT)
- [ ] Change Log entry

{cxJourneyFile} Section 4:
- [ ] Narrative summary paragraph
- [ ] Friction Point Summary Table with all columns
- [ ] Friction by Type breakdown table
- [ ] Friction Statistics table
- [ ] Section Confidence and Basis

{clientTouchpointsFile}:
- [ ] Each touchpoint's "Linked Friction Points" section updated
</verification>
```

### 8. Summary and Transition

Display:
```
**Friction Points Captured**

| Metric | Value |
|--------|-------|
| Total Friction Points | {{total_friction_points}} |
| P1 (Critical) | {{p1_count}} |
| P2 (High) | {{p2_count}} |
| P3/P4 (Medium/Low) | {{p3p4_count}} |
| Total CES Impact | {{total_ces_impact}} |
| Enhancement Ideas | {{total_enhancement_ideas}} |
| Quick Wins | {{quick_win_count}} |
| Confidence | {{section_4_confidence}} |

Next, we'll identify the "moments that matter" and analyze overall CES.
```

### 9. Proceed to Next Step

Display:
```
**Progress: Step 4 of 8 - Friction Points Complete**

Now let's identify the critical moments and analyze client effort across the journey.
```

```
<action>Load, read entire file, then execute {nextStepFile}</action>
```

---

## CRITICAL STEP COMPLETION NOTE

This is an auto-proceed step. IMMEDIATELY after [all friction points captured] and [output files updated], load and read fully `{nextStepFile}` to execute and begin moments that matter identification.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:
- Friction points identified for each touchpoint with friction
- Each friction point has FP# ID
- Impact analysis complete (severity, CES impact, frequency)
- Root cause captured
- Enhancement ideas captured with EI# IDs
- Linked to JT# touchpoints
- Linked to PP# pain points where applicable
- Confidence assessment captured
- Both output files updated
- Ready to proceed to Step 5

### SYSTEM FAILURE:
- Did not assign FP# IDs
- Did not link to JT# touchpoints
- Did not capture enhancement ideas
- Did not assess severity and CES impact
- Started discussing moments that matter
- Did not update output files
- Skipped to later steps

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
