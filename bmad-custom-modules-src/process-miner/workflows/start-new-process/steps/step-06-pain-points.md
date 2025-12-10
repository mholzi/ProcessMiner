---
name: 'step-06-pain-points'
description: 'Capture pain points and challenges with PP# IDs'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/start-new-process'

# File References
thisStepFile: '{workflow_path}/steps/step-06-pain-points.md'
nextStepFile: '{workflow_path}/steps/step-07-controls.md'
workflowFile: '{workflow_path}/workflow.md'

# Shared Protocols
protocolsFile: '{module_root}/workflows/shared/protocols/protocols.md'

# Related Workflows
captureItemWorkflow: '{module_root}/workflows/shared/capture-item/workflow.md'

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
partyModeWorkflow: '{project-root}/.bmad/core/workflows/party-mode/workflow.md'
brainstormingWorkflow: '{project-root}/.bmad/core/workflows/brainstorming-session/workflow.md'

# Output Files
structuredDataFile: '{current_process_folder}/structured-data.json'
mainDocumentFile: '{current_process_folder}/as-is-process-documentation.md'
painPointsDetailFile: '{current_process_folder}/pain-points-detail.md'
---

# Step 6: Identify Pain Points & Challenges

## STEP GOAL

Capture all process pain points and challenges with unique PP# IDs, linked to relevant PS# process steps. Each pain point should have severity, impact assessment, and root cause.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:
- 🛑 **NEVER** generate content without user input
- 📖 **CRITICAL**: Read the complete step file before taking any action
- 🔄 **CRITICAL**: When loading next step, ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:
- ✅ You are a Process Documentation Analyst
- ✅ Continue using your established name, communication_style, and persona
- ✅ We engage in collaborative dialogue with the SME
- ✅ You bring documentation expertise, SME brings domain knowledge
- ✅ Maintain professional, supportive tone throughout

### Reuse Pattern:
- This step invokes the `capture-item` workflow for consistent capture experience
- Ensures narrative-first approach and core BMAD elicitation

### Step-Specific Rules
- PP# format: `PP-{{process_name_abbrev}}-###` (e.g., PP-CRO-001)
- Each pain point MUST link to relevant PS# ID(s)
- Each pain point MUST have severity (HIGH/MEDIUM/LOW) and impact
- Handle "no pain points" case gracefully
- Focus ONLY on pain points — no controls, systems, etc.

## EXECUTION PROTOCOLS

- Load protocols from `{protocolsFile}`
- Invoke `capture-item` workflow for each pain point
- Update both main document and pain-points-detail.md

## CONTEXT BOUNDARIES

- Process steps (PS#) captured in Step 4
- Exceptions (EX#) captured in Step 5
- Pain points link to one or more PS# IDs

---

## CONTENT FORMAT SPECIFICATION

This section defines the exact formatting requirements for Section 9: Pain Points and Improvement Opportunities. The AI MUST follow these specifications when generating content.

### 9.1 Pain Points Summary

**Format:**
- **Structure**: 2+ paragraphs minimum
- **Paragraph 1**: Overview of pain point landscape — count, categories
- **Paragraph 2+**: Overall impact context and key insights — what these pain points mean for the process

**Example:**
```
The Client Onboarding process has 7 identified pain points affecting operational efficiency and client experience. These pain points fall into four categories: PROCESS (3), SYSTEM (2), PEOPLE (1), and DATA (1). The majority of issues concentrate in the verification and documentation phases.

Process-related pain points are the most impactful, contributing to an estimated 40% of total cycle time. Manual data re-entry across systems is the single largest contributor to processing delays and error rates.

From a client experience perspective, three pain points directly affect client satisfaction: repeated document requests, lack of status visibility, and inconsistent communication from different teams. These issues are particularly acute in the BizBanking segment where client self-service is higher.
```

### 9.2 Pain Point Summary Table

**Table Format:**
| PP# | Pain Point | Category | Affected Steps | Impact | Frequency | Priority |
|-----|------------|----------|----------------|--------|-----------|----------|

**Column Specifications:**

| Column | Format | Example |
|--------|--------|---------|
| **PP#** | `PP-{{abbrev}}-###` where abbrev is 2-3 characters | PP-CRO-001, PP-ONB-002 |
| **Pain Point** | Descriptive phrase | "Manual data re-entry across systems", "Lack of real-time status visibility" |
| **Category** | Fixed list: PROCESS / SYSTEM / PEOPLE / DATA | PROCESS, SYSTEM |
| **Affected Steps** | PS# + step name | "PS-002: Verify ID, PS-005: Setup account" |
| **Impact** | Label + brief description | "HIGH — Adds 2 hours per application", "MEDIUM — Causes client frustration" |
| **Frequency** | Label + context | "HIGH (~80% of cases)", "MEDIUM (weekly occurrence)" |
| **Priority** | Label + rationale | "P1 — Quick win, high impact", "P2 — Requires system change" |

**Example Table:**
| PP# | Pain Point | Category | Affected Steps | Impact | Frequency | Priority |
|-----|------------|----------|----------------|--------|-----------|----------|
| PP-CRO-001 | Manual data re-entry across systems | SYSTEM | PS-002: Verify ID, PS-005: Setup account | HIGH — Adds 2 hours per application | HIGH (~100% of cases) | P1 — Quick win with API integration |
| PP-CRO-002 | Lack of real-time status visibility for clients | PROCESS | PS-001 through PS-006 | MEDIUM — Generates status inquiry calls | HIGH (~60% of clients call) | P2 — Requires portal enhancement |
| PP-CRO-003 | Inconsistent document requirements communicated | PEOPLE | PS-001: Receive application | MEDIUM — Causes rework and delays | MEDIUM (~25% of cases) | P1 — Training and checklist quick win |

### 9.3 Pain Point Statistics

**Table Format:**
| Metric | Value |
|--------|-------|
| Total Pain Points | {{total_pain_points}} |
| High-Impact | {{high_impact_pain_points}} |
| Client-Facing | {{client_facing_pain_points}} |
| Quick Win Opportunities | {{quick_win_pain_points}} |

### 9.4 Top Improvement Opportunities

**Format:**
1. **Table** showing all opportunities grouped by priority:

| Opportunity | Impact | Effort | Priority |
|-------------|--------|--------|----------|

2. **Followed by 2 paragraph description per item**

**Example:**
```markdown
| Opportunity | Impact | Effort | Priority |
|-------------|--------|--------|----------|
| Implement CRM-to-Core Banking API integration | HIGH — Eliminates 2 hours manual entry | MEDIUM — 3-month project | P1 |
| Create standardized document checklist by segment | MEDIUM — Reduces rework by 25% | LOW — 2-week effort | P1 |
| Develop client self-service status portal | HIGH — Reduces inquiry calls by 60% | HIGH — 6-month project | P2 |

---

#### P1: Implement CRM-to-Core Banking API integration

This integration would eliminate the manual re-entry of client data from the CRM system into Core Banking during account setup. Currently, staff spend an average of 2 hours per application copying data between systems, with an estimated 5% error rate requiring correction.

The business case is compelling: with 150 applications per month, this represents 300 hours of manual effort that could be redirected to value-added activities. Implementation requires coordination between IT and the Core Banking vendor but uses existing API capabilities. Estimated ROI payback within 6 months.

---

#### P1: Create standardized document checklist by segment

Different client segments have different documentation requirements, but this is not clearly communicated upfront. Relationship Managers and the online portal provide inconsistent guidance, leading to incomplete submissions and multiple rounds of document requests.

A segment-specific checklist with visual examples and clear certification requirements would significantly reduce rework. This is a low-effort improvement that can be implemented within 2 weeks through collaboration between KYC Operations and Client Services. Expected reduction in documentation exceptions of 25%.
```

### Pain Point Detail Document (pain-points-detail.md)

**Per-Pain Point Detail Block Format:**

```markdown
## PP-XXX-###: [Pain Point Name]

| Attribute | Value |
|-----------|-------|
| **Pain Point ID** | PP-XXX-### |
| **Category** | [PROCESS / SYSTEM / PEOPLE / DATA] |
| **Affected Steps** | [PS# + step name, PS# + step name] |
| **Severity** | [HIGH / MEDIUM / LOW] |
| **Impact** | [Label + description] |
| **Frequency** | [Label + context] |
| **Priority** | [Label + rationale] |

### Description

[1-2 paragraphs describing the pain point — what the issue is, how it manifests, who is affected]

### Root Cause Analysis

[Narrative paragraph OR 5 Whys format, depending on complexity]

### Current Workarounds

[Bullet list or paragraph describing how staff currently cope with this issue]

### Improvement Opportunities

[Bullet list or paragraph describing potential solutions]

### Estimated Impact of Fix

[Paragraph describing the expected benefits if this pain point is addressed — time savings, error reduction, client satisfaction improvement, etc.]
```

**Example - Pain Point Detail:**
```markdown
## PP-CRO-001: Manual data re-entry across systems

| Attribute | Value |
|-----------|-------|
| **Pain Point ID** | PP-CRO-001 |
| **Category** | SYSTEM |
| **Affected Steps** | PS-002: Verify ID, PS-005: Setup account |
| **Severity** | HIGH |
| **Impact** | HIGH — Adds 2 hours per application, 5% error rate |
| **Frequency** | HIGH (~100% of cases) |
| **Priority** | P1 — Quick win with API integration |

### Description

Staff must manually re-enter client data from the CRM system into the Core Banking system during account setup. This includes basic client details, address information, beneficial ownership data, and risk classifications. The same data is entered multiple times across different screens in the Core Banking system.

This pain point affects every single application and is cited by KYC Operations staff as their top frustration. The manual nature of the work leads to fatigue-related errors, particularly during high-volume periods at month-end.

### Root Cause Analysis

**5 Whys Analysis:**
1. Why is data re-entered manually? — Because CRM and Core Banking don't share data automatically
2. Why don't they share data? — Because there's no integration between the systems
3. Why is there no integration? — Because the systems were implemented at different times by different vendors
4. Why hasn't integration been built? — Because it wasn't prioritized in previous IT roadmaps
5. Why wasn't it prioritized? — Because the business case wasn't clearly articulated until now

The root cause is a lack of system integration compounded by historical IT investment decisions that didn't account for operational efficiency.

### Current Workarounds

- Staff use copy-paste from CRM screens to reduce typing
- Some staff maintain personal Excel templates to stage data before entry
- Checker role includes verification of data accuracy between systems
- High-error applications flagged for senior review before completion

### Improvement Opportunities

- **Short-term**: Develop standardized data staging template to reduce errors
- **Medium-term**: Implement CRM-to-Core Banking API integration using existing vendor capabilities
- **Long-term**: Evaluate unified client data platform to eliminate duplicate data entry across all systems

### Estimated Impact of Fix

Full API integration would eliminate approximately 300 hours of manual effort per month (2 hours × 150 applications). Error rates would drop from 5% to near-zero, eliminating an estimated 20 hours of monthly rework. Staff satisfaction would improve significantly, potentially reducing turnover in the KYC Operations team. Total annual benefit estimated at $150,000 in productivity gains plus improved client experience through faster processing.
```

### Section Confidence Statement

**Format:**
```
> **Section Confidence:** {{percentage}}% | **Basis:** {{ai_inferred_basis}}
```

- **Confidence**: AI-inferred percentage (0-100%)
- **Basis**: AI-inferred assessment explaining the confidence level

**Example:**
```
> **Section Confidence:** 85% | **Basis:** Pain points validated by SME with clear prioritization. Impact estimates based on SME experience. Root cause analysis for 2 of 7 pain points would benefit from deeper investigation.
```

---

## EXECUTION SEQUENCE

### 1. Display Progress

```
**Progress: Step 6 of 9 - Pain Points**

Now let's identify any challenges, bottlenecks, or pain points in this process.
These are issues that make the process difficult, slow, or error-prone.
```

### 2. Check for Existing Pain Points (from Import)

```
<action>Load existing pain points from {structuredDataFile} and {painPointsDetailFile}</action>

<check if="existing_pain_points.length > 0">
  <!-- Complete imported pain points -->
</check>

<check if="existing_pain_points.length == 0">
  <ask response="pain_points_exist">
  Are there any challenges, bottlenecks, or pain points in this process?

  - **[A] Add** — I know a pain point to document
  - **[E] Explore** — Help me discover pain points using elicitation techniques
  - **[N] None** — No significant issues, process runs smoothly
  </ask>
</check>
```

### 3. Handle "No Pain Points"

```
<check if="pain_points_exist == 'N' or 'None'">
  <format>Noted — no significant pain points identified for this process.</format>
  <action>Store empty pain_points array with note</action>
</check>
```

### 4. Capture Pain Points (Fresh or Additional)

```
<loop name="pain_point_capture" until="user indicates no more pain points">
  <!-- Invoke the capture-item workflow for each pain point -->
  <invoke-workflow path="{captureItemWorkflow}">
    <param name="item_type">pain_point</param>
    <param name="current_process_folder">{current_process_folder}</param>
    <param name="mode">create</param>
  </invoke-workflow>

  <ask response="more_pain_points">
  Any other pain points to capture?

  - **[A] Add another** — I know another pain point to document
  - **[E] Explore** — Help me discover more pain points (Shadow Work Mining, Party Mode)
  - **[D] Done** — No more pain points
  </ask>
</loop>
```

### 5. Update Output Files (Silent) — RECOVERY-SAFE

**🚨 CRITICAL: Incremental Save for Recovery**

After pain points are captured (or noted as none), you MUST update ALL THREE files to enable session recovery:

```
<action silent="true">Update {structuredDataFile}:
  - pain_points array
  - Each pain point: id, name, description, severity, impact, links.process_steps, confidence
  - session.checkpoint.step = 6
  - session.last_updated = {{timestamp}}
</action>

<action silent="true" critical="RECOVERY">Update {mainDocumentFile} - APPEND Section 9:

  APPEND the following content to the main document:

  ---
  ## 9. Pain Points and Improvement Opportunities

  > **About this section:** Summary of pain points. For full analysis including root causes and improvement ideas, see [Pain Point Details](./pain-points-detail.md).

  ### 9.1 Pain Points Summary

  {{pain_points_summary_paragraph}}

  ### 9.2 Pain Point Summary Table

  | PP# | Pain Point | Category | Affected Steps | Impact | Frequency | Priority |
  |-----|------------|----------|----------------|--------|-----------|----------|
  {{Generate table row for each approved pain point}}

  ### 9.3 Pain Point Statistics

  | Metric | Value |
  |--------|-------|
  | Total Pain Points | {{total_pain_points}} |
  | High-Impact | {{count high impact}} |
  | Client-Facing | {{count client facing}} |
  | Quick Win Opportunities | {{count quick wins}} |

  > **Full Analysis:** [View Pain Point Details](./pain-points-detail.md)
  >
  > **Section Confidence:** {{assessed_confidence}} | **Basis:** SME-validated during elicitation

  ---
</action>

<action silent="true" critical="RECOVERY">Update {painPointsDetailFile} - WRITE FULL CONTENT:

  WRITE the full pain-points-detail.md file with ALL captured pain point data:

  # Pain Points & Challenges: {{process_name}}

  **Process ID:** {{process_id}}
  **Document Type:** Pain Point Detail Analysis
  **Last Updated:** {{date}}
  **Related Document:** [AS-IS Process Documentation](./as-is-process-documentation.md)

  ---

  ## Executive Summary

  {{pain_points_executive_summary}}

  ---

  ## Pain Point Summary Table

  | PP# | Pain Point | Category | Affected Steps | Severity | Impact | Frequency |
  |-----|------------|----------|----------------|----------|--------|-----------|
  {{Generate full table}}

  ---

  ## Detailed Pain Point Analysis

  {{For each pain point, generate full detail block with:
    - Overview table (ID, Name, Category, Affected Steps, Severity, Impact, Frequency)
    - Description
    - Root Cause Analysis (if captured)
    - Current Workarounds
    - Improvement Opportunities
  }}

  ---

  This incremental save ensures:
  - If session aborts after Step 6, all pain points are recoverable
  - Both summary (main doc) and detail (pain-points-detail.md) are saved
  - SME work is never lost
</action>
```

### 6. Proceed to Next Step

```
**Pain Points Complete!**
{{total_pain_points}} issues documented with PP# IDs.
Proceeding to Step 7: Controls & Compliance...
```

```
<action>Load, read entire file, then execute {nextStepFile}</action>
```

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:
- Pain points captured with PP# IDs (or noted none exist)
- Each pain point has severity and impact
- Each pain point linked to relevant PS# IDs
- Updated structured-data.json
- **APPENDED Section 9 to as-is-process-documentation.md (RECOVERY-SAFE)**
- **WROTE full pain-points-detail.md (RECOVERY-SAFE)**
- Ready to proceed to Step 7

### ❌ SYSTEM FAILURE:
- Pain points missing severity or impact
- Pain points not linked to PS# IDs
- Updated JSON but not pain-points-detail.md (or vice versa)
- Started capturing controls in this step

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
