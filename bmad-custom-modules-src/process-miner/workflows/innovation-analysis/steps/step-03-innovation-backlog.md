---
name: 'step-03-innovation-backlog'
description: 'Generate innovation idea backlog with weighted 6-dimension feasibility scoring, dependencies, and synergies'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/innovation-analysis'

# File References
thisStepFile: '{workflow_path}/steps/step-03-innovation-backlog.md'
nextStepFile: '{workflow_path}/steps/step-04-priorities.md'
workflowFile: '{workflow_path}/workflow.md'

# Shared Protocols
protocolsFile: '{module_root}/workflows/shared/protocols/protocols.md'

# Scoring Configuration
scoringConfig: '{workflow_path}/config/scoring.yaml'

# Output Files
innovationAnalysisFile: '{current_process_folder}/innovation-analysis.md'
innovationIdeasDetailFile: '{current_process_folder}/innovation-ideas-detail.md'

# Input Files
structuredDataFile: '{current_process_folder}/structured-data.json'
painPointsDetailFile: '{current_process_folder}/pain-points-detail.md'

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
---

# Step 3: Generate Innovation Backlog (with Feasibility)

## STEP GOAL

Identify innovation opportunities from pain points and market research, assess feasibility using weighted 6-dimension scoring formula, capture dependencies, time-to-value estimates, innovation types, and synergies.

**Progress: Step 3 of 5** | Innovation Backlog | Est. time: 45-60 min

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:
- **NEVER** generate final content without user validation
- **CRITICAL**: Read the complete step file before taking any action
- **CRITICAL**: When loading next step, ensure entire file is read
- YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:
- You are an Innovation Analyst assessing feasibility and building the backlog
- Continue using your established name, communication_style, and persona
- We engage in collaborative dialogue, not command-response
- You bring innovation methodology and scoring expertise, user brings process and organizational knowledge

### Step-Specific Rules:
- Each innovation MUST have ALL 6 feasibility dimensions scored
- **FORBIDDEN** to skip feasibility assessment for any innovation
- Weighted scoring formula MUST be applied consistently
- Dependencies MUST be captured for each innovation
- Innovation type (Incremental/Adjacent/Transformational) MUST be classified

---

## WEIGHTED SCORING CONFIGURATION

### Formula:
```
Feasibility Score = (Technical × 0.20) + (Regulatory × 0.25) + (ROI × 0.20) +
                    (Complexity × 0.10) + (Adoption × 0.15) + (Competitive × 0.10)
```

### Scale: 1-4 for each dimension

### Thresholds:
- **High Feasibility:** ≥ 3.0
- **Medium Feasibility:** 2.0 - 2.9
- **Low Feasibility:** < 2.0

### Dimension Definitions:

| Dimension | Weight | 4 | 3 | 2 | 1 |
|-----------|--------|---|---|---|---|
| Technical | 0.20 | Ready to go | Needs some work | Significant effort | Not feasible |
| Regulatory | 0.25 | No issues | Minor considerations | Needs approval | Blocked |
| ROI | 0.20 | Strong ROI | Positive ROI | Break-even | Negative ROI |
| Complexity | 0.10 | Simple | Moderate | Complex | Very Complex |
| Adoption | 0.15 | High adoption | Moderate adoption | Uncertain | Low adoption |
| Competitive | 0.10 | First mover | Fast follower | Table stakes | No advantage |

---

## CONTENT FORMAT SPECIFICATION

This section defines the exact formatting requirements for Section 4 (Innovation Backlog) and Section 5 (Feasibility Matrix). The AI MUST follow these specifications when generating content.

### Section 4: Innovation Backlog

#### 4.1 Innovation Ideas Summary Table

| Column | Content | Formatting Rules |
|--------|---------|------------------|
| **II ID** | Innovation identifier | Format: II-{ABBREV}-### (e.g., II-ONB-001) |
| **Innovation Idea** | Short descriptive name | 5-10 words |
| **Category** | Innovation category | Process / Technology / Business Model / Customer Experience |
| **Source** | Where idea originated | Pain Point / Competitor / Fintech / Trend / Internal |
| **Status** | Current status | New / Under Review / Approved / Deferred |
| **Strategic Fit** | Alignment with strategy | High / Medium / Low |

**Example - Innovation Ideas Summary:**
```
| II ID | Innovation Idea | Category | Source | Status | Strategic Fit |
|-------|-----------------|----------|--------|--------|---------------|
| II-ONB-001 | AI-powered document extraction and validation | Technology | Trend TR-ONB-001 | Under Review | High |
| II-ONB-002 | Video-based identity verification | Technology | Competitor COMP-ONB-002 | Under Review | High |
| II-ONB-003 | Pre-populated application from accounting software | Process | Fintech FIN-ONB-002 | New | Medium |
| II-ONB-004 | Automated decisioning for simple structures | Process | Pain Point PP-ONB-005 | Approved | High |
| II-ONB-005 | Real-time application status notifications | Customer Experience | Pain Point PP-ONB-008 | Approved | High |
```

#### 4.2 Innovation Details

**Format:**
- **Structure**: Per-innovation blocks with overview table + description paragraph
- **Overview Table**: Key attributes in table format
- **Description**: 1-2 paragraphs explaining the innovation

**Per-Innovation Block Structure:**
```
### II-XXX-###: [Innovation Name]

#### Overview

| Attribute | Value |
|-----------|-------|
| **Innovation ID** | II-XXX-### |
| **Innovation Name** | [Short descriptive name] |
| **Category** | [Process / Technology / Business Model / Customer Experience] |
| **Source** | [Origin: Pain Point, Competitor, Fintech, Trend, Internal] |
| **Related Items** | [PP#, TR#, COMP#, FIN# references] |
| **Strategic Fit** | [High / Medium / Low] |

#### Description

[1-2 paragraphs describing what this innovation is, what problem it solves, and why it matters]
```

**Example - Innovation Detail:**
```
### II-ONB-001: AI-powered document extraction and validation

#### Overview

| Attribute | Value |
|-----------|-------|
| **Innovation ID** | II-ONB-001 |
| **Innovation Name** | AI-powered document extraction and validation |
| **Category** | Technology |
| **Source** | Trend TR-ONB-001, Pain Point PP-ONB-003 |
| **Related Items** | TR-ONB-001, PP-ONB-003, PP-ONB-007, COMP-ONB-002 |
| **Strategic Fit** | High |

#### Description

This innovation replaces manual document review with AI-powered extraction and validation. Machine learning models trained on business registration documents, financial statements, and identity documents would automatically extract key data fields and validate against external sources. The system would flag exceptions for human review while enabling straight-through processing for standard applications.

The innovation directly addresses pain point PP-ONB-003 (manual document processing delays) and PP-ONB-007 (inconsistent data entry). By reducing document processing time from 45 minutes to under 5 minutes per application, this enables same-day decisioning for straightforward cases. Competitor Bank B has already deployed similar technology, making this a competitive necessity rather than a differentiator.
```

#### 4.3 Innovation Categories

**Format:**
- **Structure**: Table with counts + brief description per category
- **Table Columns**: Category | Count | % of Total | Top Innovation
- **Descriptions**: 1-2 sentences per category explaining what it includes

**Example - Innovation Categories:**
```
| Category | Count | % of Total | Top Innovation |
|----------|-------|------------|----------------|
| Process | 5 | 33% | II-ONB-004 - Automated decisioning |
| Technology | 6 | 40% | II-ONB-001 - AI document extraction |
| Business Model | 1 | 7% | II-ONB-009 - Embedded banking partnerships |
| Customer Experience | 3 | 20% | II-ONB-005 - Real-time status notifications |

**Process Innovation** focuses on optimizing how work gets done within existing systems — streamlining workflows, automating manual steps, and improving handoffs between teams.

**Technology Innovation** introduces new tools, platforms, or capabilities — AI/ML applications, new integrations, and digital platform enhancements.

**Business Model Innovation** explores new ways to deliver services or create value — partnerships, alternative channels, and new service delivery models.

**Customer Experience Innovation** improves the client-facing journey — reducing friction, improving communication, and enhancing self-service capabilities.
```

### Section 5: Feasibility Matrix

#### 5.1 Six-Dimension Scoring Table

| Column | Content | Formatting Rules |
|--------|---------|------------------|
| **II ID** | Innovation identifier | Format: II-{ABBREV}-### |
| **Technical** | Technical feasibility | Score 1-5 |
| **Business** | Business value | Score 1-5 |
| **Strategic** | Strategic alignment | Score 1-5 |
| **Resource** | Resource availability | Score 1-5 |
| **Risk** | Risk level (inverted: 5=low risk) | Score 1-5 |
| **Customer** | Customer impact | Score 1-5 |
| **Total Score** | Sum or weighted average | Calculated total |

**Example - Feasibility Matrix:**
```
| II ID | Technical | Business | Strategic | Resource | Risk | Customer | Total Score |
|-------|-----------|----------|-----------|----------|------|----------|-------------|
| II-ONB-001 | 4 | 5 | 5 | 3 | 4 | 4 | 25 |
| II-ONB-002 | 4 | 4 | 5 | 4 | 3 | 5 | 25 |
| II-ONB-003 | 3 | 3 | 4 | 4 | 4 | 4 | 22 |
| II-ONB-004 | 5 | 5 | 5 | 4 | 3 | 4 | 26 |
| II-ONB-005 | 5 | 4 | 4 | 5 | 5 | 5 | 28 |
```

#### 5.2 Dimension Definitions

**Format:**
- **Structure**: Brief definitions + scoring rubric table
- **Definitions**: 1-2 sentences per dimension explaining what it measures
- **Rubric Table**: Score | Description for each dimension

**Example - Dimension Definitions:**
```
**Dimension Definitions:**

- **Technical Feasibility**: Can we build this with current or near-term technology capabilities? Considers existing systems, integration complexity, and technical maturity.
- **Business Value**: Does this deliver measurable business value? Considers efficiency gains, revenue impact, and cost reduction.
- **Strategic Alignment**: Does this support our strategic priorities? Considers alignment with digital transformation, client experience, and growth objectives.
- **Resource Availability**: Do we have the people, skills, and budget to deliver? Considers team capacity, skill gaps, and competing priorities.
- **Risk Level**: What is the risk of failure or negative impact? (Inverted scale: 5 = low risk, 1 = high risk)
- **Customer Impact**: How much will this improve the client experience? Considers effort reduction, satisfaction improvement, and competitive positioning.

**Scoring Rubric:**

| Score | Technical | Business | Strategic | Resource | Risk | Customer |
|-------|-----------|----------|-----------|----------|------|----------|
| 5 | Ready to deploy | Transformative value | Core strategic priority | Fully available | Minimal risk | Major improvement |
| 4 | Minor build required | Strong value | Strong alignment | Mostly available | Low risk | Significant improvement |
| 3 | Moderate build | Moderate value | Partial alignment | Some gaps | Moderate risk | Moderate improvement |
| 2 | Significant build | Limited value | Weak alignment | Significant gaps | High risk | Minor improvement |
| 1 | Not feasible | No clear value | Not aligned | Not available | Very high risk | No improvement |
```

#### 5.3 Feasibility Analysis

**Format:**
- **Structure**: 1-2 paragraphs per innovation explaining key feasibility drivers
- **Content**: For each innovation, explain the scores — what drives feasibility up or down

**Example - Feasibility Analysis:**
```
**II-ONB-001: AI-powered document extraction and validation** (Score: 25)

This innovation scores highly on business value and strategic alignment as it directly addresses a major operational bottleneck and supports the digital transformation priority. Technical feasibility is strong (4) because proven solutions exist in the market, though integration with legacy systems will require careful planning. The main constraint is resource availability (3) — the AI/ML team is currently committed to other projects, which would delay initiation. Risk is moderate (4) as similar implementations at other banks have been successful, though model accuracy for complex documents will need validation.

**II-ONB-004: Automated decisioning for simple structures** (Score: 26)

This innovation achieves the highest overall score due to strong technical feasibility — the decisioning logic already exists in policy documents and just needs to be codified. Business value is transformative (5) as it would reduce decision time from 2 days to under 1 hour for 60% of applications. Strategic alignment is perfect (5) as this is explicitly called out in the digital transformation roadmap. The primary risk (3) relates to regulatory acceptance of automated decisions, which will require early engagement with the compliance team to validate the approach.

**II-ONB-005: Real-time application status notifications** (Score: 28)

This is the highest-scoring innovation due to low technical risk and high customer impact. The notification infrastructure already exists for other products, making this a configuration exercise rather than a build. Customer impact is rated 5 because client research consistently identifies status uncertainty as a top frustration. Risk is minimal (5) as this is a well-understood capability with no regulatory implications.
```

#### 5.4 Priority Matrix

**Format:**
- **Structure**: Table with quadrant assignments + narrative explanation per quadrant
- **Table Columns**: Quadrant | Innovations | Recommendation
- **Narrative**: 1-2 sentences per quadrant explaining strategic implications

**Quadrant Definitions:**
- **Quick Wins**: High Feasibility + High Impact — implement first
- **Strategic Bets**: High Impact + Lower Feasibility — invest carefully
- **Fill-Ins**: Lower Impact + High Feasibility — do if capacity allows
- **Reconsider**: Lower Impact + Lower Feasibility — deprioritize or drop

**Example - Priority Matrix:**
```
| Quadrant | Innovations | Recommendation |
|----------|-------------|----------------|
| Quick Wins | II-ONB-005, II-ONB-004 | Implement immediately — high value, low risk |
| Strategic Bets | II-ONB-001, II-ONB-002 | Prioritize with careful planning — high value, needs investment |
| Fill-Ins | II-ONB-003, II-ONB-007 | Include if capacity allows — moderate value, easy to do |
| Reconsider | II-ONB-009, II-ONB-010 | Deprioritize — limited value relative to effort |

**Quick Wins** (II-ONB-005, II-ONB-004) should be the immediate focus. These innovations deliver high customer and business value with minimal risk and resource requirements. Status notifications can be implemented within weeks, while automated decisioning can be delivered in a single sprint once compliance approval is secured.

**Strategic Bets** (II-ONB-001, II-ONB-002) require more significant investment but deliver transformative value. AI document extraction should be prioritized as it enables multiple downstream improvements. Video identity verification is a competitive necessity that should be fast-followed once a vendor is selected.

**Fill-Ins** (II-ONB-003, II-ONB-007) are worthwhile if capacity allows but should not displace higher-priority items. These can be scheduled for later phases or picked up opportunistically.

**Reconsider** (II-ONB-009, II-ONB-010) items should be deferred or dropped from this analysis. The business model innovations require market conditions that don't yet exist, while some process improvements have limited impact relative to implementation effort.
```

### Section Confidence Statement

**Format:**
```
> **Section Confidence:** {{percentage}}% | **Basis:** {{ai_inferred_basis}}
```

**Example:**
```
> **Section Confidence:** 85% | **Basis:** Innovation backlog derived from pain point analysis and market research with SME validation. Feasibility scores based on SME assessment; technical validation with IT would strengthen confidence.
```

---

## PHASE A: ANALYZE [AUTO - NO USER INTERRUPTION]

### A.1 Load Inputs

Read and analyze:
- Step 2 output (Market Research from `{innovationAnalysisFile}`)
- `{painPointsDetailFile}` - Source for pain point → innovation mapping
- `{structuredDataFile}` - Process context

### A.2 Identify Innovation Opportunities

Generate innovation ideas from:

1. **Pain Point → Innovation Mapping**
   - For each PP#, identify potential innovations
   - Link back to source pain point
   - Consider severity and frequency

2. **Competitor Gap Opportunities**
   - What do competitors (COMP#) do that we don't?
   - Where can we leapfrog?

3. **Fintech Differentiator Opportunities**
   - Ideas inspired by fintech disruptors (FIN#)
   - Partnership vs build considerations

4. **Best Practice Applications**
   - Industry best practices applicable here
   - Implementation patterns

5. **Technology Trend Opportunities**
   - Emerging tech applications (TR#)
   - AI/ML, RPA, automation opportunities

6. **Regulatory-Enabled Opportunities**
   - Innovations enabled by upcoming regulations
   - First-mover advantages

### A.3 Categorize Each Innovation

Assign category:
- **Process Innovation** - improve how work gets done
- **Technology Innovation** - new tools or platforms
- **Business Model Innovation** - new revenue or delivery models
- **Customer Experience Innovation** - improve client journey

### A.4 Classify Innovation Type

For each innovation:
- **Incremental:** Improve existing capability
- **Adjacent:** Extend to new area
- **Transformational:** Create new capability

### A.5 Identify Initial Dependencies

For each innovation:
- What needs to exist first?
- Which other innovations does this depend on?
- External dependencies (vendors, regulations)?

### A.6 Output: Draft Backlog

Create preliminary backlog with:
- Innovation ID (II-{abbrev}-001, II-{abbrev}-002, etc.)
- Description
- Source (pain point, competitor, trend, etc.)
- Category
- Innovation type
- Preliminary dependencies

**[Proceed directly to Phase B - NO user interaction yet]**

---

## PHASE B: RESEARCH [AUTO - NO USER INTERRUPTION]

### B.1 Implementation Intelligence

For each innovation, research:
- Implementation examples in banking
- Vendor solutions available
- Time-to-implement benchmarks
- Cost benchmarks

### B.2 Risk Intelligence

Research:
- Common failure points
- Regulatory hurdles
- Technology risks
- Change management risks

### B.3 Dependency Analysis

Research:
- Prerequisite capabilities
- Cross-innovation dependencies
- External dependencies (vendors, regulations)

### B.4 Output: Research Findings

Compile per-innovation:
- Implementation evidence
- Risk factors
- Dependency validation

**[Proceed directly to Phase C with combined A+B findings]**

---

## PHASE C: ELICIT [INTERACTIVE - ONE TOPIC AT A TIME]

**Standard Topic Pattern:** Present findings → Ask validation → WAIT → Incorporate feedback → **Decision** → WAIT → Next topic

---

### TOPIC 1: Backlog Overview

Present summary table:

| II# | Innovation | Category | Type | Source |
|-----|-----------|----------|------|--------|
| II-{abbrev}-001 | {{innovation}} | {{category}} | {{type}} | {{source}} |

**Breakdown:**
- By Category: Process ({{n}}), Technology ({{n}}), Business Model ({{n}}), CX ({{n}})
- By Type: Incremental ({{n}}), Adjacent ({{n}}), Transformational ({{n}})

**Ask:** "Is this a reasonable set of opportunities? Any gaps? Any items to remove? Any ideas I've missed?"

**Decision:** [A] Approve | [B] Add/remove items | [E] Elicit more

---

### TOPIC 2: Innovation Feasibility Review (Per Innovation)

**For EACH innovation (iterate one by one):**

```
<loop name="feasibility_assessment" for="each innovation">

  <format>
  ---
  **Innovation: II-{abbrev}-{{seq}}**

  **Name:** {{innovation.name}}
  **Description:** {{innovation.description}}
  **Source:** {{innovation.source}}
  **Category:** {{innovation.category}}
  **Type:** {{innovation.type}}

  **Research Findings:**
  {{innovation.research_summary}}
  </format>

  <format>
  **Feasibility Assessment (6 Dimensions)**

  Score each dimension 1-4:
  </format>

  <ask response="technical_score">
  **Technical Feasibility (Weight: 0.20)**
  Can we build it with current/near-term capabilities?

  - [ ] 4 - Ready to go (existing capabilities)
  - [ ] 3 - Needs some work (minor gaps)
  - [ ] 2 - Significant effort (major build)
  - [ ] 1 - Not feasible (beyond capability)
  </ask>

  <ask response="regulatory_score">
  **Regulatory Feasibility (Weight: 0.25)** - HIGHEST WEIGHT
  Any regulatory barriers or requirements?

  - [ ] 4 - No issues (fully compliant)
  - [ ] 3 - Minor considerations (low risk)
  - [ ] 2 - Needs approval (regulatory review required)
  - [ ] 1 - Blocked (regulatory barrier)
  </ask>

  <ask response="roi_score">
  **ROI Feasibility (Weight: 0.20)**
  Is the business case clear?

  - [ ] 4 - Strong ROI (clear business case)
  - [ ] 3 - Positive ROI (good return)
  - [ ] 2 - Break-even (marginal value)
  - [ ] 1 - Negative ROI (value unclear)
  </ask>

  <ask response="complexity_score">
  **Complexity (Weight: 0.10)**
  How hard to implement?

  - [ ] 4 - Simple (quick implementation)
  - [ ] 3 - Moderate (manageable effort)
  - [ ] 2 - Complex (significant work)
  - [ ] 1 - Very Complex (major undertaking)
  </ask>

  <ask response="adoption_score">
  **Adoption (Weight: 0.15)**
  Will clients/users adopt it?

  - [ ] 4 - High adoption (client demand exists)
  - [ ] 3 - Moderate adoption (likely uptake)
  - [ ] 2 - Uncertain (needs validation)
  - [ ] 1 - Low adoption (resistance expected)
  </ask>

  <ask response="competitive_score">
  **Competitive Advantage (Weight: 0.10)**
  Does it differentiate us?

  - [ ] 4 - First mover (market leadership)
  - [ ] 3 - Fast follower (competitive parity)
  - [ ] 2 - Table stakes (catch-up)
  - [ ] 1 - No advantage (commoditized)
  </ask>

  <action>
  Calculate weighted score:
  Score = (Technical × 0.20) + (Regulatory × 0.25) + (ROI × 0.20) +
          (Complexity × 0.10) + (Adoption × 0.15) + (Competitive × 0.10)

  Classify feasibility:
  - ≥ 3.0: High Feasibility
  - 2.0 - 2.9: Medium Feasibility
  - < 2.0: Low Feasibility
  </action>

  <format>
  **Calculated Feasibility Score: {{score}}** ({{feasibility_level}})

  | Dimension | Score | Weighted |
  |-----------|-------|----------|
  | Technical | {{tech}} | {{tech × 0.20}} |
  | Regulatory | {{reg}} | {{reg × 0.25}} |
  | ROI | {{roi}} | {{roi × 0.20}} |
  | Complexity | {{comp}} | {{comp × 0.10}} |
  | Adoption | {{adopt}} | {{adopt × 0.15}} |
  | Competitive | {{compet}} | {{compet × 0.10}} |
  | **TOTAL** | | **{{score}}** |
  </format>

  <ask response="time_to_value">
  **Time-to-Value**
  How quickly can this deliver value?

  - [ ] Quick (0-6 months)
  - [ ] Medium (6-12 months)
  - [ ] Long (12+ months)
  </ask>

  <ask response="risk_level">
  **Risk Level**
  What's the overall risk?

  - [ ] Low - minimal risk factors
  - [ ] Medium - manageable risks
  - [ ] High - significant risks to mitigate
  </ask>

  <ask response="key_risks">
  What are the key risks for this innovation?
  </ask>

  <ask response="dependencies">
  What does this innovation depend on?
  (Other innovations, systems, regulatory changes, etc.)
  </ask>

  <ask response="synergies">
  What synergies exist with other innovations?
  (Which other innovations would this enable or benefit from?)
  </ask>

  <ask response="innovation_decision">
  **Decision for II-{abbrev}-{{seq}}:**

  - [K] Keep - include in backlog as assessed
  - [M] Modify - change scores or details
  - [R] Remove - exclude from backlog
  </ask>

  <check if="innovation_decision == 'M'">
    <ask response="modification_details">What would you like to modify?</ask>
    <action>Apply modifications and recalculate score</action>
  </check>

</loop>
```

---

### TOPIC 3: New Ideas

**Ask:** "Are there any innovations NOT captured that should be included? Internal ideas? Strategic initiatives?"

For each new idea:
1. Add II-{abbrev}-XXX ID
2. Run full feasibility assessment (all 6 dimensions)
3. Capture time-to-value, risks, dependencies, synergies

---

### TOPIC 4: Dependency Map Review

Present dependency map:

**Foundation Innovations** (enable others):
{{list innovations that are dependencies for others}}

**Dependent Innovations** (require others first):
{{list innovations with dependencies}}

**Independent Innovations** (can proceed alone):
{{list innovations with no dependencies}}

**Dependency Diagram:**
```
II-001 → II-003 → II-007
       ↘ II-004
II-002 → II-005
```

**Ask:** "Are the dependency relationships correct? Any missing dependencies? Any circular dependencies to resolve?"

**Decision:** [A] Approve | [B] Amend | [E] Elicit more

---

## OUTPUT APPROVAL

Present complete Innovation Backlog:

```
**Innovation Backlog Summary**

| Metric | Value |
|--------|-------|
| Total Innovations | {{total}} |
| High Feasibility (≥3.0) | {{high_count}} |
| Medium Feasibility (2.0-2.9) | {{medium_count}} |
| Low Feasibility (<2.0) | {{low_count}} |
| Removed | {{removed_count}} |

**By Category:**
- Process: {{process_count}}
- Technology: {{tech_count}}
- Business Model: {{bm_count}}
- Customer Experience: {{cx_count}}

**By Type:**
- Incremental: {{incremental_count}}
- Adjacent: {{adjacent_count}}
- Transformational: {{transformational_count}}

**Dependency Summary:**
- Foundation (enable others): {{foundation_count}}
- Dependent (require others): {{dependent_count}}
- Independent: {{independent_count}}
```

**Ask:** "Do you approve this Innovation Backlog? [Y] Yes | [N] No - needs changes"

- IF N: "What needs to change?" → iterate on specific item
- IF Y: Proceed to append and continue

---

## APPEND TO DOCUMENT

**On Approval:**

1. APPEND the approved Innovation Backlog section to `{innovationAnalysisFile}`:
   - Section 4: Innovation Backlog (ideas summary, details, categories)
   - Section 5: Feasibility Matrix (6-dimension scoring, analysis, priority matrix diagram)

2. UPDATE `{innovationIdeasDetailFile}` with detailed innovation entries:
   - For EACH approved innovation (II#):
     - Populate the detailed section using the template format
     - Include all 6-dimension feasibility scores with notes
     - Include dependencies, synergies, time-to-value, risk level
     - Include source, category, type, and all captured metadata
     - Link to related pain points (PP#) and process steps (PS#)
   - Update statistics section with counts by category, source, fit level
   - Update priority matrix section (Quick Wins, Strategic Bets, etc.)

3. Update frontmatter: add "step-03" to stepsCompleted array in both files

4. Display: "Step 3 Complete: Innovation Backlog added to Innovation Analysis document and Innovation Ideas Detail log"

---

## MENU OPTIONS

**Select an Option:** [A] Advanced Elicitation | [P] Party Mode | [C] Continue to Step 4

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

ONLY WHEN [C continue option] is selected and [innovation backlog approved and appended to document], will you then load and read fully `{nextStepFile}` to execute and begin priority generation.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:
- All innovation opportunities identified from pain points, competitors, fintech, best practices, and tech trends
- Each innovation assessed with ALL 6 feasibility dimensions using weighted scoring
- Weighted feasibility score calculated correctly for each innovation
- Dependencies and synergies captured for all innovations
- User validated each innovation with Keep/Modify/Remove decision
- New user-suggested ideas captured and assessed
- Dependency map reviewed and approved
- Innovation Backlog section appended to innovation-analysis.md
- Innovation Ideas Detail file (innovation-ideas-detail.md) populated with all approved innovations
- Menu presented and user input handled correctly

### SYSTEM FAILURE:
- Skipping feasibility assessment for any innovation
- Not applying weighted scoring formula consistently
- Proceeding without user validation per innovation
- Not capturing dependencies or synergies
- Generating backlog content without user approval
- Not updating innovation-ideas-detail.md with approved innovations
- Proceeding to next step without user selecting 'C'

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
