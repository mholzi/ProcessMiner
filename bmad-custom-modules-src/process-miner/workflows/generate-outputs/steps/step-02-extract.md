---
name: 'step-02-extract'
description: 'Silently extract and synthesize data from source documents with Amazon 6-Pager narrative quality'

# Path Definitions
workflow_path: '{module_root}/workflows/generate-outputs'
module_root: '{project-root}/bmad-custom-modules-src/process-miner'

# File References
thisStepFile: '{workflow_path}/steps/step-02-extract.md'
nextStepFile: '{workflow_path}/steps/step-03-generate.md'
workflowFile: '{workflow_path}/workflow.md'

# No menu task references needed - this is a silent auto-proceed step
---

# Step 2: Silent Data Extraction & Narrative Synthesis

## STEP GOAL:

To silently and autonomously extract data from source documents AND synthesize it into compelling narrative content that follows Amazon 6-Pager principles. This step operates WITHOUT user interaction - all quality decisions are made automatically based on the source documentation.

---

## ⚠️ SILENT EXECUTION MODE

<!--
THIS STEP RUNS SILENTLY WITHOUT USER INTERACTION

The source documents have already been validated by upstream analysts.
Step-04-review provides human review AFTER document generation.
This step extracts and synthesizes - it does NOT pause for validation.

CRITICAL: Do NOT display quality assessments, do NOT ask questions,
do NOT wait for user confirmation. Extract, transform, store, proceed.
-->

### AUTONOMOUS OPERATION PRINCIPLES

| Principle | Implementation |
|-----------|----------------|
| **No User Prompts** | Never display "Does this look correct?" or similar |
| **No Quality Questions** | Self-assess internally, do not display assessments |
| **Auto-Strengthen** | If content is weak, strengthen it automatically |
| **Silent Progress** | Do not narrate extraction progress to user |
| **Auto-Proceed** | When complete, immediately proceed to step-03 |

---

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🔇 SILENT MODE: No user interaction during this step
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When extraction complete, auto-proceed to next step
- 🤖 YOU ARE AN AUTONOMOUS EXTRACTOR, not a facilitator

### Role Reinforcement:

- ✅ You are a document synthesizer operating in AUTONOMOUS MODE
- ✅ You apply Amazon 6-Pager quality standards AUTOMATICALLY
- ✅ You strengthen weak content WITHOUT user interaction
- ✅ All decisions are based on source documentation - 100% data-driven
- ✅ User will review the FINAL document in step-04, not work-in-progress

### Step-Specific Rules:

- 🎯 Focus on SILENT extraction and transformation
- 🚫 FORBIDDEN to display quality assessments to user
- 🚫 FORBIDDEN to ask "Does this look correct?" or any similar question
- 🚫 FORBIDDEN to present menus or wait for user input
- 🔄 Auto-strengthen any weak content using Amazon 6-Pager principles
- ➡️ Auto-proceed to step-03 when extraction complete

## EXECUTION PROTOCOLS:

- 🎯 Load all relevant source documents SILENTLY
- 🎯 Extract data AND craft narrative for each section AUTONOMOUSLY
- 🎯 Self-assess quality internally (do not display to user)
- 🎯 Apply automatic strengthening for weak content
- 💾 Store NARRATIVE-READY content in session variables for step-03
- 🔄 Auto-proceed to step-03 when extraction complete
- 🚫 FORBIDDEN to wait for user input during extraction

## CONTEXT BOUNDARIES:

- Session variables from step-01 (or step-01b) are available
- `update_mode` indicates 'full', 'incremental', or null (new)
- Source documents have been pre-validated by upstream analysts
- All quality decisions made based on source documentation

---

## AMAZON 6-PAGER QUALITY STANDARDS (Applied Automatically)

### Narrative Quality Checklist (Internal Self-Assessment)

For each section, internally verify:

| Quality Check | Auto-Strengthen If... |
|---------------|----------------------|
| **Hook** | Opening doesn't create urgency → Add impact statement |
| **Specificity** | Vague descriptions → Replace with concrete numbers from source |
| **Honesty** | Sugar-coated content → Make it uncomfortable if data warrants |
| **Evidence** | Claims without data → Add source reference or remove claim |
| **Ownership** | Actions without names → Add "Owner: TBD" placeholder |
| **Consequences** | Missing "if we don't act" → Derive from impact data |

### Auto-Transformation Rules

| If Source Has... | Transform To... |
|------------------|-----------------|
| "The process could be improved" | "The process fails X% at step Y" (from metrics) |
| "Baseline: Not established" | "Baseline: UNKNOWN ⚠️ - Gap requiring action" |
| "Some challenges exist" | "We have N critical gaps: [list from source]" |
| "The team should consider" | "[Role] will deliver [thing] by [date]" or "Owner: TBD" |
| "Performance has room for improvement" | "We are X% below target. Impact: €Y" (from metrics) |

---

## SILENT EXTRACTION SEQUENCE:

### 1. Load Source Documents (Silent)

Load all relevant documents from `{current_process_folder}`:

**Primary Source Document:**
- `{source_document_path}` (as determined in step-01)

**Companion Detail Documents (if exist):**
- exceptions-detail.md
- pain-points-detail.md
- control-points-detail.md
- friction-points-detail.md
- client-touchpoints-detail.md
- innovation-market-analysis.md

**Do NOT display loading progress to user.**

---

### 2. Extract and Transform All Sections (Silent)

For each of the 6 Amazon 6-Pager sections:
1. Extract raw data from source documents
2. Transform to narrative following Amazon principles
3. Self-assess quality internally
4. Auto-strengthen if below quality bar
5. Store in session variable

**Do NOT display section content or quality assessments to user.**

---

#### SECTION 1: Introduction (Silent Extraction)

**Extract from source:**
- Process/journey name and ID
- Business unit and scope
- Key metrics (especially problem indicators)
- Impact data (cost, volume, risk)

**Auto-Transform to Narrative:**
- Create hook that establishes urgency using extracted impact data
- Define scope clearly from source metadata
- State the "why now" from metrics trends

**Auto-Strengthen if needed:**
- If no clear problem statement → derive from pain points/exceptions count
- If no impact data → note as gap in document

**Store as:** `extracted_introduction`

---

#### SECTION 2: Goals (Silent Extraction)

**Extract from source:**
- Current metrics (from Key Metrics tables)
- Baseline values
- Target values
- KPIs and success measures

**Auto-Transform to Narrative:**
- Create SMART goals table
- Flag missing baselines as gaps (don't accept "Not established")
- Add vision statement derived from process purpose

**Auto-Strengthen if needed:**
- If baseline missing → mark as "UNKNOWN ⚠️ - Measurement gap"
- If target missing → mark as "TBD - Requires stakeholder input"

**Store as:** `extracted_goals`

---

#### SECTION 3: Tenets (Silent Extraction)

**Extract from source:**
- Stated principles
- Constraints mentioned
- Non-negotiables
- Compliance requirements

**Auto-Transform to Narrative:**
- Convert principles to trade-off resolvers
- Each tenet must answer "X over Y when they conflict"
- Derive from control points and compliance requirements

**Auto-Strengthen if needed:**
- If tenets are platitudes → make them specific trade-offs
- If no clear constraints → derive from regulatory controls

**Store as:** `extracted_tenets`

---

#### SECTION 4: State of the Business (Silent Extraction)

**Extract from source:**
- All key metrics
- Summary tables
- Current state descriptions
- Issues and gaps
- Top pain points / friction points / exceptions

**Auto-Transform to Narrative:**
- Create executive summary (3-4 hard-hitting sentences)
- Build scorecard from metrics
- "What's Working" from positive indicators
- "What's NOT Working" - brutally honest from issues data
- Top 5 critical items from prioritized pain points

**Auto-Strengthen if needed:**
- If "What's NOT Working" is too gentle → strengthen using actual failure data
- If Top 5 lacks evidence → add source references

**Store as:** `extracted_state`

---

#### SECTION 5: Lessons Learned (Silent Extraction)

**Extract from source:**
- Root cause analysis
- Gap analysis findings
- Validation notes
- Failures and issues
- Historical context

**Auto-Transform to Narrative:**
- "What We Got Right" - specific successes
- "What We Got Wrong" - uncomfortable truths (CRITICAL: do not sugar-coat)
- Root causes table with accountability
- Key insights (actionable, not observational)

**Auto-Strengthen if needed:**
- If lessons are too polite → strengthen to make them uncomfortable
- If no accountability → add "Accountability: TBD"
- If symptoms not root causes → note as "Root cause analysis needed"

**Store as:** `extracted_lessons`

---

#### SECTION 6: Strategic Priorities (Silent Extraction)

**Extract from source:**
- Pain points with priority ratings
- Improvement opportunities
- Enhancement ideas
- Recommendations
- Quick wins identified

**Auto-Transform to Narrative:**
- 3 priorities with: Objective, Why Now, Actions, Success Criteria, Consequences
- Quick Wins table (low effort, high impact)
- Next Steps with ownership and deadlines

**Auto-Strengthen if needed:**
- If "Why Now" weak → add urgency from impact data
- If actions lack owners → add "Owner: TBD"
- If consequences vague → make specific using metrics

**Store as:** `extracted_priorities`

---

#### APPENDIX Data (Silent Extraction)

**Extract from source:**
- Complete registers (all items)
- Diagrams (Mermaid)
- Supporting tables
- Source document references
- Contributors list

**Store as:** `extracted_appendix`

---

### 3. Internal Quality Summary (Not Displayed)

After all sections extracted, internally calculate:

| Section | Quality Score | Auto-Strengthened |
|---------|---------------|-------------------|
| Introduction | {1-5} | {yes/no} |
| Goals | {1-5} | {yes/no} |
| Tenets | {1-5} | {yes/no} |
| State of Business | {1-5} | {yes/no} |
| Lessons Learned | {1-5} | {yes/no} |
| Strategic Priorities | {1-5} | {yes/no} |

**Store as:** `quality_scores` (for potential debugging, not displayed)

---

### 4. Auto-Proceed to Generation

**Do NOT present a menu.**

After all sections extracted and stored:

1. Set `extraction_complete` = true
2. Immediately load, read entire file, then execute `{nextStepFile}`

---

## SESSION VARIABLES SET BY THIS STEP

| Variable | Description |
|----------|-------------|
| `extracted_introduction` | Narrative-ready introduction content |
| `extracted_goals` | Narrative-ready goals content |
| `extracted_tenets` | Narrative-ready tenets content |
| `extracted_state` | Narrative-ready state of business content |
| `extracted_lessons` | Narrative-ready lessons learned content |
| `extracted_priorities` | Narrative-ready strategic priorities content |
| `extracted_appendix` | Appendix data references |
| `quality_scores` | Per-section quality assessment (internal) |
| `extraction_complete` | Boolean - all sections extracted |

---

## CRITICAL STEP COMPLETION NOTE

This is an **AUTO-PROCEED** step with NO user interaction.

When extraction of all 6 sections is complete:
1. Store all extracted content in session variables
2. Set `extraction_complete` = true
3. **Immediately** load, read entire file, then execute `{nextStepFile}` to begin management summary generation

**Do NOT:**
- Present a menu
- Ask for user confirmation
- Display extraction results
- Wait for any user input

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- All source documents loaded SILENTLY
- All 6 sections extracted with NARRATIVE QUALITY
- Weak content auto-strengthened based on Amazon 6-Pager principles
- Quality self-assessment completed internally (not displayed)
- All session variables populated for step-03
- Auto-proceed to step-03-generate executed WITHOUT user interaction

### ❌ SYSTEM FAILURE:

- Displaying quality assessments to user
- Asking "Does this look correct?" or any validation question
- Presenting a menu or waiting for user input
- Accepting vague content without auto-strengthening
- Not storing all required session variables
- Not auto-proceeding to next step

**Master Rule:** This step runs SILENTLY. Any user interaction during extraction is FORBIDDEN and constitutes SYSTEM FAILURE.
