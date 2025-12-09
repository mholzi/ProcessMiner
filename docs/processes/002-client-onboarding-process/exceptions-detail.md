# Exception Paths & Variations: Client Onboarding process

**Process ID:** COB-002
**Document Type:** Exception Detail Analysis
**Last Updated:** 2025-12-09
**Status:** COMPLETE
**Related Document:** [AS-IS Process Documentation](./as-is-process-documentation.md)

---

## Executive Summary

The Client Onboarding process has 6 identified exception paths. The most critical is an AML/Sanctions Hit (EX-COB-003), which triggers immediate escalation to Compliance leadership and potential regulatory reporting. This occurs rarely but has severe consequences.

The most frequent exception is High-Risk Client Escalation (EX-COB-004), occurring in approximately 25% of cases where the risk assessment determines enhanced due diligence is required. This adds approval layers but is a controlled variation rather than a process failure.

Incomplete Documentation (EX-COB-001) is the primary source of onboarding delays, often requiring multiple follow-up cycles with the client before proceeding.

---

## Exception Summary Table

> **Quick Reference:** All identified exceptions with impact and frequency at a glance. Click any EX# for full details below.

| EX# | Exception Name | Trigger Condition | Affected Steps | Frequency | Business Impact | Handling Owner |
|-----|----------------|-------------------|----------------|-----------|-----------------|----------------|
| EX-COB-001 | Incomplete Documentation | Client unable to provide required documents | PS-COB-002, PS-COB-003 | MEDIUM | MEDIUM | Relationship Manager |
| EX-COB-002 | Failed KYC Verification | Identity verification fails or documents invalid | PS-COB-003 | LOW | HIGH | Compliance Officer |
| EX-COB-003 | AML/Sanctions Hit | Client matches sanctions list or PEP database | PS-COB-004 | LOW | CRITICAL | Compliance Leadership |
| EX-COB-004 | High-Risk Client Escalation | Risk rating requires senior approval | PS-COB-005 | MEDIUM | MEDIUM | Senior Compliance Officer |
| EX-COB-005 | System Downtime | Core Banking or KYC Platform unavailable | PS-COB-003, PS-COB-006 | LOW | HIGH | IT Support / Operations |
| EX-COB-006 | Product Not Available | Requested product not available for client type | PS-COB-007 | LOW | LOW | Onboarding Specialist |

---

## Exception Statistics

| Metric | Value |
|--------|-------|
| Total Exceptions Identified | 6 |
| Critical Impact Exceptions | 1 |
| High Impact Exceptions | 2 |
| Medium Impact Exceptions | 2 |
| Low Impact Exceptions | 1 |
| Frequently Occurring (MEDIUM+) | 2 |
| Exceptions Requiring Manual Intervention | 6 |
| Exceptions with Documented Procedures | 6 |

---

## Detailed Exception Analysis

### EX-COB-001: Incomplete Documentation

| Attribute | Detail |
|-----------|--------|
| **Exception ID** | EX-COB-001 |
| **Exception Name** | Incomplete Documentation |
| **Trigger Condition** | Client unable to provide required documents |
| **Affected Process Steps** | PS-COB-002 (Document Collection), PS-COB-003 (KYC Verification) |
| **Frequency** | MEDIUM - occurs in ~20-30% of cases |
| **Business Impact** | MEDIUM |
| **Confidence** | HIGH |

**Description:**
Client is unable to provide one or more required documents for KYC verification. This is the most common cause of onboarding delays and directly contributes to SLA breaches.

**Handling Procedure:**
1. RM follows up with client to identify which documents are missing
2. RM provides specific checklist and guidance on acceptable alternatives
3. RM sets deadline for document submission (typically 5-7 business days)
4. If not resolved within 10 days, case is paused and client notified
5. Case can be resumed when documents are provided

**Root Cause Analysis:**
- Clients often unaware of full documentation requirements upfront
- Document checklist not always provided at initial contact
- Some required documents take time to obtain (e.g., audited financials)

**Related Pain Points:** PP-COB-001 (Document Chase)

---

### EX-COB-002: Failed KYC Verification

| Attribute | Detail |
|-----------|--------|
| **Exception ID** | EX-COB-002 |
| **Exception Name** | Failed KYC Verification |
| **Trigger Condition** | Identity verification fails or documents invalid |
| **Affected Process Steps** | PS-COB-003 (KYC Verification) |
| **Frequency** | LOW - occurs in <5% of cases |
| **Business Impact** | HIGH |
| **Confidence** | HIGH |

**Description:**
Identity verification fails due to document issues (expired, fraudulent, or inconsistent information) or inability to verify identity through standard channels.

**Handling Procedure:**
1. Case returned to RM with specific failure reasons
2. RM contacts client to request correct/valid documentation
3. Re-verification attempted with new documents
4. If repeated failure (2+ attempts), escalate to Compliance Manager
5. Compliance Manager makes final decision: approve with override, request additional verification, or decline

**Root Cause Analysis:**
- Document quality issues (poor scans, expired documents)
- Name/address mismatches between documents
- Rare cases of attempted fraud

**Related Controls:** CP-COB-001 (KYC Verification Check), CP-COB-006 (Document Authenticity Check)

---

### EX-COB-003: AML/Sanctions Hit

| Attribute | Detail |
|-----------|--------|
| **Exception ID** | EX-COB-003 |
| **Exception Name** | AML/Sanctions Hit |
| **Trigger Condition** | Client matches sanctions list or PEP database |
| **Affected Process Steps** | PS-COB-004 (AML Screening) |
| **Frequency** | LOW - occurs in <1% of cases |
| **Business Impact** | CRITICAL |
| **Confidence** | HIGH |

**Description:**
During AML screening, the client (or associated parties) matches an entry on global sanctions lists, PEP databases, or adverse media screening. This is the most severe exception with potential regulatory and reputational consequences.

**Handling Procedure:**
1. **IMMEDIATE:** Case frozen - no further processing
2. **IMMEDIATE:** Escalate to Compliance Leadership (within 1 hour)
3. Compliance Leadership initiates investigation
4. Determine if hit is true positive or false positive
5. If true positive: Engage Legal, prepare for potential regulatory reporting
6. If false positive: Document rationale, obtain senior sign-off, continue processing
7. All decisions and investigations fully documented in audit trail

**Root Cause Analysis:**
- Client or beneficial owner appears on sanctions list
- Client identified as Politically Exposed Person
- Adverse media indicates potential money laundering risk

**Related Controls:** CP-COB-002 (AML/Sanctions Screening), CP-COB-007 (PEP Enhanced Due Diligence)

**Regulatory Implications:**
- Potential SAR (Suspicious Activity Report) filing requirement
- Must not proceed with onboarding until resolved
- Full audit trail required for regulatory inquiry

---

### EX-COB-004: High-Risk Client Escalation

| Attribute | Detail |
|-----------|--------|
| **Exception ID** | EX-COB-004 |
| **Exception Name** | High-Risk Client Escalation |
| **Trigger Condition** | Risk rating requires senior approval |
| **Affected Process Steps** | PS-COB-005 (Risk Assessment) |
| **Frequency** | MEDIUM - occurs in ~25% of cases |
| **Business Impact** | MEDIUM |
| **Confidence** | HIGH |

**Description:**
The risk assessment process assigns the client a risk rating that requires approval from Senior Compliance Officer or Risk Committee. This is a controlled variation rather than a process failure — it ensures appropriate oversight for higher-risk relationships.

**Handling Procedure:**
1. Compliance Officer completes risk assessment with HIGH or ELEVATED rating
2. Case automatically routed to Senior Compliance Officer
3. Senior CO reviews assessment, may request additional information
4. For very high risk: Case escalated to Risk Committee
5. Enhanced due diligence documentation required (source of wealth, business rationale)
6. Approval or decline decision documented with rationale
7. If approved: Continue to Account Setup with documented conditions

**Root Cause Analysis:**
- Client industry is inherently higher risk (e.g., cash-intensive business)
- Complex ownership structure or offshore entities
- Geographic risk factors
- PEP status or adverse media findings

**Related Controls:** CP-COB-003 (Risk Rating Approval), CP-COB-007 (PEP Enhanced Due Diligence)

**Related Pain Points:** PP-COB-005 (Risk Rating Subjectivity)

---

### EX-COB-005: System Downtime

| Attribute | Detail |
|-----------|--------|
| **Exception ID** | EX-COB-005 |
| **Exception Name** | System Downtime |
| **Trigger Condition** | Core Banking or KYC Platform unavailable |
| **Affected Process Steps** | PS-COB-003 (KYC Verification), PS-COB-006 (Account Setup) |
| **Frequency** | LOW - occurs rarely but impacts multiple cases |
| **Business Impact** | HIGH |
| **Confidence** | HIGH |

**Description:**
Critical systems (Core Banking or KYC Platform) are unavailable due to planned maintenance, technical issues, or outages. This blocks processing for all affected cases.

**Handling Procedure:**
1. IT Support notifies Operations and Compliance of outage
2. All affected cases queued for processing when system restored
3. Client notified of delay if SLA at risk (RM responsibility)
4. **Critical cases only:** Manual workaround procedures may be invoked
5. Once restored: Queued cases processed in priority order (SLA risk first)
6. SLA clock may be paused during documented system outage

**Root Cause Analysis:**
- Planned maintenance windows
- Infrastructure failures
- Third-party system dependencies

**Related Pain Points:** PP-COB-003 (KYC Platform Slowness)

---

### EX-COB-006: Product Not Available

| Attribute | Detail |
|-----------|--------|
| **Exception ID** | EX-COB-006 |
| **Exception Name** | Product Not Available |
| **Trigger Condition** | Requested product not available for client type |
| **Affected Process Steps** | PS-COB-007 (Product Activation) |
| **Frequency** | LOW - occurs in <5% of cases |
| **Business Impact** | LOW |
| **Confidence** | HIGH |

**Description:**
During product activation, it's discovered that one or more requested products are not available for the client's segment, geography, or entity type.

**Handling Procedure:**
1. Onboarding Specialist identifies unavailable product(s)
2. Onboarding Specialist proposes alternative products
3. RM discusses alternatives with client
4. Client confirms revised product selection
5. Continue with activation of available/alternative products
6. If no acceptable alternative: Defer product activation, complete onboarding with available products

**Root Cause Analysis:**
- Product eligibility rules not verified at initial stage
- Recent changes to product availability
- Client segment mismatch

---

## Exception Patterns & Insights

### Clustering Analysis

> *Are there patterns in when/why exceptions occur?*

**Document-Related Exceptions (EX-COB-001, EX-COB-002):**
Both relate to client documentation quality and completeness. These are the primary source of delays and could be reduced through better upfront communication and document checklists.

**Compliance-Triggered Exceptions (EX-COB-003, EX-COB-004):**
These are "controlled variations" — they exist by design to ensure regulatory compliance. Focus should be on handling efficiency rather than reduction.

**Operational Exceptions (EX-COB-005, EX-COB-006):**
System and configuration issues that are addressed through IT and product management rather than process change.

### High-Impact Exception Summary

> *Exceptions requiring priority attention in transformation planning*

| Priority | EX# | Exception | Rationale |
|----------|-----|-----------|-----------|
| 1 | EX-COB-003 | AML/Sanctions Hit | CRITICAL impact, regulatory implications |
| 2 | EX-COB-002 | Failed KYC Verification | HIGH impact, potential client loss |
| 3 | EX-COB-005 | System Downtime | HIGH impact, affects multiple cases |

### Exception-to-Pain-Point Mapping

> *How do exceptions relate to identified pain points?*

| EX# | Related Pain Points (PP#) | Connection |
|-----|---------------------------|------------|
| EX-COB-001 | PP-COB-001 | Document Chase exacerbates incomplete documentation |
| EX-COB-004 | PP-COB-005 | Risk Rating Subjectivity leads to inconsistent escalations |
| EX-COB-005 | PP-COB-003 | System slowness may indicate infrastructure issues |

---

## Recommendations for TO-BE Design

> *Key considerations for the Transformation Agent when addressing exceptions*

### Reduce Exception Frequency

1. **EX-COB-001:** Implement upfront document validation and automated reminders to reduce incomplete documentation cases
2. **EX-COB-002:** Add document quality checks at upload to catch issues before KYC verification

### Improve Exception Handling

1. **EX-COB-003:** Ensure AML screening tools integrate seamlessly with escalation workflows
2. **EX-COB-004:** Standardize risk scoring (addresses PP-COB-005) to reduce unnecessary escalations

### Build Resilience

1. **EX-COB-005:** Consider offline/degraded mode capabilities for critical functions
2. **EX-COB-006:** Validate product eligibility earlier in process (at Initial Contact)

---

## Change Log

| Date | Contributor | Role | Changes |
|------|-------------|------|---------|
| 2025-12-09 | Markus | CEO | Initial exception analysis - COMPLETE |

---

_Generated by ProcessMiner Process Documentation Analyst_
_Document ID: COB-002-exceptions_
_Status: COMPLETE_
