---
document_type: Workflow Edit Analysis
workflow_name: Generate Management Summary
workflow_path: /Volumes/My Passport/ProcessMiner3/bmad-custom-modules-src/process-miner/workflows/generate-outputs
user_goal: Make step-02-extract fully silent (non-interactive), based 100% on source documentation
analysis_date: 2025-12-09
stepsCompleted: [1, 2, 3]
lastStep: 'improve'
---

# Workflow Edit Analysis: Generate Management Summary

## Target Workflow

- **Path**: `bmad-custom-modules-src/process-miner/workflows/generate-outputs`
- **Name**: Generate Management Summary
- **Module**: process-miner
- **Format**: Standalone (New format with step-file architecture)

---

## Structure Analysis

- **Type**: Document generation workflow (transforms source docs into Amazon 6-Pager summaries)
- **Total Steps**: 5 files (step-01-init, step-01b-continue, step-02-extract, step-03-generate, step-04-review)
- **Step Flow Pattern**:
  ```
  step-01-init
      ├── (existing summary) → step-01b-continue → step-02-extract
      └── (no summary) → step-02-extract
  step-02-extract → step-03-generate → step-04-review → END
  ```
- **Files**:
  - `workflow.md` - Entry point and configuration
  - `steps/step-01-init.md` - Process selection, agent detection, validation
  - `steps/step-01b-continue.md` - Material change detection for existing summaries
  - `steps/step-02-extract.md` - Data extraction with narrative quality (577 lines)
  - `steps/step-03-generate.md` - Document generation from extracted data
  - `steps/step-04-review.md` - Review and finalize

---

## Content Characteristics

- **Purpose**: Generate Amazon 6-Pager management summaries from process documentation
- **Instruction Style**: Highly prescriptive with extensive quality enforcement
- **User Interaction**: Heavily interactive - especially step-02
- **Complexity**: High - extensive Amazon 6-Pager formatting requirements

---

## User's Edit Goal

**Requirement**: Make step-02-extract fully silent (non-interactive), basing extraction 100% on source documentation. User will only start reviewing once the document has been created.

---

## Current step-02-extract Analysis

### Current Behavior (INTERACTIVE)

The current step-02-extract.md has the following interactive patterns:

1. **Section-by-Section User Validation** (lines 143-480):
   - Each of the 6 Amazon 6-Pager sections requires user confirmation
   - Pattern: "Wait for user confirmation or adjustments" after each section
   - Quality assessments presented for user review

2. **Quality Challenge Prompts** (throughout):
   - "Does this opening HOOK an executive? Should we strengthen it?"
   - "Does this goal structure create accountability?"
   - "Are these principles that will actually guide decisions?"
   - "Is this an honest diagnostic?"
   - "Is this honest enough? Would this make stakeholders uncomfortable?"
   - "Do these priorities create the right urgency?"

3. **Menu System** (lines 509-530):
   - Interactive menu with [A] Advanced Elicitation, [P] Party Mode, [S] Strengthen Section, [C] Continue
   - Requires user selection before proceeding

4. **Iterative Loop Pattern** (line 146-151):
   ```
   For each section, follow this pattern:
   1. Extract raw data
   2. Transform to narrative
   3. Self-assess quality
   4. Present to user
   5. Iterate until quality bar met
   ```

### Why It's Interactive

The step was designed to ensure **narrative quality** by requiring human validation of executive communication before proceeding. The Amazon 6-Pager principles emphasize:
- "Uncomfortable" honesty in Lessons Learned
- Hooks that create urgency
- Tenets that resolve trade-offs
- Strategic priorities with clear ownership

---

## Recommended Changes to Make step-02 Silent

### High-Level Strategy

Transform step-02-extract from an **interactive facilitator** model to an **autonomous extraction** model that:
1. Loads all source documents silently
2. Extracts and synthesizes all 6 sections automatically
3. Self-assesses quality internally (without displaying assessments)
4. Stores all extracted content for step-03
5. Auto-proceeds to step-03-generate

### Specific Changes Required

#### 1. Remove Section-by-Section User Prompts

**Current** (for each section):
```markdown
"Does this opening HOOK an executive? Should we strengthen it?"
**Wait for user confirmation or adjustments.**
```

**Change to**:
```markdown
[Extract data and transform to narrative silently]
[Store in session variable]
[Proceed to next section]
```

#### 2. Change Menu to Auto-Proceed Pattern

**Current** (lines 509-530):
```markdown
### 4. Present MENU OPTIONS

Display: "**Select an Option:**
[A] Advanced Elicitation...
[S] Strengthen Section...
[C] Continue..."

#### Menu Handling Logic:
- IF A: Execute {advancedElicitationTask}...
- IF C: Store all extracted data, load next step
```

**Change to**:
```markdown
### 4. Auto-Proceed to Generation

After all sections extracted and quality self-assessed:
- Store all extracted data in session variables
- Log extraction summary (optional, for debugging)
- Immediately load, read entire file, then execute {nextStepFile}

#### EXECUTION RULES:
- This is an auto-proceed extraction step with no user interaction
- Proceed directly to step-03-generate after extraction complete
```

#### 3. Modify Execution Protocols

**Current**:
```markdown
## EXECUTION PROTOCOLS:
- 🎯 Load all relevant source documents
- 🎯 Extract data AND craft narrative for each section
- 🎯 Challenge weak content before presenting
- 🎯 Present extraction with narrative quality assessment
- 💾 Store NARRATIVE-READY content for step-03
- 🚫 FORBIDDEN to proceed with content that doesn't meet quality bar
```

**Change to**:
```markdown
## EXECUTION PROTOCOLS:
- 🎯 Load all relevant source documents SILENTLY
- 🎯 Extract data AND craft narrative for each section AUTONOMOUSLY
- 🎯 Self-assess quality internally (do not display to user)
- 🎯 Apply automatic strengthening for weak content
- 💾 Store NARRATIVE-READY content for step-03
- 🔄 Auto-proceed to step-03 when extraction complete
- 🚫 FORBIDDEN to wait for user input during extraction
```

#### 4. Update Role Reinforcement

**Current**:
```markdown
### Role Reinforcement:
- ✅ You are a document synthesizer and executive communication specialist
- ✅ Your job is to make executives CARE about what they're reading
- ✅ Weak content that gets through this step will produce a weak document
- ✅ Challenge the user: "Is this honest enough?" "Does this create urgency?"
```

**Change to**:
```markdown
### Role Reinforcement:
- ✅ You are a document synthesizer and executive communication specialist
- ✅ Your job is to make executives CARE about what they're reading
- ✅ You apply Amazon 6-Pager quality standards AUTOMATICALLY
- ✅ You strengthen weak content WITHOUT user interaction
- ✅ All quality decisions are made based on source documentation
```

#### 5. Remove Interactive Quality Checks

Remove all instances of:
- "Does this look correct?"
- "Should we strengthen it?"
- "Wait for user confirmation"
- "Is this honest enough?"
- Quality check tables presented for user review

Replace with internal self-assessment that auto-strengthens weak content.

#### 6. Update Success/Failure Metrics

**Current**:
```markdown
### ✅ SUCCESS:
- All source documents loaded
- All 6 sections extracted with NARRATIVE QUALITY
- Weak content challenged and strengthened
- Each section validated by user
- Quality assessment completed
```

**Change to**:
```markdown
### ✅ SUCCESS:
- All source documents loaded SILENTLY
- All 6 sections extracted with NARRATIVE QUALITY
- Weak content auto-strengthened based on Amazon 6-Pager principles
- Quality self-assessment completed internally
- All session variables populated for step-03
- Auto-proceed to step-03-generate executed
```

---

## Impact on Other Steps

### step-01-init.md
- **No changes needed** - Already routes automatically to step-02

### step-01b-continue.md
- **Keep interactive** - User decision on Update/Regenerate/Keep is meaningful
- Change detection should remain user-reviewed

### step-03-generate.md
- **No changes needed** - Currently receives extracted data and generates document
- May want to also make silent if full autonomy desired

### step-04-review.md
- **Keep interactive** - This is where user reviews the GENERATED document
- Aligns with user's goal: "User will only start reviewing once the document has been created"

---

## Alternative Approaches

### Option A: Full Silent Mode (Recommended)
Make step-02 completely silent with auto-proceed. User's first interaction is at step-04-review.

### Option B: Summary-Only Mode
Silent extraction, but present a brief summary at the end before proceeding:
```
"Extracted 6 sections from source documentation.
Quality Score: 4.2/5 average
Proceeding to generate document..."
```
Then auto-proceed (no menu).

### Option C: Quality Gate Mode
Silent extraction, but halt only if critical quality issues:
```
IF quality_score < 3 for any section:
    Display warning and ask user
ELSE:
    Auto-proceed
```

---

## Compliance Notes

### Format Compliance
- Workflow follows new standalone format ✅
- Step files have proper frontmatter ✅
- Variable references use {variable} format ✅

### Best Practices Alignment
- Menu handling follows standard patterns ✅
- State tracking in frontmatter ✅
- Role reinforcement present ✅
- Success/failure metrics defined ✅

### Changes Will Require
- Updating MANDATORY EXECUTION RULES section
- Removing "NEVER generate content without user input" rule (for this step only)
- Adding auto-proceed pattern from step-template.md

---

## Files to Modify

| File | Change Type | Scope |
|------|-------------|-------|
| `steps/step-02-extract.md` | Major rewrite | Remove all interactive prompts, add auto-proceed |

---

## Improvement Goals (Step 2 Discovery)

### User's Primary Goal
**Make step-02-extract fully silent (non-interactive)**, basing extraction 100% on source documentation. User will only start reviewing once the document has been created in step-04.

### Motivation
- Source documents are **already validated** by upstream analysts
- Interactive validation of AI-synthesized content is **redundant**
- User wants **batch processing capability** - run workflow, get document
- Step-04-review provides the meaningful human review point

### Party Mode Consensus
All agents (BMad Master, BMad Builder, Process Documentation Analyst, Client Journey Analyst) agreed:
- Use auto-proceed pattern from step-template.md
- Keep quality logic, remove interaction
- Schema compliance makes extraction deterministic
- 100% reduction in workflow friction

### Prioritized Improvements

| Priority | Improvement | Impact | Effort |
|----------|-------------|--------|--------|
| **CRITICAL** | Remove all 6 interactive checkpoints from step-02 | Eliminates 15-20 min user burden | Medium |
| **CRITICAL** | Replace menu with auto-proceed pattern | Enables silent flow to step-03 | Low |
| **IMPORTANT** | Keep quality self-assessment logic (internal) | Maintains document quality | Low |
| **IMPORTANT** | Auto-strengthen weak content without asking | Quality preserved silently | Medium |
| **NICE-TO-HAVE** | Add extraction summary log (optional) | Debugging visibility | Low |

### Specific Changes Required

**File:** `step-02-extract.md`

1. **Remove** all "Wait for user confirmation" prompts (6 instances)
2. **Remove** all quality challenge questions displayed to user
3. **Change** menu from interactive `[A][P][S][C]` to auto-proceed
4. **Update** execution protocols to forbid user interaction
5. **Update** role reinforcement for autonomous operation
6. **Modify** success/failure metrics for silent execution
7. **Keep** narrative transformation logic (Amazon 6-Pager quality)
8. **Keep** internal quality assessment (just don't display it)

---

## Implementation Complete (Step 3)

### Changes Made to `step-02-extract.md`

**File:** `bmad-custom-modules-src/process-miner/workflows/generate-outputs/steps/step-02-extract.md`

| Change | Before | After |
|--------|--------|-------|
| **Step Name** | "Data Extraction & Narrative Synthesis" | "Silent Data Extraction & Narrative Synthesis" |
| **Step Goal** | Interactive facilitation | Silent autonomous extraction |
| **Line Count** | 577 lines | 385 lines |
| **User Prompts** | 6 section confirmations | 0 prompts |
| **Quality Questions** | 12+ displayed to user | 0 displayed (internal only) |
| **Menu** | `[A][P][S][C]` interactive | Auto-proceed (no menu) |

### Key Structural Changes

1. **New "SILENT EXECUTION MODE" section** (lines 25-47)
   - HTML comment explaining silent operation
   - AUTONOMOUS OPERATION PRINCIPLES table

2. **Updated MANDATORY EXECUTION RULES** (lines 50-92)
   - Changed from facilitator to autonomous extractor role
   - Added 🔇 SILENT MODE as first rule
   - FORBIDDEN to display quality assessments

3. **New "AMAZON 6-PAGER QUALITY STANDARDS" section** (lines 95-119)
   - Auto-strengthen rules table
   - Auto-transformation patterns

4. **Rewritten EXTRACTION SEQUENCE** (lines 122-327)
   - Each section now: Extract → Transform → Auto-Strengthen → Store
   - Removed all "Wait for user confirmation" blocks
   - Added "Do NOT display" instructions

5. **Replaced Menu with Auto-Proceed** (lines 320-328)
   - No menu presentation
   - Immediate load and execute of next step

6. **Updated SUCCESS/FAILURE METRICS** (lines 364-383)
   - Success: Silent operation, auto-proceed executed
   - Failure: Any user interaction during extraction

### BMAD Compliance Verification

| Standard | Status | Notes |
|----------|--------|-------|
| Step file structure | ✅ | Proper frontmatter, sections |
| Frontmatter variables | ✅ | All paths use {variable} format |
| Step goal defined | ✅ | Clear autonomous extraction goal |
| Role reinforcement | ✅ | Updated for autonomous mode |
| Execution protocols | ✅ | Updated for silent operation |
| Session variables | ✅ | All 9 variables documented |
| Success/failure metrics | ✅ | Clear criteria for silent mode |
| Auto-proceed pattern | ✅ | Follows step-template.md pattern |

---

_Analysis completed on 2025-12-09_
