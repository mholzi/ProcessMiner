---
name: 'step-08-regulatory-change'
description: 'Assess impact of upcoming regulatory changes'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/control-compliance-analysis'

# File References
thisStepFile: '{workflow_path}/steps/step-08-regulatory-change.md'
nextStepFile: '{workflow_path}/steps/step-09-audit-findings.md'
workflowFile: '{workflow_path}/workflow.md'

# Output Files
complianceAssessmentFile: '{current_process_folder}/compliance-control-assessment.md'
---

# Step 8: Regulatory Change Impact

## STEP GOAL

Identify upcoming regulatory changes and assess their impact on the process. Assign RCI# IDs. This corresponds to **Section 7** of the compliance-control-assessment template. Critical for ensuring TO-BE designs address emerging regulations, not just current state.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:
- **NEVER** generate content without user input
- **CRITICAL**: Read the complete step file before taking any action
- YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:
- You are a Control Analyst
- Regulatory change awareness - TO-BE must address emerging regulations, not just current state
- Direct about upcoming impacts - no sugar-coating

### Step-Specific Rules:
- Each regulatory change gets RCI# ID: RCI-{process_abbreviation}-###
- MUST link to REG# regulations affected
- Assess impact and action required
- **FORBIDDEN** to start audit findings capture in this step (that's Step 9)

---

## CONTENT FORMAT SPECIFICATION

This step produces **Section 7: Regulatory Change Impact** of the compliance-control-assessment template.

### Section 7: Regulatory Change Impact
**Format:** Narrative intro + table + per-change detail blocks + horizon scanning

**Structure:**
1. **Narrative Introduction** (2-3 paragraphs):
   - Overview of the regulatory change landscape
   - Why tracking regulatory changes matters for this process
   - Summary of upcoming impacts for non-specialists

2. **Regulatory Change Summary Table:**
   | RCI# | Regulation (REG#) | Change Description | Effective Date | Impact Level | Status |
   |------|-------------------|-------------------|----------------|--------------|--------|

3. **Per-Change Detail Blocks** (for High and Medium impact changes):
   Each block includes 1-2 paragraphs covering:
   - What is changing and why
   - How it affects this process specifically
   - Which controls (CP#) will need modification
   - Actions required to achieve compliance
   - Current implementation status

4. **Horizon Scanning Narrative** (1-2 paragraphs):
   - Regulations on the horizon that may affect this process
   - Emerging regulatory themes to watch
   - Implications for TO-BE transformation design

### Writing Guidelines for Section 7:
- Explain regulatory changes in plain language, not legal jargon
- Focus on practical implications for the process
- Be specific about what actions are required
- Connect changes to existing controls that will be affected
- Emphasize the importance for TO-BE design consideration

---

## EXECUTION SEQUENCE

### 1. Display Progress and Context

```
**Progress: Step 8 of 10 - Regulatory Change Impact**

Any transformation must address not just current regulations, but upcoming changes too.

Let's identify regulatory changes that will affect this process.
```

### 2. Upcoming Regulatory Changes

```
<ask response="regulatory_changes_known">
Are you aware of any upcoming regulatory changes that will affect this process?

- [ ] Yes - I know of specific changes
- [ ] Possibly - I've heard of some but not sure of impact
- [ ] No - not aware of any
</ask>

<check if="regulatory_changes_known != 'No'">

  <loop name="regulatory_change_capture" until="user says done">

    <ask response="rci.regulation">
    Which regulation is changing? (Enter REG# or new regulation name)
    </ask>

    <format>
    **Regulatory Change** → Assigning ID: RCI-{process_abbreviation}-{{next_id_padded}}
    </format>

    <ask response="rci.change_description">
    What is the change?
    </ask>

    <ask response="rci.effective_date">
    When does/did it take effect?
    </ask>

    <ask response="rci.impact_level">
    What is the impact on this process?
    - [ ] High - Major process/control changes required
    - [ ] Medium - Some adjustments needed
    - [ ] Low - Minor updates
    - [ ] None - No impact on this process
    </ask>

    <ask response="rci.action_required">
    What action is required to comply?
    </ask>

    <ask response="rci.affected_controls">
    Which controls (CP#) will be affected?
    </ask>

    <ask response="rci.status">
    What is the implementation status?
    - [ ] Not started
    - [ ] In progress
    - [ ] Completed
    </ask>

  </loop>

</check>
```

### 3. Horizon Scanning

```
<ask response="horizon_items">
Are there any regulations "on the horizon" that may affect this process in the future?
(Even if not yet finalized)
</ask>
```

### 4. Update Output File

```
<action silent="true">
Update {complianceAssessmentFile} Section 7 (Regulatory Change Impact):

Build table:
| RCI# | Regulation | Change Description | Effective Date | Impact | Action Required |

Section Confidence: {{section_7_confidence}}
</action>
```

### 5. Proceed to Next Step

Display:
```
**Progress: Step 8 of 11 - Regulatory Change Assessment Complete**

Now let's capture any open audit findings that affect this process.
```

```
<action>Load, read entire file, then execute {nextStepFile}</action>
```

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:
- Upcoming regulatory changes identified with RCI# IDs
- Impact assessed for each
- Actions required documented
- Output file updated

**Master Rule:** Skipping steps is FORBIDDEN and constitutes SYSTEM FAILURE.
