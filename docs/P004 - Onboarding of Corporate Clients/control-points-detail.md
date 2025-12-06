# Control Points & Compliance: Onboarding of Corporate Clients

**Process ID:** P004
**Document Type:** Control Point Detail Analysis
**Last Updated:** 2025-12-04
**Related Document:** [AS-IS Process Documentation](./as-is-process-documentation.md)

---

## Executive Summary

**8 controls** have been identified for the Corporate Client Onboarding process through Regulatory Framework Mapping:

| Status | Count | Controls |
|--------|-------|----------|
| ✅ **Existing** | 2 | CP-OCC-001 (KYC), CP-OCC-006 (TCF) |
| 🟡 **Needs Formalization** | 3 | CP-OCC-002 (AML), CP-OCC-004 (Sanctions), CP-OCC-008 (Defence DD) |
| 🔴 **Critical Gaps** | 3 | CP-OCC-003 (GDPR Consent), CP-OCC-005 (FATCA/CRS), CP-OCC-007 (DSR) |

**Critical Findings:**
- 🚨 **GDPR Non-Compliance** — No consent management for 13 communication touchpoints (AF-2024-023)
- 🚨 **FATCA/CRS Non-Compliance** — No tax self-certification collection (AF-2024-042)
- ⚠️ **AML Evidence Gap** — Screening logs not retained for required period (AF-2024-051)

**Regulatory Coverage:** 1 of 6 regulations fully compliant (TCF only)

---

## Control Point Summary Table

> **Quick Reference:** All identified control points with compliance mapping at a glance. Click any CP# for full details below.

| CP# | Control Name | Type | Regulation/Policy | Process Step | Effectiveness | Risk Level | Status |
|-----|--------------|------|-------------------|--------------|---------------|------------|--------|
| CP-OCC-001 | KYC Check and Approval | Preventive | KYC | Pre-process | Medium | Medium | ✅ Existing |
| CP-OCC-002 | AML Transaction Screening | Detective | AML | Ongoing | Not Assessed | High | 🟡 NEW |
| CP-OCC-003 | GDPR Consent Management | Preventive | GDPR | Pre-Day 1, All comms | Does Not Exist | Critical | 🔴 GAP |
| CP-OCC-004 | Sanctions List Screening | Preventive | Sanctions | Pre-process, Ongoing | Implied | Critical | 🟡 NEW |
| CP-OCC-005 | FATCA/CRS Self-Certification | Preventive | FATCA/CRS | Day 1 | Does Not Exist | High | 🔴 GAP |
| CP-OCC-006 | TCF Communication Standards | Preventive | TCF | All 13 steps | Effective | Medium | ✅ Existing |
| CP-OCC-007 | Data Subject Rights Process | Corrective | GDPR | On request | Does Not Exist | High | 🔴 GAP |
| CP-OCC-008 | Defence Sector Enhanced DD | Preventive | Sanctions | Pre-process | Medium | High | 🟡 NEW |

**Legend:** ✅ Existing = Documented and operating | 🟡 NEW = Needs formalization | 🔴 GAP = Does not exist

---

## Control Statistics

| Metric | Value |
|--------|-------|
| Total Control Points | 8 |
| ✅ Existing & Documented | 2 |
| 🟡 NEW (Needs Formalization) | 3 |
| 🔴 GAP (Does Not Exist) | 3 |
| Regulatory Controls | 8 |
| Internal Policy Controls | 0 |
| Automated Controls | 0 |
| Semi-Automated Controls | 1 |
| Manual Controls | 1 |
| High-Effectiveness Controls | 1 |
| Controls Needing Improvement | 4 |
| Critical Risk Controls Missing | 2 |

---

## Regulatory Coverage Matrix

> *Mapping of regulations to controls - ensures complete compliance coverage*

| Regulation | Requirement | Control(s) | Coverage Status | Risk |
|------------|-------------|------------|-----------------|------|
| **KYC** | Client identity verification, UBO, authorized signatories | CP-OCC-001 | ⚠️ Partial | High |
| **AML** | CDD, sanctions screening, ongoing monitoring, SAR | CP-OCC-001, CP-OCC-002 🟡 | ⚠️ Partial | High |
| **GDPR** | Consent, data subject rights, privacy notice | CP-OCC-003 🔴, CP-OCC-007 🔴 | 🚨 Non-Compliant | Critical |
| **Sanctions** | Pre-onboarding screening, ongoing re-screening | CP-OCC-004 🟡, CP-OCC-008 🟡 | ⚠️ Partial | Critical |
| **FATCA/CRS** | Self-certification, tax residency reporting | CP-OCC-005 🔴 | 🚨 Non-Compliant | High |
| **TCF** | Clear communications, fair treatment | CP-OCC-006 | ✅ Compliant | Medium |

**Legend:** 🔴 = GAP (does not exist) | 🟡 = NEW (needs formalization) | ✅ = Existing

---

## Control Type Breakdown

| Type | Count | Automated | Semi-Auto | Manual | Effectiveness Avg |
|------|-------|-----------|-----------|--------|-------------------|
| Preventive | 6 | 2 | 2 | 2 | Varies |
| Detective | 1 | 1 | 0 | 0 | Not Assessed |
| Corrective | 1 | 0 | 0 | 1 | Does Not Exist |

**By Status:**
| Status | Count | Controls |
|--------|-------|----------|
| ✅ Existing | 2 | CP-OCC-001, CP-OCC-006 |
| 🟡 Needs Formalization | 3 | CP-OCC-002, CP-OCC-004, CP-OCC-008 |
| 🔴 Critical Gap | 3 | CP-OCC-003, CP-OCC-005, CP-OCC-007 |

---

## Detailed Control Point Analysis

### CP-OCC-001: KYC Check and Approval

#### Overview

| Attribute | Value |
|-----------|-------|
| **Control ID** | CP-OCC-001 |
| **Name** | KYC Check and Approval |
| **Type** | Preventive |
| **System** | dbCLM |
| **Process Step** | Pre-process (before Day 1) |
| **Method** | Semi-automated |
| **Effectiveness** | Medium |
| **Risk Level** | Medium |

#### Description

KYC verification is performed in the dbCLM system before the client enters the onboarding journey. This is a gate control — clients cannot proceed to Day 1 activities until KYC is cleared.

#### Regulatory Mapping

| Regulation | How This Control Addresses It |
|------------|-------------------------------|
| KYC | Verifies client identity before onboarding |
| AML | Screens for anti-money laundering red flags |

#### Defence Sector Enhancement

Defence sector clients (EX-OCC-001) require additional manual KYC Team approval beyond the standard semi-automated check, resulting in 3-5 business day delay.

#### Effectiveness Assessment

| Factor | Assessment |
|--------|------------|
| Design Effectiveness | Medium — Semi-automated with manual override capability |
| Operating Effectiveness | Medium — Generally effective but occasional gaps or workarounds |
| Improvement Opportunities | Consider full automation, enhanced monitoring |

#### Audit Findings

| Finding ID | Description | Severity | Status |
|------------|-------------|----------|--------|
| AF-2024-017 | KYC documentation incomplete for 12% of corporate clients | High | Open |

---

### CP-OCC-002: AML Transaction Screening 🟡 NEW

#### Overview

| Attribute | Value |
|-----------|-------|
| **Control ID** | CP-OCC-002 |
| **Name** | AML Transaction Screening |
| **Status** | 🟡 Needs Formalization |
| **Type** | Detective |
| **System** | AML System (TBD) |
| **Process Step** | Ongoing (post-onboarding) |
| **Method** | Automated |
| **Effectiveness** | Not Assessed |
| **Risk Level** | High |

#### Description

Ongoing transaction monitoring to detect suspicious patterns, unusual activity, and potential money laundering indicators. While initial AML screening occurs at the KYC gate (CP-OCC-001), this control addresses the requirement for continuous monitoring throughout the client relationship.

Currently, this control is implied within CP-OCC-001 but is not formally documented as a separate control. The 180-day onboarding journey does not include transactions, but the handoff to ongoing monitoring systems must be documented.

#### Regulatory Mapping

| Regulation | How This Control Addresses It |
|------------|-------------------------------|
| AML | Continuous monitoring for suspicious activity patterns |
| AML | Alert generation for investigation |
| AML | SAR filing trigger identification |

#### Key Requirements

- **Ongoing Monitoring** - Continuous screening of client activity for suspicious patterns
- **Alert Management** - System-generated alerts for investigation and disposition
- **SAR Triggers** - Automatic identification of reportable suspicious activity
- **Record Retention** - 7-year retention of all screening logs and alert dispositions

#### Effectiveness Assessment

| Factor | Assessment |
|--------|------------|
| Design Effectiveness | Not Assessed — Control not yet formalized |
| Operating Effectiveness | Not Assessed — Control not yet formalized |
| Improvement Opportunities | Formalize as separate control, document handoff from onboarding to monitoring |

#### Audit Findings

| Finding ID | Description | Severity | Status |
|------------|-------------|----------|--------|
| AF-2024-051 | AML screening logs not retained for required 7-year period | High | Open |

#### Remediation Required

1. Document AML transaction monitoring as formal control (CP-OCC-002)
2. Define handoff point from onboarding to ongoing monitoring
3. Implement log retention for 7-year period
4. Document alert investigation and disposition procedures

---

### CP-OCC-003: GDPR Consent Management 🔴 GAP

#### Overview

| Attribute | Value |
|-----------|-------|
| **Control ID** | CP-OCC-003 |
| **Name** | GDPR Consent Management |
| **Status** | 🔴 CRITICAL GAP - Does Not Exist |
| **Type** | Preventive |
| **System** | CRM (to be implemented) |
| **Process Step** | Pre-Day 1, All 13 communication touchpoints |
| **Method** | To be determined |
| **Effectiveness** | Does Not Exist |
| **Risk Level** | Critical |

#### Description

**THIS CONTROL DOES NOT EXIST.**

The corporate client onboarding process sends 13 communications over 180 days (SMS, email, video, phone calls, social media) without capturing consent for marketing communications. This represents a critical GDPR compliance gap.

GDPR requires explicit, informed consent for marketing communications, with clear opt-out mechanisms. Currently, no consent is captured at any point in the onboarding journey.

#### Regulatory Mapping

| Regulation | Requirement Not Met |
|------------|---------------------|
| GDPR Art. 6 | No lawful basis documented for processing |
| GDPR Art. 7 | No consent capture mechanism |
| GDPR Art. 21 | No opt-out mechanism for direct marketing |
| ePrivacy | Electronic communications sent without consent |

#### Process Touchpoints Affected

| Step | Activity | Impact |
|------|----------|--------|
| PS-01-002 | Initial SMS & email campaigns | ❌ No consent |
| PS-01-003 | Demo video | ❌ No consent for video analytics |
| PS-01-004 | Welcome email | ❌ No consent |
| PS-02-001 | Check-in call (Genesys) | ❌ No consent for call recording |
| PS-02-002 | Day 14 email campaign | ❌ No consent |
| PS-02-006 | Call centre engagement | ❌ No consent |
| PS-02-007 | Social media campaign | ❌ No consent for data sharing |

#### Effectiveness Assessment

| Factor | Assessment |
|--------|------------|
| Design Effectiveness | N/A — Control does not exist |
| Operating Effectiveness | N/A — Control does not exist |
| Gap Severity | 🚨 CRITICAL — Regulatory fine up to 4% global revenue |

#### Audit Findings

| Finding ID | Description | Severity | Status |
|------------|-------------|----------|--------|
| AF-2024-023 | GDPR consent not captured for marketing communications | Critical | Open |

#### Remediation Required

1. **Immediate:** Implement consent capture at onboarding registration (Pre-Day 1)
2. Design consent management system integrated with CRM
3. Implement granular consent options (SMS, email, phone, social)
4. Add opt-out mechanism to all communications
5. Create consent audit trail with timestamps
6. Update privacy notice to describe all processing activities

---

### CP-OCC-004: Sanctions List Screening 🟡 NEW

#### Overview

| Attribute | Value |
|-----------|-------|
| **Control ID** | CP-OCC-004 |
| **Name** | Sanctions List Screening |
| **Status** | 🟡 Needs Formalization |
| **Type** | Preventive |
| **System** | Sanctions Screening Tool |
| **Process Step** | Pre-process, Ongoing |
| **Method** | Automated |
| **Effectiveness** | Implied (not formally assessed) |
| **Risk Level** | Critical |

#### Description

Screening of corporate clients, beneficial owners, and authorized signatories against EU, UN, OFAC, and local sanctions lists. This control is currently implied through the defence sector exception (EX-OCC-001) but is not formally documented as applying to all clients.

Sanctions screening must occur at onboarding and on an ongoing basis as sanctions lists are updated (often daily).

#### Regulatory Mapping

| Regulation | How This Control Addresses It |
|------------|-------------------------------|
| EU Sanctions | Screens against EU consolidated list |
| UN Sanctions | Screens against UN Security Council lists |
| OFAC | Screens against SDN and other OFAC lists |
| Local | Screens against local regulatory lists |

#### Key Requirements

- **Pre-Onboarding Screening** - All parties screened before relationship establishment
- **Beneficial Owner Screening** - All UBOs (>25%) screened
- **Authorized Signatory Screening** - All signatories screened
- **Real-Time Updates** - Daily list updates applied
- **Ongoing Re-Screening** - Existing clients re-screened when lists update
- **Match Escalation** - Potential matches immediately escalated and blocked

#### Effectiveness Assessment

| Factor | Assessment |
|--------|------------|
| Design Effectiveness | Implied — Defence sector enhanced screening suggests capability exists |
| Operating Effectiveness | Partial — EX-OCC-001 shows screening occurs for high-risk sectors |
| Improvement Opportunities | Formalize for all clients, document ongoing re-screening |

#### Audit Findings

| Finding ID | Description | Severity | Status |
|------------|-------------|----------|--------|
| AF-2024-031 | Defence sector screening delays exceed SLA | Medium | In Remediation |

#### Remediation Required

1. Document sanctions screening as formal control for ALL clients
2. Define screening scope (entity, UBOs, signatories)
3. Document ongoing re-screening process
4. Establish SLA for potential match investigation

---

### CP-OCC-005: FATCA/CRS Self-Certification 🔴 GAP

#### Overview

| Attribute | Value |
|-----------|-------|
| **Control ID** | CP-OCC-005 |
| **Name** | FATCA/CRS Self-Certification |
| **Status** | 🔴 GAP - Does Not Exist |
| **Type** | Preventive |
| **System** | dbCLM (to be implemented) |
| **Process Step** | Day 1 (Sign in) |
| **Method** | Manual / Semi-automated |
| **Effectiveness** | Does Not Exist |
| **Risk Level** | High |

#### Description

**THIS CONTROL DOES NOT EXIST.**

FATCA and CRS require financial institutions to collect tax self-certification from corporate clients at account opening. This includes tax residency, entity classification, and controlling person information. Currently, there is no evidence that self-certification is collected during the corporate client onboarding process.

#### Regulatory Mapping

| Regulation | Requirement Not Met |
|------------|---------------------|
| FATCA | No self-certification form collected |
| CRS | No tax residency declaration |
| FATCA | No controlling person identification for passive NFEs |
| CRS | No TIN collection |

#### Key Requirements Not Met

- **Self-Certification Collection** - W-8BEN-E or equivalent not collected
- **Entity Classification** - No determination of entity type (FI, Active NFFE, Passive NFFE)
- **Controlling Person Identification** - For Passive NFEs, controlling persons not identified
- **TIN Collection** - Tax Identification Numbers not collected
- **Annual Reporting** - Cannot report without underlying data

#### Effectiveness Assessment

| Factor | Assessment |
|--------|------------|
| Design Effectiveness | N/A — Control does not exist |
| Operating Effectiveness | N/A — Control does not exist |
| Gap Severity | ⚠️ HIGH — 30% withholding on US-source payments, tax penalties |

#### Audit Findings

| Finding ID | Description | Severity | Status |
|------------|-------------|----------|--------|
| AF-2024-042 | No evidence of FATCA self-certification collection | High | Open |

#### Remediation Required

1. Integrate self-certification collection into Day 1 sign-in process
2. Create/obtain appropriate self-certification forms
3. Implement entity classification logic
4. Add controlling person collection for Passive NFEs
5. Implement TIN validation
6. Create link to annual reporting process

---

### CP-OCC-006: TCF Communication Standards ✅ EXISTING

#### Overview

| Attribute | Value |
|-----------|-------|
| **Control ID** | CP-OCC-006 |
| **Name** | TCF Communication Standards |
| **Status** | ✅ Existing |
| **Type** | Preventive |
| **System** | Campaign Tool, Email System |
| **Process Step** | All 13 communication touchpoints |
| **Method** | Template-based |
| **Effectiveness** | Effective |
| **Risk Level** | Medium |

#### Description

Template-based controls ensure all communications during the 180-day onboarding journey meet Treating Customers Fairly (TCF) standards. Communications are reviewed by Compliance before deployment, and standardized templates ensure consistency across channels.

This is the only regulation with effective control coverage in the current process.

#### Regulatory Mapping

| Regulation | How This Control Addresses It |
|------------|-------------------------------|
| TCF | Standardized templates ensure clear, fair messaging |
| TCF | Compliance review before deployment |
| TCF | Consistent treatment across channels |
| Consumer Duty | Communications designed to support good outcomes |

#### Key Control Activities

- **Template Management** - Pre-approved templates for all communication types
- **Compliance Review** - All new/changed templates reviewed before use
- **Channel Consistency** - Same messaging standards across SMS, email, phone, social
- **Script Standards** - Call centre scripts follow TCF principles

#### Effectiveness Assessment

| Factor | Assessment |
|--------|------------|
| Design Effectiveness | Effective — Template-based approach ensures consistency |
| Operating Effectiveness | Effective — Compliance review prevents non-compliant communications |
| Improvement Opportunities | Extend to cover GDPR consent messaging |

#### Audit Findings

| Finding ID | Description | Severity | Status |
|------------|-------------|----------|--------|
| AF-2024-048 | Communication scripts updated | Medium | ✅ Closed |

---

### CP-OCC-007: Data Subject Rights Process 🔴 GAP

#### Overview

| Attribute | Value |
|-----------|-------|
| **Control ID** | CP-OCC-007 |
| **Name** | Data Subject Rights Process |
| **Status** | 🔴 GAP - Does Not Exist |
| **Type** | Corrective |
| **System** | DPO System (to be implemented) |
| **Process Step** | On request (any time during journey) |
| **Method** | Manual |
| **Effectiveness** | Does Not Exist |
| **Risk Level** | High |

#### Description

**THIS CONTROL DOES NOT EXIST.**

GDPR provides individuals with rights to access, rectify, erase, restrict, and port their personal data. The corporate client onboarding process collects personal data of client representatives across 13 touchpoints, but there is no documented process to handle data subject rights requests within the mandated 30-day timeframe.

#### Regulatory Mapping

| Regulation | Requirement Not Met |
|------------|---------------------|
| GDPR Art. 15 | Right of access — no process to provide data copies |
| GDPR Art. 16 | Right to rectification — no process to correct data |
| GDPR Art. 17 | Right to erasure — no process to delete data on request |
| GDPR Art. 18 | Right to restriction — no process to restrict processing |
| GDPR Art. 20 | Right to portability — no process to export data |
| GDPR Art. 21 | Right to object — no process to stop processing |

#### Key Requirements Not Met

- **Request Intake** - No channel for receiving DSR requests
- **Identity Verification** - No process to verify requestor identity
- **Data Discovery** - No ability to find all data across 7 systems
- **Response Timeline** - No tracking to ensure 30-day response
- **Escalation** - No escalation for complex requests

#### Process Impact

If a client representative submits a data subject request during the 180-day journey:
- No defined process to receive the request
- No ability to identify all data held across SMS, email, Genesys, CRM, etc.
- No ability to respond within 30 days
- Risk of regulatory complaint

#### Effectiveness Assessment

| Factor | Assessment |
|--------|------------|
| Design Effectiveness | N/A — Control does not exist |
| Operating Effectiveness | N/A — Control does not exist |
| Gap Severity | ⚠️ HIGH — Regulatory action, complaints |

#### Remediation Required

1. Create DSR intake channel (email, web form)
2. Implement identity verification process
3. Map all personal data across 7 systems
4. Create data discovery procedures
5. Implement 30-day tracking and escalation
6. Train staff on DSR handling
7. Create response templates

---

### CP-OCC-008: Defence Sector Enhanced Due Diligence 🟡 NEW

#### Overview

| Attribute | Value |
|-----------|-------|
| **Control ID** | CP-OCC-008 |
| **Name** | Defence Sector Enhanced Due Diligence |
| **Status** | 🟡 Needs Formalization (exists as EX-OCC-001) |
| **Type** | Preventive |
| **System** | dbCLM |
| **Process Step** | Pre-process (before Day 1) |
| **Method** | Manual |
| **Effectiveness** | Medium |
| **Risk Level** | High |

#### Description

Enhanced due diligence for corporate clients in the defence sector. This control currently exists as exception EX-OCC-001 but should be formalized as a control. Defence sector clients are subject to heightened sanctions risk and require additional KYC Team approval before entering the standard onboarding journey.

The control results in a 3-5 business day delay while enhanced screening and approval occurs.

#### Regulatory Mapping

| Regulation | How This Control Addresses It |
|------------|-------------------------------|
| Sanctions | Enhanced screening for high-risk sector |
| AML | Additional due diligence for elevated risk |
| KYC | Enhanced verification for defence clients |

#### Key Control Activities

- **Sector Identification** - Identify clients in defence sector at registration
- **Enhanced Screening** - Additional sanctions and PEP screening
- **KYC Team Review** - Manual review and approval required
- **Documentation** - Enhanced documentation requirements
- **Approval Gate** - Cannot proceed until KYC Team approves

#### Effectiveness Assessment

| Factor | Assessment |
|--------|------------|
| Design Effectiveness | Effective — Enhanced screening for high-risk sector |
| Operating Effectiveness | Medium — SLA delays noted in audit findings |
| Improvement Opportunities | Reduce SLA delays, formalize as control |

#### Audit Findings

| Finding ID | Description | Severity | Status |
|------------|-------------|----------|--------|
| AF-2024-031 | Defence sector screening delays exceed SLA | Medium | In Remediation |

#### Remediation Required

1. Formalize EX-OCC-001 as control CP-OCC-008
2. Document enhanced DD procedures
3. Address SLA delays identified in AF-2024-031
4. Define escalation path for complex cases

---

## Control Framework Analysis

### Controls by Risk Level

| Risk Level | Control Count | Gap Count | Coverage |
|------------|---------------|-----------|----------|
| Critical | - | - | - |
| High | - | - | - |
| Medium | - | - | - |
| Low | - | - | - |

### Control Gaps Identified

> *Areas where controls are missing or insufficient - identified during Regulatory Framework Mapping (Section 1)*

| Gap ID | Regulation | Missing Control | Risk Level | Audit Finding | Recommended Action |
|--------|------------|-----------------|------------|---------------|-------------------|
| GAP-001 | GDPR | CP-OCC-003: Consent Management | 🚨 Critical | AF-2024-023 | Implement consent capture for all 13 communication touchpoints |
| GAP-002 | GDPR | CP-OCC-007: Data Subject Rights | ⚠️ High | - | Create DSR handling procedure (access, erasure, portability) |
| GAP-003 | FATCA/CRS | CP-OCC-005: Self-Certification | ⚠️ High | AF-2024-042 | Integrate tax self-certification into Day 1 onboarding |

**Controls Needing Formalization (exist informally):**

| Control ID | Regulation | Description | Current State | Action Required |
|------------|------------|-------------|---------------|-----------------|
| CP-OCC-002 | AML | Transaction Screening | Implied in CP-OCC-001 | Document as separate control, add ongoing monitoring |
| CP-OCC-004 | Sanctions | Sanctions List Screening | Implied via EX-OCC-001 | Formalize for all clients, not just defence sector |
| CP-OCC-008 | Sanctions | Defence Sector Enhanced DD | Exists as EX-OCC-001 | Formalize as control with documented procedure |

### Orphan Controls

> *Controls without clear regulatory requirement (potential waste)*

*To be captured*

### Uncontrolled Requirements

> *Regulatory requirements without adequate controls (compliance risk)*

| Regulation | Requirement | Process Impact | Priority | Potential Fine/Penalty |
|------------|-------------|----------------|----------|------------------------|
| **GDPR** | Consent for marketing communications | All 13 touchpoints send comms without consent | 🚨 Critical | Up to 4% global revenue |
| **GDPR** | Data subject rights handling | No process to respond within 30 days | ⚠️ High | Regulatory action |
| **FATCA/CRS** | Tax self-certification at onboarding | Not collected from corporate clients | ⚠️ High | 30% withholding, tax penalties |
| **AML** | 7-year record retention | Screening logs not retained | ⚠️ High | Cannot demonstrate compliance |
| **KYC** | Periodic refresh | No control for refresh during 180-day journey | Medium | Stale client data |

---

## Segregation of Duties Matrix

> *Critical for banking compliance - who can do what*

| Function | Maker | Checker | Approver | System Enforced |
|----------|-------|---------|----------|-----------------|
| - | - | - | - | - |

---

## Audit Readiness Assessment

### Audit Trail Completeness

| Process Area | Trail Complete | Trail Partial | Trail Missing |
|--------------|----------------|---------------|---------------|
| - | - | - | - |

### Last Audit Findings (if available)

*To be captured*

### Remediation Status

*To be captured*

---

## Recommendations

### Critical (Compliance Risk)

*To be captured*

### High Priority (Control Improvement)

*To be captured*

### Medium Priority (Optimization)

*To be captured*

---

## Input for Downstream Agents

### For Control Analyst Agent

> *Detailed input for control effectiveness analysis*

*To be captured*

### For Transformation Agent

> *Controls that must be preserved/enhanced in TO-BE*

*To be captured*

### For IT Architect

> *Control automation opportunities and system requirements*

*To be captured*

---

## Regulatory Quick Reference

### Applicable Regulations

| Regulation | Scope | Key Requirements | Controls Mapped |
|------------|-------|------------------|-----------------|
| - | - | - | - |

### Upcoming Regulatory Changes

> *Regulations that may impact this process*

*To be captured*

---

## Change Log

| Date | Contributor | Role | Changes |
|------|-------------|------|---------|
| 2025-12-04 | Control Analyst | Regulatory Framework Mapping | Added 7 control gaps from Section 1 analysis (3 critical gaps, 3 to formalize, 1 existing) |
| 2025-12-04 | Control Analyst | Regulatory Framework Mapping | Updated Regulatory Coverage Matrix with 6 regulations |
| 2025-12-04 | Control Analyst | Regulatory Framework Mapping | Added Uncontrolled Requirements section |
| 2025-12-04 | Peter | COO | Added CP-OCC-001 KYC Check and Approval (dbCLM, semi-automated, medium effectiveness) |
| 2025-12-04 | Markus | CEO | Initial control point analysis |

---

_Generated by ProcessMiner Process Documentation Analyst_
_Document ID: P004-controls_
