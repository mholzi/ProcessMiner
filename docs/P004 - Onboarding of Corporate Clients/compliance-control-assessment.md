# Compliance & Control Assessment: Onboarding of Corporate Clients

**Document Type:** Regulatory & Control Analysis
**Process ID:** P004
**Business Unit:** All segments
**Region:** Single region
**Control Analyst:** Markus (COO)
**Date:** 2025-12-04
**Version:** 1.0 (Complete Assessment)

---

## Executive Summary

### Overall Compliance Status: ⚠️ PARTIAL COMPLIANCE

| Metric | Value |
|--------|-------|
| Regulations Assessed | 6 |
| Compliant | 1 (17%) |
| Partially Compliant | 3 (50%) |
| Non-Compliant | 2 (33%) |

### Key Findings

**🚨 Critical Issues (Require Immediate Action)**
1. **GDPR Non-Compliance** - No consent management for 13 communication touchpoints over 180-day journey. Open audit finding AF-2024-023.
2. **FATCA/CRS Non-Compliance** - No evidence of tax self-certification collection. Open audit finding AF-2024-042.

**⚠️ High Priority Issues**
3. KYC documentation incomplete for 12% of corporate clients
4. AML screening logs not retained for required period
5. Data Subject Rights process does not exist

### Control Inventory Summary

| Category | Count |
|----------|-------|
| Total Controls Required | 8 |
| Existing & Effective | 1 |
| Existing & Partially Effective | 4 |
| Critical Gaps (Missing) | 3 |

### Risk Exposure

| Risk Level | Regulations | Potential Impact |
|------------|-------------|------------------|
| 🚨 Critical | GDPR | Fine up to 4% global revenue |
| 🚨 Critical | FATCA/CRS | Tax penalties, withholding |
| ⚠️ High | KYC, AML | Regulatory censure |
| Medium | Sanctions | Operational delays |

### Top 5 Recommendations

| # | Action | Priority | Target |
|---|--------|----------|--------|
| 1 | Implement GDPR consent management | 🚨 Critical | Immediate |
| 2 | Implement FATCA/CRS self-certification | 🚨 Critical | Q1 2025 |
| 3 | Create Data Subject Rights procedure | ⚠️ High | Q1 2025 |
| 4 | Remediate KYC documentation gaps | ⚠️ High | Q1 2025 |
| 5 | Implement AML log retention | ⚠️ High | Q1 2025 |

### Audit Finding Status

| Status | Count |
|--------|-------|
| Open - Critical | 1 |
| Open - High | 3 |
| In Remediation | 1 |
| Closed | 1 |

**Workflow Progress:**
- [x] Section 1: Regulatory Framework Mapping
- [x] Section 2: Control Point Inventory
- [x] Section 3: Compliance Gap Analysis
- [x] Section 4: Control Effectiveness Assessment
- [x] Section 5-8: Audit Trail, Risk Matrix, Recommendations

---

## 1. Regulatory Framework Mapping

### 1.1 Applicable Regulations

| # | Regulation | Full Name | Scope | Current Control Coverage | Gap Status |
|---|------------|-----------|-------|-------------------------|------------|
| 1 | **KYC** | Know Your Customer | Client identity verification for corporate clients, beneficial ownership, authorized signatories | CP-OCC-001 (Partial - Medium effectiveness) | Partial coverage |
| 2 | **AML** | Anti-Money Laundering | Screening, monitoring, suspicious activity reporting, record-keeping | CP-OCC-001 (Partial - Medium effectiveness) | Partial coverage |
| 3 | **GDPR** | General Data Protection Regulation | Personal data protection for client representatives across all communications | **No controls documented** | **CRITICAL GAP** |
| 4 | **Sanctions** | EU/UN/OFAC Sanctions Regulations | Sanctions screening for individuals, entities, countries | Implied via EX-OCC-001 (Defence sector hold) | Not explicitly documented |
| 5 | **FATCA/CRS** | Foreign Account Tax Compliance Act / Common Reporting Standard | Tax residency reporting for corporate clients and controlling persons | Not documented | Gap |
| 6 | **TCF** | Treating Customers Fairly / Consumer Duty | Fair treatment throughout 180-day onboarding journey | Not documented | Gap |

#### Regulation Details

**KYC (Know Your Customer)**

**Regulatory Authority:** Local banking regulator

**Overview:**

Know Your Customer (KYC) is a fundamental regulatory requirement in financial services that mandates banks to verify the identity of their clients before establishing a business relationship. For corporate clients, this extends beyond simple identification to understanding the ownership structure, the individuals who ultimately control the entity, and those authorized to act on its behalf. The regulation establishes a critical first line of defense against financial crime by ensuring the bank knows exactly who it is doing business with.

In the context of corporate client onboarding, KYC serves as the gateway control for the entire 180-day journey. The process cannot begin until KYC verification is complete—this is a hard gate that prevents any of the 13 communication touchpoints from being triggered for unverified clients. This is particularly critical because the subsequent journey involves sharing sensitive product information, collecting feedback, and building a trusted banking relationship that assumes the client's legitimacy has been established.

Failure to comply with KYC requirements exposes the bank to regulatory sanctions, reputational damage, and potential facilitation of money laundering or terrorist financing. The local banking regulator conducts periodic examinations specifically focused on KYC compliance, and deficiencies can result in enforcement actions, fines, or restrictions on business activities. Audit finding AF-2024-017 indicates 12% of corporate clients have incomplete KYC documentation.

**Key Requirements:**

- **Legal Entity Verification** - Confirm the corporate client legally exists via commercial register extract (less than 3 months old), certificate of incorporation, and articles of association. The bank must verify the entity is properly constituted under applicable law.
- **Beneficial Ownership (UBO)** - Identify all natural persons owning more than 25% of the entity or exercising control through other means. The complete ownership chain must be traced to natural persons, with documentary evidence for each level.
- **Authorized Signatories** - Verify individuals authorized to act on behalf of the entity through board resolutions, powers of attorney, and specimen signatures. Only verified signatories should receive communications and transact.
- **Source of Funds** - Understand and document the origin of funds to be deposited, with enhanced due diligence for high-risk sources or unusual patterns.
- **Ongoing Monitoring** - Periodic refresh of KYC information based on client risk rating (typically 1-3 years), with event-driven reviews for material changes.

**Process Touchpoints:**

| Step | Activity | KYC Impact | If Not Met |
|------|----------|------------|------------|
| Pre-Day 1 (Gate) | dbCLM KYC Check (CP-OCC-001) | Full KYC pack verification required | ❌ Process BLOCKED - cannot enter Day 1 |
| PS-01-001 to PS-02-008 | All 13 communications | Assumes client identity verified at gate | ⚠️ Communications sent to unverified entity |
| Day 30+ | Relationship continues | Periodic refresh may be due | ⚠️ Account restrictions if refresh overdue |
| EX-OCC-001 | Defence sector clients | Enhanced KYC approval by KYC Team | ❌ 3-5 day hold until approval |

**Current Control Coverage:**
- **CP-OCC-001** - KYC Check and Approval in dbCLM covers initial verification (semi-automated, Medium effectiveness)
- **GAP:** No documented control for periodic KYC refresh during or after 180-day journey
- **GAP:** No verification that communication recipients match authorized signatories
- **Audit Finding:** AF-2024-017 - KYC documentation incomplete for 12% of corporate clients

---

**AML (Anti-Money Laundering)**

**Regulatory Authority:** Local banking regulator, FATF Guidelines

**Overview:**

Anti-Money Laundering (AML) regulations require financial institutions to implement systems and controls to prevent, detect, and report money laundering and terrorist financing activities. These requirements go beyond initial client verification to encompass ongoing monitoring of client behavior, transaction patterns, and changes in risk profile throughout the banking relationship. AML is closely linked to KYC but extends into the operational phase of client relationships.

For the corporate client onboarding process, AML requirements apply at two critical points: the initial screening at the pre-process gate (checking against sanctions lists, PEP databases, and adverse media), and ongoing monitoring as the relationship develops. While the 180-day onboarding journey focuses on communications rather than transactions, the bank must maintain the capability to detect and report suspicious activities that may emerge during this period, including unusual patterns in client responsiveness or attempts to bypass normal procedures.

Non-compliance with AML regulations carries severe consequences including substantial fines, criminal liability for individuals, and potential loss of banking license. Recent enforcement actions in the industry have resulted in multi-billion euro penalties. Audit finding AF-2024-051 indicates AML screening logs are not being retained for the required period, creating evidence gaps for regulatory examinations.

**Key Requirements:**

- **Customer Due Diligence (CDD)** - Risk-based assessment of each corporate client at onboarding, with enhanced due diligence for higher-risk clients (certain industries, geographies, ownership structures).
- **Sanctions Screening** - Screen clients, beneficial owners, and authorized persons against EU, UN, OFAC, and local sanctions lists at onboarding and on an ongoing basis as lists are updated.
- **PEP Screening** - Identify Politically Exposed Persons among beneficial owners and authorized signatories, applying enhanced due diligence where identified.
- **Ongoing Monitoring** - Continuous monitoring of client activity for suspicious patterns, with systems to generate alerts for investigation.
- **Suspicious Activity Reporting (SAR)** - File reports with the Financial Intelligence Unit when suspicious activity is identified, within mandated timeframes.
- **Record Retention** - Maintain all AML-related records for minimum 7 years after relationship ends, including screening logs, alert dispositions, and SAR filings.

**Process Touchpoints:**

| Step | Activity | AML Impact | If Not Met |
|------|----------|------------|------------|
| Pre-Day 1 (Gate) | AML screening via CP-OCC-001 | Initial sanctions/PEP screening | ❌ Process BLOCKED - potential sanctions breach |
| PS-01-001 | Sign in | Risk rating assigned | ⚠️ Inappropriate risk treatment |
| PS-02-001 to PS-02-008 | Ongoing communications | Monitor for behavioral red flags | ⚠️ Missed suspicious activity indicators |
| Day 180+ | Relationship established | Ongoing monitoring begins | ⚠️ Regulatory breach if not implemented |

**Current Control Coverage:**
- **CP-OCC-001** - Initial AML screening at onboarding gate (partial coverage)
- **GAP:** No documented control for ongoing AML monitoring during 180-day journey
- **GAP:** Transaction monitoring not applicable to this process but handoff to monitoring systems not documented
- **Audit Finding:** AF-2024-051 - AML screening logs not retained for required 7-year period

---

**GDPR (General Data Protection Regulation)**

**Regulatory Authority:** EU Data Protection Authorities / Local Data Protection Authority

**Overview:**

The General Data Protection Regulation (GDPR) is the EU's comprehensive data protection framework that governs how organizations collect, process, store, and share personal data of individuals. It establishes strict requirements for lawful processing, transparency, data subject rights, and organizational accountability. GDPR applies to all processing of personal data of EU residents, regardless of where the processing takes place, with significant extraterritorial reach.

This regulation is critically important for the corporate client onboarding process because every single one of the 13 communication touchpoints involves processing personal data of client representatives. The process collects and uses names, email addresses, phone numbers, and communication preferences across multiple channels (SMS, email, video, phone calls, social media) over a 180-day period. Each touchpoint represents a data processing activity that requires a lawful basis, appropriate consent management, and the ability to respond to data subject rights requests.

Non-compliance with GDPR carries the highest potential penalties of any regulation affecting this process—fines up to €20 million or 4% of global annual turnover, whichever is greater. The regulation also provides individuals with private rights of action. **Audit finding AF-2024-023 identifies that GDPR consent is not being captured for marketing communications, representing a critical compliance gap.** This is the most severe regulatory exposure identified for this process.

**Key Requirements:**

- **Lawful Basis** - Establish and document a valid legal basis for each processing activity (consent, contract, legitimate interest, etc.). Marketing communications typically require explicit consent.
- **Consent Management** - Where consent is the lawful basis, capture explicit, informed, freely-given consent with clear opt-out mechanisms. Consent must be as easy to withdraw as to give.
- **Privacy Notice** - Provide clear information about what data is collected, why, how long it's kept, and who it's shared with, at the point of collection.
- **Data Subject Rights** - Implement processes to handle access requests, erasure requests ("right to be forgotten"), data portability, and objection to processing within mandated 30-day timeframe.
- **Data Minimization** - Collect only personal data that is necessary for the stated purpose, and retain it only as long as needed.
- **Security** - Implement appropriate technical and organizational measures to protect personal data, including encryption, access controls, and breach detection.
- **Breach Notification** - Report personal data breaches to the supervisory authority within 72 hours, and to affected individuals without undue delay where there is high risk.

**Process Touchpoints:**

| Step | Activity | GDPR Impact | If Not Met |
|------|----------|-------------|------------|
| Pre-Day 1 | Client registration | Privacy notice, consent capture required | ❌ Unlawful processing from Day 1 |
| PS-01-002 | Initial SMS & email campaigns | Consent for marketing comms required | ❌ **CURRENT GAP** - no consent captured |
| PS-01-003 | Demo video | Video analytics may process personal data | ⚠️ Undisclosed processing |
| PS-01-004 | Welcome email | Direct marketing requires consent | ❌ **CURRENT GAP** |
| PS-02-001 | Check-in call (Genesys) | Call recording requires notice/consent | ⚠️ Potential unlawful recording |
| PS-02-002 | Day 14 email campaign | Marketing consent required | ❌ **CURRENT GAP** |
| PS-02-006 | Call centre engagement (Genesys) | Call recording, feedback collection | ⚠️ Data subject rights must be handleable |
| PS-02-007 | Social media campaign | Third-party platform processing | ⚠️ Data sharing to social media platforms |
| All steps | Any DSR received | Must respond within 30 days | ❌ **NO PROCESS EXISTS** |

**Current Control Coverage:**
- **CP-OCC-003** - GDPR Consent Management: **DOES NOT EXIST - CRITICAL GAP**
- **CP-OCC-007** - Data Subject Rights Process: **DOES NOT EXIST - CRITICAL GAP**
- **GAP:** No consent capture mechanism for any of 13 communication touchpoints
- **GAP:** No documented process to handle data subject access/erasure requests
- **GAP:** Privacy notice provision not documented
- **Audit Finding:** AF-2024-023 - GDPR consent not captured for marketing communications (CRITICAL - Open)

---

**Sanctions Regulations (EU/UN/OFAC)**

**Regulatory Authority:** EU Council, UN Security Council, US Treasury OFAC

**Overview:**

Sanctions regulations prohibit financial institutions from conducting business with designated individuals, entities, and countries. These regulations are enforced by multiple authorities—the EU implements UN Security Council sanctions and adds its own designations, while US OFAC sanctions have extraterritorial reach affecting any transaction touching the US financial system. Sanctions violations are treated as among the most serious regulatory breaches, with potential criminal liability.

For the corporate client onboarding process, sanctions compliance requires screening all parties involved—the corporate entity itself, all beneficial owners, and all authorized signatories—against applicable sanctions lists before establishing a relationship. The defence sector exception (EX-OCC-001) already recognizes that certain industry sectors require enhanced scrutiny, but sanctions screening applies to all corporate clients regardless of sector. Additionally, sanctions lists are updated frequently (sometimes daily), requiring ongoing screening throughout the relationship.

Sanctions violations can result in severe penalties including criminal prosecution of individuals, substantial fines (potentially hundreds of millions of euros), and reputational damage that can threaten the institution's viability. US secondary sanctions can cut institutions off from the US financial system entirely. Audit finding AF-2024-031 notes that defence sector screening is experiencing SLA delays.

**Key Requirements:**

- **Pre-Onboarding Screening** - Screen all corporate clients, beneficial owners (>25%), and authorized signatories against EU, UN, OFAC, and local sanctions lists before relationship establishment.
- **Real-Time List Updates** - Implement systems to receive and apply sanctions list updates as they are published, typically daily for OFAC and EU lists.
- **Ongoing Screening** - Re-screen existing clients when lists are updated to identify newly designated parties.
- **Country Sanctions** - Identify and apply restrictions for transactions involving sanctioned countries or territories.
- **Enhanced Due Diligence** - Apply heightened scrutiny for clients in high-risk sectors (defence, dual-use goods, high-risk jurisdictions).
- **Escalation and Blocking** - Immediately escalate potential matches for investigation and block relationships/transactions pending resolution.

**Process Touchpoints:**

| Step | Activity | Sanctions Impact | If Not Met |
|------|----------|------------------|------------|
| Pre-Day 1 (Gate) | Sanctions screening | Block sanctioned parties from entering | ❌ Sanctions violation - criminal liability |
| EX-OCC-001 | Defence sector clients | Enhanced screening, KYC Team approval | ⚠️ Higher risk sector requires extra scrutiny |
| Ongoing | List updates received | Re-screen existing clients | ⚠️ Newly sanctioned client not identified |
| Any step | Sanctioned party identified | Immediately freeze relationship | ❌ Continued processing = active violation |

**Current Control Coverage:**
- **CP-OCC-004** - Sanctions List Screening: Implied via EX-OCC-001 but **not explicitly documented as a control**
- **EX-OCC-001** - Defence Sector Enhanced DD recognizes high-risk sector screening need
- **GAP:** Sanctions screening not explicitly documented as a formal control for all clients
- **GAP:** Ongoing re-screening process not documented
- **Audit Finding:** AF-2024-031 - Defence sector screening delays exceed SLA (Medium - In Remediation)

---

**FATCA/CRS (Tax Reporting)**

**Regulatory Authority:** US Internal Revenue Service (FATCA), OECD (CRS), Local Tax Authority

**Overview:**

The Foreign Account Tax Compliance Act (FATCA) and Common Reporting Standard (CRS) are international tax transparency frameworks that require financial institutions to identify the tax residency of account holders and report account information to relevant tax authorities. FATCA is a US law with global reach, while CRS is an OECD-led multilateral framework adopted by over 100 jurisdictions. Both require banks to collect self-certification from clients regarding their tax status.

For corporate client onboarding, FATCA/CRS requires collecting tax self-certification from the corporate entity and, in many cases, from controlling persons. This should occur at the point of onboarding—before or during the early stages of the 180-day journey—to ensure the bank can meet its reporting obligations. The information collected includes tax identification numbers, countries of tax residence, and classification of entity type (e.g., financial institution, passive non-financial entity).

Non-compliance with FATCA can result in 30% withholding on US-source payments to the institution and potential exclusion from correspondent banking relationships with US banks. CRS non-compliance results in penalties from local tax authorities and potential reputational damage. **Audit finding AF-2024-042 indicates there is no evidence of FATCA/CRS self-certification being collected from corporate clients.**

**Key Requirements:**

- **Self-Certification Collection** - Obtain completed self-certification forms from all new corporate clients at account opening, declaring tax residency, entity classification, and controlling persons.
- **Controlling Person Identification** - For passive non-financial entities, identify and collect tax residency information for controlling persons (typically those with >25% ownership or control).
- **Tax Identification Numbers** - Collect and validate Tax Identification Numbers (TINs) for all reportable jurisdictions.
- **Reasonable Explanation** - Where TINs are not provided, obtain and document a reasonable explanation.
- **Validation** - Apply reasonableness tests to self-certification information; do not accept certifications that are obviously incorrect or inconsistent.
- **Annual Reporting** - Report account holder information to local tax authority for exchange with relevant foreign tax authorities by mandated deadlines.

**Process Touchpoints:**

| Step | Activity | FATCA/CRS Impact | If Not Met |
|------|----------|------------------|------------|
| Pre-Day 1 or Day 1 | Self-certification collection | Should capture tax status at onboarding | ❌ **CURRENT GAP** - not collected |
| PS-01-001 | Sign in | Ideal point for self-certification | ❌ Not integrated into process |
| Day 30 | Account activation | Final opportunity before account is active | ⚠️ May need to restrict until obtained |
| Annual | Reporting deadline | Report to tax authority | ❌ Cannot report without data |

**Current Control Coverage:**
- **CP-OCC-005** - FATCA/CRS Self-Certification: **DOES NOT EXIST - GAP**
- **GAP:** No self-certification collection integrated into onboarding workflow
- **GAP:** No validation process for self-certification information
- **GAP:** No linkage to annual reporting process
- **Audit Finding:** AF-2024-042 - No evidence of FATCA self-certification collection (High - Open)

---

**TCF (Treating Customers Fairly)**

**Regulatory Authority:** Local banking regulator

**Overview:**

Treating Customers Fairly (TCF) is a regulatory principle that requires financial institutions to deliver fair outcomes for customers throughout the product lifecycle. It encompasses clear and transparent communications, products that meet customer needs, and service delivery that doesn't disadvantage customers. TCF principles are embedded in conduct regulation and increasingly in consumer duty frameworks that place positive obligations on firms to act in customers' best interests.

The corporate client onboarding process is fundamentally a communication journey—13 touchpoints over 180 days designed to welcome, inform, and activate new clients. Every communication in this journey must meet TCF standards: messages must be clear and not misleading, content must be appropriate for the audience, and the overall journey must serve the client's interests rather than purely the bank's commercial objectives. The multi-channel nature (SMS, email, phone, video, social media) means TCF applies across all communication formats.

While TCF violations typically carry lower direct penalties than regulations like GDPR or AML, they can result in regulatory censure, required remediation programs, and reputational damage. More importantly, failure to treat customers fairly during onboarding can undermine the client relationship from the start, leading to poor outcomes, complaints, and attrition. Audit finding AF-2024-048 (now closed) previously identified issues with communication scripts.

**Key Requirements:**

- **Clear Communications** - All communications must be clear, fair, and not misleading. Language must be appropriate for the audience, avoiding jargon or overly complex terms.
- **Appropriate Products** - Products offered or referenced during onboarding must be suitable for the client's needs and circumstances.
- **Balanced Information** - Communications must present balanced information, including relevant risks and limitations, not just benefits.
- **Accessible Channels** - Communication channels must be accessible to clients, with alternatives available where needed.
- **Complaint Handling** - Clear information about how to complain and access to effective complaint resolution.
- **No Barriers** - The process must not create unreasonable barriers to clients exercising their rights or switching products.

**Process Touchpoints:**

| Step | Activity | TCF Impact | If Not Met |
|------|----------|------------|------------|
| PS-01-002 | Initial outreach (SMS/email) | Clear, accurate welcome messaging | ⚠️ Misleading first impression |
| PS-01-003 | Demo video | Balanced product presentation | ⚠️ Over-selling, unrealistic expectations |
| PS-01-004 | Welcome email | Complete, fair information | ⚠️ Material omissions |
| PS-01-005 | Follow up call | Appropriate sales conduct | ⚠️ Pressure selling |
| PS-02-001 | Check-in call | Genuine service focus | ⚠️ Disguised sales call |
| PS-02-002 | Day 14 campaign | Relevant, targeted content | ⚠️ Irrelevant bombardment |
| PS-02-005 | Branch engagement | Appropriate advice | ⚠️ Unsuitable recommendations |
| PS-02-006 | Feedback collection | Genuine feedback mechanism | ⚠️ Tick-box exercise |
| PS-02-007 | Social media | Compliant social content | ⚠️ Misleading claims |
| All steps | 13 touchpoints total | Consistent fair treatment | ⚠️ Journey fatigue, over-contact |

**Current Control Coverage:**
- **CP-OCC-006** - TCF Communication Standards: Exists with template-based controls
- **Control Status:** Effective - templates ensure consistency, compliance review in place
- **Audit Finding:** AF-2024-048 - Communication scripts updated (CLOSED)
- **Note:** This is the only regulation with effective control coverage in the current process

#### Regulations Assessed as Out of Scope

| Regulation | Rationale |
|------------|-----------|
| ePrivacy Directive | Service communications only (not marketing) |
| PSD2 | Not payment-related process |

### 1.2 Regional Requirements

**Not applicable** - Process operates in single region only.

### 1.3 Industry Standards

| Standard | Full Name | Status | Relevance to Process |
|----------|-----------|--------|---------------------|
| **ISO 27001** | Information Security Management System | **Applicable** | Client data security across 7 systems, multi-channel communications |
| COSO | Internal Control Framework | Not Applicable | - |
| COBIT | IT Governance Framework | Not Applicable | - |
| Basel III/IV | Operational Risk Framework | Not Applicable | - |
| ISO 9001 | Quality Management System | Not Applicable | - |

#### ISO 27001 Implications

As ISO 27001 is applicable, the following areas require security controls:
- Client personal data in transit (SMS, email)
- Data at rest in dbCLM, Genesys, campaign systems
- Access controls for 7 systems
- Data retention and disposal (180-day journey + archives)
- Third-party security (social media platforms)

---

## 2. Control Point Inventory

### 2.1 Mandatory Controls

| CP# | Control Name | Type | Regulation | Owner | System | Status | Risk | Effectiveness |
|-----|--------------|------|------------|-------|--------|--------|------|---------------|
| CP-OCC-001 | KYC Verification | Preventive | KYC, AML | KYC Team | dbCLM | Existing | High | Medium |
| CP-OCC-002 | AML Transaction Screening | Detective | AML | AML Team | AML System | **New** | High | Not Assessed |
| CP-OCC-003 | GDPR Consent Management | Preventive | GDPR | DPO/Marketing | CRM | **GAP** | Critical | Does Not Exist |
| CP-OCC-004 | Sanctions List Screening | Preventive | Sanctions | Compliance | Sanctions Tool | **New** | Critical | Implied |
| CP-OCC-005 | FATCA/CRS Self-Certification | Preventive | FATCA/CRS | Tax Compliance | dbCLM | **GAP** | High | Does Not Exist |
| CP-OCC-006 | TCF Communication Standards | Preventive | TCF | Marketing/Compliance | Campaign Tool | **New** | Medium | Partial |
| CP-OCC-007 | Data Subject Rights Process | Corrective | GDPR | DPO | DPO System | **GAP** | High | Does Not Exist |
| CP-OCC-008 | Defence Sector Enhanced DD | Preventive | Sanctions | Compliance | dbCLM | Existing | High | Medium |

**Control Inventory Summary:**
- **Total Controls:** 8
- **Existing Controls:** 2
- **New Controls to Formalize:** 3
- **Critical Gaps:** 3

#### Control Details

**CP-OCC-001: KYC Verification**
- Pre-process gate control in dbCLM
- Semi-automated verification of legal entity, UBO, authorized signatories
- Audit Finding: AF-2024-017 (KYC documentation incomplete for 12%)

**CP-OCC-002: AML Transaction Screening**
- Ongoing transaction monitoring beyond initial onboarding
- Required for suspicious activity detection
- Audit Finding: AF-2024-051 (logs not retained)

**CP-OCC-003: GDPR Consent Management** ⚠️ CRITICAL GAP
- Consent capture for all 13 communication touchpoints
- Opt-out mechanism required
- Audit Finding: AF-2024-023 (consent not captured)

**CP-OCC-004: Sanctions List Screening**
- EU/UN/OFAC list screening at onboarding and ongoing
- Implicit in defence sector exception (EX-OCC-001)
- Audit Finding: AF-2024-031 (screening delays)

**CP-OCC-005: FATCA/CRS Self-Certification** ⚠️ GAP
- Tax residency collection for corporate clients and controlling persons
- Audit Finding: AF-2024-042 (no evidence of collection)

**CP-OCC-006: TCF Communication Standards**
- Fair treatment in all 13 communication steps
- Template-based control with compliance review
- Audit Finding: AF-2024-048 (closed - scripts updated)

**CP-OCC-007: Data Subject Rights Process** ⚠️ GAP
- Handling of access, erasure, portability requests
- Required under GDPR for client representatives

**CP-OCC-008: Defence Sector Enhanced DD**
- Enhanced due diligence for defence industry clients
- Formalizes existing exception EX-OCC-001
- 3-5 day approval process by KYC Team

### 2.2 Internal Policy Mapping

| CP# | Control | Linked Policy | Policy Owner | Procedure | Status |
|-----|---------|---------------|--------------|-----------|--------|
| CP-OCC-001 | KYC Verification | KYC Policy | Compliance | KYC Onboarding Procedure | Documented |
| CP-OCC-002 | AML Screening | AML Policy | AML Officer | AML Monitoring Procedure | Documented |
| CP-OCC-003 | GDPR Consent | Data Protection Policy | DPO | **No procedure exists** | ⚠️ GAP |
| CP-OCC-004 | Sanctions Screening | Sanctions Policy | Compliance | Sanctions Screening Procedure | Documented |
| CP-OCC-005 | FATCA/CRS | Tax Compliance Policy | Tax Compliance | **No procedure exists** | ⚠️ GAP |
| CP-OCC-006 | TCF Standards | Customer Communications Policy | Marketing/Compliance | Communication Templates SOP | Documented |
| CP-OCC-007 | Data Subject Rights | Data Protection Policy | DPO | **No procedure exists** | ⚠️ GAP |
| CP-OCC-008 | Defence Sector DD | High-Risk Client Policy | Compliance | Defence Sector Escalation SOP | Documented |

#### Policy Gaps

| Gap ID | Missing Element | Impact | Recommendation |
|--------|-----------------|--------|----------------|
| PG-001 | GDPR Consent Procedure | Critical | Create consent capture and management procedure for onboarding communications |
| PG-002 | FATCA/CRS Collection Procedure | High | Create self-certification collection and validation procedure |
| PG-003 | Data Subject Rights Procedure | High | Create procedure for handling access/erasure requests during onboarding |

### 2.3 Audit Requirements

#### Audit Trail Requirements by Control

| CP# | Control | Evidence Required | Retention | Frequency | System of Record |
|-----|---------|-------------------|-----------|-----------|------------------|
| CP-OCC-001 | KYC Verification | ID docs, UBO declaration, verification logs | 7 years | Per client | dbCLM |
| CP-OCC-002 | AML Screening | Screening logs, alerts, dispositions | 7 years | Continuous | AML System |
| CP-OCC-003 | GDPR Consent | Consent records, timestamps, opt-outs | Duration + 3 years | Per communication | CRM |
| CP-OCC-004 | Sanctions Screening | Screening results, list versions, escalations | 7 years | Per client + daily | Sanctions Tool |
| CP-OCC-005 | FATCA/CRS | Self-certification forms, validation | 7 years | Per client | dbCLM |
| CP-OCC-006 | TCF Standards | Approved templates, communication logs | 5 years | Per campaign | Campaign Tool |
| CP-OCC-007 | Data Subject Rights | Request logs, response evidence, timelines | 3 years | Per request | DPO System |
| CP-OCC-008 | Defence Sector DD | Enhanced DD files, approval chain | 7 years | Per client | dbCLM |

#### Open Audit Findings

| Finding ID | Control | Finding | Severity | Status | Remediation Due |
|------------|---------|---------|----------|--------|-----------------|
| AF-2024-017 | CP-OCC-001 | KYC documentation incomplete for 12% of clients | High | Open | Q1 2025 |
| AF-2024-023 | CP-OCC-003 | GDPR consent not captured for marketing comms | Critical | Open | Immediate |
| AF-2024-031 | CP-OCC-004 | Defence sector screening delays exceed SLA | Medium | Remediation | Q1 2025 |
| AF-2024-042 | CP-OCC-005 | No evidence of FATCA self-certification collection | High | Open | Q1 2025 |
| AF-2024-051 | CP-OCC-002 | AML screening logs not retained for required period | High | Open | Q1 2025 |

#### Audit Coverage

| Audit Type | Frequency | Last Audit | Next Scheduled | Controls Covered |
|------------|-----------|------------|----------------|------------------|
| Internal Audit - KYC/AML | Annual | 2024-09 | 2025-09 | CP-OCC-001, 002, 004 |
| Internal Audit - Data Protection | Annual | 2024-10 | 2025-10 | CP-OCC-003, 007 |
| External Audit - Tax Compliance | Annual | 2024-11 | 2025-11 | CP-OCC-005 |
| Regulatory Examination | Ad-hoc | 2024-06 | TBD | All |

---

## 3. Compliance Gap Analysis

### 3.1 Current vs Required

| Gap ID | Regulation | Requirement | Current State | Gap Type | Severity |
|--------|------------|-------------|---------------|----------|----------|
| GAP-001 | GDPR | Consent management for communications | No control exists (CP-OCC-003 missing) | Control Gap | 🚨 Critical |
| GAP-002 | GDPR | Data subject rights handling | No control exists (CP-OCC-007 missing) | Control Gap | ⚠️ High |
| GAP-003 | FATCA/CRS | Tax self-certification collection | No control exists (CP-OCC-005 missing) | Control Gap | ⚠️ High |
| GAP-004 | KYC | Complete documentation | 12% incomplete (AF-2024-017) | Effectiveness Gap | ⚠️ High |
| GAP-005 | AML | Log retention | Logs not retained (AF-2024-051) | Evidence Gap | ⚠️ High |
| GAP-006 | Sanctions | Screening SLA | Delays exceed SLA (AF-2024-031) | Performance Gap | Medium |

### 3.2 Risk Exposure

| Gap ID | Likelihood | Impact | Risk Rating | Exposure |
|--------|------------|--------|-------------|----------|
| GAP-001 | High | Critical | 🚨 **Critical** | Regulatory fine up to 4% revenue (GDPR) |
| GAP-002 | Medium | High | ⚠️ **High** | Regulatory fine, reputational damage |
| GAP-003 | High | High | ⚠️ **High** | Tax authority penalties, withholding |
| GAP-004 | Medium | High | ⚠️ **High** | Regulatory censure, remediation costs |
| GAP-005 | Medium | High | ⚠️ **High** | Unable to demonstrate compliance |
| GAP-006 | Low | Medium | Medium | Client delays, SLA breach |

### 3.3 Remediation Needs

| Gap ID | Remediation Action | Owner | Complexity | Target |
|--------|-------------------|-------|------------|--------|
| GAP-001 | Implement consent management in CRM | DPO + IT | High | Q1 2025 |
| GAP-002 | Create DSR handling procedure | DPO | Medium | Q1 2025 |
| GAP-003 | Add FATCA/CRS to onboarding workflow | Tax Compliance | Medium | Q1 2025 |
| GAP-004 | Remediate incomplete KYC files | KYC Team | High | Q1 2025 |
| GAP-005 | Implement AML log archival | IT + Compliance | Medium | Q1 2025 |
| GAP-006 | Review defence sector SLA | Operations | Low | Q2 2025 |

---

## 4. Control Effectiveness Assessment

### 4.1 Control Strengths

| CP# | Control | Strength | Evidence |
|-----|---------|----------|----------|
| CP-OCC-001 | KYC Verification | Gate control prevents unapproved clients | No unverified clients entered process |
| CP-OCC-001 | KYC Verification | Semi-automated reduces manual error | dbCLM system validation |
| CP-OCC-008 | Defence Sector DD | Enhanced scrutiny for high-risk | EX-OCC-001 process working |
| CP-OCC-006 | TCF Standards | Templates ensure consistency | AF-2024-048 closed (scripts updated) |

### 4.2 Control Weaknesses

| CP# | Control | Weakness | Impact | Finding |
|-----|---------|----------|--------|---------|
| CP-OCC-001 | KYC Verification | 12% documentation incomplete | Compliance risk | AF-2024-017 |
| CP-OCC-002 | AML Screening | Logs not retained | Cannot prove compliance | AF-2024-051 |
| CP-OCC-004 | Sanctions Screening | SLA breaches for defence sector | Client delays | AF-2024-031 |
| CP-OCC-003 | GDPR Consent | **Does not exist** | Critical exposure | AF-2024-023 |
| CP-OCC-005 | FATCA/CRS | **Does not exist** | Tax penalties | AF-2024-042 |
| CP-OCC-007 | Data Subject Rights | **Does not exist** | Regulatory breach | - |

### 4.3 Control Effectiveness Summary

| CP# | Control | Design | Operating | Evidence | Overall |
|-----|---------|--------|-----------|----------|---------|
| CP-OCC-001 | KYC Verification | Effective | Partially Effective | Adequate | **Partially Effective** |
| CP-OCC-002 | AML Screening | Effective | Partially Effective | Inadequate | **Partially Effective** |
| CP-OCC-003 | GDPR Consent | N/A | N/A | N/A | **Does Not Exist** |
| CP-OCC-004 | Sanctions Screening | Effective | Partially Effective | Adequate | **Partially Effective** |
| CP-OCC-005 | FATCA/CRS | N/A | N/A | N/A | **Does Not Exist** |
| CP-OCC-006 | TCF Standards | Effective | Effective | Adequate | **Effective** |
| CP-OCC-007 | Data Subject Rights | N/A | N/A | N/A | **Does Not Exist** |
| CP-OCC-008 | Defence Sector DD | Effective | Partially Effective | Adequate | **Partially Effective** |

### Improvement Opportunities

| Priority | Control | Opportunity | Benefit |
|----------|---------|-------------|---------|
| Critical | CP-OCC-003 | Implement GDPR consent control | Eliminate critical regulatory exposure |
| Critical | CP-OCC-005 | Implement FATCA/CRS collection | Eliminate tax compliance gap |
| High | CP-OCC-007 | Implement DSR process | Complete GDPR compliance |
| High | CP-OCC-001 | Remediate documentation gaps | Achieve 100% completeness |
| High | CP-OCC-002 | Implement log retention | Audit trail completeness |
| Medium | CP-OCC-004 | Optimize defence screening SLA | Improve client experience |

---

## 5. Audit Trail Requirements

| Control | Required Evidence | Current State | Gap | Retention |
|---------|-------------------|---------------|-----|-----------|
| CP-OCC-001 | ID docs, UBO, verification logs | ✅ Captured in dbCLM | 12% incomplete | 7 years |
| CP-OCC-002 | Screening logs, alerts, dispositions | ⚠️ Not retained | **Critical** | 7 years |
| CP-OCC-003 | Consent records, timestamps | ❌ Not captured | **Critical** | Duration+3yr |
| CP-OCC-004 | Screening results, list versions | ✅ Captured | - | 7 years |
| CP-OCC-005 | Self-certification forms | ❌ Not captured | **Critical** | 7 years |
| CP-OCC-006 | Approved templates, comm logs | ✅ Captured | - | 5 years |
| CP-OCC-007 | Request logs, response evidence | ❌ Not captured | **Critical** | 3 years |
| CP-OCC-008 | Enhanced DD files, approvals | ✅ Captured in dbCLM | - | 7 years |

**Audit Trail Readiness Score: 50%** (4 of 8 controls have adequate evidence)

---

## 6. Risk & Compliance Matrix

| Regulation | Control | Risk Level | Compliance Status | Audit Finding |
|------------|---------|------------|-------------------|---------------|
| **KYC** | CP-OCC-001 | High | ⚠️ Partial | AF-2024-017 |
| **AML** | CP-OCC-001, CP-OCC-002 | High | ⚠️ Partial | AF-2024-051 |
| **GDPR** | CP-OCC-003, CP-OCC-007 | Critical | 🚨 Non-Compliant | AF-2024-023 |
| **Sanctions** | CP-OCC-004, CP-OCC-008 | Critical | ⚠️ Partial | AF-2024-031 |
| **FATCA/CRS** | CP-OCC-005 | High | 🚨 Non-Compliant | AF-2024-042 |
| **TCF** | CP-OCC-006 | Medium | ✅ Compliant | AF-2024-048 (Closed) |

### Overall Compliance Status

| Status | Count | Regulations |
|--------|-------|-------------|
| ✅ Compliant | 1 | TCF |
| ⚠️ Partial | 3 | KYC, AML, Sanctions |
| 🚨 Non-Compliant | 2 | GDPR, FATCA/CRS |

---

## 7. Regulatory Change Impact

| Regulation | Upcoming Change | Effective | Impact on Process | Action Required |
|------------|-----------------|-----------|-------------------|-----------------|
| GDPR | AI Act integration | 2025 | Low - No AI in current process | Monitor |
| AML | 6AMLD implementation | 2025 | Medium - Enhanced due diligence | Review CP-OCC-002 |
| Sanctions | EU Sanctions Package updates | Ongoing | Medium - List updates | Ensure CP-OCC-004 captures updates |
| FATCA/CRS | CRS 2.0 (crypto assets) | 2026 | Low - Corporate clients | Monitor |
| TCF | Consumer Duty evolution | 2025 | Low - B2B process | Monitor |

**Regulatory Change Risk: Low-Medium** - No major changes requiring immediate action, but monitor AML/Sanctions evolution.

---

## 8. Control Improvement Recommendations

| # | Recommendation | Priority | Gap/Finding | Owner | Target | Effort |
|---|----------------|----------|-------------|-------|--------|--------|
| R-001 | **Implement GDPR consent management** | 🚨 Critical | GAP-001, AF-2024-023 | DPO + IT | Immediate | High |
| R-002 | **Implement FATCA/CRS self-certification** | 🚨 Critical | GAP-003, AF-2024-042 | Tax Compliance | Q1 2025 | Medium |
| R-003 | **Create Data Subject Rights procedure** | ⚠️ High | GAP-002 | DPO | Q1 2025 | Medium |
| R-004 | **Remediate KYC documentation gaps** | ⚠️ High | GAP-004, AF-2024-017 | KYC Team | Q1 2025 | High |
| R-005 | **Implement AML log retention** | ⚠️ High | GAP-005, AF-2024-051 | IT + Compliance | Q1 2025 | Medium |
| R-006 | **Optimize defence sector screening SLA** | Medium | GAP-006, AF-2024-031 | Operations | Q2 2025 | Low |
| R-007 | **Formalize sanctions screening control** | Medium | - | Compliance | Q2 2025 | Low |
| R-008 | **Enhance AML ongoing monitoring** | Medium | - | AML Team | Q2 2025 | Medium |

### Remediation Roadmap

**Q1 2025 (Immediate Priority)**
- R-001: GDPR Consent Management [CRITICAL]
- R-002: FATCA/CRS Collection [CRITICAL]
- R-003: Data Subject Rights [HIGH]
- R-004: KYC Remediation [HIGH]
- R-005: AML Log Retention [HIGH]

**Q2 2025**
- R-006: Defence Screening SLA [MEDIUM]
- R-007: Formalize Sanctions Control [MEDIUM]
- R-008: AML Ongoing Monitoring [MEDIUM]

### Investment Summary

| Priority | Count | Estimated Effort | Key Dependencies |
|----------|-------|------------------|------------------|
| Critical | 2 | High | IT, DPO, Tax Compliance |
| High | 3 | Medium-High | KYC Team, IT, DPO |
| Medium | 3 | Low-Medium | Operations, Compliance |

---

## Change Log

| Date | Contributor | Role | Changes |
|------|-------------|------|---------|
| 2025-12-04 | Markus | COO | **Document Complete (v1.0)** - All 8 sections finalized |
| 2025-12-04 | Markus | COO | Completed Sections 3-8 - Gap Analysis, Effectiveness, Risk Matrix, Recommendations |
| 2025-12-04 | Markus | COO | Completed Section 2 - Control Point Inventory (8 controls, 3 policy gaps, 5 open audit findings) |
| 2025-12-04 | Markus | COO | Completed Section 1 - Regulatory Framework Mapping (6 regulations, 1 standard) |

---

_Generated by ProcessMiner Control Analyst_
_Document ID: P004-compliance-control-assessment_
