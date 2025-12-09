---
name: 'step-02-regulatory-framework'
description: 'Map applicable regulations, regional requirements, and industry standards'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/control-compliance-analysis'

# File References
thisStepFile: '{workflow_path}/steps/step-02-regulatory-framework.md'
nextStepFile: '{workflow_path}/steps/step-03-control-inventory.md'
workflowFile: '{workflow_path}/workflow.md'

# Shared Protocols
protocolsFile: '{module_root}/workflows/shared/protocols/protocols.md'

# Output Files
complianceAssessmentFile: '{current_process_folder}/compliance-control-assessment.md'

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
---

# Step 2: Regulatory Framework Mapping

## STEP GOAL

Identify and document all applicable regulations, regional requirements, and industry standards that govern this process. Assign REG# IDs to each regulation. This corresponds to **Section 1** of the compliance-control-assessment template.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:
- **NEVER** generate content without user input
- **CRITICAL**: Read the complete step file before taking any action
- **CRITICAL**: When loading next step, ensure entire file is read
- YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:
- You are a Control Analyst (Compliance & Control Specialist)
- Continue using your established name, communication_style, and persona
- Use precise regulatory language with zero ambiguity
- Speak in traceability terms: "This regulation requires..."

### Step-Specific Rules:
- Each regulation gets a unique REG# ID using format: REG-{process_abbreviation}-### (e.g., REG-ONB-001)
- Must capture specific requirements, not just regulation names
- Link regulations to jurisdiction/region
- **FORBIDDEN** to start cataloging controls in this step (that's Step 3)

## COMMON BANKING REGULATIONS REFERENCE

| Category | EU | UK | US | Global |
|----------|----|----|----|----|
| AML/KYC | AMLD 4/5/6 | MLR 2017 | BSA/AML | FATF |
| Data Privacy | GDPR | UK GDPR | CCPA/GLBA | - |
| Capital/Risk | CRR/CRD IV | UK CRR | Basel III | Basel III/IV |
| Markets | MiFID II | UK MiFID | Dodd-Frank | - |
| Consumer | PSD2 | FCA PRIN | CFPB | - |
| Fraud | - | - | - | PCI-DSS |

## EXECUTION PROTOCOLS

- Load protocols from `{protocolsFile}` for elicitation techniques
- Reference region from Step 1 to guide regulatory mapping
- Use advanced-elicitation-task for deep questioning when needed
- Capture both mandatory and best-practice requirements

## CONTEXT BOUNDARIES

- Session initialized in Step 1
- Region and business unit identified
- AS-IS process steps loaded and available
- This step produces Section 1 of the compliance assessment

---

## EXECUTION SEQUENCE

### 1. Display Progress and Context

```
**Progress: Step 2 of 10 - Regulatory Framework Mapping**

Let's identify all regulations that apply to this process.

Region: {region}
Business Unit: {business_unit}
Process: {current_process_name}

I'll ask about:
1. Core banking regulations
2. Regional/jurisdictional requirements
3. Industry standards and best practices
```

### 2. Core Banking Regulations

```
<format>
**Core Banking Regulations**

Based on your region ({region}) and process type, let's identify applicable regulations.
</format>

<ask response="aml_kyc_applicable">
Does this process involve client identification, transaction monitoring, or suspicious activity?
(Would AML/KYC regulations apply?)

- [ ] Yes - AML/KYC regulations apply
- [ ] No - Not applicable
- [ ] Partially - Some aspects apply
</ask>

<check if="aml_kyc_applicable != 'No'">
  <ask response="aml_regulations">
  Which AML/KYC regulations specifically apply?
  (Select all that apply, or add others)

  {{#if region == 'EU'}}
  - [ ] AMLD 4 (4th Anti-Money Laundering Directive)
  - [ ] AMLD 5 (5th Anti-Money Laundering Directive)
  - [ ] AMLD 6 (6th Anti-Money Laundering Directive)
  {{/if}}
  {{#if region == 'UK'}}
  - [ ] MLR 2017 (Money Laundering Regulations)
  - [ ] JMLSG Guidance
  {{/if}}
  {{#if region == 'US'}}
  - [ ] BSA (Bank Secrecy Act)
  - [ ] USA PATRIOT Act
  - [ ] FinCEN Regulations
  {{/if}}
  - [ ] FATF Recommendations
  - [ ] Other: ___
  </ask>
</check>

<ask response="data_privacy_applicable">
Does this process handle personal data or client information?
(Would data privacy regulations apply?)

- [ ] Yes - Data privacy regulations apply
- [ ] No - Not applicable
</ask>

<check if="data_privacy_applicable == 'Yes'">
  <ask response="privacy_regulations">
  Which data privacy regulations specifically apply?

  {{#if region == 'EU'}}
  - [ ] GDPR (General Data Protection Regulation)
  {{/if}}
  {{#if region == 'UK'}}
  - [ ] UK GDPR
  - [ ] Data Protection Act 2018
  {{/if}}
  {{#if region == 'US'}}
  - [ ] GLBA (Gramm-Leach-Bliley Act)
  - [ ] CCPA (California Consumer Privacy Act)
  {{/if}}
  - [ ] Other: ___
  </ask>
</check>

<ask response="other_core_regulations">
Are there other core regulations that apply to this process?
(e.g., MiFID II for markets, PSD2 for payments, Basel for capital)

- [ ] Yes - I'll specify which ones
- [ ] No - We've covered the core regulations
</ask>
```

### 3. Capture Regulation Details

```
<loop name="regulation_capture" for="each regulation identified">

  <format>
  **Regulation: {{regulation.name}}** → Assigning ID: REG-{process_abbreviation}-{{next_id_padded}}
  </format>

  <ask response="regulation.jurisdiction">
  What is the jurisdiction of this regulation?
  (e.g., EU, UK, US Federal, State-specific)
  </ask>

  <ask response="regulation.applicability">
  How does this regulation apply to the process?
  - [ ] Fully applicable - all requirements apply
  - [ ] Partially applicable - specific sections apply
  - [ ] Reference only - guides best practices
  </ask>

  <ask response="regulation.specific_requirements">
  What are the specific requirements this regulation imposes on this process?
  (Be specific - these will be matched to controls)
  </ask>

  <ask response="regulation.compliance_status">
  What is the current compliance status?
  - [ ] Compliant - all requirements met
  - [ ] Partially Compliant - some gaps exist
  - [ ] Non-Compliant - significant gaps
  - [ ] Unknown - needs assessment
  </ask>

  <ask response="regulation.key_articles">
  Which specific articles/sections are relevant?
  (e.g., "GDPR Article 6 - Lawfulness", "AMLD5 Article 14 - CDD")
  </ask>

</loop>
```

### 4. Regional Requirements

```
<format>
**Regional/Local Requirements**

Beyond core regulations, are there regional or local requirements specific to {region}?
</format>

<ask response="regional_requirements">
Are there additional regional requirements?
(e.g., central bank guidelines, local regulator requirements, state-specific rules)

- [ ] Yes - I'll specify
- [ ] No - core regulations cover it
</ask>

<check if="regional_requirements == 'Yes'">
  <loop name="regional_capture" until="user says done">
    <ask response="regional.name">What is the regional requirement?</ask>
    <ask response="regional.authority">Which authority issues this?</ask>
    <ask response="regional.specific_requirements">What does it require?</ask>
  </loop>
</check>
```

### 5. Industry Standards

```
<format>
**Industry Standards & Best Practices**

Now let's capture any industry standards that apply (voluntary but expected).
</format>

<ask response="industry_standards">
Which industry standards apply to this process?

- [ ] ISO 27001 (Information Security)
- [ ] ISO 22301 (Business Continuity)
- [ ] PCI-DSS (Payment Card Industry)
- [ ] SOC 2 (Service Organization Controls)
- [ ] COBIT (Control Objectives for IT)
- [ ] COSO (Internal Control Framework)
- [ ] Industry-specific standards: ___
- [ ] None applicable
</ask>

<check if="industry_standards selected">
  <loop name="standard_capture" for="each selected standard">
    <ask response="standard.applicability">How does {{standard.name}} apply?</ask>
    <ask response="standard.certification_status">Is certification required or held?</ask>
  </loop>
</check>
```

### 6. Capture Confidence

```
<ask response="section_1_confidence">
How confident are you in the regulatory mapping we captured?

- [ ] High - I know the regulatory landscape well
- [ ] Medium - Generally confident, may have missed some
- [ ] Low - Would benefit from legal/compliance review
</ask>

<ask response="section_1_confidence_basis">
What's the basis for this confidence? (e.g., recent compliance audit, legal review, assumption)
</ask>
```

### 7. Update Output File

```
<action silent="true">
Update {complianceAssessmentFile} Section 1 (Regulatory Framework Mapping):

1.1 Applicable Regulations:
Build table with all REG# entries:
| REG# | Regulation | Jurisdiction | Applicability | Compliance Status |

1.2 Regional Requirements:
Narrative of regional requirements

1.3 Industry Standards:
List of applicable standards with status

Section Confidence: {{section_1_confidence}}
Confidence Basis: {{section_1_confidence_basis}}
</action>
```

### 8. Summary and Transition

Display:
```
**Regulatory Framework Mapped**

| Metric | Value |
|--------|-------|
| Total Regulations | {{total_regulations}} |
| Fully Applicable | {{fully_applicable}} |
| Partially Applicable | {{partially_applicable}} |
| Regional Requirements | {{regional_count}} |
| Industry Standards | {{standards_count}} |
| Confidence | {{section_1_confidence}} |

**Key Regulations:**
{{for each top_regulation}}
- REG-{process_abbreviation}-{{id}}: {{name}} ({{compliance_status}})
{{/for}}

Next, we'll catalog all control points and map them to these regulations.
```

### 9. Proceed to Next Step

Display:
```
**Progress: Step 2 of 10 - Regulatory Framework Complete**

Now let's identify and catalog all control points for this process.
```

```
<action>Load, read entire file, then execute {nextStepFile}</action>
```

---

## CRITICAL STEP COMPLETION NOTE

This is an auto-proceed step. IMMEDIATELY after [regulations mapped] and [output file updated], load and read fully `{nextStepFile}` to execute and begin control point inventory.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:
- All applicable regulations identified
- Each regulation has REG# ID in correct format
- Specific requirements captured (not just names)
- Compliance status assessed
- Regional requirements captured
- Industry standards identified
- Confidence assessment captured
- Output file updated
- Ready to proceed to Step 3

### SYSTEM FAILURE:
- Did not assign REG# IDs
- Captured only regulation names without requirements
- Did not assess compliance status
- Started cataloging controls
- Did not update output file
- Skipped to later steps

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
