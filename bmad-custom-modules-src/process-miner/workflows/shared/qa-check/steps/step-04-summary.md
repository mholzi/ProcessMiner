---
name: 'step-04-summary'
description: 'Present full QA summary with findings details and fix options - INTERACTIVE'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/shared/qa-check'

# File References
thisStepFile: '{workflow_path}/steps/step-04-summary.md'
workflowFile: '{workflow_path}/workflow.md'

# Output Files
qa_report_output: '{current_process_folder}/qa-report.md'
qa_report_template: '{module_root}/templates/qa-report.md'
structuredDataFile: '{current_process_folder}/structured-data.json'

# Execution Mode
execution_mode: interactive
---

# Step 4: QA Summary & Fix Options (INTERACTIVE)

## STEP GOAL

Present the complete QA review results to the user. Show summary, full details of all findings, and offer fix options. This is the FIRST user interaction since process selection.

## EXECUTION MODE: INTERACTIVE

**This is the only interactive step.** User sees results and can:
- Review all findings
- Apply fixes (auto or manual)
- Generate report
- Update process status

---

## DISPLAY SEQUENCE

### 1. Present Executive Summary

Display:
```
═══════════════════════════════════════════════════════════════════════════════
                         QA REVIEW COMPLETE
═══════════════════════════════════════════════════════════════════════════════

Process: {current_process_name} ({current_process_id})
Reviewer: {contributor_name} ({contributor_role})
Duration: {qa_start_time} → {qa_end_time}

───────────────────────────────────────────────────────────────────────────────
                            ASSESSMENT: {assessment}
───────────────────────────────────────────────────────────────────────────────

{IF assessment == "BLOCKED":}
⛔ BLOCKED - Critical issues must be resolved before approval

{IF assessment == "CONDITIONAL":}
⚠️ CONDITIONAL - High-priority issues should be addressed

{IF assessment == "ACCEPTABLE":}
✅ ACCEPTABLE - Documentation meets quality standards

═══════════════════════════════════════════════════════════════════════════════
```

### 2. Present Findings Summary Table

Display:
```
                           FINDINGS SUMMARY
───────────────────────────────────────────────────────────────────────────────

| Severity     | Count | Description                        |
|--------------|-------|----------------------------------- |
| 🔴 CRITICAL  | {n}   | Must fix before approval           |
| 🟠 HIGH      | {n}   | Should fix soon                    |
| 🟡 MEDIUM    | {n}   | Should fix eventually              |
| 🟢 LOW       | {n}   | Nice to fix                        |
|--------------|-------|----------------------------------- |
| **TOTAL**    | {n}   |                                    |

───────────────────────────────────────────────────────────────────────────────

By Validation Phase:
| Phase                    | Findings |
|--------------------------|----------|
| 1. ID Integrity          | {n}      |
| 2. Cross-Document        | {n}      |
| 3. Completeness          | {n}      |
| 4. Compliance            | {n}      |
| 5. Data Quality          | {n}      |
| Init/Additional          | {n}      |

───────────────────────────────────────────────────────────────────────────────
```

### 3. Present All Findings (Detailed)

Display:
```
═══════════════════════════════════════════════════════════════════════════════
                           DETAILED FINDINGS
═══════════════════════════════════════════════════════════════════════════════
```

#### 3a. CRITICAL Findings (if any)

```
───────────────────────────────────────────────────────────────────────────────
🔴 CRITICAL FINDINGS ({count})
These MUST be fixed before the process can be approved.
───────────────────────────────────────────────────────────────────────────────

{FOR EACH critical finding:}

┌─────────────────────────────────────────────────────────────────────────────┐
│ #{finding.id}: {finding.title}                                              │
├─────────────────────────────────────────────────────────────────────────────┤
│ Severity:    🔴 CRITICAL                                                    │
│ Category:    {finding.category}                                             │
│ Location:    {finding.location}                                             │
├─────────────────────────────────────────────────────────────────────────────┤
│ ISSUE:                                                                      │
│ {finding.description}                                                       │
├─────────────────────────────────────────────────────────────────────────────┤
│ IMPACT:                                                                     │
│ {finding.impact}                                                            │
├─────────────────────────────────────────────────────────────────────────────┤
│ EVIDENCE:                                                                   │
│ {finding.evidence}                                                          │
├─────────────────────────────────────────────────────────────────────────────┤
│ RECOMMENDATION:                                                             │
│ {finding.recommendation}                                                    │
└─────────────────────────────────────────────────────────────────────────────┘

```

#### 3b. HIGH Findings (if any)

```
───────────────────────────────────────────────────────────────────────────────
🟠 HIGH FINDINGS ({count})
These should be fixed before production use.
───────────────────────────────────────────────────────────────────────────────

{FOR EACH high finding - same box format as CRITICAL}
```

#### 3c. MEDIUM Findings (if any)

```
───────────────────────────────────────────────────────────────────────────────
🟡 MEDIUM FINDINGS ({count})
These should be addressed when possible.
───────────────────────────────────────────────────────────────────────────────

{FOR EACH medium finding - condensed format:}

#{finding.id}: {finding.title}
  Location: {finding.location}
  Issue: {finding.description}
  Fix: {finding.recommendation}

```

#### 3d. LOW Findings (if any)

```
───────────────────────────────────────────────────────────────────────────────
🟢 LOW FINDINGS ({count})
Suggestions for improvement.
───────────────────────────────────────────────────────────────────────────────

{FOR EACH low finding - list format:}

• #{finding.id}: {finding.title} ({finding.location})

```

### 4. Present Fix Options Menu

Display:
```
═══════════════════════════════════════════════════════════════════════════════
                              FIX OPTIONS
═══════════════════════════════════════════════════════════════════════════════

What would you like to do?

[1] 🔧 Auto-Fix Available Issues
    Automatically fix issues that have safe, deterministic fixes.
    ({auto_fixable_count} issues can be auto-fixed)

[2] 📋 Review & Fix Individual Findings
    Go through each finding one by one with fix options.

[3] 📝 Add All to Backlog
    Mark all findings as acknowledged and add to process backlog.

[4] 📄 Generate QA Report Only
    Save the QA report without making any fixes.

[5] ❌ Exit Without Saving
    Discard results and exit.

───────────────────────────────────────────────────────────────────────────────
Enter your choice (1-5):
```

### 5. Handle User Selection

#### Option 1: Auto-Fix Available Issues

```
<action>
Identify auto-fixable issues:
- Missing metadata fields → Can auto-populate with defaults
- Invalid date formats → Can auto-correct
- Missing schema fields → Can add empty structure
- Some ID format issues → Can auto-correct

FOR EACH auto-fixable finding:
  Display:
  "Auto-fixing: {finding.title}"
  "  Before: {before_value}"
  "  After: {after_value}"

  Apply fix to appropriate file.
  Mark finding as FIXED.

After all fixes:
  Display:
  "✅ Auto-fixed {count} issues"
  "Remaining issues: {remaining_count}"

  Return to Fix Options Menu with updated counts.
</action>
```

#### Option 2: Review & Fix Individual Findings

```
<action>
FOR EACH finding (starting with CRITICAL):
  Display finding details (box format)

  Display:
  "Options for this finding:"
  "[A] Auto-fix (if available)"
  "[M] Mark for manual fix"
  "[B] Add to backlog"
  "[S] Skip"
  "[N] Next (don't change status)"

  Wait for user input.

  Based on selection:
  - A: Apply auto-fix if available, mark FIXED
  - M: Mark as MANUAL_FIX_REQUIRED
  - B: Mark as BACKLOGGED
  - S: Mark as SKIPPED
  - N: Leave as-is, move to next

After all findings reviewed:
  Display summary of decisions.
  Return to Fix Options Menu.
</action>
```

#### Option 3: Add All to Backlog

```
<action>
FOR EACH finding:
  Mark as BACKLOGGED

Display:
"✅ All {count} findings added to backlog"
"These will be tracked for future resolution."

Proceed to report generation.
</action>
```

#### Option 4: Generate QA Report Only

```
<action>
Proceed directly to report generation.
</action>
```

#### Option 5: Exit Without Saving

```
<action>
Display:
"⚠️ Are you sure? QA results will be lost. (Y/N)"

IF Y:
  Display: "QA review discarded. Returning to menu."
  Exit workflow.

IF N:
  Return to Fix Options Menu.
</action>
```

### 6. Generate QA Report

```
<action>
Load {qa_report_template}

Populate template with:
- All session info
- All findings with their final status (FIXED, BACKLOGGED, SKIPPED, OPEN)
- Summary statistics
- Assessment
- Recommendations based on assessment

Write to {qa_report_output}

Display:
"✅ QA Report saved to:"
"{qa_report_output}"
</action>
```

### 7. Update Process Status

```
<action>
Update {structuredDataFile} validation section:

{
  "validation": {
    "status": "{assessment}",
    "last_review": "{timestamp}",
    "reviewer": "{contributor_name}",
    "findings_summary": {
      "critical": {remaining_critical},
      "high": {remaining_high},
      "medium": {remaining_medium},
      "low": {remaining_low},
      "fixed": {fixed_count},
      "backlogged": {backlogged_count}
    },
    "qa_report": "{qa_report_output}"
  }
}

Save file.

Display:
"✅ Process status updated in structured-data.json"
</action>
```

### 8. Present Final Summary

Display:
```
═══════════════════════════════════════════════════════════════════════════════
                         QA REVIEW FINALIZED
═══════════════════════════════════════════════════════════════════════════════

Process: {current_process_name} ({current_process_id})
Final Assessment: {assessment}

───────────────────────────────────────────────────────────────────────────────

Findings Disposition:
| Status     | Count |
|------------|-------|
| Fixed      | {n}   |
| Backlogged | {n}   |
| Skipped    | {n}   |
| Open       | {n}   |

───────────────────────────────────────────────────────────────────────────────

Files Updated:
✅ {qa_report_output}
✅ {structuredDataFile}

───────────────────────────────────────────────────────────────────────────────

{IF assessment == "BLOCKED":}
⛔ NEXT STEPS:
1. Address the {critical_count} CRITICAL findings
2. Run QA Check again after fixes
3. Obtain approval before production use

{IF assessment == "CONDITIONAL":}
⚠️ NEXT STEPS:
1. Process may be used with documented exceptions
2. Address HIGH findings within reasonable timeframe
3. Schedule follow-up review

{IF assessment == "ACCEPTABLE":}
✅ NEXT STEPS:
1. Process documentation is approved for use
2. Address LOW/MEDIUM findings during next update cycle
3. Recommended: Quarterly re-review

═══════════════════════════════════════════════════════════════════════════════

Thank you for completing the QA review, {contributor_name}.

What would you like to do next?

[1] View full QA report
[2] Run another QA check (different process)
[3] Return to agent menu
[4] Exit

───────────────────────────────────────────────────────────────────────────────
```

### 9. Handle Final Navigation

```
<action>
Based on user selection:

IF 1: Display full content of {qa_report_output}
      Then return to this menu.

IF 2: Restart workflow from process selection.

IF 3: Return control to parent agent.

IF 4: Display goodbye message and end session.
</action>
```

---

## SUCCESS CRITERIA

- ✅ Full summary displayed to user
- ✅ All findings shown with details
- ✅ User given fix options
- ✅ Fixes applied as requested
- ✅ QA report generated and saved
- ✅ Process status updated
- ✅ Clear next steps provided

---

## NOTES

This is the ONLY step where user sees output and provides input. All previous steps ran silently to optimize the user experience - they don't have to wait through each phase, they just see the final comprehensive results.
