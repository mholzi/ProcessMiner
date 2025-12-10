---
name: 'step-05-exceptions'
description: 'Capture process exceptions and variations with EX# IDs'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/start-new-process'

# File References
thisStepFile: '{workflow_path}/steps/step-05-exceptions.md'
nextStepFile: '{workflow_path}/steps/step-06-pain-points.md'
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
exceptionsDetailFile: '{current_process_folder}/exceptions-detail.md'
---

# Step 5: Identify Process Exceptions & Variations

## STEP GOAL

Capture all process exceptions and variations with unique EX# IDs, linked to relevant PS# process steps. Each exception should have trigger, handling procedure, and frequency.

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
- EX# format: `EX-{{process_name_abbrev}}-###` (e.g., EX-CRO-001)
- Each exception MUST link to relevant PS# ID(s)
- Handle "no exceptions" case gracefully
- Focus ONLY on exceptions — no pain points, controls, etc.

## EXECUTION PROTOCOLS

- Load protocols from `{protocolsFile}`
- Invoke `capture-item` workflow for each exception
- Update both main document and exceptions-detail.md

## CONTEXT BOUNDARIES

- Process steps (PS#) captured in Step 4
- Exceptions link to one or more PS# IDs
- `documents_uploaded` flag may influence initial draft

---

## CONTENT FORMAT SPECIFICATION

This section defines the exact formatting requirements for Section 3: Exception Paths and Variations. The AI MUST follow these specifications when generating content.

### 3.1 Exception Summary

**Format:**
- **Structure**: 2 paragraphs minimum
- **Paragraph 1**: Overview of exception landscape — count, general categories
- **Paragraph 2**: Impact context and key insights — what these exceptions mean for the process

**Example:**
```
The Client Onboarding process has identified 5 exception paths that deviate from the standard flow. These exceptions fall into three categories: documentation-related (2), system-related (1), and compliance-related (2). The majority of exceptions occur during the verification phase of the process.

Documentation exceptions have the highest frequency, affecting approximately 30% of all applications, and are the primary driver of processing delays. Compliance-related exceptions, while less frequent, carry higher impact due to regulatory implications and require senior oversight for resolution.
```

### 3.2 Exception Summary Table

**Table Format:**
| EX# | Exception | Trigger | Affected Steps | Frequency | Impact |
|-----|-----------|---------|----------------|-----------|--------|

**Column Specifications:**

| Column | Format | Example |
|--------|--------|---------|
| **EX#** | `EX-{{abbrev}}-###` where abbrev is 2-3 characters | EX-CRO-001, EX-ONB-002 |
| **Exception** | Descriptive phrase | "Incomplete client documentation", "System timeout during verification" |
| **Trigger** | Brief condition statement | "Missing KYC documents", "AML system unavailable" |
| **Affected Steps** | PS# + step name | "PS-002: Verify ID, PS-003: Check completeness" |
| **Frequency** | Label + context | "HIGH (~30% of cases)", "MEDIUM (~10% of cases)", "LOW (rare)" |
| **Impact** | Label + brief description | "HIGH — Delays onboarding by 2-3 days", "MEDIUM — Requires manual workaround" |

**Example Table:**
| EX# | Exception | Trigger | Affected Steps | Frequency | Impact |
|-----|-----------|---------|----------------|-----------|--------|
| EX-CRO-001 | Incomplete client documentation | Client fails to provide required KYC documents | PS-002: Verify ID, PS-003: Check completeness | HIGH (~30% of cases) | MEDIUM — Delays processing by 1-2 days |
| EX-CRO-002 | Failed sanctions screening | Client or beneficial owner flagged by AML system | PS-002: Verify ID | LOW (2-3% of cases) | HIGH — Requires compliance escalation and senior review |

### 3.3 Exception Statistics

**Table Format:**
| Metric | Value |
|--------|-------|
| Total Exceptions | {{total_exceptions}} |
| High-Impact Exceptions | {{high_impact_exceptions}} |
| Frequently Occurring | {{frequent_exceptions}} |

### Exception Detail Document (exceptions-detail.md)

**Per-Exception Detail Block Format:**

```markdown
## EX-XXX-###: [Exception Name]

| Attribute | Value |
|-----------|-------|
| **Exception ID** | EX-XXX-### |
| **Category** | [Documentation / System / Compliance / Process] |
| **Affected Steps** | [PS# + step name, PS# + step name] |
| **Frequency** | [Label + context] |
| **Impact** | [Label + description] |
| **Handling Owner** | [Business Unit / Role] |

### Description

[1-2 paragraphs describing the exception — what happens, when it occurs, who is affected]

### Trigger Conditions

[Paragraph or bullet list describing specific conditions that cause this exception]

### Current Handling Procedure

[Narrative paragraph OR numbered steps, depending on complexity]

### Root Cause Analysis

[Paragraph analyzing why this exception occurs — systemic issues, process gaps, external factors]

### Improvement Opportunities

[Bullet list or paragraph describing potential improvements to reduce frequency or impact]
```

**Example - Exception Detail:**
```markdown
## EX-CRO-001: Incomplete client documentation

| Attribute | Value |
|-----------|-------|
| **Exception ID** | EX-CRO-001 |
| **Category** | Documentation |
| **Affected Steps** | PS-002: Verify ID, PS-003: Check completeness |
| **Frequency** | HIGH (~30% of cases) |
| **Impact** | MEDIUM — Delays processing by 1-2 days |
| **Handling Owner** | KYC Ops / Maker |

### Description

This exception occurs when a client application cannot proceed through verification due to missing or incomplete documentation. Common missing items include certified copies of identification, proof of address dated within 3 months, and beneficial ownership declarations for corporate clients.

The exception is most prevalent in the BizBanking segment where clients self-submit applications without relationship manager guidance. It results in the application being placed on hold while the client is contacted for additional documentation.

### Trigger Conditions

- Client submits application without all required KYC documents
- Documents provided are expired, illegible, or do not meet certification requirements
- Corporate structure documentation is incomplete or missing beneficial owner information

### Current Handling Procedure

1. KYC Maker identifies missing documentation during verification (PS-002)
2. Maker updates case status to "Pending Documentation" in CRM
3. Automated email sent to client listing required documents
4. Case placed in 5-day follow-up queue
5. If documents received, case returns to verification queue
6. If no response after 5 days, Relationship Manager contacted for intervention

### Root Cause Analysis

The primary root cause is insufficient upfront guidance to clients on documentation requirements. The online application portal lists requirements but does not prevent submission of incomplete applications. Additionally, document requirements vary by client type and segment, creating confusion for clients unfamiliar with the process.

### Improvement Opportunities

- Implement mandatory document upload checks in the online portal before application submission
- Create segment-specific document checklists with visual examples
- Add real-time document validation to flag issues before submission
- Consider document collection service for LargeCap segment to reduce client burden
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
> **Section Confidence:** 80% | **Basis:** Core exceptions identified and validated by SME. Frequency estimates based on SME experience, not system data. Root causes partially explored — may benefit from deeper analysis.
```

---

## EXECUTION SEQUENCE

### 1. Display Progress

```
**Progress: Step 5 of 9 - Process Exceptions**

Now let's capture any exceptions or variations from the standard flow.
These are alternative paths that happen when something unusual occurs.
```

### 2. Check for Existing Exceptions (from Import)

```
<action>Load existing exceptions from {structuredDataFile} and {exceptionsDetailFile}</action>

<check if="existing_exceptions.length > 0">
  <!-- Complete imported exceptions -->
</check>

<check if="existing_exceptions.length == 0">
  <ask response="exceptions_exist">
  Does this process have exception paths or variations from the standard flow?

  - **[A] Add** — I know an exception to document
  - **[E] Explore** — Help me discover exceptions using elicitation techniques
  - **[N] None** — Mostly standard flow, rare exceptions only
  </ask>
</check>
```

### 3. Handle "No Exceptions"

```
<check if="exceptions_exist == 'N' or 'None'">
  <format>Noted — minimal exception handling, primarily standard flow.</format>
  <action>Store empty process_exceptions array with note</action>
</check>
```

### 4. Capture Exceptions (Fresh or Additional)

```
<loop name="exception_capture" until="user indicates no more exceptions">
  <!-- Invoke the capture-item workflow for each exception -->
  <invoke-workflow path="{captureItemWorkflow}">
    <param name="item_type">exception</param>
    <param name="current_process_folder">{current_process_folder}</param>
    <param name="mode">create</param>
  </invoke-workflow>

  <ask response="more_exceptions">
  Any other exceptions to capture?

  - **[A] Add another** — I know another exception to document
  - **[E] Explore** — Help me discover more exceptions
  - **[D] Done** — No more exceptions
  </ask>
</loop>
```

### 5. Update Output Files (Silent) — RECOVERY-SAFE

**🚨 CRITICAL: Incremental Save for Recovery**

After exceptions are captured (or noted as none), you MUST update ALL THREE files to enable session recovery:

```
<action silent="true">Update {structuredDataFile}:
  - process_exceptions array
  - Each exception: id, name, description, frequency, handling, links.process_steps, confidence
  - session.checkpoint.step = 5
  - session.last_updated = {{timestamp}}
</action>

<action silent="true" critical="RECOVERY">Update {mainDocumentFile} - APPEND Section 3:

  APPEND the following content to the main document:

  ---
  ## 3. Exception Paths and Variations

  > **About this section:** Summary of exceptions. For full details including root cause analysis and handling procedures, see [Exception Details](./exceptions-detail.md).

  ### 3.1 Exception Summary

  {{exceptions_summary_paragraph}}

  ### 3.2 Exception Summary Table

  | EX# | Exception | Trigger | Affected Steps | Frequency | Impact |
  |-----|-----------|---------|----------------|-----------|--------|
  {{Generate table row for each approved exception}}

  ### 3.3 Exception Statistics

  | Metric | Value |
  |--------|-------|
  | Total Exceptions | {{total_exceptions}} |
  | High-Impact Exceptions | {{count high impact}} |
  | Frequently Occurring | {{count frequent}} |

  > **Full Analysis:** [View Exception Details](./exceptions-detail.md)
  >
  > **Section Confidence:** {{assessed_confidence}} | **Basis:** SME-validated during elicitation

  ---
</action>

<action silent="true" critical="RECOVERY">Update {exceptionsDetailFile} - WRITE FULL CONTENT:

  WRITE the full exceptions-detail.md file with ALL captured exception data:

  # Exception Paths & Variations: {{process_name}}

  **Process ID:** {{process_id}}
  **Document Type:** Exception Detail Analysis
  **Last Updated:** {{date}}
  **Related Document:** [AS-IS Process Documentation](./as-is-process-documentation.md)

  ---

  ## Executive Summary

  {{exceptions_executive_summary}}

  ---

  ## Exception Summary Table

  | EX# | Exception Name | Trigger Condition | Affected Steps | Frequency | Business Impact | Handling Owner |
  |-----|----------------|-------------------|----------------|-----------|-----------------|----------------|
  {{Generate full table}}

  ---

  ## Detailed Exception Analysis

  {{For each exception, generate full detail block with:
    - Overview table (ID, Name, Category, Affected Steps, Frequency, Impact, Owner)
    - Trigger Conditions
    - Current Handling Procedure
    - Root Cause Analysis (if captured)
    - Improvement Opportunities (if captured)
  }}

  ---

  This incremental save ensures:
  - If session aborts after Step 5, all exceptions are recoverable
  - Both summary (main doc) and detail (exceptions-detail.md) are saved
  - SME work is never lost
</action>
```

### 6. Proceed to Next Step

```
**Process Exceptions Complete!**
{{total_exceptions}} exceptions documented with EX# IDs.
Proceeding to Step 6: Pain Points & Challenges...
```

```
<action>Load, read entire file, then execute {nextStepFile}</action>
```

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:
- Exceptions captured with EX# IDs (or noted none exist)
- Each exception linked to relevant PS# IDs
- Updated structured-data.json
- **APPENDED Section 3 to as-is-process-documentation.md (RECOVERY-SAFE)**
- **WROTE full exceptions-detail.md (RECOVERY-SAFE)**
- Ready to proceed to Step 6

### ❌ SYSTEM FAILURE:
- Exceptions not linked to PS# IDs
- Updated JSON but not exceptions-detail.md (or vice versa)
- Started capturing pain points in this step

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
