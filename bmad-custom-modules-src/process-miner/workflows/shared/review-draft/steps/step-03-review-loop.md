---
name: 'step-03-review-loop'
description: 'Section-by-section, subsection-by-subsection document review with confidence scoring'

# Path Definitions
workflow_path: '{project-root}/.bmad/custom/modules/process-miner/workflows/review-draft'

# File References
thisStepFile: '{workflow_path}/steps/step-03-review-loop.md'
nextStepFile: '{workflow_path}/steps/step-04-summary.md'
workflowFile: '{workflow_path}/workflow.md'

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
partyModeWorkflow: '{project-root}/.bmad/core/workflows/party-mode/workflow.md'
brainstormingWorkflow: '{project-root}/.bmad/core/workflows/brainstorming-session/workflow.md'
---

# Step 3: Section Review Loop

## STEP GOAL:

To systematically review each section of the document, drilling into subsections, calculating confidence scores, generating clarification questions, and capturing SME validation or corrections.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- NEVER generate content without user input
- CRITICAL: Read the complete step file before taking any action
- CRITICAL: When loading next step, ensure entire file is read
- YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:

- You are a document review facilitator
- If you already have been given a name, communication_style and identity, continue to use those while playing this new role
- We engage in collaborative dialogue, not command-response
- You bring document analysis expertise, user brings domain knowledge
- AI drafts clarifications, SME validates - never ask SME to write from scratch

### Step-Specific Rules:

- Focus on ONE SUBSECTION at a time - never show all subsections together
- Calculate confidence score before showing each subsection
- Generate clarification questions if confidence < 90%
- Show before/after for all corrections
- Track all changes with contributor attribution

## EXECUTION PROTOCOLS:

- Save progress to review-state.json after each subsection
- Present standard 5-option menu for each subsection
- Use numbered options only (never text-based)
- Update document immediately when corrections are approved

## CONTEXT BOUNDARIES:

- Document is loaded (from step-01/02)
- Schema is resolved (may be auto-discovery mode)
- review-state.json contains section inventory
- Contributor info available from session

## DISPLAY RULES (CRITICAL):

### NO EMOJIS
- Do not use any emojis or icons in output
- Use plain text only

### EXACT OPTIONS FORMAT
Every review prompt MUST use this format:
```
| # | Action |
|---|--------|
| 1 | Approve - Content is accurate and complete |
| 2 | Minor Correction - Small wording/content fixes |
| 3 | Full Elicitation - Significant expansion using brainstorming |
| 4 | Skip to Next - Review this later |
| 5 | Return to Section Menu |

Select action (1-5):
```

## REVIEW SEQUENCE:

### 1. Display Section Menu

Present the section review menu:
```
**Document Review - Section Selection**

| # | Section | Status | Confidence |
|---|---------|--------|------------|
| 1 | [Section 1 title] | [pending/approved/etc] | [score or --] |
| 2 | [Section 2 title] | [pending/approved/etc] | [score or --] |
...

| # | Action |
|---|--------|
| 1-N | Select section number to review |
| a | Review all sections sequentially |
| p | Follow priority order (lowest confidence first) |
| c | Complete review - proceed to summary |

Select option:
```

### 2. Handle Section Selection

**If specific section (1-N):**
- Load that section for review
- Proceed to subsection loop

**If 'a' (all sequential):**
- Queue all pending sections
- Start with first pending section

**If 'p' (priority order):**
- Sort sections by confidence (lowest first)
- Queue in that order

**If 'c' (complete):**
- Check if any sections still pending
- If pending remain: Warn user, confirm intent
- If all reviewed: Proceed to step-04-summary

### 3. Enter Section

When entering a section:
```
---
**Entering Section [N]: [Title]**
---
```

**Parse section for subsections:**
- Find all ### headers within the ## section
- Build subsection inventory (e.g., 1.1, 1.2, 1.3)
- If no subsections: Treat entire section as one unit

### 4. Subsection Review Loop

For each subsection (or section if no subsections):

#### 4a. Calculate Confidence Score

Analyze subsection content and calculate confidence (0-100%):

**Completeness factors (50% weight):**
- All required fields populated (no [TBD], [Unknown], TODO, ...)
- Sufficient detail depth (not just bullet points)
- Cross-references present where expected (PS#, CP#, SYS#, etc.)
- No incomplete sentences or trailing "..."

**Accuracy factors (50% weight):**
- Consistency with other sections (no contradictions)
- Terminology matches defined terms
- IDs referenced actually exist
- Logical flow and coherence

Store: `subsection_confidence` (integer 0-100)

#### 4b. Generate Clarification Questions (if needed)

If confidence < 90%, generate prioritized clarification questions:

- Focus on ONE specific issue per question
- Order by impact on confidence (highest impact first)
- Make questions specific and actionable
- Include context about why this matters

Store: `clarification_questions` (array, ordered by priority)

#### 4c. Display Subsection

```
---
**Subsection [N.M]: [Title]**

| Confidence | [X]% |
|------------|------|

---

[subsection content from document]

---
```

#### 4d. Confidence-Driven Clarification Loop (if < 90%)

**CRITICAL:** User cannot approve a section until confidence reaches >= 90%. The loop continues until either:
- Confidence reaches >= 90% (then show final review menu)
- User chooses to skip the section entirely (mark as "skipped - needs attention")

If confidence < 90%:

```
Confidence: [X]% (requires 90% to approve)

I have [N] question(s) that could improve this section.

---
**Clarification [1] of [N]:**

[question text]

*Why this matters:* [rationale]
---

| # | Action |
|---|--------|
| a | Answer this question |
| s | Skip this question (move to next question) |
| e | Elicitation options (brainstorming, party mode, etc.) |
| x | Skip entire section - review later |

Select:
```

**Handle clarification response:**

- If 'a' (answer):
  - Collect user's answer
  - Incorporate into subsection content
  - Recalculate confidence
  - Show updated content with new confidence
  - **If confidence still < 90%:** Continue loop (next question or offer elicitation)
  - **If confidence >= 90%:** Exit loop, proceed to final review menu

- If 's' (skip question):
  - Move to next clarification question
  - If no more questions and confidence still < 90%: Show elicitation options

- If 'e' (elicitation):
  - Show elicitation sub-menu (same as Option 3 in final review menu)
  - After elicitation, recalculate confidence
  - If still < 90%, continue clarification loop

- If 'x' (skip section):
  - Mark section as "skipped - needs attention"
  - Return to section menu
  - Section will appear as incomplete in summary

**After all questions exhausted and confidence still < 90%:**
```
All clarification questions answered but confidence is still [X]%.

| # | Action |
|---|--------|
| e | Elicitation options - Use advanced techniques to improve content |
| c | Add custom correction - Provide additional information |
| x | Skip section - Review later (will appear as incomplete) |

Select:
```

**Loop continues until confidence >= 90% or user skips section.**

#### 4e. Final Review Menu

**Only shown when confidence >= 90%:**

```
| # | Action |
|---|--------|
| 1 | Approve - Content is accurate and complete |
| 2 | Minor Correction - Small wording/content fixes |
| 3 | Full Elicitation - Significant expansion using brainstorming |
| 4 | Skip to Next - Review this later |
| 5 | Return to Section Menu |

Select action (1-5):
```

### 5. Handle Review Actions

#### Option 1: Approve
- Mark subsection as approved
- Update confidence to HIGH in tracking
- Save to review-state.json
- Proceed to next subsection

#### Option 2: Minor Correction
```
What needs to be corrected?
```

After user input:
- AI applies corrections
- Show before/after:
```
**BEFORE:**
[original text]

**AFTER:**
[corrected text]

Apply this correction? (y/n):
```

If confirmed:
- Apply correction to document
- Recalculate confidence
- Log correction in review-state.json
- Show: "Correction applied. New confidence: [X]%"

#### Option 3: Full Elicitation

Display sub-menu:
```
**Rewrite Options:**
- **[A] Advanced Elicitation** — Use structured techniques (5 Whys, SIPOC, etc.)
- **[P] Party Mode** — Get multiple AI agent perspectives
- **[B] Brainstorming** — Creative exploration session
- **[Q] Quick Questions** — Targeted clarification (3-5 questions)
- **[X] Back** — Return to review menu
```

**Handle sub-menu selection:**

**If 'A' (Advanced Elicitation):**
- Load `{advancedElicitationTask}`
- Execute with subsection context
- Return with refined content
- Show proposed expansion
- Get user approval (y/n)
- Apply to document

**If 'P' (Party Mode):**
- Load `{partyModeWorkflow}`
- Execute with subsection as topic
- Return with consensus output
- Show proposed expansion
- Get user approval (y/n)
- Apply to document

**If 'B' (Brainstorming):**
- Load `{brainstormingWorkflow}`
- Execute with subsection context
- Return with ideas incorporated
- Show proposed expansion
- Get user approval (y/n)
- Apply to document

**If 'Q' (Quick Questions):**
- Generate 3-5 targeted questions based on gaps
- Collect answers one at a time
- Incorporate answers into content
- Show proposed expansion
- Get user approval (y/n)
- Apply to document

**If 'X' (Back):**
- Return to standard review menu (options 1-5)

#### Option 4: Skip
- Mark subsection as "skipped"
- Proceed to next subsection
- Will appear as pending in summary

#### Option 5: Return to Section Menu
- Save current progress
- Return to section selection menu

### 6. Track Progress

After each subsection:
- Update review-state.json:
  ```json
  {
    "sections": [{
      "id": N,
      "status": "in_progress",
      "subsections": [
        { "id": "1.1", "status": "approved", "confidence": 95 },
        { "id": "1.2", "status": "corrected", "confidence": 88 }
      ],
      "current_subsection": "1.3"
    }]
  }
  ```
- Update `last_updated` timestamp

### 7. Section Complete

When all subsections in a section are reviewed:
```
---
**Section [N] Complete**

| Subsection | Status | Confidence |
|------------|--------|------------|
| [N.1] | [status] | [X]% |
| [N.2] | [status] | [X]% |
...

**Section Average Confidence:** [X]%

| # | Action |
|---|--------|
| 1 | Return to Section Menu |
| 2 | Continue to next section |

Select:
```

Update section status in review-state.json based on subsection results.

### 8. All Sections Complete

When all sections have been reviewed (or user selects 'c' from menu):

```
**All sections reviewed.**

| Section | Status | Confidence |
|---------|--------|------------|
...

Ready to generate review summary.
```

### 9. Present MENU OPTIONS

Display: **Select an Option:** [A] Advanced Elicitation [C] Continue to Summary

#### Menu Handling Logic:

- IF A: Execute {advancedElicitationTask} for overall document review
- IF C: Update review-state.json (current_step: 4), then load, read entire file, then execute `{nextStepFile}`
- IF Any other comments or queries: help user respond then redisplay menu

---

## REVIEW COMMANDS

Support these commands throughout review:

- **[back]** - Return to previous subsection
- **[jump X.Y]** - Jump to specific subsection
- **[status]** - Show review progress summary
- **[save]** - Save current progress
- **[help]** - Show available commands

---

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN user selects C and all desired sections are reviewed, will you:

1. Update review-state.json with `current_step: 4`
2. Load, read entire file, then execute `{nextStepFile}` to generate summary

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- Each subsection reviewed individually (never all at once)
- Confidence calculated before each review
- Clarification questions generated when confidence < 90%
- **Approval only allowed when confidence >= 90%**
- **Clarification loop continues until confidence >= 90% or user skips section**
- Elicitation options offered when clarification questions exhausted but confidence still < 90%
- Standard 5-option menu used consistently (only after confidence >= 90%)
- Before/after shown for all corrections
- Progress saved to review-state.json after each subsection
- Changes attributed to contributor

### SYSTEM FAILURE:

- Showing all subsections at once
- Using emojis in output
- **Allowing user to approve a section with confidence < 90%**
- **Showing final review menu (with Approve option) when confidence < 90%**
- **Exiting clarification loop before confidence reaches 90% (unless user explicitly skips section)**
- Using custom options instead of standard 5
- Not calculating confidence scores
- Not generating clarification questions when needed
- Not saving progress regularly
- Asking SME to write from scratch (AI should draft)

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE. **Approval requires >= 90% confidence - no exceptions.**
