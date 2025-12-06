# Exception Details: Onboarding of a client

**Process ID:** P001
**Parent Document:** [As-Is Process Documentation](./as-is-process-documentation.md)
**Last Updated:** 2025-12-03
**Version:** 1.0 (Test Data)

---

## About This Document

This document provides detailed analysis of all exceptions and variations identified in the Onboarding of a client process. Each exception includes root cause analysis, handling procedures, and improvement recommendations.

For summary view, see the [main process documentation](./as-is-process-documentation.md#3-exception-paths-and-variations).

---

## Exception Index

| EX# | Exception Name | Impact | Frequency |
|-----|----------------|--------|-----------|
| EX-01-001 | CEO Approval Required for Defence Clients | High | Low (2%) |
| EX-01-002 | Customer Unresponsive | Medium | Medium (15%) |
| EX-01-003 | KYC Documentation Incomplete | High | Medium (10%) |

**Statistics:**
- Total Exceptions: 3
- High Impact: 2
- Medium Impact: 1
- Regulatory-Driven: 2

---

## Detailed Exception Analysis

### EX-01-001: CEO Approval Required for Defence Clients

**Completeness:** 90% | **Confidence:** HIGH

#### Exception Summary

Clients operating in the Defence sector (identified by NACE code) require explicit CEO approval before onboarding can proceed. This is a regulatory-driven control to manage reputational and compliance risk.

#### Trigger Conditions

- Client NACE code = Defence sector (NACE codes: 25.4, 30.4)
- Applies to all segments (BizBanking, MidCap, LargeCap)
- Triggered during initial KYC screening

#### Affected Process Steps

- PS-01-001 (Sign In) - Approval gate before account activation

#### Frequency & Impact

| Attribute | Value |
|-----------|-------|
| Frequency | Low (2% of new clients) |
| Impact | High |
| Detection Point | Sign In (Day 1) |
| Average Delay | 3-5 business days |

#### Handling Procedure

1. CRM flags client during KYC screening
2. Onboarding workflow paused automatically
3. Compliance team reviews client documentation
4. Compliance prepares CEO briefing memo
5. CEO reviews and approves/rejects
6. If approved: Workflow resumes, client notified
7. If rejected: Client declined, ACO notifies client

#### Root Cause

Regulatory requirement under AML/sanctions regulations for clients in sensitive industries. Internal risk appetite also limits exposure to defence sector.

#### Escalation Path

```
Compliance Officer → Head of Compliance → CEO
```

#### SLA

- Compliance review: 24 hours
- CEO decision: 48 hours
- Total: 3-5 business days

---

### EX-01-002: Customer Unresponsive

**Completeness:** 85% | **Confidence:** HIGH

#### Exception Summary

Customer does not respond to contact attempts during the onboarding journey. After 3 failed attempts, the process enters a dormant state.

#### Trigger Conditions

- No response to 3 consecutive contact attempts
- Applies to any communication channel (phone, email, SMS)
- Typically occurs at PS-01-004 or PS-01-005

#### Affected Process Steps

- PS-01-004 (Customer Follow-up)
- PS-01-005 (Bank Check-in)

#### Frequency & Impact

| Attribute | Value |
|-----------|-------|
| Frequency | Medium (15% of new clients) |
| Impact | Medium |
| Detection Point | Day 5-30 |
| Revenue Impact | Lost activation opportunity |

#### Handling Procedure

1. After 3rd failed contact attempt, CRM flags account
2. Account moves to "Dormant - Unresponsive" status
3. Digital Team sends "We miss you" email sequence (3 emails over 2 weeks)
4. If still no response after 30 days:
   - Account remains active but marked dormant
   - Excluded from standard onboarding metrics
   - Re-engagement campaign triggered at Day 90
5. If customer responds at any point: Resume normal flow

#### Root Cause

- Incorrect contact information (30%)
- Customer changed mind about banking relationship (25%)
- Customer already has primary bank elsewhere (20%)
- Poor timing of contact attempts (15%)
- Other/Unknown (10%)

#### Improvement Recommendations

1. Verify contact information at account opening
2. Offer self-service scheduling for follow-up calls
3. Implement multi-channel contact (not just phone)
4. A/B test contact timing strategies

---

### EX-01-003: KYC Documentation Incomplete

**Completeness:** 90% | **Confidence:** HIGH

#### Exception Summary

Customer cannot provide all required KYC documentation at sign-up. Process pauses until documentation is complete.

#### Trigger Conditions

- Missing identity documents (passport, ID card)
- Missing proof of address
- Missing company documents (for business clients)
- Document quality issues (blurry, expired)

#### Affected Process Steps

- PS-01-001 (Sign In) - Cannot complete until resolved

#### Frequency & Impact

| Attribute | Value |
|-----------|-------|
| Frequency | Medium (10% of new clients) |
| Impact | High |
| Detection Point | Day 1 |
| Average Resolution | 2-7 days |

#### Handling Procedure

1. System identifies missing/invalid documents
2. Onboarding paused, account in "Pending KYC" status
3. Automated email sent with specific document requirements
4. Customer uploads documents via secure portal or email
5. Compliance reviews within 24 hours
6. If complete: Account activated, onboarding resumes
7. If incomplete: Follow-up request sent, max 3 attempts
8. After 30 days incomplete: Account application cancelled

#### Root Cause

- Customer misunderstands requirements (40%)
- Technical upload issues (25%)
- Document not readily available to customer (20%)
- Expired documents (10%)
- Other (5%)

#### Compliance Notes

- GDPR: Documents retained for regulatory period only
- AML: All KYC decisions logged for audit trail
- Right to appeal: Customer can request manual review

#### Improvement Recommendations

1. Clearer upfront communication of document requirements
2. Real-time document validation with feedback
3. Support chat during upload process
4. Alternative document acceptance policy

---

## Change Log

| Date | Contributor | Role | Changes |
|------|-------------|------|---------|
| 2025-12-03 | Markus | CEO | Document initialized |
| 2025-12-03 | Markus | CEO | Created EX-01-001 during review |
| 2025-12-03 | Markus | CEO | Added mock test data for EX-01-002, EX-01-003 |

---

_Generated by ProcessMiner Process Documentation Analyst_
