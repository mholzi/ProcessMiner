# Client Touchpoints Detail: Client Onboarding

**Document Type:** Client Touchpoint Analysis
**Process ID:** COB-003
**Business Unit:** BizBanking
**Last Updated:** 2025-12-09
**Version:** 1.0.0

---

## Overview

This document provides detailed analysis of each client touchpoint in the Client Onboarding journey. For summary view, see [CX Journey Documentation](./cx-journey-documentation.md).

---

## JT-COB-001: Application Submission

| Attribute | Value |
|-----------|-------|
| **Stage** | Initiation |
| **Channel** | Business Portal / RM / Branch / Partner |
| **Process Step Link** | PS-COB-001 |
| **CES Contribution** | 8 |

### What the Client SEES
- Online application form (15+ fields)
- Document checklist (5-8 required documents)
- Progress indicator
- Estimated completion time

### What the Client DOES
1. Complete business details (company name, registration, address)
2. Enter director/shareholder information
3. Gather required documents (CRO cert, ID, proof of address, business plan if <2 years)
4. Scan or photograph documents
5. Upload documents to portal OR hand to RM
6. Sign application (paper or e-sign where available)
7. Submit and receive confirmation

### Client Effort Analysis

| Effort Type | Count | Notes |
|-------------|-------|-------|
| Data Entry Fields | 15-20 | Varies by channel |
| Documents Required | 5-8 | Standard vs Complex |
| Time to Complete | 30-60 mins | Excluding document gathering |
| Document Gathering | 1-3 days | If not readily available |

### Emotional Journey

| Phase | Emotion | Trigger |
|-------|---------|---------|
| Start | Optimistic | Beginning new banking relationship |
| Mid | Frustrated | Document requirements extensive |
| End | Anxious | Uncertainty about completeness |

### Pain Point Links
- PP-COB-001: Manual document chasing (if incomplete)
- PP-COB-004: Paper-based signatures (40% of applications)

---

## JT-COB-002: Document Request

| Attribute | Value |
|-----------|-------|
| **Stage** | Initiation |
| **Channel** | Email / Phone |
| **Process Step Link** | PS-COB-001 |
| **CES Contribution** | 6 |
| **Frequency** | 30% of applications |

### What the Client SEES
- "Missing Documents" email template
- List of outstanding items
- Follow-up phone calls
- Deadline reminder

### What the Client DOES
1. Read notification
2. Understand what's missing (often unclear)
3. Locate or obtain missing documents
4. Scan/photograph documents
5. Email back or upload to portal
6. Confirm receipt

### Client Effort Analysis

| Effort Type | Count | Notes |
|-------------|-------|-------|
| Follow-up Cycles | 2-3 | Average per incomplete application |
| Days Added | 2-5 | Delay to process |
| Emails/Calls | 4-6 | Back and forth |

### Emotional Journey

| Phase | Emotion | Trigger |
|-------|---------|---------|
| Notification | Surprised | Thought submission was complete |
| Chase | Frustrated | Unclear requirements, repeat requests |
| Resolution | Relieved | Finally resolved, but trust eroded |

### Pain Point Links
- PP-COB-001: Manual document chasing (PRIMARY)

### Enhancement Ideas
- EI-COB-001: Real-time completeness validation at submission
- EI-COB-002: Clear document checklist with examples
- EI-COB-003: Automated reminder system with smart escalation

---

## JT-COB-003: ID Verification

| Attribute | Value |
|-----------|-------|
| **Stage** | Verification |
| **Channel** | Digital (Jumio) / In-person |
| **Process Step Link** | PS-COB-002 |
| **CES Contribution** | 3 |

### What the Client SEES
- Jumio verification prompt
- Instructions for selfie and ID photo
- "Verification in progress" message
- Success/retry notification

### What the Client DOES
1. Receive verification link/prompt
2. Position for selfie capture
3. Photograph front/back of ID
4. Wait for automated verification
5. Retry if quality issues (10% of cases)

### Client Effort Analysis

| Effort Type | Count | Notes |
|-------------|-------|-------|
| Time | 3-5 mins | Including retries |
| Attempts | 1-2 | Lighting/quality issues |
| Technical Skill | Low | Smartphone camera use |

### Emotional Journey

| Phase | Emotion | Trigger |
|-------|---------|---------|
| Start | Neutral | Expected step |
| Process | Mild Frustration | If multiple retries needed |
| Success | Satisfied | Quick confirmation |

---

## JT-COB-004: Information Request

| Attribute | Value |
|-----------|-------|
| **Stage** | Verification |
| **Channel** | Email / Phone |
| **Process Step Link** | PS-COB-002 |
| **CES Contribution** | 4 |
| **Frequency** | 20% of applications (complex structures) |

### What the Client SEES
- KYC analyst email with questions
- Ownership structure queries
- Source of funds questions
- Request for additional documentation

### What the Client DOES
1. Read and understand questions
2. Consult accountant/solicitor if needed
3. Gather supporting documents
4. Compose response
5. Submit additional information

### Client Effort Analysis

| Effort Type | Count | Notes |
|-------------|-------|-------|
| Questions | 3-8 | Varies by complexity |
| Days to Respond | 2-5 | If professional advice needed |
| Professional Fees | €200-500 | If accountant/solicitor involved |

### Emotional Journey

| Phase | Emotion | Trigger |
|-------|---------|---------|
| Receipt | Confused | Technical/legal questions |
| Research | Stressed | Need external help |
| Response | Anxious | Uncertainty if sufficient |

### Exception Links
- EX-COB-005: Complex Ownership Structure

---

## JT-COB-005: Credit Decision

| Attribute | Value |
|-----------|-------|
| **Stage** | Decision |
| **Channel** | Email / Phone |
| **Process Step Link** | PS-COB-003 |
| **CES Contribution** | 2 |
| **Conditional** | Only if overdraft requested |

### What the Client SEES
- Decision notification (approve/decline/refer)
- Terms and conditions (if approved)
- Decline rationale (if declined)
- Alternative offer (account-only if credit declined)

### What the Client DOES
1. Receive notification
2. Review decision and terms
3. Accept terms (digital or wet signature)
4. Query if unclear or declined

### Emotional Journey

| Phase | Emotion | Trigger |
|-------|---------|---------|
| Waiting | Anxious | Uncertainty of outcome |
| Approval | Relieved/Happy | Positive outcome |
| Decline | Disappointed | But offered alternative |

### Exception Links
- EX-COB-003: Credit Decline

---

## JT-COB-006: Account Details Receipt

| Attribute | Value |
|-----------|-------|
| **Stage** | Activation |
| **Channel** | Email / Post |
| **Process Step Link** | PS-COB-004 |
| **CES Contribution** | 2 |

### What the Client SEES
- Welcome email with account numbers
- IBAN and BIC details
- Fee schedule
- Debit card dispatch notification
- Physical welcome pack (posted)

### What the Client DOES
1. Receive and review details
2. Store account information securely
3. Wait for physical card (3-5 days)
4. Set up payee details with suppliers/customers

### Emotional Journey

| Phase | Emotion | Trigger |
|-------|---------|---------|
| Receipt | Excited | Finally tangible progress |
| Review | Satisfied | Account numbers received |
| Waiting | Impatient | Card not yet arrived |

---

## JT-COB-007: Online Banking Setup

| Attribute | Value |
|-----------|-------|
| **Stage** | Activation |
| **Channel** | Portal / Mobile App |
| **Process Step Link** | PS-COB-004 |
| **CES Contribution** | 4 |

### What the Client SEES
- Activation email with temporary credentials
- App download link
- Setup wizard
- Security configuration options

### What the Client DOES
1. Download mobile app
2. Enter temporary credentials
3. Set permanent password
4. Configure 2FA (Strong Customer Authentication)
5. Set transaction limits
6. Explore dashboard

### Client Effort Analysis

| Effort Type | Count | Notes |
|-------------|-------|-------|
| Steps | 6-8 | First-time setup |
| Time | 10-15 mins | Including 2FA setup |
| Technical Skill | Medium | App/security familiarity |

### Emotional Journey

| Phase | Emotion | Trigger |
|-------|---------|---------|
| Start | Eager | Access to new account |
| Setup | Mild Frustration | Multiple security steps |
| Complete | Satisfied | Can see account, ready to use |

### Control Links
- CP-COB-004: Strong Customer Authentication (PSD2)

---

## JT-COB-008: Welcome Call

| Attribute | Value |
|-----------|-------|
| **Stage** | Relationship |
| **Channel** | Phone |
| **Process Step Link** | PS-COB-005 |
| **CES Contribution** | 5 |

### What the Client SEES
- Incoming call from unknown number
- Voicemail if missed
- Multiple call attempts over several days

### What the Client DOES
1. Recognize bank call (or miss it)
2. Answer or return call
3. Discuss activation confirmation
4. Review immediate banking needs
5. Establish RM relationship

### Client Effort Analysis

| Effort Type | Count | Notes |
|-------------|-------|-------|
| Call Attempts | 3+ | 70% require multiple attempts |
| Time to Connect | 3-5 days | Due to scheduling difficulties |
| Call Duration | 10-15 mins | Once connected |

### Emotional Journey

| Phase | Emotion | Trigger |
|-------|---------|---------|
| Missed Calls | Annoyed | Interrupted, unknown number |
| Voicemail | Obligated | Must call back |
| Connected | Appreciative | Personal touch, helpful |

### Pain Point Links
- PP-COB-006: Welcome call scheduling

### Enhancement Ideas
- EI-COB-004: Self-service call scheduling via portal
- EI-COB-005: Video call option
- EI-COB-006: Chat-based onboarding alternative

---

## JT-COB-009: First Transaction

| Attribute | Value |
|-----------|-------|
| **Stage** | Activation |
| **Channel** | Portal / Mobile App |
| **Process Step Link** | PS-COB-005 |
| **CES Contribution** | 2 |

### What the Client SEES
- Account dashboard with balance
- Transfer/payment screens
- Transaction confirmation
- Receipt/reference

### What the Client DOES
1. Log into online banking
2. Add payee (supplier/customer)
3. Initiate first transfer
4. Confirm with 2FA
5. Verify completion

### Emotional Journey

| Phase | Emotion | Trigger |
|-------|---------|---------|
| Initiation | Excited | Finally using account |
| Execution | Confident | Familiar banking actions |
| Completion | Satisfied | Journey complete, value realized |

---

## Summary Statistics

| Metric | Value |
|--------|-------|
| **Total Touchpoints** | 9 |
| **Total CES (All Clients)** | 36 (base) |
| **Total CES (With Friction)** | 46 (if doc chase + complex) |
| **Highest CES Touchpoint** | JT-COB-001 (8) |
| **Most Problematic** | JT-COB-002, JT-COB-008 |

---

## Cross-Reference Summary

### Touchpoint to Process Step Mapping

| Touchpoint | Process Step |
|------------|--------------|
| JT-COB-001 | PS-COB-001 |
| JT-COB-002 | PS-COB-001 |
| JT-COB-003 | PS-COB-002 |
| JT-COB-004 | PS-COB-002 |
| JT-COB-005 | PS-COB-003 |
| JT-COB-006 | PS-COB-004 |
| JT-COB-007 | PS-COB-004 |
| JT-COB-008 | PS-COB-005 |
| JT-COB-009 | PS-COB-005 |

### Touchpoint to Pain Point Mapping

| Touchpoint | Pain Points |
|------------|-------------|
| JT-COB-001 | PP-COB-001, PP-COB-004 |
| JT-COB-002 | PP-COB-001 |
| JT-COB-004 | PP-COB-002 |
| JT-COB-008 | PP-COB-006 |

---

_Generated by ProcessMiner Client Journey Analyst_
_Document ID: COB-003-touchpoints_
