# Control Points & Compliance: Client Onboarding process

**Process ID:** COB-002
**Document Type:** Control Point Detail Analysis
**Last Updated:** 2025-12-09
**Status:** COMPLETE
**Related Document:** [AS-IS Process Documentation](./as-is-process-documentation.md)

---

## Executive Summary

The Client Onboarding process has 8 identified control points ensuring regulatory compliance and operational integrity.

**Regulatory Controls (5):**
- KYC Verification (CP-COB-001) and Document Authenticity (CP-COB-006) ensure client identity is properly verified per KYC regulations
- AML Screening (CP-COB-002) and PEP Enhanced Due Diligence (CP-COB-007) address anti-money laundering requirements and FATF guidelines
- Risk Rating Approval (CP-COB-003) ensures risk-based approach per regulatory expectations

**Internal Controls (3):**
- Four-Eyes Account Setup (CP-COB-004) enforces segregation of duties for account creation
- Final Onboarding Approval (CP-COB-005) provides management sign-off before client activation
- Audit Trail Logging (CP-COB-008) ensures complete traceability for audit and regulatory inquiries

**Control Type Distribution:**
- PREVENTIVE: 6 controls (75%)
- DETECTIVE: 2 controls (25%)
- CORRECTIVE: 0 controls

All controls trace to specific regulatory requirements or internal policies, ensuring banking compliance is maintained throughout the onboarding process.

---

## Control Point Summary Table

> **Quick Reference:** All identified control points with compliance mapping at a glance. Click any CP# for full details below.

| CP# | Control Name | Type | Regulation/Policy | Process Step | Effectiveness |
|-----|--------------|------|-------------------|--------------|---------------|
| CP-COB-001 | KYC Verification Check | PREVENTIVE | AML/KYC Regulations | PS-COB-003 | HIGH |
| CP-COB-002 | AML/Sanctions Screening | PREVENTIVE | AML Regulations | PS-COB-004 | HIGH |
| CP-COB-003 | Risk Rating Approval | PREVENTIVE | Internal Risk Policy | PS-COB-005 | MEDIUM |
| CP-COB-004 | Four-Eyes Account Setup | DETECTIVE | Internal Policy - SoD | PS-COB-006 | HIGH |
| CP-COB-005 | Final Onboarding Approval | PREVENTIVE | Internal Policy | PS-COB-007 | MEDIUM |
| CP-COB-006 | Document Authenticity Check | PREVENTIVE | KYC Regulations | PS-COB-003 | MEDIUM |
| CP-COB-007 | PEP Enhanced Due Diligence | PREVENTIVE | AML / FATF Guidelines | PS-COB-004, PS-COB-005 | HIGH |
| CP-COB-008 | Audit Trail Logging | DETECTIVE | Data Protection / Audit | All Steps | HIGH |

---

## Control Statistics

| Metric | Value |
|--------|-------|
| Total Control Points | 8 |
| Regulatory Controls | 5 |
| Internal Policy Controls | 3 |
| PREVENTIVE Controls | 6 |
| DETECTIVE Controls | 2 |
| CORRECTIVE Controls | 0 |
| HIGH Effectiveness | 5 |
| MEDIUM Effectiveness | 3 |

---

## Regulatory Coverage Matrix

> *Mapping of regulations to controls — ensures complete compliance coverage*

| Regulation | Requirement | Control(s) | Coverage Status |
|------------|-------------|------------|-----------------|
| AML/KYC Regulations | Verify client identity | CP-COB-001, CP-COB-006 | COVERED |
| AML Regulations | Screen against sanctions | CP-COB-002 | COVERED |
| AML Regulations | PEP identification | CP-COB-007 | COVERED |
| FATF Guidelines | Enhanced due diligence for PEPs | CP-COB-007 | COVERED |
| Internal Risk Policy | Risk-based approach | CP-COB-003 | COVERED |
| Segregation of Duties | Four-eyes principle | CP-COB-004 | COVERED |
| Data Protection | Audit trail | CP-COB-008 | COVERED |
| Internal Policy | Management approval | CP-COB-005 | COVERED |

---

## Control Type Breakdown

| Type | Count | Controls | Effectiveness Avg |
|------|-------|----------|-------------------|
| PREVENTIVE | 6 | CP-COB-001, 002, 003, 005, 006, 007 | HIGH |
| DETECTIVE | 2 | CP-COB-004, 008 | HIGH |
| CORRECTIVE | 0 | - | N/A |

---

## Detailed Control Point Analysis

### CP-COB-001: KYC Verification Check

| Attribute | Detail |
|-----------|--------|
| **Control ID** | CP-COB-001 |
| **Control Name** | KYC Verification Check |
| **Control Type** | PREVENTIVE |
| **Regulation/Policy** | AML/KYC Regulations |
| **Process Step** | PS-COB-003 (KYC Verification) |
| **Effectiveness** | HIGH |
| **Confidence** | HIGH |

**Description:**
Verify client identity against provided documentation and regulatory requirements. This is a core regulatory control ensuring the bank knows who it is doing business with.

**Control Objective:**
Prevent onboarding of clients whose identity cannot be adequately verified, protecting the bank from fraud and regulatory non-compliance.

**Control Activities:**
1. Review submitted identity documents
2. Verify document validity (not expired, matches requirements)
3. Cross-reference information across documents
4. Confirm identity through verification services
5. Document verification outcome

**Evidence/Documentation:**
- Completed KYC verification checklist
- Copies of verified documents in DMS
- Verification outcome recorded in KYC Platform

**Testing Approach:**
- Sample testing of completed KYC files
- Verify all required documents present
- Confirm verification steps completed

---

### CP-COB-002: AML/Sanctions Screening

| Attribute | Detail |
|-----------|--------|
| **Control ID** | CP-COB-002 |
| **Control Name** | AML/Sanctions Screening |
| **Control Type** | PREVENTIVE |
| **Regulation/Policy** | AML Regulations |
| **Process Step** | PS-COB-004 (AML Screening) |
| **Effectiveness** | HIGH |
| **Confidence** | HIGH |

**Description:**
Screen client against global sanctions lists, PEP databases, and adverse media to identify potential money laundering or sanctions risks.

**Control Objective:**
Prevent onboarding of sanctioned individuals/entities and identify potential money laundering risks before establishing a banking relationship.

**Control Activities:**
1. Screen client name against sanctions lists (OFAC, EU, UN, local)
2. Screen against PEP databases
3. Screen against adverse media sources
4. Review any hits for relevance (true positive vs false positive)
5. Escalate confirmed hits per exception procedure (EX-COB-003)

**Evidence/Documentation:**
- Screening results report from KYC Platform
- Hit resolution documentation (if applicable)
- Escalation records for confirmed hits

**Testing Approach:**
- Verify all clients screened before onboarding
- Sample test hit resolution decisions
- Confirm escalation procedures followed for confirmed hits

**Related Exceptions:** EX-COB-003 (AML/Sanctions Hit)

---

### CP-COB-003: Risk Rating Approval

| Attribute | Detail |
|-----------|--------|
| **Control ID** | CP-COB-003 |
| **Control Name** | Risk Rating Approval |
| **Control Type** | PREVENTIVE |
| **Regulation/Policy** | Internal Risk Policy |
| **Process Step** | PS-COB-005 (Risk Assessment) |
| **Effectiveness** | MEDIUM |
| **Confidence** | HIGH |

**Description:**
Assign and approve risk rating based on client profile and due diligence findings. Ensures appropriate level of ongoing monitoring is applied based on risk.

**Control Objective:**
Implement risk-based approach to client onboarding, ensuring higher-risk clients receive appropriate scrutiny and approval.

**Control Activities:**
1. Assess client against risk factors (industry, geography, structure, etc.)
2. Assign risk rating (Low, Medium, High)
3. Document rationale for rating
4. High-risk ratings require senior approval (see EX-COB-004)
5. Risk rating determines ongoing monitoring requirements

**Evidence/Documentation:**
- Risk assessment form/record in KYC Platform
- Approval record for high-risk ratings
- Documentation of rating rationale

**Testing Approach:**
- Sample review of risk ratings vs client profiles
- Verify consistency of ratings across similar clients
- Confirm senior approval obtained for high-risk ratings

**Effectiveness Note:** Rated MEDIUM due to subjectivity concerns (see PP-COB-005). Standardized scoring matrix recommended.

**Related Pain Points:** PP-COB-005 (Risk Rating Subjectivity)
**Related Exceptions:** EX-COB-004 (High-Risk Client Escalation)

---

### CP-COB-004: Four-Eyes Account Setup

| Attribute | Detail |
|-----------|--------|
| **Control ID** | CP-COB-004 |
| **Control Name** | Four-Eyes Account Setup |
| **Control Type** | DETECTIVE |
| **Regulation/Policy** | Internal Policy - Segregation of Duties |
| **Process Step** | PS-COB-006 (Account Setup) |
| **Effectiveness** | HIGH |
| **Confidence** | HIGH |

**Description:**
Require second person review/approval for account creation in Core Banking. Enforces segregation of duties to prevent errors and fraud.

**Control Objective:**
Prevent unauthorized or erroneous account creation through dual approval, reducing fraud risk and data entry errors.

**Control Activities:**
1. First operator creates account in Core Banking
2. Account marked as "pending approval"
3. Second operator (different person) reviews account details
4. Second operator approves or rejects
5. Rejections returned to first operator with reasons

**Evidence/Documentation:**
- System audit trail showing maker and checker
- Approval timestamps in Core Banking
- Rejection records (if any)

**Testing Approach:**
- Verify all accounts have different maker and checker
- Sample test accuracy of approved accounts
- Review rejection handling

---

### CP-COB-005: Final Onboarding Approval

| Attribute | Detail |
|-----------|--------|
| **Control ID** | CP-COB-005 |
| **Control Name** | Final Onboarding Approval |
| **Control Type** | PREVENTIVE |
| **Regulation/Policy** | Internal Policy |
| **Process Step** | PS-COB-007 (Product Activation) |
| **Effectiveness** | MEDIUM |
| **Confidence** | HIGH |

**Description:**
Management sign-off required before client activation and product enablement. Final checkpoint before client is fully onboarded.

**Control Objective:**
Ensure management oversight of all onboarding completions, providing final checkpoint for quality and compliance.

**Control Activities:**
1. All prior steps completed and documented
2. Onboarding Specialist prepares case for final approval
3. Manager reviews case completeness
4. Manager approves or returns for correction
5. Upon approval, products activated

**Evidence/Documentation:**
- Final approval record in system
- Manager sign-off timestamp
- Case completion checklist

**Testing Approach:**
- Verify all onboarded clients have final approval
- Sample test case completeness at approval point
- Verify manager authority levels

**Effectiveness Note:** Rated MEDIUM as effectiveness depends on thoroughness of manager review.

---

### CP-COB-006: Document Authenticity Check

| Attribute | Detail |
|-----------|--------|
| **Control ID** | CP-COB-006 |
| **Control Name** | Document Authenticity Check |
| **Control Type** | PREVENTIVE |
| **Regulation/Policy** | KYC Regulations |
| **Process Step** | PS-COB-003 (KYC Verification) |
| **Effectiveness** | MEDIUM |
| **Confidence** | HIGH |

**Description:**
Verify authenticity of submitted documents using validation tools and manual review. Prevents acceptance of fraudulent or altered documents.

**Control Objective:**
Detect and reject fraudulent, altered, or invalid documents before accepting them for KYC verification.

**Control Activities:**
1. Visual inspection of document quality
2. Check for signs of tampering or alteration
3. Verify security features (where applicable)
4. Use document validation tools (where available)
5. Reject suspicious documents and request alternatives

**Evidence/Documentation:**
- Document review notes in KYC Platform
- Rejection records for fraudulent documents
- Escalation records for suspicious cases

**Testing Approach:**
- Sample review of accepted documents
- Verify validation steps completed
- Review rejection/escalation handling

**Effectiveness Note:** Rated MEDIUM as manual review has limitations. Enhanced tooling could improve effectiveness.

**Related Exceptions:** EX-COB-002 (Failed KYC Verification)

---

### CP-COB-007: PEP Enhanced Due Diligence

| Attribute | Detail |
|-----------|--------|
| **Control ID** | CP-COB-007 |
| **Control Name** | PEP Enhanced Due Diligence |
| **Control Type** | PREVENTIVE |
| **Regulation/Policy** | AML Regulations / FATF Guidelines |
| **Process Step** | PS-COB-004 (AML Screening), PS-COB-005 (Risk Assessment) |
| **Effectiveness** | HIGH |
| **Confidence** | HIGH |

**Description:**
Enhanced due diligence procedures for Politically Exposed Persons including source of wealth verification. Addresses heightened risks associated with PEPs.

**Control Objective:**
Apply enhanced scrutiny to PEP relationships as required by FATF guidelines, ensuring appropriate risk mitigation for higher-risk relationships.

**Control Activities:**
1. Identify PEP status during AML screening
2. Trigger enhanced due diligence workflow
3. Obtain and verify source of wealth documentation
4. Document business rationale for relationship
5. Require senior management approval for PEP relationships
6. Establish enhanced ongoing monitoring

**Evidence/Documentation:**
- PEP identification record
- Source of wealth documentation
- Senior management approval
- Enhanced monitoring plan

**Testing Approach:**
- Verify all PEPs identified and EDD completed
- Sample test source of wealth verification
- Confirm senior approval obtained

---

### CP-COB-008: Audit Trail Logging

| Attribute | Detail |
|-----------|--------|
| **Control ID** | CP-COB-008 |
| **Control Name** | Audit Trail Logging |
| **Control Type** | DETECTIVE |
| **Regulation/Policy** | Data Protection / Internal Audit Policy |
| **Process Step** | All Steps (PS-COB-001 through PS-COB-008) |
| **Effectiveness** | HIGH |
| **Confidence** | HIGH |

**Description:**
Complete audit trail of all actions, decisions, and approvals throughout the onboarding process. Ensures full traceability for regulatory and audit inquiries.

**Control Objective:**
Maintain complete, immutable record of all onboarding activities to support regulatory inquiries, audits, and investigations.

**Control Activities:**
1. Log all user actions in systems (who, what, when)
2. Record all decisions with rationale
3. Capture approval timestamps and approvers
4. Maintain document version history
5. Ensure logs cannot be altered or deleted

**Evidence/Documentation:**
- System audit logs (CRM, KYC Platform, Core Banking)
- Decision records with rationale
- Approval chains and timestamps

**Testing Approach:**
- Verify audit trail completeness for sample cases
- Confirm logs are immutable
- Test retrieval for regulatory inquiry simulation

---

## Control Framework Analysis

### Controls by Risk Level

| Risk Level | Control Count | Coverage |
|------------|---------------|----------|
| Critical (Sanctions) | 2 | CP-COB-002, CP-COB-007 |
| High (KYC/Identity) | 2 | CP-COB-001, CP-COB-006 |
| High (Fraud) | 1 | CP-COB-004 |
| Medium (Process) | 2 | CP-COB-003, CP-COB-005 |
| Medium (Audit) | 1 | CP-COB-008 |

### Control Gaps Identified

> *Areas where controls may need strengthening*

1. **No CORRECTIVE controls:** All controls are preventive or detective. Consider adding corrective controls for exception handling.
2. **Document authenticity (CP-COB-006):** Manual process has limitations. Consider enhanced document verification technology.
3. **Risk rating consistency (CP-COB-003):** Effectiveness reduced by subjectivity. Standardized scoring matrix would strengthen this control.

### Orphan Controls

> *Controls without clear regulatory requirement (potential waste)*

None identified — all controls trace to regulatory requirements or documented internal policies.

### Uncontrolled Requirements

> *Regulatory requirements without adequate controls (compliance risk)*

None identified — regulatory coverage matrix shows all requirements have mapped controls.

---

## Segregation of Duties Matrix

> *Critical for banking compliance — who can do what*

| Function | Maker | Checker | Approver | System Enforced |
|----------|-------|---------|----------|-----------------|
| Client Record Creation | RM | - | - | No |
| Document Upload | RM | - | - | No |
| KYC Verification | Compliance Officer | - | - | No |
| AML Screening | Compliance Officer | - | Compliance Manager (for hits) | Partial |
| Risk Rating | Compliance Officer | - | Senior CO (for high risk) | Partial |
| Account Setup | Operations (Maker) | Operations (Checker) | - | **Yes** |
| Product Activation | Onboarding Specialist | - | Manager | Partial |

**Recommendation:** Strengthen system enforcement of segregation of duties across more process steps.

---

## Audit Readiness Assessment

### Audit Trail Completeness

| Process Area | Trail Complete | Trail Partial | Trail Missing |
|--------------|----------------|---------------|---------------|
| KYC Verification | Yes | - | - |
| AML Screening | Yes | - | - |
| Risk Assessment | Yes | - | - |
| Account Setup | Yes | - | - |
| Approvals | Yes | - | - |
| Document Handling | - | Yes (DMS) | - |

### Last Audit Findings (if available)

*To be captured from Compliance/Audit team.*

### Remediation Status

*No outstanding remediation items identified in this documentation exercise.*

---

## Recommendations

### Critical (Compliance Risk)

None — all regulatory requirements have mapped controls.

### High Priority (Control Improvement)

1. **CP-COB-003:** Implement standardized risk scoring matrix to improve consistency
2. **CP-COB-006:** Evaluate enhanced document verification technology

### Medium Priority (Optimization)

1. Strengthen system enforcement of segregation of duties
2. Consider adding CORRECTIVE controls for exception handling
3. Enhance audit trail for document handling

---

## Input for Downstream Agents

### For Control Analyst Agent

> *Detailed input for control effectiveness analysis*

- 8 controls documented with effectiveness ratings
- 5 HIGH effectiveness, 3 MEDIUM effectiveness
- Key improvement area: Risk rating consistency (CP-COB-003)
- All regulatory requirements covered

### For Transformation Agent

> *Controls that must be preserved/enhanced in TO-BE*

- **Must Preserve:** All regulatory controls (CP-COB-001, 002, 006, 007)
- **Must Preserve:** Audit trail (CP-COB-008)
- **Enhance:** Risk rating (CP-COB-003) with automated scoring
- **Enhance:** Segregation of duties with system enforcement

### For IT Architect

> *Control automation opportunities and system requirements*

- Four-eyes control currently system-enforced in Core Banking
- Opportunity: Extend system enforcement to other approval points
- Opportunity: Automated risk scoring tool
- Requirement: Immutable audit logging across all systems

---

## Regulatory Quick Reference

### Applicable Regulations

| Regulation | Scope | Key Requirements | Controls Mapped |
|------------|-------|------------------|-----------------|
| AML/KYC Regulations | Client identity verification | Know Your Customer, verify identity | CP-COB-001, CP-COB-006 |
| AML Regulations | Financial crime prevention | Sanctions screening, PEP identification | CP-COB-002, CP-COB-007 |
| FATF Guidelines | International standards | Enhanced due diligence for PEPs | CP-COB-007 |
| Data Protection | Privacy and records | Audit trail, data retention | CP-COB-008 |

### Upcoming Regulatory Changes

> *Regulations that may impact this process*

*To be monitored by Compliance team. No specific changes identified during this documentation exercise.*

---

## Change Log

| Date | Contributor | Role | Changes |
|------|-------------|------|---------|
| 2025-12-09 | Markus | CEO | Initial control point analysis - COMPLETE |

---

_Generated by ProcessMiner Process Documentation Analyst_
_Document ID: COB-002-controls_
_Status: COMPLETE_
