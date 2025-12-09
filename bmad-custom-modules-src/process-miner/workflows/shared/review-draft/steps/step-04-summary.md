---
name: 'step-04-summary'
description: 'Cross-section consistency check, generate review summary and update change log'

# Path Definitions
workflow_path: '{project-root}/.bmad/custom/modules/process-miner/workflows/review-draft'
module_root: '{project-root}/bmad-custom-modules-src/process-miner'

# File References
thisStepFile: '{workflow_path}/steps/step-04-summary.md'
workflowFile: '{workflow_path}/workflow.md'

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
partyModeWorkflow: '{project-root}/.bmad/core/workflows/party-mode/workflow.md'
brainstormingWorkflow: '{project-root}/.bmad/core/workflows/brainstorming-session/workflow.md'
---

# Step 4: Review Summary and Completion

## STEP GOAL:

To verify cross-section consistency, generate a comprehensive review summary, and update the document's change log with session details.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- NEVER generate content without user input
- CRITICAL: Read the complete step file before taking any action
- YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:

- You are a document review facilitator
- If you already have been given a name, communication_style and identity, continue to use those while playing this new role
- We engage in collaborative dialogue, not command-response
- You bring summary and reporting expertise, user brings validation authority

### Step-Specific Rules:

- **Run cross-section consistency check FIRST before any statistics**
- **Require >= 90% overall consistency confidence before proceeding to summary**
- Focus on accurate summary of review results
- Calculate confidence changes correctly
- Generate professional change log entry
- Proceed directly to next actions after saving

## EXECUTION PROTOCOLS:

- **Perform cross-section consistency check first**
- **Loop through inconsistencies one-by-one until 90% consistency achieved**
- Calculate all statistics from review-state.json
- Show confidence changes (before vs after)
- Generate change log entry for user approval
- Save document with change log
- Proceed directly to next actions

## CONTEXT BOUNDARIES:

- Document has been reviewed (from step-03)
- review-state.json contains complete review data
- All section statuses and confidence scores available
- Contributor info available for attribution
- Detail documents may exist (e.g., control-points-detail.md, exceptions-detail.md)

## SUMMARY SEQUENCE:

### 1. Cross-Section Consistency Check

**CRITICAL:** This check must complete with >= 90% consistency confidence before proceeding to review statistics.

#### 1a. Scan for Cross-References

Scan the entire document and any associated detail documents for ID references:

**Reference Types to Check:**

| ID Pattern | Source Section | Target Section/Document |
|------------|----------------|-------------------------|
| PS# (e.g., PS-001) | Process Steps | Section 2: Process Steps |
| EXC# (e.g., EXC-001) | Exception Paths | Section 3 / exceptions-detail.md |
| CP# (e.g., CP-001) | Control Points | Section 4 / control-points-detail.md |
| SYS# (e.g., SYS-001) | System Dependencies | Section 5 |
| GAP# (e.g., GAP-001) | Process Gaps | Section 8 |
| PP# (e.g., PP-001) | Pain Points | Section 9 / pain-points-detail.md |

**Check Types:**

1. **Forward References:** ID mentioned in one section → verify it exists in target section
2. **Backward References:** Item in detail doc → verify summary exists in main doc
3. **Bidirectional Links:** Exception references CP# → verify CP references back to exception
4. **Count Consistency:** Main doc says "3 control points" → verify detail doc has 3 items

#### 1b. Build Inconsistency List

For each inconsistency found, record:

```json
{
  "inconsistencies": [
    {
      "id": "INC-001",
      "type": "missing_reference",
      "severity": "high",
      "source": "Section 3: Exception Paths",
      "source_text": "...triggers CP-003...",
      "target": "Section 4: Control Points",
      "issue": "CP-003 referenced but does not exist in control points",
      "suggested_fix": "Add CP-003 to control points or update reference"
    },
    {
      "id": "INC-002",
      "type": "missing_backlink",
      "severity": "medium",
      "source": "control-points-detail.md",
      "source_text": "CP-001: Document Verification",
      "target": "Section 4 summary table",
      "issue": "CP-001 exists in detail but not in main doc summary",
      "suggested_fix": "Add CP-001 row to Section 4 summary table"
    }
  ]
}
```

#### 1c. Calculate Consistency Confidence

Calculate overall consistency confidence:

```
total_references = count of all cross-references found
valid_references = count of references that resolve correctly
consistency_confidence = (valid_references / total_references) * 100
```

**If no cross-references found:** Set consistency_confidence = 100%

#### 1d. Display Consistency Summary

```
---
**Cross-Section Consistency Check**

| Metric | Value |
|--------|-------|
| Total Cross-References | [n] |
| Valid References | [n] |
| Inconsistencies Found | [n] |
| **Consistency Confidence** | [X]% |

Target: 90%
```

#### 1e. Consistency Resolution Loop (if < 90%)

**CRITICAL:** User cannot proceed to review summary until consistency confidence reaches >= 90%. The loop continues until either:
- Consistency reaches >= 90%
- User chooses to skip consistency check (mark as "consistency not verified")

If consistency_confidence < 90%:

```
Consistency: [X]% (requires 90% to proceed)

I found [N] inconsistency(ies) that need resolution.

---
**Inconsistency [1] of [N]:**

| Field | Value |
|-------|-------|
| Type | [missing_reference / missing_backlink / count_mismatch / etc.] |
| Severity | [high / medium / low] |
| Source | [section/document where reference appears] |
| Target | [section/document where it should resolve] |

**Issue:** [description of the inconsistency]

**Source Text:**
> [quoted text containing the reference]

**Suggested Fix:** [AI-generated suggestion]

---

| # | Action |
|---|--------|
| a | Apply suggested fix |
| c | Custom correction - provide your own fix |
| e | Elicitation options (brainstorming, party mode, etc.) |
| s | Skip this inconsistency |
| x | Skip consistency check - proceed without verification |

Select:
```

**Handle response:**

- If 'a' (apply suggested fix):
  - Show before/after preview
  - Get user confirmation (y/n)
  - Apply fix to document and/or detail document
  - Recalculate consistency confidence
  - **If confidence still < 90%:** Continue to next inconsistency
  - **If confidence >= 90%:** Exit loop, proceed to statistics

- If 'c' (custom correction):
  - Collect user's correction
  - Show before/after preview
  - Get user confirmation (y/n)
  - Apply correction
  - Recalculate consistency confidence
  - Continue loop if < 90%

- If 'e' (elicitation):
  - Show elicitation sub-menu:
    ```
    **Resolution Options:**
    - **[A] Advanced Elicitation** — Use structured techniques
    - **[P] Party Mode** — Get multiple AI agent perspectives
    - **[B] Brainstorming** — Creative exploration session
    - **[X] Back** — Return to inconsistency menu
    ```
  - Execute selected elicitation
  - Show proposed resolution
  - Get user approval
  - Apply if approved
  - Recalculate consistency confidence
  - Continue loop if < 90%

- If 's' (skip inconsistency):
  - Mark as "skipped - unresolved"
  - Move to next inconsistency
  - Note: Skipped inconsistencies count against confidence

- If 'x' (skip consistency check):
  - Warn user: "Proceeding without consistency verification. Document may contain cross-reference errors."
  - Mark consistency_check as "skipped"
  - Proceed to statistics

**After all inconsistencies processed and confidence still < 90%:**

```
All inconsistencies reviewed but consistency is still [X]%.

| # | Action |
|---|--------|
| r | Review skipped inconsistencies again |
| e | Elicitation options for bulk resolution |
| x | Proceed anyway (not recommended) |

Select:
```

#### 1f. Consistency Check Complete

When consistency_confidence >= 90%:

```
---
**Consistency Check Passed**

| Metric | Value |
|--------|-------|
| Consistency Confidence | [X]% |
| Inconsistencies Resolved | [n] |
| Inconsistencies Skipped | [n] |

Proceeding to content coherence check...
---
```

Update review-state.json:
```json
{
  "consistency_check": {
    "completed": true,
    "confidence": X,
    "total_references": N,
    "valid_references": N,
    "resolved": N,
    "skipped": N
  }
}
```

### 2. Content Coherence Check

**CRITICAL:** After ID consistency is verified, perform a semantic analysis to detect content that no longer fits together logically.

#### 2a. Reload All Documents

Load the latest version of all documents:
- Main process documentation (as-is-process-documentation.md)
- All detail documents (control-points-detail.md, exceptions-detail.md, pain-points-detail.md, etc.)
- structured-data.json

#### 2b. Semantic Coherence Analysis

Analyze the full document set for content coherence issues:

**Coherence Check Categories:**

| Category | What to Check | Example Issue |
|----------|---------------|---------------|
| **Terminology Drift** | Same concept described with different terms across sections | "approval workflow" in Section 2 vs "authorization process" in Section 4 |
| **Contradictory Statements** | Facts that conflict between sections | Section 2 says "3 approvers required" but Section 4 says "single approval sufficient" |
| **Orphaned Context** | References to content that was edited/removed elsewhere | "As described in the exception handling above..." but that exception was deleted |
| **Temporal Inconsistency** | Timeline/sequence mismatches | Step 3 says "after manager approval" but Step 2 doesn't mention manager approval |
| **Scope Mismatch** | Detail doc has more/fewer items than main doc describes | Main doc says "5 control points" but detail doc lists 7 |
| **Role Inconsistency** | Different roles assigned to same responsibility | Section 2: "HR Manager approves" vs Section 5: "Team Lead approves" |
| **System Dependency Gaps** | Systems mentioned in steps but not in system dependencies | Process step mentions "SAP" but SYS# section doesn't include it |
| **Metric/KPI Misalignment** | KPIs that don't match the process as documented | KPI measures "approval time" but process has no approval step |

#### 2c. Build Coherence Issue List

For each coherence issue found, record:

```json
{
  "coherence_issues": [
    {
      "id": "COH-001",
      "category": "contradictory_statements",
      "severity": "high",
      "locations": [
        {"section": "Section 2: Process Steps", "text": "Requires 3 approvers..."},
        {"section": "Section 4: Control Points", "text": "Single approval sufficient..."}
      ],
      "issue": "Conflicting approval requirements between process steps and control points",
      "impact": "Users may follow incorrect procedure; audit risk",
      "clarification_question": "Which approval requirement is correct: 3 approvers or single approval? Has this changed recently?"
    }
  ]
}
```

#### 2d. Calculate Coherence Confidence

```
total_coherence_checks = count of semantic checks performed
issues_found = count of coherence issues detected
coherence_confidence = 100 - (issues_found * weight_factor)
```

**Weight factors by severity:**
- High severity: -15% each
- Medium severity: -8% each
- Low severity: -3% each

**Target:** >= 85% coherence confidence

#### 2e. Display Coherence Summary

```
---
**Content Coherence Check**

| Metric | Value |
|--------|-------|
| Coherence Checks Performed | [n] |
| Issues Found | [n] (High: [n], Medium: [n], Low: [n]) |
| **Coherence Confidence** | [X]% |

Target: 85%
```

#### 2f. Coherence Resolution Loop (if < 85%)

**CRITICAL:** User should address coherence issues before proceeding. The loop continues until either:
- Coherence reaches >= 85%
- User chooses to skip coherence check (mark as "coherence not verified")

If coherence_confidence < 85%:

```
Coherence: [X]% (target: 85%)

I found [N] content coherence issue(s) that need attention.

---
**Coherence Issue [1] of [N]:**

| Field | Value |
|-------|-------|
| Category | [terminology_drift / contradictory_statements / etc.] |
| Severity | [high / medium / low] |
| Impact | [description of potential impact] |

**Locations:**

**Location 1:** [Section/Document name]
> [quoted text]

**Location 2:** [Section/Document name]
> [quoted text]

**Issue:** [description of the coherence problem]

---

| # | Action |
|---|--------|
| a | AI suggests resolution (show proposed changes) |
| c | Custom correction - provide your own fix |
| q | Add to clarification questions for SME |
| s | Skip this issue |
| x | Skip coherence check - proceed without verification |

Select:
```

**Handle response:**

- If 'a' (AI suggests):
  - Generate proposed resolution for both/all locations
  - Show before/after for each affected location
  - Get user confirmation (y/n)
  - Apply fixes to all affected documents
  - Recalculate coherence confidence
  - Continue loop if < 85%

- If 'c' (custom correction):
  - Ask user which location(s) to update
  - Collect correction(s)
  - Show before/after
  - Apply corrections
  - Recalculate coherence confidence
  - Continue loop if < 85%

- If 'q' (add to clarification questions):
  - Add the auto-generated clarification_question to pending questions list
  - Mark issue as "pending clarification"
  - Move to next issue
  - Questions will be presented in Section 3

- If 's' (skip issue):
  - Mark as "skipped - unresolved"
  - Move to next issue

- If 'x' (skip coherence check):
  - Warn user: "Proceeding without coherence verification. Document may contain logical inconsistencies."
  - Mark coherence_check as "skipped"
  - Proceed to clarification questions

#### 2g. Coherence Check Complete

When coherence_confidence >= 85% (or user skips):

```
---
**Coherence Check Complete**

| Metric | Value |
|--------|-------|
| Coherence Confidence | [X]% |
| Issues Resolved | [n] |
| Issues Skipped | [n] |
| Pending Clarifications | [n] |

Proceeding to clarification questions...
---
```

Update review-state.json:
```json
{
  "coherence_check": {
    "completed": true,
    "confidence": X,
    "issues_found": N,
    "resolved": N,
    "skipped": N,
    "pending_clarifications": N
  }
}
```

### 3. Clarification Questions for SME

**Purpose:** Present any unresolved questions that require human domain expertise to answer.

#### 3a. Compile Clarification Questions

Gather questions from:
1. Coherence issues marked "pending clarification" (from Section 2)
2. AI-generated questions based on document analysis
3. Low-confidence sections that weren't fully resolved in Step 3

**AI-Generated Question Categories:**

| Category | Trigger | Example Question |
|----------|---------|------------------|
| **Missing Context** | Vague or incomplete descriptions | "The document mentions 'standard approval process' - can you describe what this entails?" |
| **Assumed Knowledge** | References to undocumented procedures | "Step 4 says 'follow escalation procedure' - is this documented elsewhere or should we capture it here?" |
| **Edge Cases** | Process paths not covered | "What happens if the manager is unavailable for more than 5 days?" |
| **Outdated Indicators** | Content that may be stale | "This section mentions 'legacy system X' - is this still in use?" |
| **Validation Needs** | Critical facts requiring confirmation | "The 72-hour SLA mentioned - is this still the current requirement?" |

#### 3b. Display Clarification Questions

If there are pending clarification questions:

```
---
**Clarification Questions**

The following questions require your input to ensure document accuracy:

**Question [1] of [N]:**

| Source | [coherence_issue / ai_analysis / low_confidence_section] |
|--------|----------------------------------------------------------|
| Related Section | [Section name] |
| Priority | [high / medium / low] |

**Question:**
[The clarification question text]

**Context:**
> [relevant excerpt from document]

**Why this matters:**
[Explanation of impact if not clarified]

---

| # | Action |
|---|--------|
| a | Answer this question |
| d | Defer - answer later (will be logged) |
| n | Not applicable - remove question |
| e | Elicitation options for complex answer |

Select:
```

**Handle response:**

- If 'a' (answer):
  - Collect user's answer
  - AI incorporates answer into relevant document section(s)
  - Show before/after preview
  - Get confirmation
  - Apply changes
  - Mark question as resolved
  - Move to next question

- If 'd' (defer):
  - Log question in review-state.json as "deferred"
  - Add to "Attention Needed" section of summary
  - Move to next question

- If 'n' (not applicable):
  - Remove question from list
  - Move to next question

- If 'e' (elicitation):
  - Show elicitation sub-menu (Advanced Elicitation, Party Mode, Brainstorming)
  - Execute selected technique with question context
  - Present resulting answer/content
  - Get user validation
  - Apply if approved

#### 3c. Clarification Complete

After all questions processed:

```
---
**Clarification Complete**

| Metric | Value |
|--------|-------|
| Questions Answered | [n] |
| Questions Deferred | [n] |
| Questions Removed | [n] |

Proceeding to review statistics...
---
```

Update review-state.json:
```json
{
  "clarification_questions": {
    "completed": true,
    "total": N,
    "answered": N,
    "deferred": N,
    "removed": N
  }
}
```

### 4. Calculate Review Statistics

From review-state.json, calculate:

```
sections_total = count of sections
sections_approved = count where status = "approved"
sections_corrected = count where status = "corrected"
sections_skipped = count where status = "skipped"
sections_pending = count where status = "pending"
completion_percentage = (approved + corrected) / total * 100

corrections_made = count of corrections tracked
clarifications_answered = count of clarification responses
```

### 3. Calculate Confidence Changes

For each section, compare before vs after:

**Before confidence:** Initial score from step-03 first calculation
**After confidence:** Final score after review/corrections

Determine change indicator:
- Improved: after > before
- Unchanged: after == before
- Decreased: after < before (rare, but possible if content removed)

### 3a. Sync Confidence to structured-data.json

**CRITICAL:** Update the JSON file to match the calculated overall confidence from the markdown review.

```
<action>
// Calculate overall document confidence (average of section confidences)
overall_confidence_numeric = average(all section after_confidence values)

// Map numeric confidence to categorical value for JSON
IF overall_confidence_numeric >= 90:
  json_confidence = "HIGH"
ELSE IF overall_confidence_numeric >= 70:
  json_confidence = "MEDIUM"
ELSE:
  json_confidence = "LOW"

// Load structured-data.json from {current_process_folder}
structured_data = load("{current_process_folder}/structured-data.json")

// Update metadata.confidence if it differs
IF structured_data.metadata.confidence != json_confidence:
  old_value = structured_data.metadata.confidence
  structured_data.metadata.confidence = json_confidence

  // Also update validation section with review details
  structured_data.validation.last_review = {{timestamp}}
  structured_data.validation.reviewer = {contributor_name}
  structured_data.validation.overall_confidence_score = overall_confidence_numeric

  // Save the updated JSON
  save(structured_data, "{current_process_folder}/structured-data.json")

  // Record the sync action
  confidence_sync_result = {
    "synced": true,
    "old_value": old_value,
    "new_value": json_confidence,
    "numeric_score": overall_confidence_numeric
  }
ELSE:
  confidence_sync_result = {
    "synced": false,
    "reason": "Values already match"
  }

Store confidence_sync_result in review-state.json
</action>
```

**Display confidence sync result (if changed):**

```
---
**Confidence Synchronized**

| Source | Value |
|--------|-------|
| Calculated (Markdown) | [overall_confidence_numeric]% |
| Mapped to JSON | [json_confidence] |
| Previous JSON Value | [old_value] |

✅ structured-data.json updated with confidence: [json_confidence]
---
```

### 4. Display Review Summary

```
---
**Review Complete!**
---

**Document:** [filename]
**Reviewer:** [contributor_name] ([contributor_role])
**Date:** [current date]

**Results:**

| Metric | Count |
|--------|-------|
| Approved | [n] sections |
| Corrected | [n] sections |
| Skipped | [n] sections |
| Pending | [n] sections |
| **Total** | [n] sections |
| **Completion** | [x]% |
```

### 5. Show Confidence Changes

```
---
**Confidence Score Changes:**

| Section | Before | After | Change |
|---------|--------|-------|--------|
| [Section 1] | [X]% | [Y]% | [+/-Z%] |
| [Section 2] | [X]% | [Y]% | [+/-Z%] |
...

**Summary:** [n] sections improved, [n] unchanged.
```

### 6. Show Changes Made (if any)

If corrections were made during review:

```
---
**Changes Made During Review:**

**Section [N]: [Title]**
- [description of change 1]
- [description of change 2]

**Section [M]: [Title]**
- [description of change]
...
```

### 7. Show Pending Items (if any)

If sections were skipped or remain pending:

```
---
**Attention Needed:**

| Section | Status | Reason |
|---------|--------|--------|
| [Section X] | Skipped | [reason if captured] |
| [Section Y] | Pending | Not reviewed |
...
```

### 8. Generate Change Log Entry

Prepare change log entry for approval:

```
---
**Change Log Entry (Preview):**

| Date | Contributor | Role | Changes |
|------|-------------|------|---------|
| [date] | [name] | [role] | Reviewed: [n] approved, [n] corrected. [confidence summary]. |
```

Ask user:
```
| # | Action |
|---|--------|
| 1 | Approve and append this change log entry |
| 2 | Edit the change log entry |
| 3 | Skip change log update |

Select (1-3):
```

**If option 1:** Append to document's Change Log section
**If option 2:** Collect edits, show updated, confirm
**If option 3:** Skip (warn that review won't be logged)

### 9. Save Document

After change log decision:
- Save the document with any final updates
- Confirm save: "Document saved."

### 10. Update Review State

Update review-state.json:
```json
{
  "status": "completed",
  "completed_at": "[timestamp]",
  "summary": {
    "approved": N,
    "corrected": N,
    "skipped": N,
    "pending": N,
    "completion_percentage": X
  }
}
```

### 11. Offer Next Actions

```
---
**What would you like to do next?**

| # | Action |
|---|--------|
| 1 | Review pending/skipped sections |
| 2 | Start new review session |
| 3 | Exit workflow |

Select (1-3):
```

**If Option 1:**
- Filter to only pending/skipped sections
- Return to step-03-review-loop with filtered list

**If Option 2:**
- Ask: Create new session for same document or different document?
- If same: Clear review-state.json, return to step-01-init
- If different: Clear session, return to step-01-init

**If Option 3:**
- Display completion message
- End workflow

### 12. Workflow Complete

If user selects exit:

```
---
**Review Workflow Complete**

Document: [filename]
Reviewer: [name]
Completion: [x]%

Thank you for your review. The document has been updated and the change log reflects your contributions.

To resume or start a new review, run *review-draft again.
---
```

---

## CRITICAL STEP COMPLETION NOTE

This is the final step of the workflow. Upon completion:

1. Document is saved with change log entry
2. review-state.json is updated with completion status
3. Optional exports are generated
4. User can exit or loop back for more reviews

No next step file to load - workflow ends here or loops back.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- **Cross-section consistency check performed FIRST**
- **Consistency confidence >= 90% achieved before proceeding to coherence check**
- **Inconsistencies flagged one-by-one with resolution options**
- **Content coherence check performed AFTER consistency check**
- **Coherence confidence >= 85% achieved before proceeding to clarification questions**
- **Coherence issues flagged one-by-one with resolution options (including "add to clarification questions")**
- **Clarification questions compiled from coherence issues, AI analysis, and low-confidence sections**
- **Clarification questions presented one-by-one with answer/defer/remove options**
- **All documents reloaded before coherence check to ensure latest versions analyzed**
- Accurate statistics calculated from review-state.json
- Confidence changes correctly compared (before vs after)
- **Confidence synced to structured-data.json (H/M/L mapped from numeric score)**
- Professional change log entry generated
- Document saved with all updates
- review-state.json marked as completed (including consistency_check, coherence_check, clarification_questions, and confidence_sync_result data)
- User given clear next action options
- Proceeds directly to next actions without export prompt

### SYSTEM FAILURE:

- **Skipping cross-section consistency check**
- **Proceeding to coherence check with consistency confidence < 90% (unless user explicitly skips)**
- **Skipping content coherence check**
- **Proceeding to clarification questions with coherence confidence < 85% (unless user explicitly skips)**
- **Not reloading all documents before coherence check (analyzing stale content)**
- **Not generating clarification questions from coherence issues marked "pending clarification"**
- **Showing all coherence issues at once instead of one-by-one**
- **Showing all clarification questions at once instead of one-by-one**
- **Not checking detail documents (control-points-detail.md, etc.) for consistency and coherence**
- **Not syncing confidence to structured-data.json (leaving JSON and markdown out of sync)**
- Incorrect statistics or confidence calculations
- Not offering change log entry
- Not saving document
- Not updating review-state.json completion status
- Forcing user through unnecessary steps

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
