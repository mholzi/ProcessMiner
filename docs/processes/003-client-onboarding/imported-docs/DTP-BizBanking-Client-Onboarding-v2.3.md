# DTP-BB-ONB-001: BizBanking Client Onboarding

**Document Type:** Detailed Task Procedure (DTP)
**Version:** 2.3
**Effective Date:** 2024-06-15
**Review Date:** 2025-06-15
**Owner:** BizBanking Operations
**Classification:** Internal Use Only

---

## 1. Purpose

This DTP provides step-by-step instructions for onboarding new BizBanking clients (businesses with annual turnover up to €10M). It covers the end-to-end process from initial application receipt through account activation and first transaction capability.

---

## 2. Scope

**Applies to:**
- New BizBanking client applications (sole traders, partnerships, limited companies)
- Turnover band: €0 - €10M annual revenue
- Products: Business Current Account, Business Savings, Overdraft facility

**Out of Scope:**
- MidCap clients (€10M - €50M) - see DTP-MC-ONB-001
- LargeCap clients (€50M+) - see DTP-LC-ONB-001
- Product cross-sells post-onboarding

---

## 3. Roles and Responsibilities

| Role | Responsibility |
|------|----------------|
| Relationship Manager (RM) | Initial client contact, application gathering, client communication |
| KYC Analyst | Identity verification, document validation, risk assessment |
| Credit Analyst | Financial assessment, credit decisioning (if overdraft requested) |
| Operations Officer | Account setup, system configuration, card ordering |
| Compliance Officer | Enhanced Due Diligence reviews, PEP/Sanctions escalations |
| Team Lead | Escalation handling, SLA breach management |

---

## 4. Process Triggers

The onboarding process is initiated when:
1. New client completes online application via Business Portal
2. RM submits paper application on behalf of walk-in client
3. Referral from branch network with completed application pack
4. Partner channel submission (accountants, solicitors)

---

## 5. Detailed Process Steps

### Step 1: Application Receipt & Initial Triage
**Owner:** Operations Officer
**System:** CRM, Document Management System (DMS)
**SLA:** Same business day

1.1. Receive application notification in CRM queue
1.2. Verify application completeness checklist:
   - [ ] Application form signed
   - [ ] Company registration documents (CRO extract)
   - [ ] ID for all directors/beneficial owners
   - [ ] Proof of address (utility bill <3 months)
   - [ ] Business plan or financial projections (if <2 years trading)
1.3. If incomplete, send "Missing Documents" email template (TPL-BB-001)
1.4. If complete, create case in Onboarding Workflow System (OWS)
1.5. Assign KYC priority based on complexity:
   - Standard: Single director, simple structure
   - Complex: Multiple directors, corporate shareholders, foreign elements

### Step 2: KYC & Identity Verification
**Owner:** KYC Analyst
**System:** KYC Platform, World-Check, Companies Registration Office Portal
**SLA:** 2 business days (Standard), 5 business days (Complex)

2.1. Verify company registration via CRO portal
2.2. Confirm Ultimate Beneficial Owners (UBOs) - 25%+ ownership threshold
2.3. Screen all directors and UBOs against:
   - World-Check (PEP & Sanctions)
   - Internal watchlists
   - Adverse media search
2.4. Verify ID documents using IDV platform (Jumio integration)
2.5. Verify proof of address documents
2.6. Complete Customer Risk Assessment (CRA) form:
   - Industry risk rating
   - Geographic risk rating
   - Product risk rating
   - Overall risk score (Low/Medium/High)
2.7. If High Risk or PEP identified → escalate to Compliance Officer
2.8. Document all verification steps in KYC Platform audit trail
2.9. Update case status to "KYC Complete" or "KYC Pending - Escalated"

### Step 3: Credit Assessment (If Overdraft Requested)
**Owner:** Credit Analyst
**System:** Credit Decisioning System (CDS), Bureau Link
**SLA:** 3 business days

3.1. Pull credit bureau report for company and directors
3.2. Review financial statements (if available):
   - P&L analysis
   - Balance sheet review
   - Cash flow assessment
3.3. Calculate key ratios:
   - Debt service coverage
   - Current ratio
   - Gearing ratio
3.4. Complete credit scorecard in CDS
3.5. Generate credit recommendation:
   - Approve (within delegated authority)
   - Refer to Credit Committee
   - Decline
3.6. If approved, document facility terms and conditions
3.7. Update case status to "Credit Complete"

### Step 4: Account Setup & Configuration
**Owner:** Operations Officer
**System:** Core Banking System (CBS), Card Management System
**SLA:** 1 business day (post KYC/Credit approval)

4.1. Create customer master record in CBS
4.2. Open Business Current Account (BCA)
4.3. Configure account parameters:
   - Statement frequency (monthly default)
   - Interest application
   - Fee package assignment
4.4. Set up online banking access:
   - Create primary user (main contact)
   - Generate temporary credentials
   - Configure transaction limits
4.5. Order business debit card via Card Management System
4.6. If overdraft approved:
   - Create facility in CBS
   - Link to BCA
   - Set up monitoring alerts
4.7. Generate Welcome Pack documents
4.8. Update case status to "Account Created"

### Step 5: Client Communication & Activation
**Owner:** Relationship Manager
**System:** CRM, Email, Core Banking System
**SLA:** 1 business day

5.1. Send Welcome Email with:
   - Account details
   - Online banking activation instructions
   - RM contact details
   - Key product information
5.2. Schedule welcome call within 5 business days
5.3. Conduct welcome call:
   - Confirm receipt of materials
   - Walk through online banking activation
   - Discuss immediate banking needs
   - Set expectations for ongoing relationship
5.4. Document call notes in CRM
5.5. Update case status to "Active - Onboarding Complete"

### Step 6: Post-Onboarding Quality Check
**Owner:** Team Lead
**System:** OWS, Quality Management System
**SLA:** Within 10 business days of activation

6.1. Random sample 20% of completed onboardings
6.2. Review against quality checklist:
   - [ ] All mandatory documents present
   - [ ] KYC screening completed correctly
   - [ ] Risk rating appropriate
   - [ ] Account configured correctly
   - [ ] Client communication timely
6.3. Document findings in Quality Management System
6.4. Feedback to relevant team member if issues identified
6.5. Escalate systemic issues to Process Owner

---

## 6. Exception Handling

### EX-1: Incomplete Documentation
- If documents still missing after 2 reminders (10 business days), escalate to RM
- RM to contact client directly
- If no response after 20 business days, application auto-expires

### EX-2: KYC Screening Hit
- Any World-Check hit requires Compliance Officer review
- True positive PEP: Enhanced Due Diligence (EDD) required
- True positive Sanctions: Immediate escalation to MLRO, do not proceed

### EX-3: Credit Decline
- RM notifies client with decline reasons (where permissible)
- Offer account-only (no overdraft) as alternative
- Document decline in CRM for future reference

### EX-4: System Downtime
- If CBS unavailable >4 hours, activate BCP manual process
- Log all manual entries for system reconciliation
- Notify affected clients of potential delays

### EX-5: Complex Ownership Structure
- Structures with >3 layers require Senior KYC Analyst review
- Foreign corporate shareholders require additional due diligence
- Trust structures require legal review before proceeding

---

## 7. Systems & Tools

| System | Purpose | Access Level |
|--------|---------|--------------|
| CRM (Salesforce) | Client relationship management, case tracking | All roles |
| OWS (Onboarding Workflow System) | Process orchestration, SLA tracking | All roles |
| KYC Platform (Fenergo) | KYC case management, document storage | KYC Analyst, Compliance |
| World-Check (Refinitiv) | PEP & Sanctions screening | KYC Analyst, Compliance |
| CBS (Temenos T24) | Account creation, transaction processing | Operations, RM |
| CDS (Credit Decisioning) | Credit assessment, scorecards | Credit Analyst |
| DMS (OpenText) | Document storage, archival | All roles |
| Card Management (Marqeta) | Debit card ordering, management | Operations |

---

## 8. SLAs & KPIs

| Metric | Target | Measurement |
|--------|--------|-------------|
| End-to-end onboarding time (Standard) | 5 business days | Application receipt to activation |
| End-to-end onboarding time (Complex) | 10 business days | Application receipt to activation |
| KYC completion rate | 95% within SLA | KYC step completion |
| Document request turnaround | 24 hours | Time to send missing doc request |
| Welcome call completion | 100% within 5 days | Call completed post-activation |
| Quality check pass rate | 98% | Monthly quality review |
| Customer satisfaction (NPS) | >50 | Post-onboarding survey |

---

## 9. Regulatory Requirements

| Regulation | Requirement | Control |
|------------|-------------|---------|
| CDD Regulations 2010 | Customer identification | Step 2: KYC verification |
| AML Act 2010 | Beneficial owner identification | Step 2.2: UBO identification |
| GDPR | Data protection, consent | Step 1: Privacy notice, data consent |
| PSD2 | Strong Customer Authentication | Step 4.4: Online banking setup |
| Consumer Protection Code | Disclosure requirements | Step 5.1: Welcome pack |

---

## 10. Known Issues & Pain Points

1. **Manual document chasing** - No automated reminders for missing documents, relies on Operations Officer to manually track and send emails. Average 2-3 follow-ups per application.

2. **System switching** - Staff must access 6+ systems during onboarding. No single view of client. Copy-paste between systems leads to data entry errors.

3. **KYC screening false positives** - World-Check generates high volume of false positives (~40%), requiring manual review. Common names particularly problematic.

4. **Paper-based signatures** - Many clients still submit paper applications. Manual digitization creates 1-2 day delay.

5. **Credit bureau delays** - Bureau response times vary (instant to 24hrs). No visibility on when data will be available.

6. **Welcome call scheduling** - RMs struggle to reach clients. Average 3 attempts before successful contact. No self-service scheduling option.

---

## 11. Change Log

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2022-01-15 | J. Murphy | Initial release |
| 2.0 | 2023-03-01 | S. O'Brien | Added Fenergo KYC platform integration |
| 2.1 | 2023-09-15 | S. O'Brien | Updated SLAs, added quality check step |
| 2.2 | 2024-02-01 | M. Kelly | Added complex structure exception handling |
| 2.3 | 2024-06-15 | M. Kelly | Updated system list, added pain points section |

---

## 12. Appendices

### Appendix A: Document Checklist
- Application Form (F-BB-001)
- CRO Company Printout (or Certificate of Incorporation)
- Memorandum & Articles of Association
- Director ID (Passport or National ID)
- Director Proof of Address
- UBO ID and Address (if different from directors)
- Financial Statements (2 years if available)
- Business Plan (if <2 years trading)

### Appendix B: Email Templates
- TPL-BB-001: Missing Documents Request
- TPL-BB-002: Application Received Confirmation
- TPL-BB-003: Welcome Email
- TPL-BB-004: Application Expired Notification

### Appendix C: Escalation Matrix
| Issue Type | First Escalation | Second Escalation | Timeline |
|------------|------------------|-------------------|----------|
| SLA Breach | Team Lead | Operations Manager | Immediate |
| Compliance Concern | Compliance Officer | MLRO | Same day |
| Credit Exception | Credit Manager | Head of Credit | 24 hours |
| System Issue | IT Service Desk | IT Manager | Per severity |
| Client Complaint | RM Manager | Head of BizBanking | Same day |

---

**Document End**
