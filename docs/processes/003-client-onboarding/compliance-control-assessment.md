# Compliance & Control Assessment: Client Onboarding

**Document Type:** Regulatory & Control Analysis
**Business Unit:** Corporate Bank
**Region:** EU (European Union)
**Control Analyst:** Markus
**Date:** 2025-12-10
**Version:** 1.0.0-DRAFT

---

## Executive Summary

The Client Onboarding process for the Corporate Bank operates within a robust compliance and control framework that effectively manages regulatory risk. This assessment mapped **6 applicable regulations** (including AMLD 5/6, GDPR, PSD2, and CRD IV/CRR) to **16 control points** covering identity verification, data protection, credit assessment, and operational integrity.

**Overall Compliance Posture: SOLID BUT NOT COMPLETE**

The process demonstrates strong control effectiveness, with 81% of controls rated Effective or Highly Effective. The KYC and AML control clusters are particularly strong, benefiting from purpose-built systems (Fenergo, World-Check, Jumio) and clear accountability structures. Automated controls consistently outperform manual controls.

However, the assessment identified **6 compliance gaps** and **3 weak controls** that require attention:

**Priority Issues:**
1. **Missing DPIA** (GAP-COB-003) - GDPR requirement, blocks transformation
2. **Partner channel reliance** (GAP-COB-006) - AML liability exposure
3. **Welcome call ineffective** (CP-COB-015) - 33% completion rate, disclosure risk

**Key Finding:** Controls fail at the point of human execution under pressure, not at design. The three weak controls are all manual processes that rely on staff completing tasks consistently. Automation and system enforcement will improve effectiveness.

**Recommendation:** Address the two Critical priority recommendations within 30 days (DPIA, Partner Reliance), and pursue the High priority client communication redesign to address the audit finding.

### Key Metrics

| Metric | Value |
|--------|-------|
| Total Regulations Mapped | 6 |
| Total Control Points | 16 |
| Compliance Gaps Identified | 6 |
| Critical/High Risk Gaps | 2 |
| Open Audit Findings | 3 |
| Average Control Effectiveness | 4.1/5 |
| Controls Needing Improvement | 3 |
| Improvement Recommendations | 10 |

### Confidence Summary

| Section | Confidence Level |
|---------|-----------------|
| Regulatory Framework | HIGH |
| Control Inventory | HIGH |
| Compliance Gaps | MEDIUM |
| Control Effectiveness | MEDIUM |
| Audit Trail | HIGH |
| Risk Matrix | HIGH |
| Regulatory Change | MEDIUM |
| Open Audit Findings | HIGH |
| Recommendations | HIGH |
| **Overall** | **MEDIUM-HIGH** |

---

## 1. Regulatory Framework Mapping

> **Section Confidence:** HIGH | **Basis:** Recent compliance audit completed Q3 2024, regulatory mapping reviewed by Legal and Compliance teams

### 1.1 Applicable Regulations

The Client Onboarding process operates within a complex regulatory landscape shaped primarily by EU anti-money laundering directives, data protection requirements, and payment services regulations. As an EU-based Corporate Bank, the process must comply with multiple overlapping regulatory frameworks that govern how client identity is verified, personal data is processed, and financial services are provisioned.

The regulatory requirements interact in important ways. AML directives mandate extensive identity verification and beneficial ownership identification, while GDPR constrains how long this data can be retained and how it must be protected. PSD2 adds authentication requirements for account access, and the Consumer Credit Directive applies additional disclosure and assessment requirements when overdraft facilities are requested. This creates a compliance matrix where controls must satisfy multiple regulatory objectives simultaneously.

Key compliance considerations include: maintaining a defensible audit trail for all CDD decisions, ensuring data processing has a lawful basis under GDPR while meeting AML retention requirements, implementing Strong Customer Authentication without creating excessive friction, and ensuring creditworthiness assessments meet both prudential and consumer protection standards.

| REG# | Regulation | Jurisdiction | Applicability | Compliance Status |
|------|------------|--------------|---------------|-------------------|
| REG-COB-001 | AMLD 5 (5th Anti-Money Laundering Directive) | EU | Fully Applicable | Compliant |
| REG-COB-002 | AMLD 6 (6th Anti-Money Laundering Directive) | EU | Fully Applicable | Compliant |
| REG-COB-003 | GDPR (General Data Protection Regulation) | EU | Fully Applicable | Compliant |
| REG-COB-004 | PSD2 (Payment Services Directive 2) | EU | Partially Applicable | Compliant |
| REG-COB-005 | CRD IV/CRR (Capital Requirements) | EU | Partially Applicable | Compliant |
| REG-COB-006 | Consumer Credit Directive | EU | Partially Applicable | Compliant |

#### REG-COB-001: AMLD 5 (5th Anti-Money Laundering Directive)

The 5th Anti-Money Laundering Directive is the cornerstone regulation for the Client Onboarding process. It establishes the mandatory Customer Due Diligence (CDD) framework that determines how the bank must identify clients, verify their identity, and understand the purpose of the business relationship.

**Specific Requirements Applicable to This Process:**
- Customer identification and verification before establishing business relationship
- Beneficial Owner identification for all entities with 25%+ ownership
- PEP (Politically Exposed Person) screening for all directors and UBOs
- Sanctions screening against EU consolidated lists
- Risk-based approach to CDD intensity
- Enhanced Due Diligence for high-risk clients
- Ongoing monitoring requirements

**Key Articles:** Article 13 (CDD Measures), Article 14 (Timing of Verification), Article 18 (EDD Situations), Article 30 (Beneficial Ownership Registers)

**Current Compliance Posture:** Fully compliant. CDD processes embedded in KYC verification step (PS-COB-002) with World-Check screening integration and Fenergo case management.

#### REG-COB-002: AMLD 6 (6th Anti-Money Laundering Directive)

AMLD 6 extends the AML framework with harmonized definitions of money laundering offences and introduces corporate criminal liability. While primarily a criminal law directive, it reinforces the importance of robust AML controls.

**Specific Requirements Applicable to This Process:**
- Extended list of predicate offences requiring enhanced vigilance
- Corporate liability for AML failures
- Enhanced penalties for non-compliance

**Key Articles:** Article 3 (Money Laundering Offences), Article 7 (Corporate Liability)

**Current Compliance Posture:** Fully compliant. Training updated to reflect extended predicate offences.

#### REG-COB-003: GDPR (General Data Protection Regulation)

GDPR governs all personal data processing within the Client Onboarding process. Every piece of client information collected—from ID documents to contact details—falls under GDPR requirements.

**Specific Requirements Applicable to This Process:**
- Lawful basis for processing (legitimate interest for AML, contract for account services)
- Explicit consent required for marketing communications
- Privacy notice provision at point of collection
- Data minimization—collect only what's necessary
- Retention limits aligned with regulatory requirements
- Right to erasure (with AML retention exceptions)
- Data breach notification within 72 hours
- Data Protection Impact Assessment for high-risk processing

**Key Articles:** Article 6 (Lawfulness of Processing), Article 7 (Conditions for Consent), Article 13 (Information to Data Subject), Article 17 (Right to Erasure), Article 32 (Security of Processing), Article 33 (Breach Notification)

**Current Compliance Posture:** Fully compliant. Consent captured at PS-COB-001, privacy notice provided, retention policy aligned with AML requirements.

#### REG-COB-004: PSD2 (Payment Services Directive 2)

PSD2 applies to the account activation phase, requiring Strong Customer Authentication (SCA) when clients access their accounts online for the first time.

**Specific Requirements Applicable to This Process:**
- Strong Customer Authentication for online account access
- Two of three factors: knowledge, possession, inherence
- Secure communication standards for credential delivery

**Key Articles:** Article 97 (Authentication), Regulatory Technical Standards on SCA

**Current Compliance Posture:** Fully compliant. SCA implemented at PS-COB-004 via automated control CP-COB-004.

#### REG-COB-005: CRD IV/CRR (Capital Requirements Directive/Regulation)

CRD IV/CRR applies when the client requests an overdraft facility, requiring credit risk assessment aligned with prudential standards.

**Specific Requirements Applicable to This Process:**
- Credit risk assessment using approved methodologies
- Affordability and responsible lending checks
- Documentation of credit decisions
- Risk rating and provisioning

**Key Articles:** Article 79 (Credit Risk Management), Article 107 (Approaches to Credit Risk)

**Current Compliance Posture:** Fully compliant. Credit assessment at PS-COB-003 uses approved scorecards and bureau data.

#### REG-COB-006: Consumer Credit Directive

The Consumer Credit Directive applies when overdraft facilities are offered to business clients who are natural persons (sole traders).

**Specific Requirements Applicable to This Process:**
- Pre-contractual information (SECCI form)
- Creditworthiness assessment
- 14-day right of withdrawal
- Clear disclosure of APR and total cost

**Key Articles:** Article 5 (Pre-contractual Information), Article 8 (Creditworthiness Assessment)

**Current Compliance Posture:** Fully compliant for applicable client types. Disclosure provided at PS-COB-005.

### 1.2 Regional Requirements

Beyond the core EU regulations, the Client Onboarding process must comply with requirements from the Central Bank of Ireland as the national competent authority. These regional requirements provide additional specificity on how EU directives should be implemented and add Ireland-specific consumer protection measures.

The Central Bank's Consumer Protection Code is particularly relevant, as it establishes conduct standards that go beyond EU minimum requirements. The AML/CFT Guidelines provide practical implementation guidance that shapes how the bank operationalizes its AML controls.

| Requirement | Authority | Specific Requirements | Impact on Process |
|-------------|-----------|----------------------|-------------------|
| Consumer Protection Code 2012 | Central Bank of Ireland | Suitability assessment, product disclosure, complaints handling, vulnerable customer provisions | Affects PS-COB-005 (Client Communication) - enhanced disclosure requirements |
| CBI AML/CFT Guidelines | Central Bank of Ireland | Risk-based approach implementation, transaction monitoring thresholds, SAR reporting procedures | Affects PS-COB-002 (KYC) - specific guidance on risk rating methodology |

### 1.3 Industry Standards

The Client Onboarding process aligns with several industry standards that, while not legally mandated, represent expected best practices and provide frameworks for control design. These standards often inform internal audit approaches and are referenced by regulators as benchmarks for good practice.

ISO 27001 certification is particularly important given the sensitivity of client data processed during onboarding. PCI-DSS compliance is mandatory for the card issuance component. COSO provides the overarching internal control framework that guides how controls are designed and assessed.

| Standard | Applicability | Certification Status | Key Requirements |
|----------|---------------|---------------------|------------------|
| ISO 27001 | Information security controls for client data protection | Certified (Annual Audit) | Access controls, encryption, incident management, business continuity |
| PCI-DSS | Card data handling during debit card issuance | Certified (Level 1) | Cardholder data protection, network security, access management |
| COSO | Internal control framework for control design | Framework Adopted | Control environment, risk assessment, control activities, monitoring |

---

## 2. Control Point Inventory

> **Section Confidence:** HIGH | **Basis:** Internal Audit completed control testing in Q3 2024, no material findings

### 2.1 Mandatory Controls

The Client Onboarding process is governed by 16 control points that ensure regulatory compliance and operational integrity. The control framework is anchored by AMLD 5/6 requirements, which drive the majority of controls in the KYC verification phase. These controls are complemented by GDPR-mandated data protection controls, PSD2 authentication requirements, and credit-related controls for overdraft processing.

The regulatory control design follows a preventive-first philosophy—the majority of controls (12 of 16) are preventive, designed to stop compliance issues before they occur rather than detecting them after the fact. This is appropriate for a regulated onboarding process where remediation after the fact may not be possible (e.g., once a relationship is established with a sanctioned entity, unwinding is costly and reputationally damaging).

Control execution is a mix of automated, semi-automated, and manual. Fully automated controls (4) include screening, authentication, and bureau checks. Semi-automated controls (4) combine system calculations with human judgment. Manual controls (8) rely on trained staff following documented procedures. The manual control concentration in KYC reflects the complexity of identity verification and the judgment required for risk assessment.

| CP# | Control Name | Regulation (REG#) | Process Step (PS#) | Type | Execution |
|-----|--------------|-------------------|--------------------|----- |-----------|
| CP-COB-001 | Customer Identification | REG-COB-001 | PS-COB-002 | Preventive | Semi-Automated |
| CP-COB-002 | Beneficial Owner Identification | REG-COB-001 | PS-COB-002 | Preventive | Manual |
| CP-COB-003 | Data Protection Consent | REG-COB-003 | PS-COB-001 | Preventive | Manual |
| CP-COB-004 | Strong Customer Authentication | REG-COB-004 | PS-COB-004 | Preventive | Automated |
| CP-COB-005 | Product Disclosure | REG-COB-006 | PS-COB-005 | Preventive | Manual |
| CP-COB-006 | Document Completeness Check | REG-COB-001, REG-COB-003 | PS-COB-001 | Preventive | Manual |
| CP-COB-007 | PEP & Sanctions Screening | REG-COB-001, REG-COB-002 | PS-COB-002 | Preventive | Automated |
| CP-COB-008 | Customer Risk Assessment | REG-COB-001 | PS-COB-002 | Preventive | Semi-Automated |
| CP-COB-009 | EDD Escalation | REG-COB-001 | PS-COB-002 | Detective | Manual |
| CP-COB-010 | Credit Bureau Check | REG-COB-005, REG-COB-006 | PS-COB-003 | Preventive | Automated |
| CP-COB-011 | Creditworthiness Assessment | REG-COB-005, REG-COB-006 | PS-COB-003 | Preventive | Semi-Automated |
| CP-COB-012 | Credit Approval Authority | REG-COB-005 | PS-COB-003 | Preventive | Manual |

#### Key Mandatory Controls

**CP-COB-001: Customer Identification** is the foundational CDD control required by AMLD 5. It verifies customer identity using official documents, with Jumio providing automated document verification supplemented by KYC Analyst review. This control must complete before any business relationship is established.

**CP-COB-007: PEP & Sanctions Screening** provides automated screening against World-Check databases. Every director and UBO is screened against PEP lists, sanctions lists (EU, UN, OFAC), and adverse media. True positives require Compliance escalation; false positives are documented and cleared by the KYC Analyst.

**CP-COB-004: Strong Customer Authentication** implements PSD2 requirements for online banking access. The system enforces two-factor authentication combining something the client knows (password) with something they possess (mobile device). This control is fully automated with no bypass capability.

### 2.2 Internal Policies

Beyond regulatory requirements, the Client Onboarding process implements controls driven by internal policy and risk management standards. These controls fill gaps not addressed by regulation and implement the bank's risk appetite.

Internal policy controls focus on operational integrity and segregation of duties. The maker-checker control for account creation and the quality sampling review are key internal controls that protect against operational errors and ensure consistent execution.

| CP# | Control Name | Policy | Process Step (PS#) | Type |
|-----|--------------|--------|--------------------|----- |
| CP-COB-013 | Account Configuration Verification | Operational Risk Policy | PS-COB-004 | Detective |
| CP-COB-014 | Four-Eyes Account Creation | SoD Policy | PS-COB-004 | Preventive |
| CP-COB-015 | Welcome Call Quality | Customer Experience Policy | PS-COB-005 | Detective |
| CP-COB-016 | Quality Sampling Review | Quality Assurance Policy | PS-COB-006 | Detective |

### 2.3 Audit Requirements

All controls produce evidence that supports internal audit, regulatory examination, and external audit requirements. Evidence retention follows the longer of regulatory requirements (7 years for AML, 6 years for GDPR) or internal policy (10 years for customer records).

The audit trail is critical for demonstrating compliance. Each control is designed to produce defensible evidence that can be presented to regulators, auditors, or courts if challenged. Evidence quality varies—automated controls produce complete, timestamped logs while manual controls rely on form completion and case notes.

| CP# | Control Name | Evidence Produced | Retention Period |
|-----|--------------|-------------------|------------------|
| CP-COB-001 | Customer Identification | Jumio verification report, ID document copies, KYC case notes | 7 years post-relationship |
| CP-COB-002 | Beneficial Owner Identification | UBO declaration, ownership structure, ID verification | 7 years post-relationship |
| CP-COB-003 | Data Protection Consent | Signed consent form, CRM consent timestamp | 6 years post-relationship |
| CP-COB-004 | Strong Customer Authentication | Authentication logs, SCA completion records | 5 years |
| CP-COB-005 | Product Disclosure | Welcome email, document delivery confirmation | 6 years post-relationship |
| CP-COB-006 | Document Completeness Check | OWS checklist, rejection codes | 7 years post-relationship |
| CP-COB-007 | PEP & Sanctions Screening | World-Check results, clearance notes | 7 years post-relationship |
| CP-COB-008 | Customer Risk Assessment | Risk assessment form, rating justification | 7 years post-relationship |
| CP-COB-009 | EDD Escalation | EDD review form, Compliance sign-off | 7 years post-relationship |
| CP-COB-010 | Credit Bureau Check | Bureau report, pull timestamp | 7 years |
| CP-COB-011 | Creditworthiness Assessment | Scorecard output, financial analysis | 7 years |
| CP-COB-012 | Credit Approval Authority | Approval record, committee minutes | 7 years |
| CP-COB-013 | Account Configuration Verification | Configuration checklist, T24 screenshots | 10 years |
| CP-COB-014 | Four-Eyes Account Creation | Maker/Checker IDs, approval timestamp | 10 years |
| CP-COB-015 | Welcome Call Quality | CRM call notes, call recording | 6 years |
| CP-COB-016 | Quality Sampling Review | Quality review form, findings log | 3 years |

---

## 3. Compliance Gap Analysis

> **Section Confidence:** MEDIUM | **Basis:** Self-assessment, would benefit from legal/compliance validation

### 3.1 Current vs Required

The compliance gap analysis identified **6 gaps** between regulatory requirements and the current control framework. While the Client Onboarding process has strong controls for core CDD and identity verification, gaps exist primarily in peripheral areas: lifecycle management (ongoing monitoring handover), data protection (DPIA, breach controls), and third-party reliance (partner channel due diligence).

The overall compliance posture is **solid but not complete**. No critical gaps exist that would create immediate regulatory sanction risk. However, two high-risk gaps require attention within 30 days: the missing DPIA for high-risk data processing, and the lack of formal Third Party Reliance agreements for partner channel submissions. These gaps represent compliance debt that could become problematic during regulatory inspection or audit.

For readers unfamiliar with regulatory compliance, the key concern is this: while the bank does a thorough job verifying client identity at onboarding, there are documentation and process gaps that could result in regulatory findings. None of these gaps mean the bank is currently non-compliant in practice—but they mean the bank may struggle to demonstrate compliance if challenged.

| GAP# | Requirement (REG#) | Current State | Gap Description | Risk Level | Priority |
|------|-------------------|---------------|-----------------|------------|----------|
| GAP-COB-001 | REG-COB-001: Ongoing monitoring | Monitoring exists separately | No formal handover from onboarding to AML Operations | Medium | 90 days |
| GAP-COB-002 | REG-COB-003: Breach notification | Bank-wide procedure exists | No onboarding-specific breach detection control | Medium | 90 days |
| GAP-COB-003 | REG-COB-003: DPIA requirement | No DPIA on file | Missing Data Protection Impact Assessment for process | High | 30 days |
| GAP-COB-004 | REG-COB-003: Right to erasure | Informal understanding | No documented GDPR/AML retention conflict resolution | Low | Next cycle |
| GAP-COB-005 | REG-COB-006: Withdrawal right | Disclosure provided | Withdrawal process not documented as control | Low | Next cycle |
| GAP-COB-006 | REG-COB-001: Third party reliance | No formal agreement | Partner channel CDD reliance not formalized | High | 30 days |

#### GAP-COB-003: Missing Data Protection Impact Assessment

GDPR Article 35 requires a Data Protection Impact Assessment for processing "likely to result in a high risk to the rights and freedoms of natural persons." The Client Onboarding process clearly qualifies—it processes identity documents, financial information, and makes decisions that affect individuals' access to financial services.

**Current State:** No DPIA exists for this process. The last privacy review was conducted in 2022 and did not follow DPIA methodology.

**Why This Matters:** A regulatory inspection by the Data Protection Commission would likely identify this as a compliance finding. Additionally, any significant changes to the onboarding process (such as implementing AI for document verification) would require a DPIA as a precondition. This gap blocks certain transformation initiatives.

**Recommended Remediation:** Commission a DPIA from the Data Protection Officer within 30 days. The DPIA should document data flows, identify risks, and confirm mitigation measures. Cost estimate: internal DPO effort or €5-10k for external review.

#### GAP-COB-006: Partner Channel Third Party Reliance

AMLD 5 permits reliance on third parties for CDD, but requires documented due diligence on those third parties and formal agreements specifying responsibilities. Currently, partner channel submissions (accountants, solicitors representing clients) proceed without formal Third Party Reliance agreements.

**Current State:** Partners submit applications on behalf of clients, and the bank accepts their preliminary CDD work. However, there is no documented assessment of partner AML procedures, no formal reliance agreement, and no ongoing monitoring of partner compliance.

**Why This Matters:** If a partner performs inadequate CDD and the bank onboards a client who later is found to be high-risk or involved in money laundering, the bank inherits full regulatory liability. The 15% of applications coming through partner channels represent uncontrolled compliance risk.

**Recommended Remediation:** Implement a Third Party Reliance framework including: (1) due diligence questionnaire for all partners, (2) formal reliance agreements specifying CDD responsibilities, (3) annual review of partner AML procedures. This should be completed within 30 days given the regulatory risk.

### 3.2 Risk Exposure

The overall risk exposure from identified gaps is **moderate**. There are no critical gaps that would create immediate regulatory sanction risk or material compliance breach. However, the two high-risk gaps (DPIA, Partner Reliance) represent significant compliance exposure that requires management attention.

In practical terms, this means: if a regulator inspected tomorrow, they would likely find issues to comment on, but these would be "areas for improvement" rather than enforcement actions. However, if the bank is planning any significant transformation of the onboarding process, these gaps need to be closed first—regulators expect enhanced controls before approving new approaches.

The medium-risk gaps (ongoing monitoring handover, breach controls) are operational rather than fundamental. They represent areas where documentation doesn't fully reflect practice, rather than areas where practice is deficient.

| Risk Level | Gap Count | Key Areas Affected | Remediation Urgency |
|------------|-----------|-------------------|---------------------|
| Critical | 0 | - | Immediate |
| High | 2 | Data Protection (DPIA), AML (Partner Reliance) | 30 days |
| Medium | 2 | Ongoing Monitoring, Breach Response | 90 days |
| Low | 2 | Retention Policy, Withdrawal Process | Next review cycle |

### 3.3 Remediation Needs

Remediation efforts should focus first on the two high-risk gaps, both of which can be closed with reasonable effort. The DPIA requires DPO engagement but is a standard exercise. The Third Party Reliance framework requires Compliance effort but templates exist from industry guidance.

Medium-priority items can be addressed through documentation updates rather than process changes. The low-priority items should be included in the next annual compliance review rather than consuming immediate resources.

| GAP# | Remediation Action | Owner | Priority | Target Completion |
|------|-------------------|-------|----------|-------------------|
| GAP-COB-003 | Commission and complete DPIA for Client Onboarding process | Data Protection Officer | High | 30 days |
| GAP-COB-006 | Implement Third Party Reliance framework for partner channels | Compliance Officer | High | 30 days |
| GAP-COB-001 | Document formal handover to AML Operations with risk rating transfer | Compliance Officer | Medium | 90 days |
| GAP-COB-002 | Add breach detection checkpoint with escalation to DPO | Data Protection Officer | Medium | 90 days |
| GAP-COB-004 | Document retention policy with GDPR Article 17 exemption justification | Data Protection Officer | Low | Next cycle |
| GAP-COB-005 | Document withdrawal process and add to Welcome Pack | Operations Manager | Low | Next cycle |

---

## 4. Control Effectiveness Assessment

> **Section Confidence:** MEDIUM | **Basis:** Combination of Q3 2024 audit results and operational observation

### 4.1 Control Strengths

The Client Onboarding control framework demonstrates strong overall effectiveness, with 13 of 16 controls (81%) rated as Effective or Highly Effective. The most effective controls share common characteristics: they are automated or semi-automated, have clear single ownership, and produce complete audit evidence.

A clear pattern emerges: **automated controls outperform manual controls**. The four fully automated controls (SCA, PEP screening, bureau check, consent capture) all achieve ratings of 4.4 or higher. This is not surprising—automation removes human variability and ensures consistent execution. The implication for transformation is clear: automation investments in control execution will improve effectiveness.

The KYC control cluster (CP-COB-001 through CP-COB-009) is particularly strong, reflecting the investment the bank has made in AML compliance. The combination of Jumio for document verification, World-Check for screening, and Fenergo for case management provides a solid technical foundation. Human judgment is still required, but it's supported by effective tooling.

| CP# | Control Name | Effectiveness Rating | Key Strength |
|-----|--------------|---------------------|--------------|
| CP-COB-004 | Strong Customer Authentication | 5.0 (Highly Effective) | Fully automated, system-enforced, no bypass |
| CP-COB-003 | Data Protection Consent | 4.8 (Highly Effective) | Embedded in application, system blocks without consent |
| CP-COB-010 | Credit Bureau Check | 4.8 (Highly Effective) | Automated pull, complete evidence |
| CP-COB-001 | Customer Identification | 4.6 (Highly Effective) | Jumio automation, comprehensive case records |
| CP-COB-009 | EDD Escalation | 4.6 (Highly Effective) | Clear Compliance ownership, documented decisions |
| CP-COB-012 | Credit Approval Authority | 4.6 (Highly Effective) | System-enforced limits, cannot override |
| CP-COB-014 | Four-Eyes Account Creation | 4.6 (Highly Effective) | T24 maker-checker enforcement |
| CP-COB-007 | PEP & Sanctions Screening | 4.4 (Effective) | Automated, complete logs |
| CP-COB-008 | Customer Risk Assessment | 4.4 (Effective) | Required for all cases, clear methodology |
| CP-COB-011 | Creditworthiness Assessment | 4.4 (Effective) | Scorecard-driven, documented decisions |
| CP-COB-016 | Quality Sampling Review | 4.4 (Effective) | Consistent 20% sample, findings actioned |
| CP-COB-002 | Beneficial Owner Identification | 3.8 (Effective) | Generally effective, complex cases challenging |
| CP-COB-006 | Document Completeness Check | 3.8 (Effective) | Mostly effective, some leakage |

#### Highlight: CP-COB-004 Strong Customer Authentication

The SCA control is the gold standard for control effectiveness in this process. It achieves a perfect 5.0 rating because it is fully automated with no manual override capability. The control cannot be bypassed, produces complete logs, and operates in real-time. This demonstrates what's possible when controls are designed into systems rather than bolted on as manual checks. Other controls should aspire to this level of automation where feasible.

#### Highlight: CP-COB-009 EDD Escalation

The EDD escalation control demonstrates that manual controls can be highly effective when they have clear ownership, documented triggers, and formal sign-off requirements. The Compliance Officer owns the decision, the triggers are defined, and every escalation produces a documented decision. This is the model for effective manual controls: clear accountability, defined criteria, complete evidence.

### 4.2 Control Weaknesses

Three controls fall below the Effective threshold, representing areas where the bank's control framework needs strengthening. These weaknesses share a common theme: they are manual controls that rely on human execution under operational pressure, with inadequate systematic support.

The weakest control—Welcome Call Quality at 2.2—is not just a control effectiveness issue but a fundamental process design issue. The control is trying to achieve something (verify client understanding through a phone call) that the process design makes difficult (clients are hard to reach). This suggests the control objective is correct but the control mechanism is wrong.

The other two weak controls (Product Disclosure at 2.8, Account Configuration Verification at 2.8) suffer from similar issues: they are manual checks performed under time pressure with inadequate tooling support. Staff know what they should do, but operational reality makes consistent execution difficult.

| CP# | Control Name | Rating | Key Issue | Dimension Most Affected |
|-----|--------------|--------|-----------|------------------------|
| CP-COB-015 | Welcome Call Quality | 2.2 (Ineffective) | 33% first-attempt success, many clients unreached | Consistency (2/5) |
| CP-COB-005 | Product Disclosure | 2.8 (Partially Effective) | Call completion variable, no understanding verification | Detection (2/5) |
| CP-COB-013 | Account Configuration Verification | 2.8 (Partially Effective) | Manual verification rushed, checklist compliance poor | Evidence Quality (2/5) |

#### CP-COB-015: Welcome Call Quality - Fundamental Effectiveness Issue

This control is designed to verify that clients have received their credentials and understand how to use their account. In practice, only 33% of welcome calls connect on the first attempt, and many clients are never reached. The control is not achieving its objective.

**Root Cause:** The control mechanism (phone call) doesn't match modern client behavior. Business owners are busy and don't answer unknown numbers. The process schedules calls without client input on preferred times.

**Impact:** Clients may activate accounts without understanding key features. Disclosure requirements may not be fully met. Client experience suffers when calls come at inconvenient times.

**Improvement Approach:** Replace or supplement phone calls with self-service options: video walkthrough, in-app onboarding wizard, scheduled callback booking. The control objective is valid; the mechanism needs to change.

#### CP-COB-013: Account Configuration Verification - Process Pressure Issue

This control is supposed to verify that account setup matches the application before going live. In practice, checklist completion is inconsistent, and the verification is often rushed at end of day when Operations Officers are under pressure to clear queues.

**Root Cause:** Manual verification without system support. No forcing function to ensure checklist completion. Time pressure prioritizes throughput over verification.

**Impact:** Configuration errors may reach clients, requiring post-activation correction. Operational risk from mismatched products or limits.

**Improvement Approach:** Implement system-assisted verification that compares T24 setup to application data automatically, flagging discrepancies for human review. Make checklist completion a gate for account activation.

#### CP-COB-005: Product Disclosure - Inconsistent Execution

Product disclosure control is partially effective: the Welcome Pack is always sent (automated), but the verification component (welcome call) is weak. There's no mechanism to confirm the client received and understood the disclosure.

**Root Cause:** Disclosure is treated as a push activity (send documents) rather than a verification activity (confirm understanding). The welcome call that should verify understanding has low completion rates.

**Impact:** Regulatory disclosure requirements met in letter (documents sent) but not necessarily in spirit (client understood). Consumer protection risk if clients complain about undisclosed fees or terms.

**Improvement Approach:** Add acknowledgment mechanism (in-app confirmation of T&Cs review), implement key terms video, track disclosure receipt and acknowledgment as distinct metrics.

### 4.3 Improvement Opportunities

Improvement efforts should focus on three themes: (1) fixing the fundamentally broken welcome call control, (2) adding system support to manual verification controls, and (3) considering automation for high-frequency manual controls.

The improvement priorities balance compliance risk, operational efficiency, and implementation effort. The welcome call issue is highest priority because it represents both a compliance risk (disclosure) and a client experience failure.

**Priority 1: Redesign Client Communication & Verification (CP-COB-005, CP-COB-015)**
- Replace phone calls with multi-channel approach: self-service scheduling, video content, in-app onboarding
- Implement disclosure acknowledgment tracking
- Expected benefit: Improve completion from 33% to 80%+, better client experience
- Effort: Medium (process redesign + some development)

**Priority 2: Automate Account Configuration Verification (CP-COB-013)**
- Build system comparison between application data and T24 setup
- Auto-flag discrepancies for human review
- Make checklist a gate for activation
- Expected benefit: Reduce configuration errors, improve evidence quality
- Effort: Medium (system development)

**Priority 3: Reduce World-Check False Positives (CP-COB-007)**
- Tune screening rules to reduce 40% false positive rate
- Implement name matching optimization
- Expected benefit: Reduce KYC analyst workload by 20-30%
- Effort: Low-Medium (configuration + testing)

**Priority 4: Enhance UBO Tracing for Complex Structures (CP-COB-002)**
- Implement automated ownership tracing tools
- Subscribe to corporate registry APIs
- Expected benefit: Improve detection of complex structures, reduce manual effort
- Effort: Medium-High (vendor selection + integration)

---

## 5. Audit Trail Requirements

> **Section Confidence:** HIGH | **Basis:** Evidence capture verified during Q3 2024 audit

The audit trail is the evidence that controls were performed. As the saying goes in compliance: "controls without evidence are unverifiable." If an auditor or regulator asks to demonstrate that a control operates effectively, the organization must be able to produce evidence—who did what, when, and what was the outcome. This section documents what evidence is captured, where it's stored, and how long it's retained.

The Client Onboarding process has a generally strong audit trail, particularly for automated controls that produce complete, timestamped logs automatically. The KYC and credit assessment phases benefit from dedicated systems (Fenergo, CDS) that were designed with audit requirements in mind. The weaker areas are manual controls where evidence capture depends on staff completing checklists and entering case notes—these produce less consistent and complete evidence.

For audit readiness, the process is well-positioned to respond to regulatory examination. Most evidence can be retrieved within hours for specific cases. The main challenge is aggregated reporting—producing statistics on control performance across all cases requires IT support for data extraction.

| ATR# | Control (CP#) | Data Elements Captured | Retention Period | Storage System | Completeness |
|------|---------------|------------------------|------------------|----------------|--------------|
| ATR-COB-001 | CP-COB-001 | ID document images, Jumio verification score, analyst ID, timestamp, verification outcome | 7 years post-relationship | Fenergo, DMS | Complete |
| ATR-COB-002 | CP-COB-002 | UBO declaration, ownership structure, verification records for each UBO | 7 years post-relationship | Fenergo, DMS | Complete |
| ATR-COB-003 | CP-COB-003 | Consent checkbox state, timestamp, privacy notice version, client IP | 6 years post-relationship | CRM | Complete |
| ATR-COB-004 | CP-COB-004 | Authentication method, device ID, timestamp, success/failure, session ID | 5 years | CBS, Security logs | Complete |
| ATR-COB-005 | CP-COB-005 | Email sent timestamp, document list, call attempt log, call notes | 6 years post-relationship | CRM, Email archive | Partial |
| ATR-COB-006 | CP-COB-006 | Checklist completion, missing items, rejection code, operator ID | 7 years post-relationship | OWS | Complete |
| ATR-COB-007 | CP-COB-007 | World-Check query, results, match/no-match, clearance notes if false positive | 7 years post-relationship | World-Check, Fenergo | Complete |
| ATR-COB-008 | CP-COB-008 | Risk factors assessed, risk score, risk rating, analyst justification | 7 years post-relationship | Fenergo | Complete |
| ATR-COB-009 | CP-COB-009 | EDD trigger, review notes, Compliance decision, sign-off timestamp | 7 years post-relationship | Fenergo | Complete |
| ATR-COB-010 | CP-COB-010 | Bureau reference, pull timestamp, bureau data snapshot | 7 years | CDS, Bureau archive | Complete |
| ATR-COB-011 | CP-COB-011 | Financial inputs, scorecard version, score output, analyst override (if any) | 7 years | CDS | Complete |
| ATR-COB-012 | CP-COB-012 | Approval authority level, approver ID, timestamp, exposure amount | 7 years | CDS | Complete |
| ATR-COB-013 | CP-COB-013 | Checklist completion (if done), screenshots (if captured) | 10 years | OWS, Manual files | Partial |
| ATR-COB-014 | CP-COB-014 | Maker ID, Checker ID, timestamps, T24 transaction reference | 10 years | CBS (T24) | Complete |
| ATR-COB-015 | CP-COB-015 | Call attempt log, call notes (if call completed), RM ID | 6 years | CRM | Partial |
| ATR-COB-016 | CP-COB-016 | Sample selection, review form, findings, feedback sent flag | 3 years | QMS | Complete |

### Audit Readiness Assessment

The process is **audit-ready** with evidence accessible for most controls within hours of request. The systems architecture supports compliance—Fenergo, CDS, and T24 were designed to produce audit trails. Access is available to Compliance, Internal Audit, and External Audit teams through standard system access.

**Strong Areas:**
- KYC evidence (CP-COB-001 through CP-COB-009): Complete, centralized in Fenergo
- Credit evidence (CP-COB-010 through CP-COB-012): Complete, in CDS with bureau archive
- Authentication logs (CP-COB-004): Complete, immutable security logs

**Gap Areas Requiring Attention:**
- **ATR-COB-005 (Product Disclosure):** Call completion evidence is inconsistent. When calls don't connect, there's limited evidence of attempts beyond system logs.
- **ATR-COB-013 (Account Configuration):** Checklist completion is not enforced, so evidence is missing for some cases. No system-generated verification evidence.
- **ATR-COB-015 (Welcome Call):** Call notes are inconsistent in detail. Recordings exist but are not systematically linked to cases.

**Recommendation:** For the three partial audit trails, implement system enforcement to ensure evidence is captured before process can proceed. This is particularly important for CP-COB-013 where checklist should gate account activation.

---

## 6. Risk & Compliance Matrix

> **Section Confidence:** HIGH | **Basis:** Risk assessment aligned with enterprise risk framework

The Risk & Compliance Matrix maps the key risks in the Client Onboarding process to the regulations that govern them and the controls that mitigate them. This provides a complete view of how well the control framework addresses the risk landscape.

The matrix uses standard risk assessment methodology: inherent risk represents the risk level without any controls in place, while residual risk represents the remaining risk after controls are applied. The goal is to reduce residual risk to acceptable levels—not to eliminate risk entirely, which would be prohibitively expensive and operationally impractical.

For readers unfamiliar with risk matrices, the key insight is this: even with good controls, some risk always remains. The question is whether the residual risk is within the organization's risk appetite. For this process, most risks are reduced to Low or Medium residual levels, which is appropriate for a well-controlled banking process. The areas where residual risk remains Medium warrant ongoing monitoring.

| RCM# | Risk | Category | Regulation (REG#) | Control (CP#) | Inherent Risk | Residual Risk | Status |
|------|------|----------|-------------------|---------------|---------------|---------------|--------|
| RCM-COB-001 | Money Laundering / Terrorist Financing | AML | REG-COB-001, REG-COB-002 | CP-COB-001, CP-COB-002, CP-COB-007, CP-COB-008, CP-COB-009 | Critical | Low | Controlled |
| RCM-COB-002 | Sanctions Breach | AML | REG-COB-001 | CP-COB-007 | Critical | Low | Controlled |
| RCM-COB-003 | Data Protection Breach | Privacy | REG-COB-003 | CP-COB-003, CP-COB-004 | High | Low | Controlled |
| RCM-COB-004 | Credit Loss from Default | Credit | REG-COB-005, REG-COB-006 | CP-COB-010, CP-COB-011, CP-COB-012 | High | Medium | Controlled |
| RCM-COB-005 | Consumer Detriment | Conduct | REG-COB-006 | CP-COB-005, CP-COB-015 | Medium | Medium | Monitored |
| RCM-COB-006 | Fraud / Identity Theft | Fraud | REG-COB-001 | CP-COB-001, CP-COB-004 | High | Low | Controlled |
| RCM-COB-007 | Operational Error | Operational | Internal Policy | CP-COB-013, CP-COB-014, CP-COB-016 | Medium | Medium | Monitored |
| RCM-COB-008 | Regulatory Sanction | Compliance | All REGs | All CPs | High | Low | Controlled |

### Risk Category Analysis

**AML Risk (RCM-COB-001, RCM-COB-002):** The inherent risk of money laundering and sanctions breach is Critical given the nature of banking. The comprehensive CDD framework—including identity verification, UBO identification, PEP/sanctions screening, and risk assessment—reduces this to Low residual risk. The control cluster is deep and layered, providing defense in depth.

**Privacy Risk (RCM-COB-003):** Data protection breach risk is managed through consent controls and authentication. The inherent High risk is reduced to Low through systematic consent capture and strong authentication. The DPIA gap (GAP-COB-003) should be closed to ensure ongoing risk management.

**Credit Risk (RCM-COB-004):** Credit loss risk remains at Medium residual level, which is appropriate—the bank accepts some credit risk in exchange for revenue. The controls ensure credit is extended responsibly, but some default is expected and provisioned for.

**Conduct Risk (RCM-COB-005):** Consumer detriment risk from inadequate disclosure remains at Medium residual level. This reflects the weak effectiveness of the welcome call control (CP-COB-015). This is the highest residual risk area and warrants improvement focus.

**Operational Risk (RCM-COB-007):** Account configuration and operational errors remain at Medium residual level due to the partial effectiveness of manual verification controls. System automation would reduce this further.

### Residual Risk Summary

| Risk Category | Inherent Risk (Avg) | Residual Risk (Avg) | Status |
|---------------|---------------------|---------------------|--------|
| AML/Sanctions | Critical | Low | ✅ Controlled |
| Privacy | High | Low | ✅ Controlled |
| Credit | High | Medium | ⚠️ Monitored |
| Conduct | Medium | Medium | ⚠️ Monitored |
| Fraud | High | Low | ✅ Controlled |
| Operational | Medium | Medium | ⚠️ Monitored |
| Compliance | High | Low | ✅ Controlled |

**Overall Assessment:** The control framework effectively reduces most risks to acceptable levels. The three areas with Medium residual risk (Credit, Conduct, Operational) are either inherently acceptable (Credit) or targeted for improvement (Conduct, Operational).

---

## 7. Regulatory Change Impact

> **Section Confidence:** MEDIUM | **Basis:** Based on current regulatory calendar, subject to change

Regulatory change is constant in banking. This section identifies upcoming regulatory changes that will impact the Client Onboarding process and assesses readiness to comply. Proactive tracking of regulatory change is essential to avoid scrambled implementations and potential non-compliance.

The EU regulatory landscape is particularly active in the AML and digital finance spaces. Several significant changes are on the horizon that will require process and control updates. The organization should budget for compliance implementation projects related to these changes.

| RCI# | Regulation (REG#) | Change Description | Effective Date | Impact Level | Status |
|------|-------------------|-------------------|----------------|--------------|--------|
| RCI-COB-001 | REG-COB-001 | AMLD Package / AMLR - New EU AML Regulation replacing directives | 2027 | High | Planning |
| RCI-COB-002 | REG-COB-001 | New EU AML Authority (AMLA) - Centralized supervision | 2026 | Medium | Monitoring |
| RCI-COB-003 | REG-COB-003 | AI Act - Regulation of AI systems including KYC automation | 2025-2026 | Medium | Assessment |
| RCI-COB-004 | REG-COB-004 | PSD3/PSR - Payment Services Regulation updates | 2026 | Medium | Monitoring |
| RCI-COB-005 | REG-COB-003 | eIDAS 2.0 - European Digital Identity Wallet | 2026 | High | Planning |

### Key Regulatory Changes

#### RCI-COB-001: AMLR (AML Regulation)

The most significant upcoming change is the shift from AML Directives to a directly applicable EU Regulation. This will harmonize AML requirements across the EU, potentially requiring changes to CDD procedures, UBO identification thresholds, and screening approaches.

**Impact on Process:** May require updates to CP-COB-001, CP-COB-002, CP-COB-007, CP-COB-008. New requirements for crypto-asset customers (not currently in scope). Enhanced requirements for third-party reliance (relevant to GAP-COB-006).

**Readiness:** Planning phase. Gap analysis against draft regulation text in progress.

#### RCI-COB-005: eIDAS 2.0 - Digital Identity Wallet

The European Digital Identity Wallet will enable clients to verify their identity digitally using a government-backed credential. This presents both an opportunity (faster, higher-assurance verification) and a compliance requirement (must accept wallet credentials when mandated).

**Impact on Process:** Major opportunity to transform CP-COB-001 (Customer Identification). Could enable instant, high-assurance digital onboarding. System integration required.

**Readiness:** Early assessment. Technology evaluation for wallet integration should begin.

#### RCI-COB-003: AI Act

If the bank uses AI in any KYC processes (e.g., document verification, risk scoring), the AI Act will impose requirements on transparency, human oversight, and system validation. The current Jumio integration may be in scope.

**Impact on Process:** May require documentation of AI systems used in CP-COB-001 verification. Risk assessment for AI systems. Human oversight requirements for high-risk AI decisions.

**Readiness:** Assessment needed of current AI/ML usage in onboarding systems.

### Horizon Scanning

The regulatory horizon beyond 2027 includes:
- **Open Banking evolution** - Potential requirements for third-party data sharing
- **Sustainable finance** - ESG criteria in client assessment
- **Digital operational resilience** - DORA requirements for third-party systems

**Recommendation:** Establish quarterly regulatory change review to track developments and assess impact on the onboarding process.

---

## 8. Open Audit Findings

> **Section Confidence:** HIGH | **Basis:** Current audit tracker as of December 2025

Open audit findings represent known control weaknesses that have been formally identified through internal or external audit and are in the process of remediation. Tracking these findings ensures visibility and accountability for closure.

The Client Onboarding process currently has **3 open audit findings**, all identified in the Q3 2024 Internal Audit review. None are rated as Critical. Two are rated Medium and one is Low. All have assigned owners and remediation plans in progress.

| OAF# | Finding | Source | Date Issued | Severity | Affected Control (CP#) | Status | Target Closure |
|------|---------|--------|-------------|----------|------------------------|--------|----------------|
| OAF-COB-001 | Welcome call completion rate below target | Internal Audit Q3 2024 | 2024-09-15 | Medium | CP-COB-015 | In Progress | Q1 2025 |
| OAF-COB-002 | Inconsistent quality check documentation | Internal Audit Q3 2024 | 2024-09-15 | Low | CP-COB-016 | In Progress | Q4 2024 |
| OAF-COB-003 | Partner channel due diligence gaps | Internal Audit Q3 2024 | 2024-09-15 | Medium | CP-COB-006 | Planning | Q1 2025 |

### Finding Details

#### OAF-COB-001: Welcome Call Completion Rate

**Finding:** Internal Audit identified that the welcome call control (CP-COB-015) is not operating effectively. First-attempt success rate is 33%, and many clients never receive the intended call. This creates a gap in the disclosure verification process.

**Root Cause:** Process design issue—phone calls are scheduled without client input, and business clients are difficult to reach by phone.

**Remediation Plan:** Redesign client communication approach to include self-service scheduling, video alternatives, and in-app onboarding. Project initiated with target completion Q1 2025.

**Status:** In Progress. Business requirements gathered, vendor evaluation underway.

#### OAF-COB-002: Quality Check Documentation

**Finding:** Quality sampling review (CP-COB-016) is being performed, but documentation of findings and feedback delivery is inconsistent. Some review forms are incomplete.

**Root Cause:** Manual process without system enforcement. Quality review forms are paper-based.

**Remediation Plan:** Migrate quality review to QMS system with mandatory field completion.

**Status:** In Progress. QMS configuration underway, target completion Q4 2024.

#### OAF-COB-003: Partner Channel Due Diligence

**Finding:** Applications received through partner channels (accountants, solicitors) proceed without formal Third Party Reliance assessment. No documented due diligence on partner AML procedures.

**Root Cause:** Partner channel was established without full regulatory assessment. Gap in Third Party Reliance framework.

**Remediation Plan:** Implement Third Party Reliance framework including partner due diligence questionnaire and formal reliance agreements.

**Status:** Planning. Framework design in progress, target completion Q1 2025.

### Remediation Tracking

All findings are tracked in the enterprise audit management system with monthly progress reporting to the Audit Committee. No findings are overdue. The Q4 2024 target for OAF-COB-002 is on track for closure.

---

## 9. Control Improvement Recommendations

> **Section Confidence:** HIGH | **Basis:** Consolidated from gap analysis, effectiveness assessment, and audit findings

This section consolidates all improvement recommendations identified throughout the compliance assessment. Recommendations are prioritized based on compliance risk, operational impact, and alignment with strategic transformation initiatives.

The recommendations fall into three categories: (1) **Gap Closure** - addressing identified compliance gaps, (2) **Control Strengthening** - improving effectiveness of existing controls, and (3) **Control Optimization** - opportunities for automation and efficiency gains. All recommendations should be incorporated into the organization's compliance and transformation roadmaps.

| CIR# | Control (CP#) | Recommendation | Priority | Effort | Expected Benefit |
|------|---------------|----------------|----------|--------|------------------|
| CIR-COB-001 | GAP-COB-003 | Complete DPIA for Client Onboarding process | Critical | Low | Regulatory compliance, transformation enabler |
| CIR-COB-002 | GAP-COB-006 | Implement Third Party Reliance framework | Critical | Medium | AML compliance, liability protection |
| CIR-COB-003 | CP-COB-015 | Redesign welcome call with multi-channel approach | High | Medium | Improve completion 33%→80%, better CX |
| CIR-COB-004 | CP-COB-013 | Automate account configuration verification | High | Medium | Reduce errors, complete audit trail |
| CIR-COB-005 | CP-COB-005 | Add disclosure acknowledgment tracking | High | Low | Evidence of client understanding |
| CIR-COB-006 | GAP-COB-001 | Document AML Operations handover | Medium | Low | Complete lifecycle coverage |
| CIR-COB-007 | CP-COB-007 | Tune World-Check to reduce false positives | Medium | Low-Medium | 20-30% KYC workload reduction |
| CIR-COB-008 | CP-COB-002 | Implement automated UBO tracing | Medium | Medium-High | Better complex structure detection |
| CIR-COB-009 | GAP-COB-002 | Add breach detection control for onboarding | Low | Low | Early breach identification |
| CIR-COB-010 | GAP-COB-004 | Document GDPR/AML retention conflict resolution | Low | Low | Defensible retention policy |

### Critical Priority

**CIR-COB-001: Complete DPIA for Client Onboarding**
- **What:** Commission Data Protection Impact Assessment for the process
- **Why:** GDPR requirement for high-risk processing. Blocks transformation initiatives.
- **Owner:** Data Protection Officer
- **Target:** 30 days
- **Effort:** Low (internal DPO effort or €5-10k external)

**CIR-COB-002: Third Party Reliance Framework**
- **What:** Implement due diligence and formal agreements for partner channel referrals
- **Why:** AMLD 5 requirement. Current gap exposes bank to AML liability.
- **Owner:** Compliance Officer
- **Target:** 30 days
- **Effort:** Medium (framework design, partner engagement, legal agreements)

### High Priority

**CIR-COB-003: Redesign Client Communication**
- **What:** Replace phone-only welcome calls with multi-channel approach including self-service scheduling, video content, in-app onboarding
- **Why:** Current control is ineffective (33% completion). Addresses OAF-COB-001.
- **Owner:** Operations Manager + Digital Team
- **Target:** Q1 2025
- **Effort:** Medium (process redesign, some development)
- **Expected Benefit:** Completion rate 33%→80%+, improved client experience

**CIR-COB-004: Automate Account Configuration Verification**
- **What:** Build system comparison between application data and T24 account setup, flagging discrepancies automatically
- **Why:** Manual verification is inconsistent under time pressure. Evidence gaps.
- **Owner:** IT + Operations
- **Target:** Q2 2025
- **Effort:** Medium (system development)
- **Expected Benefit:** Reduced configuration errors, complete audit trail

**CIR-COB-005: Disclosure Acknowledgment Tracking**
- **What:** Implement in-app confirmation that client has reviewed key terms
- **Why:** Strengthens evidence that disclosure requirement was met
- **Owner:** Digital Team
- **Target:** Q1 2025
- **Effort:** Low (app update)

### Medium Priority

**CIR-COB-006:** Document formal handover from Onboarding to AML Operations
**CIR-COB-007:** Tune World-Check screening rules to reduce 40% false positive rate
**CIR-COB-008:** Implement automated UBO tracing for complex ownership structures

### Low Priority

**CIR-COB-009:** Add breach detection checkpoint with escalation to DPO
**CIR-COB-010:** Document retention policy with GDPR Article 17 exemption justification

### Transformation Considerations

Any significant transformation of the Client Onboarding process should consider the following control implications:

**Non-Negotiables (Must be preserved or enhanced):**
- Segregation of duties (maker-checker) for account creation
- AML screening before account activation
- Audit trail completeness for all control activities
- Four-eyes principle for high-risk decisions

**Automation Opportunities:**
- Document verification (Jumio enhancement, AI document reading)
- UBO tracing (corporate registry APIs)
- Risk scoring (enhanced risk models)
- Account configuration verification (system comparison)

**Regulatory Dependencies:**
- eIDAS 2.0 wallet integration (2026) - major opportunity for digital onboarding
- AMLR (2027) - may change CDD requirements, design for flexibility
- AI Act (2025-2026) - document AI usage, ensure human oversight

**Transformation Enablers:**
- Close DPIA gap (CIR-COB-001) before major changes
- Close Partner Reliance gap (CIR-COB-002) before expanding partner channel
- Strengthen weak controls before automating them

---

## Change Log

| Date | Contributor | Role | Changes |
|------|-------------|------|---------|
| 2025-12-10 | Markus | SME | Initial documentation |

---

_Generated by ProcessMiner Control Analyst_
_Document ID: COB-003-compliance_
