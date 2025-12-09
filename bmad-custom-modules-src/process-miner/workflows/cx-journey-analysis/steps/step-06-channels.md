---
name: 'step-06-channels'
description: 'Analyze channel usage, switching patterns, and optimization opportunities'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/cx-journey-analysis'

# File References
thisStepFile: '{workflow_path}/steps/step-06-channels.md'
nextStepFile: '{workflow_path}/steps/step-07-research.md'
workflowFile: '{workflow_path}/workflow.md'

# Shared Protocols
protocolsFile: '{module_root}/workflows/shared/protocols/protocols.md'

# Output Files
cxJourneyFile: '{current_process_folder}/cx-journey-documentation.md'
clientTouchpointsFile: '{current_process_folder}/client-touchpoints-detail.md'

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
---

# Step 6: Channel Analysis

## STEP GOAL

Analyze how clients use different channels throughout the journey, identify channel switching patterns and friction, and capture channel optimization opportunities.

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
- Channel analysis builds on touchpoint data from Step 3
- Each channel gets a CH# identifier
- Channel switches contribute to CES (already calculated)
- **FORBIDDEN** to start validation or gap analysis in this step

## CHANNEL TYPES REFERENCE

| Channel Type | Category | Examples |
|--------------|----------|----------|
| Branch | Physical | In-person visits |
| Phone | Voice | Call center, IVR |
| Email | Async Digital | Email communication |
| Portal | Digital Self-Service | Online banking, website |
| Mobile | Digital Self-Service | Mobile app |
| SMS | Async Digital | Text messages |
| Mail | Physical | Postal correspondence |
| RM Direct | Relationship | Relationship manager contact |

## EXECUTION PROTOCOLS

- Aggregate channel usage from touchpoints
- Identify channel switching patterns
- Analyze digital vs human balance
- Identify self-service opportunities

## CONTEXT BOUNDARIES

- Touchpoints captured in Step 3 with channel per touchpoint
- CES includes channel switching penalty
- Focus on client preference and optimization

---

## EXECUTION SEQUENCE

### 1. Display Progress and Context

```
**Progress: Step 6 of 7 - Channel Analysis**

Now let's analyze how clients interact across different channels.

We'll look at:
- Which channels are used most
- Where channel switches cause friction
- Digital vs human-assisted balance
- Self-service opportunities
```

### 2. Channel Usage Summary

```
<action>
Aggregate channel usage from captured touchpoints:

| CH# | Channel | Touchpoint Count | % of Journey | Primary Use Cases |
|-----|---------|------------------|--------------|-------------------|
{{for each channel in unique_channels}}
| CH{{index}} | {{channel.name}} | {{channel.touchpoint_count}} | {{channel.percentage}} | {{channel.use_cases}} |
{{/for}}
</action>

<format>
**Channel Distribution:**

| Metric | Value |
|--------|-------|
| Total Channels Used | {{total_channels}} |
| Digital Touchpoints | {{digital_count}} ({{digital_percentage}}%) |
| Human-Assisted | {{human_count}} ({{human_percentage}}%) |
| Physical (Branch/Mail) | {{physical_count}} ({{physical_percentage}}%) |
</format>
```

### 3. Channel Switching Analysis

```
<action>
Identify channel switches by analyzing touchpoint sequence:

Map each transition where the channel changes between consecutive touchpoints.
</action>

<format>
**Channel Switches Identified:**

| Switch # | From Channel | To Channel | At Touchpoint | Reason | Avoidable? |
|----------|--------------|------------|---------------|--------|------------|
{{for each switch}}
| {{index}} | {{from}} | {{to}} | {{touchpoint}} | {{reason}} | {{avoidable}} |
{{/for}}

Total Channel Switches: {{total_switches}}
CES Penalty (switches × 1.5): {{switch_ces_penalty}}
</format>

<ask response="switch_drivers">
For each channel switch, what drives the client to switch channels?
Are they:
- Forced (no choice)
- Preferred (client wants to)
- Required by regulation/policy
</ask>

<ask response="avoidable_switches">
Which of these channel switches could potentially be eliminated?
What would need to change to keep the client in a single channel?
</ask>
```

### 4. Channel Preference Analysis

```
<ask response="client_channel_preference">
What channels do clients PREFER to use for this journey?
(May be different from what they're currently forced to use)
</ask>

<ask response="channel_gaps">
Are there any channel gaps — places where clients expect a channel option that doesn't exist?
(e.g., "Clients want to do this on mobile but it's only available via branch")
</ask>

<ask response="channel_friction">
Which channel(s) cause the most friction for clients?
Why?
</ask>
```

### 5. Digital vs Human Balance

```
<format>
**Digital vs Human Analysis:**

Current Balance:
- Digital Touchpoints: {{digital_count}} ({{digital_percentage}}%)
- Human-Assisted: {{human_count}} ({{human_percentage}}%)
</format>

<ask response="digital_balance_assessment">
Is this balance appropriate for this journey?
- [ ] Too much human assistance - could digitize more
- [ ] Right balance - mix is appropriate
- [ ] Too digital - clients need more human support
- [ ] Varies by client segment
</ask>

<ask response="human_value_moments">
Which touchpoints specifically BENEFIT from human interaction?
(Where human touch adds value vs just being required)
</ask>

<ask response="digital_opportunities">
Which human-assisted touchpoints could potentially become self-service?
</ask>
```

### 6. Self-Service Opportunities

```
<ask response="self_service_current">
Which touchpoints are currently self-service?
How well do they work?
</ask>

<ask response="self_service_potential">
Which additional touchpoints could become self-service?
For each:
- What would need to change?
- What's the complexity?
- What's the CES reduction potential?
</ask>

<action>
Build self-service opportunity table:

| JT# | Touchpoint | Current Mode | Self-Service Feasible? | Est. CES Reduction | Complexity |
|-----|------------|--------------|------------------------|-------------------|------------|
{{for each opportunity}}
| {{jt_id}} | {{name}} | {{current}} | {{feasibility}} | {{ces_reduction}} | {{complexity}} |
{{/for}}
</action>
```

### 7. Channel Optimization Recommendations

```
<ask response="channel_quick_wins">
What are the "quick win" channel improvements that could be made?
(Low effort, high impact)
</ask>

<ask response="channel_strategic">
What strategic channel changes would transform this journey?
(Higher effort but significant improvement)
</ask>
```

### 8. AI Assessment: Section Confidence

```
<action name="assess_channel_confidence">
Based on the channel analysis captured in this step, the AI MUST:

1. Calculate section confidence:
   - Count "Accept" responses vs "Edit" responses
   - Assess channel mapping completeness (all touchpoints have channels)
   - Note quality of switching pattern data

2. Determine confidence level:
   - HIGH: All channels mapped, clear switching patterns, preference data supported
   - MEDIUM: Most channels mapped, some switching estimates, general preferences (DEFAULT if uncertain)
   - LOW: Channel gaps, uncertain switching frequency, preference assumptions

3. Generate confidence basis automatically:
   - "Based on touchpoint channel mapping" (if derived from touchpoint analysis)
   - "Based on SME validation of channel usage patterns" (if edits were minimal)
   - "Based on observed patterns, analytics recommended for validation" (if significant estimates)

CRITICAL: Do NOT ask the user for confidence level or basis.
The AI makes this judgment call based on what was captured.
</action>

<set>
section_6_confidence: {{calculated_confidence_level}}
section_6_confidence_basis: {{generated_confidence_basis}}
</set>
```

### 9. Update Output Files

```
<action name="write_cx_journey_section_6" CRITICAL="MANDATORY">
APPEND to {cxJourneyFile} - Section 6 (Channel Analysis):

IMPORTANT: You MUST write actual content, not placeholders.

---

## 6. Channel Analysis

> **About this section:** How clients interact across different channels throughout the journey.

### 6.1 Channel Usage

| CH# | Channel | Touchpoints Using | Primary Purpose | Client Preference |
|-----|---------|-------------------|-----------------|-------------------|
{{#for each channel}}
| {{ch.id}} | {{ch.name}} | {{ch.touchpoint_count}} ({{ch.touchpoint_list}}) | {{ch.primary_purpose}} | {{ch.preference}} |
{{/for}}

### 6.2 Channel Switching Analysis

{{#Write a narrative paragraph covering:}}
- Total number of channel switches in the journey
- Which switches are necessary vs avoidable
- CES penalty from channel switching
- Key pain points in channel transitions
{{/Write narrative}}

**Channel Switch Patterns:**

| From Channel | To Channel | Touchpoint | Reason | Avoidable? | CES Penalty |
|--------------|------------|------------|--------|------------|-------------|
{{#for each channel_switch}}
| {{switch.from}} | {{switch.to}} | {{switch.touchpoint}} | {{switch.reason}} | {{switch.avoidable}} | {{switch.ces}} |
{{/for}}

### 6.3 Channel Gaps

{{#Write a narrative paragraph covering:}}
- What channel options clients expect but don't have
- Where digital self-service could be added
- Channel parity issues (mobile vs web vs branch)
{{/Write narrative}}

**Identified Gaps:**

| Gap | Client Expectation | Current Reality | Impact |
|-----|-------------------|-----------------|--------|
{{#for each channel_gap}}
| {{gap.name}} | {{gap.expectation}} | {{gap.reality}} | {{gap.impact}} |
{{/for}}

> **Section Confidence:** {{section_6_confidence}} | **Basis:** {{section_6_confidence_basis}}

---

</action>

<action name="update_touchpoints_channel_details" CRITICAL="MANDATORY">
UPDATE {clientTouchpointsFile} - Add/Update channel details for each touchpoint:

For each touchpoint, ensure the "Channel Details" section has:

#### Channel Details

| Attribute | Value |
|-----------|-------|
| **Primary Channel** | {{touchpoint.primary_channel}} |
| **Alternative Channels** | {{touchpoint.alternative_channels}} |
| **Channel Switching Required** | {{touchpoint.channel_switch_required}} |
| **Self-Service Available** | {{touchpoint.self_service_available}} |
| **Digital vs Human** | {{touchpoint.digital_or_human}} |

</action>

<action name="add_channel_analysis_to_touchpoints" CRITICAL="MANDATORY">
APPEND to {clientTouchpointsFile} - Channel Analysis sections:

---

## Channel Distribution

| Channel | Touchpoint Count | % of Journey | CES Contribution |
|---------|------------------|--------------|------------------|
{{#for each channel}}
| {{ch.name}} | {{ch.touchpoint_count}} | {{ch.percentage}}% | {{ch.ces}} |
{{/for}}

## Digital vs Human Balance

{{#Write a narrative paragraph analyzing:}}
- Ratio of digital to human touchpoints
- Where human interaction adds value vs where it's friction
- Automation opportunities
{{/Write narrative}}

## Self-Service Opportunities

| JT# | Touchpoint | Current Mode | Self-Service Feasibility | Est. CES Reduction |
|-----|------------|--------------|--------------------------|-------------------|
{{#for each self_service_opportunity}}
| {{tp.id}} | {{tp.name}} | {{tp.current_mode}} | {{tp.feasibility}} | {{tp.ces_reduction}} |
{{/for}}

---

</action>

<verification>
AFTER WRITING: Confirm files contain:

{cxJourneyFile} Section 6:
- [ ] Channel Usage table with all CH# entries
- [ ] Channel Switching Analysis narrative + table
- [ ] Channel Gaps narrative + table
- [ ] Section Confidence and Basis

{clientTouchpointsFile}:
- [ ] Each touchpoint has complete "Channel Details" section
- [ ] Channel Distribution table added
- [ ] Digital vs Human Balance analysis
- [ ] Self-Service Opportunities table
</verification>
```

### 10. Summary and Transition

Display:
```
**Channel Analysis Complete**

**Channel Summary:**
| Metric | Value |
|--------|-------|
| Total Channels | {{total_channels}} |
| Digital Touchpoints | {{digital_count}} ({{digital_percentage}}%) |
| Human-Assisted | {{human_count}} ({{human_percentage}}%) |
| Channel Switches | {{total_switches}} |
| Switch CES Penalty | {{switch_ces_penalty}} |
| Confidence | {{section_6_confidence}} |

**Key Findings:**
- Channel preference: {{client_channel_preference_summary}}
- Key gaps: {{channel_gaps_summary}}
- Self-service opportunities: {{self_service_count}}

Next, we'll do a final review and generate the complete documentation.
```

### 11. Proceed to Next Step

Display:
```
**Progress: Step 6 of 8 - Channel Analysis Complete**

Now let's look at industry benchmarks and research.
```

```
<action>Load, read entire file, then execute {nextStepFile}</action>
```

---

## CRITICAL STEP COMPLETION NOTE

This is an auto-proceed step. IMMEDIATELY after [channel analysis complete] and [output files updated], load and read fully `{nextStepFile}` to execute and begin final validation.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:
- Channel usage aggregated from touchpoints
- Channel switches identified and analyzed
- Digital vs human balance assessed
- Self-service opportunities identified
- Channel gaps documented
- Optimization recommendations captured
- Confidence assessment captured
- Output files updated
- Ready to proceed to Step 7

### SYSTEM FAILURE:
- Did not aggregate channel data
- Did not identify channel switches
- Did not assess self-service opportunities
- Started validation or gap analysis
- Did not update output files
- Skipped to later steps

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
