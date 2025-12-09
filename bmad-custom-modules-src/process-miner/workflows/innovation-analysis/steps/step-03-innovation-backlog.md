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
