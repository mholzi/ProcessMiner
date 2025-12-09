---
name: 'step-01b-continue'
description: 'Handle review session continuation from previous session'

# Path Definitions
workflow_path: '{project-root}/.bmad/custom/modules/process-miner/workflows/review-draft'

# File References
thisStepFile: '{workflow_path}/steps/step-01b-continue.md'
workflowFile: '{workflow_path}/workflow.md'

# Dynamic next step - determined by review state
step02Sync: '{workflow_path}/steps/step-02-sync.md'
step03Review: '{workflow_path}/steps/step-03-review-loop.md'
step04Summary: '{workflow_path}/steps/step-04-summary.md'
---

# Step 1B: Review Session Continuation

## STEP GOAL:

To resume an existing document review session from where it was left off, ensuring smooth continuation without loss of context or progress.

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
- Maintain professional, supportive tone throughout

### Step-Specific Rules:

- Focus ONLY on analyzing and resuming review state
- FORBIDDEN to modify content reviewed in previous sessions
- Maintain continuity with previous sessions
- DETECT exact continuation point from review-state.json

## EXECUTION PROTOCOLS:

- Show your analysis of current state before taking action
- Keep existing review-state.json values intact
- Review the document's current state
- FORBIDDEN to re-review sections already approved
- Update review-state.json with continuation timestamp when resuming

## CONTEXT BOUNDARIES:

- review-state.json is already loaded (from step-01-init detection)
- Previous context = review-state.json + document state
- Section statuses already tracked in previous sessions
- Last step = determined by current_step in review-state.json

## CONTINUATION SEQUENCE:

### 1. Analyze Current State

Parse review-state.json to understand:

- `document_path`: Which document is being reviewed
- `schema_mode`: How schema was resolved
- `contributor`: Who started the review
- `started`: When review began
- `last_updated`: Last activity timestamp
- `sections`: Status of each section
- `current_step`: Which workflow step was last active
- `sync_completed`: Whether sync step was completed

**Calculate progress:**
```
sections_total = count of sections
sections_approved = count where status = "approved"
sections_corrected = count where status = "corrected"
sections_pending = count where status = "pending"
sections_in_progress = count where status = "in_progress"
completion_percentage = (approved + corrected) / total * 100
```

### 2. Load Document

Read the complete document to verify:
- Document still exists at recorded path
- Document structure matches recorded sections
- No major structural changes since last session

**If document changed significantly:**
- Warn user: "Document structure has changed since last session"
- Offer options:
  1. Continue with existing review state (may have mismatches)
  2. Start fresh review (lose previous progress)
  3. Re-scan sections and merge with existing state

### 3. Display Session Status

Present continuation summary:

```
**Existing Review Session Found**

| Field | Value |
|-------|-------|
| Document | [filename] |
| Started | [date] |
| Last Activity | [date] |
| Original Reviewer | [name] ([role]) |

**Review Progress:**
| Status | Count |
|--------|-------|
| Approved | [n] |
| Corrected | [n] |
| In Progress | [n] |
| Pending | [n] |
| **Total** | [n] |
| **Completion** | [x]% |

**Section Status:**
| # | Section | Status |
|---|---------|--------|
| 1 | [title] | [status] |
| 2 | [title] | [status] |
...
```

### 4. Determine Resume Point

Based on review-state.json, determine where to continue:

**Case A: Sync not completed (sync_completed = false)**
- If schema has sync-enabled sections: Resume at step-02-sync
- If no sync capabilities: Jump to step-03-review

**Case B: Sync completed, review in progress**
- Resume at step-03-review-loop
- Pre-select the in_progress section (if any)

**Case C: All sections reviewed**
- Resume at step-04-summary
- User can finalize or re-review specific sections

### 5. Verify Contributor

"Are you the same reviewer who started this session?

**Original reviewer:** [name] ([role])

| # | Option |
|---|--------|
| 1 | Yes, I'm [name] - continue as same reviewer |
| 2 | No, I'm a different person - add me as contributor |

Select (1-2):"

**If different contributor:**
- Collect new name and role
- Add to contributors list in review-state.json
- All changes will be attributed to new contributor

### 6. Confirm Continuation Intent

"Ready to continue your review session.

**Resume point:** [step description]
**Next action:** [what will happen next]

| # | Option |
|---|--------|
| 1 | Continue where I left off |
| 2 | Jump to a specific section |
| 3 | Re-review a completed section |
| 4 | Start completely fresh (lose progress) |

Select (1-4):"

### 7. Handle User Choice

**If Option 1 (Continue):**
- Update review-state.json: `last_updated`, `last_continued`
- Proceed to determined resume step

**If Option 2 (Jump to section):**
- Display section list with statuses
- Let user select section number
- Set that section as in_progress
- Proceed to step-03-review-loop

**If Option 3 (Re-review completed):**
- Display only approved/corrected sections
- Let user select which to re-review
- Reset that section status to "in_progress"
- Proceed to step-03-review-loop

**If Option 4 (Start fresh):**
- Confirm: "This will delete all review progress. Are you sure? (y/n)"
- If confirmed: Delete review-state.json, return to step-01-init
- If not: Return to option menu

### 8. Present MENU OPTIONS

Display: "**Resuming review session - Select an Option:** [C] Continue"

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed when user selects 'C'
- User can chat or ask questions - always respond then redisplay menu

#### Menu Handling Logic:

- IF C:
  1. Update review-state.json: add `last_continued: [current timestamp]`
  2. Based on determined resume point:
     - If resuming sync: load, read, execute `{step02Sync}`
     - If resuming review: load, read, execute `{step03Review}`
     - If resuming summary: load, read, execute `{step04Summary}`
- IF Any other comments or queries: help user respond then redisplay menu

---

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN C is selected and continuation analysis is complete, will you:

1. Update review-state.json with continuation timestamp
2. Load, read entire file, then execute the appropriate next step

Do NOT modify any section content during this continuation step.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- Correctly analyzed review-state.json
- Displayed accurate progress summary
- Verified contributor identity
- User confirmed continuation intent
- review-state.json updated with continuation info
- Review resumed at appropriate step

### SYSTEM FAILURE:

- Skipping analysis of existing state
- Modifying section content from previous sessions
- Loading wrong next step
- Not updating review-state.json with continuation info
- Proceeding without user confirmation

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
