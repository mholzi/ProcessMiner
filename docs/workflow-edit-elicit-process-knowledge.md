---
title: Workflow Edit - elicit-process-knowledge
workflow_path: .bmad/custom/modules/process-miner/workflows/elicit-process-knowledge
created: 2025-12-04
stepsCompleted: [1, 2, 3]
status: completed
---

# Workflow Edit: elicit-process-knowledge

## Step 1: Analysis

### Workflow Overview

| Attribute | Value |
|-----------|-------|
| **Name** | elicit-process-knowledge |
| **Format** | New standalone (workflow.md + steps/) |
| **Type** | Interactive document workflow |
| **Steps** | 10 files (step-00 through step-09) |
| **Module** | process-miner |

### Purpose

Extract tacit process knowledge from SMEs through progressive elicitation, producing structured documentation with full traceability.

### Structure

| Step | File | Goal |
|------|------|------|
| 0 | step-00-continuation.md | Handle session resumption |
| 1 | step-01-init.md | Session initialization & context gathering |
| 2 | step-02-existing-docs.md | Check for existing documentation |
| 3 | step-03-overview.md | High-level process overview |
| 4 | step-04-process-steps.md | Identify process steps with PS# IDs |
| 5 | step-05-exceptions.md | Capture exceptions with EX# IDs |
| 6 | step-06-pain-points.md | Identify pain points with PP# IDs |
| 7 | step-07-controls.md | Document controls with CP# IDs |
| 8 | step-08-systems.md | Catalog systems with SYS# IDs |
| 9 | step-09-validation.md | Final review and completeness check |

### User's Edit Goal

**Problem:** When SME selects "Rewrite" (R) in step-03-overview.md, they are asked to write text from scratch — this defeats the purpose of AI-assisted elicitation.

**Desired:** Add sub-menu when [R] is selected offering BMAD's full elicitation toolkit:
- [A] Advanced Elicitation
- [P] Party Mode
- [Q] Quick Questions

AI synthesizes responses into redrafted content → SME approves or iterates.

### Initial Findings

1. **Menu Mismatch:** Current UX shows `[Y] Yes, [E] Edit, [R] Rewrite` but `adaptive_approval` protocol uses `(a) Accept, (b) Elicitation, (c) Minor Changes`
2. **Missing Elicitation Path:** "Rewrite" option doesn't leverage advanced-elicitation.xml or party-mode
3. **Scope:** Change primarily affects step-03-overview.md (lines 96-129) and potentially the `adaptive_approval` protocol in protocols.md

### Files to Modify

- `steps/step-03-overview.md` - Add sub-menu logic for Rewrite option
- `protocols/protocols.md` - Potentially update `adaptive_approval` protocol

---

## Step 2: Improvement Discovery

**Goal Confirmed:** Add sub-menu when [R] Rewrite is selected, offering AI-assisted redraft options.

**Scope Analysis:**
- Steps using `adaptive_approval` protocol: step-03, step-04, step-08 → **Needed fix**
- Steps using `capture-item` workflow: step-05, step-06, step-07 → Already had similar pattern

**Decision:** Update `adaptive_approval` protocol once → automatically applies to all affected steps.

---

## Step 3: Implementation

### Change Made

**File:** `protocols/protocols.md` → `adaptive_approval` protocol

**Before:**
```
- (a) Accept
- (b) Elicitation
- (c) Minor Changes
```

**After:**
```
- [Y] Yes, Accept
- [E] Edit (minor corrections)
- [R] Rewrite → Sub-menu:
    - [A] Advanced Elicitation
    - [P] Party Mode
    - [Q] Quick Questions
    - [X] Back
```

### Steps Now Consistent

| Step | Approval Pattern | Sub-menu Available |
|------|-----------------|-------------------|
| step-03-overview | adaptive_approval | ✅ Yes |
| step-04-process-steps | adaptive_approval | ✅ Yes |
| step-05-exceptions | capture-item | ✅ Yes |
| step-06-pain-points | capture-item | ✅ Yes |
| step-07-controls | capture-item | ✅ Yes |
| step-08-systems | adaptive_approval | ✅ Yes |

---

## Summary

Single protocol update ensures consistent AI-assisted rewrite capability across all elicitation steps.
