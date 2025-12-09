---
name: 'step-01b-continue'
description: 'Detect material changes between source documents and existing management summary'

# Path Definitions
workflow_path: '{module_root}/workflows/generate-outputs'
module_root: '{project-root}/bmad-custom-modules-src/process-miner'

# File References
thisStepFile: '{workflow_path}/steps/step-01b-continue.md'
nextStepFile: '{workflow_path}/steps/step-02-extract.md'
reviewStepFile: '{workflow_path}/steps/step-04-review.md'
workflowFile: '{workflow_path}/workflow.md'

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.md'
partyModeWorkflow: '{project-root}/.bmad/core/workflows/party-mode/workflow.md'
---

# Step 1b: Material Change Detection

## STEP GOAL:

To analyze the existing management summary against current source documents, identify material changes that require summary updates, and present the user with clear options for how to proceed.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step, ensure entire file is read first
- 📋 YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:

- ✅ You are a document synthesizer and executive communication specialist
- ✅ Continue using the calling agent's communication style if available
- ✅ We engage in collaborative dialogue, not command-response
- ✅ You bring expertise in change detection and impact analysis

### Step-Specific Rules:

- 🎯 Focus ONLY on detecting and presenting changes
- 🚫 FORBIDDEN to update the summary in this step
- 🚫 FORBIDDEN to make decisions for the user about what to update
- 💬 Present changes clearly with impact assessment
- 📊 Use quantitative comparison where possible

## EXECUTION PROTOCOLS:

- 🎯 Load and analyze both existing summary and source documents
- 🎯 Compare key metrics and content sections
- 🎯 Categorize changes by materiality
- 🎯 Present clear summary of changes
- 💾 Store change analysis for downstream steps
- 🚫 FORBIDDEN to proceed without user decision

## CONTEXT BOUNDARIES:

- Session variables from step-01 are available
- `existing_summary_path` contains path to current summary
- `source_document_path` contains path to source document
- Focus on detecting differences, not on updating content

---

## CHANGE DETECTION SEQUENCE:

### 1. Load Documents

Load both documents completely:

**Existing Management Summary:**
- Path: `{existing_summary_path}`
- Extract: All sections, metrics, dates, version

**Current Source Document:**
- Path: `{source_document_path}`
- Extract: All sections, metrics, key data points

Also load companion detail documents if they exist:
- exceptions-detail.md
- pain-points-detail.md
- control-points-detail.md
- friction-points-detail.md
- client-touchpoints-detail.md

### 2. Extract Comparison Points

Based on `current_agent_id`, extract the relevant comparison metrics:

#### For process-documentation-analyst:
| Metric | From Summary | From Source |
|--------|--------------|-------------|
| Total Process Steps | | |
| Total Exceptions | | |
| Total Pain Points | | |
| Total Control Points | | |
| Total Systems | | |
| Overall Confidence | | |
| Top 5 Pain Points | | |
| Strategic Priorities | | |

#### For client-journey-analyst:
| Metric | From Summary | From Source |
|--------|--------------|-------------|
| Client Effort Score (CES) | | |
| Total Touchpoints | | |
| Total Friction Points | | |
| Moments That Matter | | |
| Enhancement Ideas | | |
| Top 5 Friction Points | | |
| Strategic Priorities | | |

#### For control-analyst:
| Metric | From Summary | From Source |
|--------|--------------|-------------|
| Total Control Points | | |
| Regulatory Controls | | |
| Compliance Coverage % | | |
| Open Audit Findings | | |
| Control Effectiveness | | |
| Critical Gaps | | |
| Strategic Priorities | | |

#### For innovation-analyst:
| Metric | From Summary | From Source |
|--------|--------------|-------------|
| Total Innovation Ideas | | |
| Market Trends Analyzed | | |
| MUST HAVE Count | | |
| Avg Feasibility Score | | |
| Quick Wins Identified | | |
| Top Priorities | | |
| Strategic Priorities | | |

### 3. Categorize Changes

Analyze differences and categorize:

#### 🔴 CRITICAL Changes (Require Immediate Update)
- Key metrics changed by >20%
- New high-priority items added
- Removed items that were in priorities
- Changed strategic recommendations
- Compliance gaps changed

#### 🟡 MATERIAL Changes (Should Update)
- Metrics changed by 10-20%
- New items added (not high priority)
- Moderate changes to analysis sections
- Updated benchmarks or targets

#### 🟢 MINOR Changes (Optional Update)
- Metrics changed by <10%
- Cosmetic or formatting changes
- Additional detail added (no impact on conclusions)
- Date/version updates only

#### ⚪ NO Changes
- Source document unchanged since summary created
- All metrics match

### 4. Generate Change Report

Create a structured change report:

```
═══════════════════════════════════════════════════════════
📊 MANAGEMENT SUMMARY CHANGE ANALYSIS
═══════════════════════════════════════════════════════════

Process: {current_process_name}
Summary Type: {current_agent_id}
Summary Last Updated: {existing_summary_modified}
Source Last Updated: {source_document_modified}

───────────────────────────────────────────────────────────
CHANGE SUMMARY
───────────────────────────────────────────────────────────

🔴 CRITICAL CHANGES: {critical_count}
🟡 MATERIAL CHANGES: {material_count}
🟢 MINOR CHANGES: {minor_count}

───────────────────────────────────────────────────────────
DETAILED CHANGES
───────────────────────────────────────────────────────────

[List each change with category, before/after values, and impact]

───────────────────────────────────────────────────────────
RECOMMENDATION
───────────────────────────────────────────────────────────

[Based on change analysis, provide recommendation]
```

### 5. Present Analysis to User

Display the change report and explain:

**If NO changes detected:**
"✅ Your management summary is current. No material changes detected between the source documentation and the existing summary.

The summary was last updated on {existing_summary_modified}.

Would you like to regenerate anyway for a fresh perspective?"

**If CRITICAL or MATERIAL changes detected:**
"⚠️ Material changes detected in the source documentation that are not reflected in the current management summary.

{change_report}

These changes should be incorporated to ensure the management summary accurately represents the current state."

**If only MINOR changes detected:**
"ℹ️ Minor changes detected. The existing summary is substantially current, but some details have changed.

{change_report}

You may choose to update or keep the current version."

---

### 6. Present MENU OPTIONS

Display: "**Select an Option:**
[U] Update Summary - Incorporate detected changes
[R] Regenerate - Create fresh summary from scratch
[K] Keep Current - No changes needed
[V] View Full Comparison - See detailed side-by-side
[A] Advanced Elicitation
[P] Party Mode"

#### Menu Handling Logic:

- IF U: Set `update_mode` = 'incremental', store `changes_to_apply`, load, read entire file, then execute `{nextStepFile}`
- IF R: Set `update_mode` = 'full', load, read entire file, then execute `{nextStepFile}`
- IF K: Display "Summary kept as-is. No changes made." → **END WORKFLOW**
- IF V: Display detailed comparison table, then redisplay menu
- IF A: Execute `{advancedElicitationTask}`, then redisplay menu
- IF P: Execute `{partyModeWorkflow}`, then redisplay menu
- IF Any other comments or queries: help user respond then [Redisplay Menu Options](#6-present-menu-options)

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'U' or 'R'
- After other menu items execution, return to this menu
- User can chat or ask questions - always respond and then redisplay menu

---

## SESSION VARIABLES SET BY THIS STEP

| Variable | Description |
|----------|-------------|
| `changes_detected` | Boolean - any changes found |
| `critical_changes` | List of critical changes |
| `material_changes` | List of material changes |
| `minor_changes` | List of minor changes |
| `change_report` | Full change report text |
| `update_mode` | 'incremental' or 'full' or null |
| `changes_to_apply` | (if incremental) Specific changes to incorporate |

---

## CRITICAL STEP COMPLETION NOTE

This step has THREE possible exits:

1. **User selects [U] Update:** Set `update_mode` = 'incremental', load, read entire file, then execute `{nextStepFile}` to extract data with focus on changes
2. **User selects [R] Regenerate:** Set `update_mode` = 'full', load, read entire file, then execute `{nextStepFile}` to extract all data fresh
3. **User selects [K] Keep:** Display confirmation, **END WORKFLOW** gracefully

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Both documents loaded and analyzed
- Changes correctly categorized
- Clear change report presented
- User given meaningful options
- Correct routing based on user choice
- Session variables set for downstream steps

### ❌ SYSTEM FAILURE:

- Proceeding without loading both documents
- Missing changes in analysis
- Incorrectly categorizing change severity
- Not presenting all options to user
- Proceeding without user decision
- Not setting update_mode correctly

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
