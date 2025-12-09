---
name: 'step-02-market-research'
description: 'Comprehensive market research including competitors, fintech disruptors, best practices, technology trends, and regulatory horizon'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/innovation-analysis'

# File References
thisStepFile: '{workflow_path}/steps/step-02-market-research.md'
nextStepFile: '{workflow_path}/steps/step-03-innovation-backlog.md'
workflowFile: '{workflow_path}/workflow.md'

# Shared Protocols
protocolsFile: '{module_root}/workflows/shared/protocols/protocols.md'

# Output Files
innovationAnalysisFile: '{current_process_folder}/innovation-analysis.md'

# Input Files
structuredDataFile: '{current_process_folder}/structured-data.json'
painPointsDetailFile: '{current_process_folder}/pain-points-detail.md'
asIsDocumentFile: '{current_process_folder}/as-is-process-documentation.md'

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
---

# Step 2: Market Research

## STEP GOAL

Conduct comprehensive market research including competitor analysis (regional focus), fintech disruptors, best practices, technology trends, and regulatory horizon. Uses web search followed by SME validation.

**Progress: Step 2 of 5** | Market Research | Est. time: 30-45 min

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:
- **NEVER** generate final content without user validation
- **CRITICAL**: Read the complete step file before taking any action
- **CRITICAL**: When loading next step, ensure entire file is read
- YOU ARE A FACILITATOR, not a content generator (except during web research)

### Role Reinforcement:
- You are an Innovation Analyst researching market opportunities
- Continue using your established name, communication_style, and persona
- We engage in collaborative dialogue, not command-response
- You bring innovation methodology, user brings process and organizational knowledge

### Step-Specific Rules:
- Focus on ACTIONABLE market intelligence
- **FORBIDDEN** to skip competitor or fintech analysis
- Research must be relevant to the specific process domain
- Flag any internal initiatives for cross-referencing
- Include regulatory horizon (upcoming regulations)

## EXECUTION PROTOCOLS:
- Execute three phases in sequence: Analyze → Research → Elicit
- Append approved output to document before proceeding
- Each phase builds on the previous
- **FORBIDDEN** to skip phases or combine them

---

## PHASE A: ANALYZE [AUTO - NO USER INTERRUPTION]

### A.1 Load Input Files

Read and analyze:
- `{structuredDataFile}` - Extract process domain, technology stack, systems
- `{painPointsDetailFile}` - Identify pain points that innovation could address
- `{asIsDocumentFile}` - Understand current process context

### A.2 Analysis Tasks

1. **Extract Process Context**
   - Process domain (account opening, lending, payments, complaints, etc.)
   - Current technology stack and systems
   - Client segments served
   - Channels and touchpoints
   - Volume and frequency metrics

2. **Identify Innovation Drivers**
   - Pain points suitable for innovation (high severity, high frequency)
   - Technology gaps in current state
   - Manual/paper-based processes ripe for automation
   - Client-facing friction points

3. **Prepare Research Queries**
   Build search queries using:
   - {bank_name} - organization name
   - {process_name} - process being analyzed
   - {region} - geographic focus

### A.3 Output: Process Context Summary

Create preliminary summary with:
- Process domain identified
- Key pain points for innovation
- Technology landscape
- Research query plan

**[Proceed directly to Phase B - NO user interaction yet]**

---

## PHASE B: RESEARCH [AUTO - NO USER INTERRUPTION]

Execute web searches for each category. Compile findings for user validation.

### B.1 Bank-Specific Research

Search queries:
- "{bank_name} {process_name} innovation digital transformation"
- "{bank_name} technology strategy fintech partnerships"
- "{bank_name} annual report innovation strategy 2024 2025"

**Extract:**
- Known innovation initiatives at the bank
- Technology partnerships
- Strategic direction

### B.2 Competitor Research (Regional)

Search queries:
- "{process_name} innovation banking competitors {region}"
- "best {process_name} banks digital leaders {region}"
- "{process_name} banking awards {region} 2024 2025"

**Extract:**
- Top 5-7 competitors for this process
- Their key innovations/differentiators
- Competitive threat level

### B.3 Fintech Disruptors

Search queries:
- "{process_name} fintech startups disrupting banking"
- "{process_name} neobank challenger bank"
- "{process_name} fintech funding 2024 2025"

**Extract:**
- Top 5-7 relevant fintechs
- What they do differently
- Threat level vs partnership potential

### B.4 Best Practices

Search queries:
- "{process_name} best practices banking 2024 2025"
- "{process_name} automation AI banking case study"
- "{process_name} Gartner Forrester McKinsey banking"

**Extract:**
- Industry best practices by category
- Benchmark metrics where available
- Case study examples

### B.5 Technology Trends

Search queries:
- "{process_name} emerging technology banking"
- "{process_name} AI ML banking applications"
- "{process_name} RPA automation banking"
- "generative AI {process_name} banking"

**Extract:**
- Applicable technologies (AI, RPA, blockchain, etc.)
- Maturity levels
- Banking-specific applications

### B.6 Regulatory Horizon

Search queries:
- "banking regulation 2025 2026 {region} {process_name}"
- "PSD3 digital euro DORA impact {process_name}"
- "{region} banking compliance upcoming requirements"

**Extract:**
- Upcoming regulations (next 2-3 years)
- Impact type: Enables / Constrains / Neutral
- Timeline and deadlines

### B.7 Output: Research Findings

Compile findings organized by category:
- Bank-specific intelligence
- Competitor landscape
- Fintech disruptors
- Industry best practices
- Technology trends
- Regulatory horizon

**[Proceed directly to Phase C with combined A+B findings]**

---

## PHASE C: ELICIT [INTERACTIVE - ONE TOPIC AT A TIME]

Present combined Analysis + Research findings, validate topic by topic.

**Standard Topic Pattern:** Present findings → Ask validation question → WAIT → Incorporate feedback → **Decision: [A] Approve | [B] Amend | [E] Elicit more** → WAIT → Next topic

---

### TOPIC 1: Competitor Landscape ({region})

Present competitor table:

| COMP# | Competitor | Strengths | Key Innovations | Threat Level |
|-------|------------|-----------|-----------------|--------------|
| COMP-{abbrev}-001 | {{competitor}} | {{strengths}} | {{innovations}} | High/Medium/Low |

Include research insight summary.

**Ask:** "Is this competitor picture accurate? Any competitors I've missed? Any threat levels to adjust?"

**Decision:** [A] Approve | [B] Amend | [E] Elicit more

---

### TOPIC 2: Fintech Disruptors

Present fintech table:

| FIN# | Fintech | What They Do | Threat Level | Partnership Potential |
|------|---------|--------------|--------------|----------------------|
| FIN-{abbrev}-001 | {{fintech}} | {{description}} | High/Medium/Low | High/Medium/Low |

**Ask:** "Is threat assessment correct? Any fintechs I've missed? Are there partnership discussions happening with any of these?"

**Decision:** [A] Approve | [B] Amend | [E] Elicit more

---

### TOPIC 3: Industry Best Practices

Present best practices by category:

**Client Experience:**
- {{practice_1}}
- {{practice_2}}

**Automation:**
- {{practice_3}}
- {{practice_4}}

**Risk & Compliance:**
- {{practice_5}}
- {{practice_6}}

**Speed & Efficiency:**
- {{practice_7}}
- {{practice_8}}

**Ask:** "Which of these are most relevant to your context? Any to deprioritize? Any I've missed?"

**Decision:** [A] Approve | [B] Amend | [E] Elicit more

---

### TOPIC 4: Technology Trends

Present technology table:

| TR# | Technology | Description | Applicability | Existing Initiative? |
|-----|-----------|-------------|---------------|---------------------|
| TR-{abbrev}-001 | {{tech}} | {{description}} | High/Medium/Low | Yes/No/Unknown |

Applicability Assessment:
- **High**: Clear use case, proven in banking
- **Medium**: Potential use case, emerging
- **Low**: Interesting but limited applicability

**Ask:** "Is the applicability assessment correct for each? Are there existing initiatives I should know about? Any vendor preferences or constraints?"

**Decision:** [A] Approve | [B] Amend | [E] Elicit more

---

### TOPIC 5: Regulatory Horizon

Present regulation table:

| Regulation | Timeline | Impact Type | {bank_name} Readiness |
|------------|----------|-------------|----------------------|
| {{regulation}} | {{date}} | Enables/Constrains/Neutral | Ready/In Progress/Not Started/Unknown |

Impact Types:
- **Enables**: Creates new opportunities or requirements that drive innovation
- **Constrains**: Limits what can be done or adds compliance burden
- **Neutral**: Minimal impact on this process

**Ask:** "Is this assessment correct? Any regulations I've missed? What's the bank's readiness level for each?"

**Decision:** [A] Approve | [B] Amend | [E] Elicit more

---

### TOPIC 6: Bank Innovation Context & Internal Initiatives

Present bank context summary:
- Innovation appetite: {innovation_appetite}
- Strategic themes: {strategic_themes}
- Technology constraints: {{identified_constraints}}

**Ask:** "Are there internal initiatives related to {process_name} that I should know about?"

For each initiative, capture:
- Initiative name
- Status (Planned/In Progress/Completed/On Hold)
- Owner/Team
- Relevance to this analysis

**Ask:** "Anything else about the bank's innovation context I should understand? Any failed attempts to avoid repeating?"

**Decision:** [A] Approve | [B] Amend | [E] Elicit more

---

### TOPIC 7: Gaps & Missing Intelligence

Summary of coverage:
- Competitors: {{competitor_count}} captured
- Fintechs: {{fintech_count}} captured
- Best Practices: {{practice_count}} captured
- Tech Trends: {{trend_count}} captured
- Regulatory: {{regulation_count}} captured
- Bank Context: Captured

**Ask:** "Is there any market intelligence I'm missing? Confidential competitive intel you can share? Industry contacts or sources I should know about?"

**Decision:** [A] Approve | [B] Amend | [E] Elicit more

---

## OUTPUT APPROVAL

### Present Complete Market Research

Display the validated Market Research section:

```
**Market Research Summary**

**Competitor Landscape ({region}):**
{{competitor_count}} competitors analyzed
Key threat: {{highest_threat_competitor}}

**Fintech Disruptors:**
{{fintech_count}} fintechs analyzed
Highest partnership potential: {{best_partnership_candidate}}

**Industry Best Practices:**
{{practice_count}} practices identified
Most relevant: {{top_3_practices}}

**Technology Trends:**
{{trend_count}} trends analyzed
Highest applicability: {{top_3_technologies}}

**Regulatory Horizon:**
{{regulation_count}} regulations tracked
Next major deadline: {{next_regulatory_deadline}}

**Bank Innovation Context:**
Innovation appetite: {innovation_appetite}
Internal initiatives: {{initiative_count}}
```

**Ask:** "Do you approve this Market Research section? [Y] Yes | [N] No - needs changes"

- IF N: "What needs to change?" → iterate on specific topic
- IF Y: Proceed to append and continue

---

## APPEND TO DOCUMENT

**On Approval:**

1. APPEND the approved Market Research content to `{innovationAnalysisFile}`:
   - Section 2: Innovation Overview (scope, objectives, strategic alignment)
   - Section 3: Market Trends (trend summary, trend analysis, competitive landscape, technology radar)
2. Update frontmatter: add "step-02" to stepsCompleted array
3. Display: "Step 2 Complete: Market Research added to Innovation Analysis document"

---

## MENU OPTIONS

**Select an Option:** [A] Advanced Elicitation | [P] Party Mode | [C] Continue to Step 3

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

ONLY WHEN [C continue option] is selected and [market research approved and appended to document], will you then load and read fully `{nextStepFile}` to execute and begin innovation backlog generation.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:
- All input files loaded and analyzed (structured data, pain points, process docs)
- External research completed for all 6 categories (bank, competitors, fintech, best practices, tech trends, regulatory)
- All 7 topics elicited with user validation (topic-by-topic approval)
- Market Research section approved and appended to output document
- Menu presented and user input handled correctly
- User confirms readiness to proceed to Step 3

### SYSTEM FAILURE:
- Skipping any of the 7 elicitation topics
- Not waiting for user approval before appending content
- Proceeding to next step without user selecting 'C'
- Not incorporating user feedback during topic review
- Generating final content without user validation
- Not executing web searches before presenting findings

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
