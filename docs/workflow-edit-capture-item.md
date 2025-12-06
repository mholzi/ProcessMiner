---
stepsCompleted: [1, 2, 3, 4, 5]
status: complete
workflow: capture-item
targetPath: .bmad/custom/modules/process-miner/workflows/capture-item
format: standalone
editGoal: Improve user experience of step-02-enhance display
---

# Workflow Edit: capture-item

## Analysis Summary

### Workflow Overview
- **Name:** Capture Item
- **Type:** Interactive data capture (5 steps)
- **Format:** New standalone with step-file architecture
- **Purpose:** Capture pain points, exceptions, and control points through narrative elicitation

### Edit Focus: User Experience

**Problem:** The current display in step-02-enhance.md (section 2) is too technical:
- Data-dump style table with Status and Req? columns
- Technical completeness metrics (score %, field counts)
- Field-by-field breakdowns that overwhelm the user

**Desired State:** Human-friendly presentation:
1. Show the description/problem statement first and prominently
2. "Current Understanding" section with natural paragraph summary
3. "What We Still Need to Work On" with prioritized open items

### Files to Modify
- `steps/step-02-enhance.md` — Section 2: Display Current State (lines 126-165)

### Analysis Confirmed
User confirmed this analysis matches their intent.

---

## Improvement Goals

### Priority: IMPORTANT (UX Enhancement)

**Goal:** Replace technical data-dump display with human-friendly presentation

### Specific Changes

#### 1. Remove Technical Elements
- Remove the field table with Status/Req? columns
- Remove completeness score and percentage
- Remove count tables (Adequate/Shallow/Missing fields)

#### 2. New Display Structure

**Section A: The Problem** (description first)
- Show `current_item.description` or Problem Description prominently
- This is what users care about most - front and center

**Section B: Current Understanding** (narrative paragraph)
- Weave ALL captured fields into natural prose
- Follow narrative structure: "This affects [steps] with [impact level] impact, occurring [frequency]. The root cause is [root cause]. Ideas for improvement include [improvement ideas]."
- Only include fields that have values (skip empty/missing)

**Section C: What We Still Need to Work On** (bullets with hints)
- List only fields that are missing or shallow
- Include the guidance hints for each (e.g., "Include numbers: time, cost, frequency...")
- Keep it actionable and helpful

#### 3. Keep Unchanged
- Menu options ([C] Continue, [Q] Quick Edit, [X] Cancel)
- Quick Edit flow
- All underlying logic for field evaluation

### User Decisions
| Question | Answer |
|----------|--------|
| Current Understanding content | ALL fields in prose with narrative structure |
| What Still Needs Work format | Bullets WITH guidance hints |
| Completeness score | Remove entirely |
| Menu options | Keep as-is |

---

## Improvement Log

### Change 1: Replaced Technical Display with Human-Friendly Summary

**File:** `steps/step-02-enhance.md`

**What Changed:**
- Renamed section from "Display Current State (Dynamic Field Table)" to "Display Current State (Human-Friendly Summary)"
- Removed technical table with Field/Value/Status/Req? columns
- Removed completeness score and percentage display
- Removed count tables (Adequate/Shallow/Missing)
- Added description display at top
- Added "Current Understanding" narrative paragraph section
- Added "What We Still Need to Work On" with hints
- Updated field hints to include `sme_quotes` and `current_workarounds`
- Updated SUCCESS/FAILURE metrics to reflect new approach

**User Approved:** Yes

### Change 2: Removed SME Quotes Field

**Files:**
- `templates/pain-points-detail.md`
- `workflows/capture-item/workflow.md`
- `workflows/capture-item/steps/step-02-enhance.md`
- `workflows/elicit-process-knowledge/steps/step-06-pain-points.md`

**What Changed:**
- Removed "SME Quotes & Evidence" section from pain points template
- Removed SME Quotes from optional_fields criteria
- Removed sme_quotes from narrative template and hints
- Removed from elicitation workflow sections list

**User Approved:** Yes

### Change 3: Added Amend Functionality to Save Step

**File:** `steps/step-05-save.md`

**What Changed:**
- Added [A] Amend option to preview menu
- Added Amend Flow with [N] Narrative, [F] Field, [B] Back options
- Users can now make last-minute changes after preview before saving

**User Approved:** Yes

---

## Validation Results

All changes validated:
- ✅ File structure intact
- ✅ Step frontmatter complete
- ✅ Menu handling properly implemented
- ✅ Success/Failure metrics updated
- ✅ No broken references

---

## Compliance Check

**Date:** 2025-12-04
**Score:** 100%
**Status:** PASS

All changes comply with BMAD standards.

---

## Completion Summary

### What Was Changed

| # | Change | Files |
|---|--------|-------|
| 1 | Human-friendly display (replaced technical table) | `step-02-enhance.md` |
| 2 | Removed SME Quotes field | 4 files |
| 3 | Added Amend functionality to save step | `step-05-save.md` |

### Impact

- Users now see a clean narrative summary instead of data tables
- Gaps are presented as actionable items with helpful hints
- Users can make last-minute edits before saving

### Next Steps

1. Test the workflow with an existing pain point
2. Gather user feedback on the new display format
3. Iterate if needed
