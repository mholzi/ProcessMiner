---
name: 'step-07-research'
description: 'Capture industry research, benchmarks, and competitive landscape for CX analysis'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/cx-journey-analysis'

# File References
thisStepFile: '{workflow_path}/steps/step-07-research.md'
nextStepFile: '{workflow_path}/steps/step-08-validation.md'
workflowFile: '{workflow_path}/workflow.md'

# Shared Protocols
protocolsFile: '{module_root}/workflows/shared/protocols/protocols.md'

# Output Files
cxJourneyFile: '{current_process_folder}/cx-journey-documentation.md'

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
---

# Step 7: Industry Research & Benchmarks

## STEP GOAL

Capture industry benchmarks, relevant trends, and competitive landscape insights to provide context for the CX analysis and inform TO-BE design. This corresponds to **Section 8** of the cx-journey-documentation template.

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
- Focus on KNOWN benchmarks and competitive insights
- Capture what SME knows, not speculative research
- Link trends to captured enhancements where relevant
- **FORBIDDEN** to start validation or gap analysis in this step

## EXECUTION PROTOCOLS

- Gather known industry benchmarks
- Capture relevant trends the SME is aware of
- Understand competitive landscape
- Link insights to enhancement opportunities

## CONTEXT BOUNDARIES

- CES baseline established in Step 5
- Enhancement ideas captured in Step 4
- This provides external context for transformation

---

## CONTENT FORMAT SPECIFICATION

This section defines the exact formatting requirements for Section 8: Industry Research & Benchmarks. The AI MUST follow these specifications when generating content.

### 8.1 Industry Benchmarks Table

| Column | Content | Formatting Rules |
|--------|---------|------------------|
| **Metric** | What is being measured | CES-related or journey-related metric |
| **Industry Average** | Typical industry performance | Number, range, or "TBD" if unknown |
| **Best-in-Class** | Top performer benchmark | Number, range, or "TBD" if unknown |
| **Our AS-IS** | Current state score | Number from CES analysis |
| **Gap** | Difference from benchmarks | Number with +/- (higher CES is worse) |

**Required Metrics:**
- Overall CES
- Journey Duration
- Digital Completion Rate
- First Contact Resolution

**Example - Industry Benchmarks:**
```
| Metric | Industry Average | Best-in-Class | Our AS-IS | Gap |
|--------|-----------------|---------------|-----------|-----|
| Overall CES | 75-85 | 40-50 | 100 | +15-25 vs average |
| Journey Duration | 5-7 business days | 1-2 business days | 5 days | Within average |
| Digital Completion Rate | 60-70% | 90%+ | 45% | -15-25% vs average |
| First Contact Resolution | 70-75% | 85%+ | 65% | -5-10% vs average |
```

**Sources Section** (after table):
- List all benchmark sources with dates
- Format: "- [Source Name] ([Date/Year])"

**Example - Sources:**
```
**Sources:**
- Forrester Banking CX Benchmarks (2024)
- Internal competitive analysis (Q2 2024)
- McKinsey Digital Banking Report (2023)
```

### 8.2 Relevant Trends Table

| Column | Content | Formatting Rules |
|--------|---------|------------------|
| **Trend** | Trend name | Short descriptive name (3-5 words) |
| **Relevance** | How relevant to this journey | High/Medium/Low |
| **Assessment** | Current adoption status | 1 sentence on current state vs trend |
| **Enhancement Alignment** | Related EI# items | EI# IDs if applicable, or "—" if none |

**Example - Relevant Trends:**
```
| Trend | Relevance | Assessment | Enhancement Alignment |
|-------|-----------|------------|----------------------|
| Digital-first onboarding | High | Partially adopted — application is digital but verification requires branch | EI-ONB-004, EI-ONB-007 |
| Real-time decisioning | High | Not adopted — decisions take 2-3 days | EI-ONB-012 |
| Biometric verification | Medium | Not adopted — exploring options | EI-ONB-004 |
| AI-powered document processing | Medium | Partially adopted — OCR in use but no intelligent extraction | EI-ONB-008 |
| Proactive notifications | High | Weak adoption — only milestone notifications, no proactive updates | EI-ONB-003, EI-ONB-005 |
| Self-service exception handling | Low | Not adopted — all exceptions require human contact | — |
```

### 8.3 Competitive Landscape

**Format:**
- **Structure**: Narrative paragraph (2-3 paragraphs) followed by competitive positioning table

**Narrative MUST cover:**
1. How competitors handle similar client journeys
2. Where we have advantages
3. Where competitors are ahead
4. What innovations competitors have adopted

**Example - Competitive Landscape Narrative:**
```
Traditional bank competitors (Bank A, Bank B) offer similar journey structures with comparable timelines (4-6 business days). However, fintech competitors (Fintech X, Fintech Y) have significantly disrupted expectations with same-day or next-day onboarding through fully digital processes and real-time verification.

Our competitive advantage lies in relationship manager support and the ability to handle complex business structures that fintechs often reject. SME clients with multi-entity structures or international requirements specifically choose traditional banks for this capability. Additionally, our branch network provides reassurance for clients who prefer face-to-face interaction for significant financial decisions.

However, competitors are ahead in digital self-service capabilities and mobile experience. Fintech X offers complete mobile application with in-app document capture, while our mobile app only supports status checking. Bank B has implemented live chat support, reducing phone wait times significantly. These gaps affect our appeal to digital-first business owners who prioritize convenience over relationship depth.
```

**Competitive Positioning Table:**

| Column | Content | Formatting Rules |
|--------|---------|------------------|
| **Aspect** | Competitive dimension | Short name |
| **Our Position** | Our current capability | Brief description |
| **Key Competitors** | What competitors offer | Brief description |
| **Gap/Advantage** | Assessment | Gap (behind)/Advantage (ahead)/Parity |

**Example - Competitive Positioning Table:**
```
| Aspect | Our Position | Key Competitors | Gap/Advantage |
|--------|--------------|-----------------|---------------|
| Onboarding Speed | 5 business days | Fintechs: Same-day; Banks: 4-6 days | Gap vs fintechs, Parity vs banks |
| Mobile Experience | Status checking only | Full mobile applications common | Gap |
| Complex Business Support | Strong multi-entity capability | Limited fintech support | Advantage |
| Digital Document Processing | Basic OCR | AI-powered extraction | Gap |
| Relationship Manager Access | Dedicated RM for all clients | RM only for premium clients | Advantage |
| Real-Time Support | Phone and email only | Live chat common | Gap |
```

### Section Confidence Statement

**Format:**
```
> **Section Confidence:** {{percentage}}% | **Basis:** {{ai_inferred_basis}}
```

**Example:**
```
> **Section Confidence:** 70% | **Basis:** Industry benchmarks based on general market awareness and published reports. Competitive analysis based on SME observation and informal research. Formal market research would strengthen findings.
```

---

## EXECUTION SEQUENCE

### 1. Display Progress and Context

```
**Progress: Step 7 of 8 - Industry Research & Benchmarks**

Let's capture what you know about industry standards and competitors.

This helps:
- Validate our CES baseline against industry norms
- Identify relevant trends for TO-BE design
- Understand competitive positioning
```

### 2. Industry Benchmarks

```
<format>
**Your Current CES Baseline:** {{total_ces}}

Let's compare against what you know about industry standards.
</format>

<ask response="benchmark_knowledge">
Do you have knowledge of industry benchmarks for this type of journey?
(e.g., from industry reports, analyst briefings, vendor comparisons)

- [ ] Yes, I have some benchmark data
- [ ] Limited - general awareness only
- [ ] No - would need to research
</ask>

<check if="benchmark_knowledge != 'No'">

  <ask response="industry_ces_average">
  What's the typical/average client effort for this journey in banking?
  (If you have CES benchmarks, share them; otherwise describe qualitatively)
  </ask>

  <ask response="best_in_class">
  Who do you consider "best-in-class" for this type of journey?
  (Could be direct competitors, fintechs, or other industries)
  What makes them best-in-class?
  </ask>

  <ask response="benchmark_source">
  Where does this benchmark information come from?
  (e.g., industry reports, vendor demos, client feedback, market research)
  </ask>

</check>

<action>
Build benchmark comparison table:

| Metric | Industry Average | Best-in-Class | Our AS-IS | Gap |
|--------|-----------------|---------------|-----------|-----|
| Overall CES | {{industry_ces_average}} | {{best_in_class_ces}} | {{total_ces}} | {{gap}} |
| Journey Duration | {{industry_duration}} | {{best_duration}} | {{our_duration}} | {{duration_gap}} |
| Digital Completion Rate | {{industry_digital}} | {{best_digital}} | {{our_digital}} | {{digital_gap}} |
</action>
```

### 3. Relevant Trends

```
<ask response="relevant_trends">
What trends in banking or CX are relevant to this journey?
(e.g., digital-first, real-time processing, AI/automation, self-service)

For each trend, tell me:
- What the trend is
- How relevant it is to this journey (High/Medium/Low)
- Whether any of our enhancement ideas (EI#) align with this trend
</ask>

<action>
Build trends table:

| Trend | Relevance | Assessment | Enhancement Alignment |
|-------|-----------|------------|----------------------|
{{for each trend}}
| {{trend.name}} | {{trend.relevance}} | {{trend.assessment}} | {{trend.ei_alignment}} |
{{/for}}
</action>
```

### 4. Competitive Landscape

```
<ask response="competitor_analysis">
How do your main competitors handle this journey compared to you?

Consider:
- Are they faster/slower?
- More/less digital?
- Better/worse client communication?
- Any features you wish you had?
</ask>

<ask response="competitive_advantage">
Where do you have a competitive ADVANTAGE in this journey?
(What do you do better than competitors?)
</ask>

<ask response="competitive_gap">
Where do competitors have an advantage over you?
(What are you trying to catch up on?)
</ask>
```

### 5. Innovation Considerations

```
<ask response="innovation_watched">
Are there any emerging technologies or approaches you're watching for this journey?
(e.g., AI decisioning, real-time verification, blockchain, biometrics)
</ask>

<ask response="innovation_constraints">
Are there any constraints that limit what innovations you can adopt?
(e.g., regulatory requirements, legacy systems, risk appetite)
</ask>
```

### 6. AI Assessment: Section Confidence

```
<action name="assess_research_confidence">
Based on the industry research captured in this step, the AI MUST:

1. Calculate section confidence:
   - Assess benchmark data quality (specific numbers vs general ranges)
   - Evaluate trend relevance to enhancement ideas
   - Note competitive insight depth

2. Determine confidence level:
   - HIGH: Specific benchmarks cited, clear trend-enhancement alignment, competitive gaps identified
   - MEDIUM: General industry awareness, some trend alignment, basic competitive context (DEFAULT)
   - LOW: Limited benchmarks, weak trend connection, competitive landscape unclear

3. Generate confidence basis automatically:
   - "Based on industry knowledge and benchmark research" (if benchmarks available)
   - "Based on general industry awareness and SME input" (if limited specifics)
   - "Based on assumptions, formal research recommended" (if significant gaps)

CRITICAL: Do NOT ask the user for confidence level or basis.
The AI makes this judgment call based on what was captured.
</action>

<set>
section_8_confidence: {{calculated_confidence_level}}
section_8_confidence_basis: {{generated_confidence_basis}}
</set>
```

### 7. Update Output File

```
<action name="write_cx_journey_section_8" CRITICAL="MANDATORY">
APPEND to {cxJourneyFile} - Section 8 (Industry Research & Benchmarks):

IMPORTANT: You MUST write actual content, not placeholders.

---

## 8. Industry Research & Benchmarks

> **About this section:** How does this journey compare to industry standards and emerging trends?

### 8.1 Industry Benchmarks

| Metric | Industry Average | Best-in-Class | Our AS-IS | Gap |
|--------|-----------------|---------------|-----------|-----|
| Overall CES | {{benchmark.industry_ces}} | {{benchmark.best_ces}} | {{our_ces}} | {{ces_gap}} |
| Journey Duration | {{benchmark.industry_duration}} | {{benchmark.best_duration}} | {{our_duration}} | {{duration_gap}} |
| Digital Completion Rate | {{benchmark.industry_digital}} | {{benchmark.best_digital}} | {{our_digital}} | {{digital_gap}} |
| First Contact Resolution | {{benchmark.industry_fcr}} | {{benchmark.best_fcr}} | {{our_fcr}} | {{fcr_gap}} |

**Sources:**
{{#for each benchmark_source}}
- {{source.name}} ({{source.date}})
{{/for}}

### 8.2 Relevant Trends

| Trend | Relevance | Assessment | Enhancement Alignment |
|-------|-----------|------------|----------------------|
{{#for each validated_trend}}
| {{trend.name}} | {{trend.relevance}} | {{trend.assessment}} | {{trend.enhancement_alignment}} |
{{/for}}

### 8.3 Competitive Landscape

{{#Write a narrative paragraph covering:}}
- How competitors handle similar client journeys
- Where we have advantages
- Where competitors are ahead
- What innovations competitors have adopted
{{/Write narrative}}

**Competitive Positioning:**

| Aspect | Our Position | Key Competitors | Gap/Advantage |
|--------|--------------|-----------------|---------------|
{{#for each competitive_aspect}}
| {{aspect.name}} | {{aspect.our_position}} | {{aspect.competitors}} | {{aspect.gap}} |
{{/for}}

> **Section Confidence:** {{section_8_confidence}} | **Basis:** {{section_8_confidence_basis}}

---

</action>

<action name="update_enhancement_alignment" CRITICAL="MANDATORY">
UPDATE {frictionPointsFile} - Enhancement Ideas Catalog:

For each enhancement idea that aligns with an industry trend:
- Add trend alignment reference
- Note if trend-driven enhancement

UPDATE {cxJourneyFile} - Section 7 (Enhancement Ideas):

Add Section 7.3 Innovation Considerations:

### 7.3 Innovation Considerations

{{#for each innovation_consideration}}
**{{innovation.name}}**
- Trend Source: {{innovation.trend_source}}
- Applicable Enhancement Ideas: {{innovation.ei_ids}}
- Implementation Complexity: {{innovation.complexity}}
- Potential CES Impact: {{innovation.ces_impact}}
{{/for}}

</action>

<verification>
AFTER WRITING: Confirm files contain:

{cxJourneyFile} Section 8:
- [ ] Industry Benchmarks table with all metrics and gaps
- [ ] Sources list
- [ ] Relevant Trends table with enhancement alignment
- [ ] Competitive Landscape narrative
- [ ] Competitive Positioning table
- [ ] Section Confidence and Basis

{cxJourneyFile} Section 7.3:
- [ ] Innovation Considerations section added

{frictionPointsFile}:
- [ ] Enhancement Ideas updated with trend alignment where applicable
</verification>
```

### 8. Summary and Transition

Display:
```
**Industry Research Captured**

| Metric | Value |
|--------|-------|
| Benchmarks Available | {{benchmark_knowledge}} |
| Relevant Trends | {{trend_count}} |
| Enhancement Alignments | {{enhancement_alignment_count}} |
| Confidence | {{section_8_confidence}} |

**Key Insights:**
- Industry gap: {{industry_gap_summary}}
- Best-in-class: {{best_in_class}}
- Key trend alignment: {{key_trend}}

Next, we'll do a final review and complete the documentation.
```

### 9. Proceed to Next Step

Display:
```
**Progress: Step 7 of 8 - Industry Research Complete**

Now let's do a final review and complete the CX documentation.
```

```
<action>Load, read entire file, then execute {nextStepFile}</action>
```

---

## CRITICAL STEP COMPLETION NOTE

This is an auto-proceed step. IMMEDIATELY after [research captured] and [output file updated], load and read fully `{nextStepFile}` to execute and begin final validation.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:
- Industry benchmarks captured (or noted as unknown)
- Relevant trends identified
- Enhancement alignments noted
- Competitive landscape understood
- Innovation considerations captured
- Confidence assessment captured
- Output file updated
- Ready to proceed to Step 8

### SYSTEM FAILURE:
- Started validation or gap analysis
- Fabricated benchmark data without user input
- Did not update output file
- Skipped to later steps

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
