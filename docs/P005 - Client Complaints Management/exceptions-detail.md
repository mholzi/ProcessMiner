# Exception Paths & Variations: Client Complaints Management

**Process ID:** P005
**Document Type:** Exception Detail Analysis
**Last Updated:** 2025-12-04
**Related Document:** [AS-IS Process Documentation](./as-is-process-documentation.md)

---

## Executive Summary

The Client Complaints Management process experiences six distinct exception scenarios that deviate from the standard complaint handling flow, collectively affecting approximately 50-60% of all complaints to some degree. These exceptions range from operational challenges (duplicate complaints, SLA breaches) to regulatory-critical scenarios (vulnerable customers, systemic issues) and require specialized handling procedures.

The most frequent exception is vulnerable customer identification (20-25% of cases), which is actually a regulatory requirement under Consumer Duty rather than a true exception, mandating enhanced care and expedited handling. SLA breaches occur in 15-20% of cases, representing the process's most significant operational challenge and creating regulatory risk. Duplicate complaints (10%) waste resources and risk client confusion. Third-party involvement (5-7%) and legal threats (2-4%) add complexity and require cross-functional coordination. Systemic issues (rare but critical) have the highest potential impact, potentially affecting hundreds of clients and triggering regulatory investigations.

Exception handling currently relies heavily on manual identification and escalation, with limited system support for detection or workflow routing. This creates inconsistency in handling and increases the risk of exceptions being missed or handled inadequately. The TO-BE process design should prioritize automated exception detection, standardized handling procedures, and improved system support to reduce handling time and ensure consistent treatment.

---

## Exception Summary Table

> **Quick Reference:** All identified exceptions with impact and frequency at a glance. Click any EX# for full details below.

| EX# | Exception Name | Trigger Condition | Affected Steps | Frequency | Business Impact | Handling Owner |
|-----|----------------|-------------------|----------------|-----------|-----------------|----------------|
| EX01 | Duplicate Complaint | Multiple entries with same client and issue | PS01, PS02 | 10% (~20/month) | Medium | Complaints Manager |
| EX02 | SLA Breach - Investigation Delay | Approaching 30-day deadline with investigation incomplete | PS05, PS08 | 15-20% (~30-40/month) | High | Department Manager |
| EX03 | Third-Party Involvement | Complaint issue originates from third-party provider action | PS05, PS06, PS07 | 5-7% (~10-15/month) | High | Investigation Owner + Third-Party Liaison |
| EX04 | Vulnerable Customer | Vulnerability flag in CRM or identified during contact | All steps | 20-25% (~40-50/month) | High | Senior Handler |
| EX05 | Legal Action Threatened | Client mentions solicitor or legal proceedings | PS05, PS07, PS08 | 2-4% (~5-8/month) | High | Investigation Owner + Legal Team |
| EX06 | Systemic Issue Identified | Complaint pattern reveals process/system failure affecting multiple clients | PS06, PS10 | Quarterly (~2-3/quarter) | Critical | Senior Management + Compliance |

---

## Exception Statistics

| Metric | Value |
|--------|-------|
| Total Exceptions Identified | 6 |
| High-Impact Exceptions | 5 |
| Frequently Occurring (>10% of cases) | 2 |
| Exceptions Requiring Manual Intervention | 6 (all) |
| Exceptions with Documented Procedures | 3 (partial documentation) |
| Exceptions Lacking Clear Ownership | 1 (EX03) |

---

## Detailed Exception Analysis

### EX01: Duplicate Complaint

#### Overview

| Attribute | Value |
|-----------|-------|
| **Exception ID** | EX01 |
| **Exception Name** | Duplicate Complaint |
| **Category** | Data Quality / Operational Inefficiency |
| **Affected Process Steps** | PS01 (Registration), PS02 (Classification) |
| **Frequency** | 15-20 times per month (~10% of complaints) |
| **Business Impact** | Medium |
| **Handling Owner** | Complaints Manager |
| **Average Resolution Time** | 15-30 minutes to identify and merge |

#### Trigger Conditions

> *What causes this exception to occur?*

Duplicate complaints occur when a client submits the same complaint through multiple channels (e.g., calls branch, then emails, then uses web portal) without realizing each creates a separate case. Also occurs when a client resubmits an existing complaint believing the original was not received or acted upon. Lack of automated duplicate detection in ServiceNow means duplicates are not flagged at entry.

#### Detection Method

> *How is this exception identified? (System alert, manual review, client complaint, etc.)*

**Current Detection:** Manual search by Customer Service staff before logging new complaint. Staff search by client name and account number, but inconsistent practice. Often duplicates only discovered when investigation owner reviews case history or client contacts bank mentioning different reference numbers.

**Detection Rate:** Estimated 70-80% detected before investigation begins. Remaining 20-30% discovered during investigation or by client feedback.

#### Business Impact Analysis

> *What happens when this exception occurs? Quantify where possible.*

**Immediate Impact:**
- Wasted time logging duplicate entry: 5-10 minutes per occurrence = ~2.5-5 hours per month
- Confusion in SLA tracking: which entry is the "official" complaint date?
- Risk of duplicate acknowledgment letters sent to client

**Downstream Effects:**
- Investigation owner may duplicate work if not caught early
- Two investigation owners may work on same complaint if routed to different departments
- Complaint statistics inflated (regulatory reporting accuracy risk)

**Client Impact:**
- Client confusion: "Why do I have two reference numbers?"
- Perception of incompetence: "The bank can't even track my complaint properly"
- Frustration if responses reference different case numbers

**Financial Impact (if applicable):**
- Staff time wasted: ~3-6 hours per month (combined detection and remediation)
- Minimal direct cost but reputational risk

**Regulatory/Compliance Risk:**
- Low direct risk, but regulatory reporting accuracy affected if duplicates not identified and merged before quarterly report
- FCA expects accurate complaint volumes

#### Current Handling Procedure

> *Step-by-step: What happens today when this exception is triggered?*

1. **Detection:** Duplicate identified by staff search or during investigation
2. **Verification:** Confirm same client, same issue, overlapping timeframes (not legitimate escalation or related but separate issue)
3. **Decision:** Determine which entry is "primary" (usually earliest registration date)
4. **Merge Process:**
   - Copy all notes and attachments from secondary case(s) to primary case
   - Add note to secondary case(s): "Duplicate - merged with [primary reference]"
   - Close secondary case(s) with status "Duplicate"
5. **Client Communication:** If client received multiple acknowledgment letters, send brief note explaining single reference number going forward
6. **Update Investigation:** Ensure investigation owner working on primary case has all information

**Average Time:** 15-30 minutes depending on how much work already done on duplicate cases

#### Escalation Path

> *When and to whom does this exception escalate?*

| Escalation Level | Trigger | Owner | SLA |
|------------------|---------|-------|-----|
| Level 1 (Standard) | Duplicate identified | Customer Service / Investigation Owner | Immediate merge |
| Level 2 (Manager) | Duplicate not caught until significant work duplicated | Complaints Manager | Same day resolution |
| Level 3 (Senior) | N/A - low severity exception | N/A | N/A |

#### System Behavior

> *How do systems respond to this exception?*

**ServiceNow:** No automated duplicate detection. No system alert. Manual search required. Merge functionality exists (can link cases and mark as duplicate) but not prominently used. Case closure reason "Duplicate" available but not consistently applied.

**Salesforce CRM:** Not involved in exception handling. CRM may show multiple complaint records if linked from ServiceNow, adding to confusion.

#### Documentation & Evidence

> *What documentation exists for this exception? What audit trail is captured?*

- **Existing Procedures:** Brief mention in ServiceNow User Guide - "Check for duplicates before logging"
- **Audit Trail Captured:** Note added to secondary case indicating duplicate status. Link to primary case sometimes created.
- **Evidence Retained:** Closed duplicate case remains in system for audit, but may not be easily identifiable in reporting

#### Root Cause Analysis

> *Why does this exception occur? (5-Whys or similar analysis)*

**5-Whys Analysis:**
1. **Why do duplicate complaints occur?** Clients submit same complaint through multiple channels.
2. **Why do clients submit through multiple channels?** They are unsure if first submission was received or want to ensure urgent attention.
3. **Why are clients unsure?** Acknowledgment may be delayed (up to 5 days), or clients don't wait for acknowledgment before re-submitting.
4. **Why doesn't ServiceNow prevent duplicates?** No duplicate detection rules configured. No unique client identifier checked at entry.
5. **Root Cause:** ServiceNow lacks duplicate detection functionality; manual search is inconsistent; clients lack confidence in single-channel submission.

**Contributing Factors:**
- Multiple complaint channels without unified intake
- No real-time acknowledgment (web portal submissions have automated instant acknowledgment, but phone/email don't)
- Staff don't always perform manual duplicate search (time pressure, inconsistent training)
- No unique client identifier used consistently across channels

#### Improvement Opportunities

> *How could this exception be prevented, detected earlier, or handled more efficiently?*

**Prevention:**
- Implement automated duplicate detection in ServiceNow based on client ID + issue keywords + date range
- Provide instant acknowledgment for all channels (including phone and email) so clients have immediate confirmation
- Educate clients on complaint process: "One submission is sufficient - you will receive acknowledgment within 5 days"

**Earlier Detection:**
- Configure ServiceNow to flag potential duplicates at case creation (fuzzy matching on client name, account, issue description)
- Require staff to confirm "Duplicate check performed" before saving new case

**More Efficient Handling:**
- Implement one-click merge functionality in ServiceNow
- Automate notification to client when duplicate merged ("We've consolidated your complaint submissions under reference [X]")

**Estimated Improvement:**
- 80-90% reduction in duplicate occurrence if automated detection implemented
- 50% reduction in handling time if merge process streamlined

#### Related Exceptions

> *Other exceptions that commonly occur together or have similar root causes*

- **Related to PP02 (Pain Point):** Lack of Automated Duplicate Detection - this exception is manifestation of that pain point
- No direct relationship to other exceptions, but exacerbates SLA pressure (EX02) if duplicates delay investigation start

---

### EX02: SLA Breach - Investigation Delay

#### Overview

| Attribute | Value |
|-----------|-------|
| **Exception ID** | EX02 |
| **Exception Name** | SLA Breach - Investigation Delay |
| **Category** | Process Failure / Resource Constraint |
| **Affected Process Steps** | PS05 (Investigation), PS08 (Final Response) |
| **Frequency** | 30-40 times per month (15-20% of complaints) |
| **Business Impact** | High |
| **Handling Owner** | Department Manager (escalation point) |
| **Average Resolution Time** | N/A - exception is the delay itself |

#### Trigger Conditions

> *What causes this exception to occur?*

SLA breach occurs when investigation cannot be completed and final response sent within 30-day internal target (or 8-week FCA maximum). Triggers include:
- Complex investigation requiring extensive evidence gathering across multiple systems
- Staff resource constraints (high workload, staff absence, skills gap)
- Third-party involvement causing delays (overlaps with EX03)
- Client or internal staff unresponsive to investigation queries
- Legal review required (overlaps with EX05)
- Incomplete initial complaint registration requiring follow-up with client for clarification

#### Detection Method

> *How is this exception identified? (System alert, manual review, client complaint, etc.)*

**Current Detection:** Weekly SLA report generated from ServiceNow showing cases approaching 30-day mark (at 20 days) and overdue cases. Complaints Manager reviews and escalates at-risk cases. No real-time alerts or dashboard.

**Detection Timing:** Typically identified at 20-25 days, providing limited time for corrective action.

**Detection Rate:** 100% eventually detected via weekly report, but often too late for proactive intervention.

#### Business Impact Analysis

> *What happens when this exception occurs? Quantify where possible.*

**Immediate Impact:**
- 30-day internal SLA breach (internal KPI failure, management escalation required)
- Potential 8-week FCA deadline breach (regulatory breach if final response not sent within 56 days)
- Holding letter sent to client extending deadline (administrative burden)

**Downstream Effects:**
- Client dissatisfaction increases with delay (higher likelihood of ombudsman escalation)
- Staff stress and morale impact (fire-fighting mode, pressure from management)
- Management focus diverted to reactive escalation handling

**Client Impact:**
- Frustration and loss of confidence in bank's complaint handling
- Increased likelihood of escalation to Financial Ombudsman Service
- Negative impact on client relationship (may close account or leave negative reviews)

**Financial Impact (if applicable):**
- Staff overtime to resolve overdue cases: estimated £2,000-3,000 per month
- Increased ombudsman referrals: each case costs ~£500 in staff time + potential adverse ruling
- Reputational cost difficult to quantify but significant

**Regulatory/Compliance Risk:**
- High risk if 8-week FCA deadline breached: regulatory reportable event, potential FCA investigation
- Repeat breaches may trigger supervisory action or fines
- Senior management accountability under SMCR (Senior Managers Certification Regime)

#### Current Handling Procedure

> *Step-by-step: What happens today when this exception is triggered?*

1. **Detection:** Weekly SLA report identifies case approaching 30-day mark (at ~20-25 days)
2. **Escalation:** Complaints Manager contacts investigation owner to assess progress
3. **Assessment:** Determine reason for delay and realistic completion timeline
4. **Decision:**
   - If completion possible within 30 days: prioritize investigation, defer other work
   - If completion not possible within 30 days: proceed with holding letter process
5. **Holding Letter (if required):**
   - Draft holding letter explaining delay reason and revised completion date
   - Manager approval required for deadline extension
   - Send to client (must reference FCA 8-week maximum deadline)
6. **Expedite Investigation:**
   - Allocate additional resources if available
   - Escalate barriers (e.g., unresponsive third party, legal review delay)
   - Daily progress tracking by manager
7. **Final Response:** Prioritize drafting and sending within revised deadline (must not exceed 8 weeks total)
8. **Post-Incident Review:** Escalate to monthly Complaints Committee, analyze root cause, identify process improvements

**Average Additional Management Time:** 1-2 hours per escalated case

#### Escalation Path

> *When and to whom does this exception escalate?*

| Escalation Level | Trigger | Owner | SLA |
|------------------|---------|-------|-----|
| Level 1 (Manager) | Case at 20+ days with no final response drafted | Department Manager | Immediate review, decision within 1 day |
| Level 2 (Senior) | Case approaching 8-week deadline (50+ days) | Head of Customer Service + Compliance Officer | Daily updates, board notification |
| Level 3 (Board) | 8-week deadline breach | CEO + FCA notification | Immediate regulatory report |

#### System Behavior

> *How do systems respond to this exception?*

**ServiceNow:** SLA countdown visible on case record. Case flagged as "At Risk" at 20 days. No proactive alerts. Weekly report generated manually via scheduled report. No automated escalation workflow.

**Issue:** Reactive rather than proactive. Staff don't see real-time SLA status during daily work. Dashboard not configured for live SLA monitoring.

#### Documentation & Evidence

> *What documentation exists for this exception? What audit trail is captured?*

- **Existing Procedures:** SLA escalation process documented in Complaints Handling Policy
- **Audit Trail Captured:** Holding letters saved to ServiceNow. Manager approval tracked. Notes added explaining delay reason. Weekly SLA reports archived.
- **Evidence Retained:** Complete case history including escalation timeline, holding letters, final resolution date

#### Root Cause Analysis

> *Why does this exception occur? (5-Whys or similar analysis)*

**5-Whys Analysis:**
1. **Why do SLA breaches occur?** Investigations take longer than 30 days to complete.
2. **Why do investigations take so long?** Evidence gathering is time-consuming and resource constraints limit investigation capacity.
3. **Why is evidence gathering time-consuming?** Systems are fragmented (must access ServiceNow, Salesforce, banking platform, document storage separately) - see PP03.
4. **Why are there resource constraints?** Investigation owner workload not balanced; staff skills vary; absence coverage inadequate.
5. **Root Cause:** System fragmentation slows investigations (PP03); resource planning inadequate; no proactive SLA visibility (PP07); complex cases not identified early for triage.

**Contributing Factors:**
- System fragmentation (PP03) - major contributor
- No real-time SLA dashboard (PP07) - prevents proactive intervention
- Inconsistent initial complaint registration - incomplete information requires follow-up
- Third-party delays (EX03)
- No case complexity triage at intake - complex cases should have longer SLA from start

#### Improvement Opportunities

> *How could this exception be prevented, detected earlier, or handled more efficiently?*

**Prevention:**
- System integration to reduce investigation time by ~40% (addresses PP03)
- Case complexity triage at registration: assign tiered SLAs (e.g., 15/30/45 days based on complexity)
- Better resource planning: workload balancing, cross-training, absence coverage planning
- Automate evidence gathering where possible (e.g., system APIs pull data into ServiceNow)

**Earlier Detection:**
- Real-time SLA dashboard visible to all staff (addresses PP07)
- Automated alerts at 10 days (33%), 20 days (66%), 25 days (83%)
- Proactive escalation workflow: case automatically escalated to manager at 20 days

**More Efficient Handling:**
- Pre-approved holding letter templates for common delay reasons (reduce approval time)
- Fast-track process for time-critical evidence gathering
- Senior management "SWAT team" to unblock barriers (e.g., expedite legal review, contact third-party executives)

**Estimated Improvement:**
- 50-60% reduction in SLA breaches if system integration and real-time monitoring implemented
- Remaining breaches (complex/unavoidable delays) handled more efficiently with reduced stress

#### Related Exceptions

> *Other exceptions that commonly occur together or have similar root causes*

- **EX03 (Third-Party Involvement):** Often causes SLA breaches due to third-party responsiveness delays
- **EX05 (Legal Action Threatened):** Legal review adds time, contributing to SLA pressure
- **PP03 (System Fragmentation):** Major root cause of investigation delays
- **PP07 (Limited SLA Visibility):** Prevents proactive SLA management

---

### EX03: Third-Party Involvement

#### Overview

| Attribute | Value |
|-----------|-------|
| **Exception ID** | EX03 |
| **Exception Name** | Third-Party Involvement |
| **Category** | External Dependency / Coordination Challenge |
| **Affected Process Steps** | PS05 (Investigation), PS06 (Root Cause), PS07 (Resolution) |
| **Frequency** | 10-15 times per month (5-7% of complaints) |
| **Business Impact** | High |
| **Handling Owner** | Investigation Owner + Third-Party Liaison (ownership unclear) |
| **Average Resolution Time** | 45-60 days (doubles standard timeframe) |

#### Trigger Conditions

> *What causes this exception to occur?*

Third-party involvement required when complaint issue originates from or involves action by external provider:
- **Card Schemes (Visa, Mastercard):** Disputed transactions, merchant issues, chargeback investigations
- **Insurance Providers:** Complaints about insurance products sold by bank but underwritten by third party
- **Investment Managers:** Investment performance or advice complaints where bank distributed but third party managed
- **Payment Processors:** International payment delays or errors involving correspondent banks
- **Credit Reference Agencies:** Credit report errors affecting bank's lending decisions
- **Outsourced Service Providers:** Call center, document processing, or other outsourced functions

#### Detection Method

> *How is this exception identified? (System alert, manual review, client complaint, etc.)*

**Detection:** Investigation owner identifies third-party involvement during initial case review (PS04-PS05). Nature of complaint makes this usually obvious (e.g., "My Visa transaction was incorrectly charged"). No system flag or automated detection.

**Detection Timing:** Usually identified within 1-3 days of case assignment.

**Challenge:** Third-party response SLA not tracked in ServiceNow. Bank's SLA clock continues ticking while waiting for third-party response.

#### Business Impact Analysis

> *What happens when this exception occurs? Quantify where possible.*

**Immediate Impact:**
- Investigation paused pending third-party response
- Bank's 30-day SLA continues running (SLA breach risk increases)
- Investigation owner must coordinate with third party (additional workload)

**Downstream Effects:**
- High likelihood of SLA breach (EX02) if third party slow to respond
- Holding letters usually required, increasing client frustration
- Multiple client updates needed to explain delays outside bank's control

**Client Impact:**
- Extended resolution timeframe (often 45-60 days vs. 30 days)
- Frustration with delays, even though client understands third-party involvement
- Perception that bank "passing the buck" rather than owning resolution

**Financial Impact (if applicable):**
- Staff time for third-party coordination: ~2-4 hours per case = ~40-80 hours per month
- Legal costs if third-party disputes liability

**Regulatory/Compliance Risk:**
- Medium-High: FCA expects bank to own complaint resolution even if third party involved
- Bank cannot simply redirect client to third party - must coordinate resolution
- Third-party delays don't exempt bank from SLA obligations

#### Current Handling Procedure

> *Step-by-step: What happens today when this exception is triggered?*

1. **Identification:** Investigation owner determines third-party involvement required
2. **Escalation to Manager:** Notify Complaints Manager and Department Manager (flag for SLA extension likely needed)
3. **Third-Party Contact:**
   - Identify appropriate contact at third party (no centralized directory, varies by provider)
   - Email third party with case details, request investigation and response
   - No formal SLA with most third parties (relationship-dependent)
4. **Bank SLA Management:**
   - Send holding letter to client explaining third-party involvement and extended timeline
   - Update ServiceNow with third-party contact details and expected response date
5. **Chase Third Party:**
   - Weekly follow-up emails if no response received
   - Escalate within third party if delays continue (often unclear who to escalate to)
6. **Receive Third-Party Response:**
   - Review third-party findings
   - Determine bank's position (accept third-party conclusion or dispute)
7. **Resolution:**
   - Draft final response incorporating third-party findings
   - If liability disputed between bank and third party, involve legal team
8. **Client Communication:**
   - Final response explains bank's and third party's roles
   - Ensure client understands outcome and any redress source (bank vs. third party)

**Average Timeline:** 45-60 days from complaint receipt to final response

#### Escalation Path

> *When and to whom does this exception escalate?*

| Escalation Level | Trigger | Owner | SLA |
|------------------|---------|-------|-----|
| Level 1 (Internal) | Third-party involvement identified | Complaints Manager | Immediate notification |
| Level 2 (Third-Party) | No response from third party after 10 days | Department Manager contacts third-party account manager | Escalate within 2 days |
| Level 3 (Executive) | Third party unresponsive, SLA breach imminent | Head of Customer Service contacts third-party executive | Immediate |
| Level 4 (Legal) | Third party disputes liability or client threatens legal action | Legal Team | Immediate |

#### System Behavior

> *How do systems respond to this exception?*

**ServiceNow:** No specific workflow for third-party cases. Investigation owner manually tracks third-party contact and response in case notes. No integration with third-party systems. No separate SLA tracking for third-party response time vs. bank response time.

**Third-Party Systems:** No integration. All communication via email. No shared case management system or API integration.

**Gap:** No visibility of third-party investigation progress. Bank reliant on third-party voluntary updates.

#### Documentation & Evidence

> *What documentation exists for this exception? What audit trail is captured?*

- **Existing Procedures:** Brief guidance in Complaints Handling Policy: "Contact relevant third party and coordinate response." No detailed third-party contact directory or escalation procedures.
- **Audit Trail Captured:** Email correspondence with third party saved to ServiceNow. Third-party response letter attached. Client holding letters and updates saved.
- **Evidence Retained:** Full third-party investigation report (if provided). Often third party provides limited detail, creating evidential gaps.

#### Root Cause Analysis

> *Why does this exception occur? (5-Whys or similar analysis)*

**Root Cause:** Bank's product distribution model relies on third-party providers for certain products/services. Complaint handling process not designed with third-party coordination in mind.

**Contributing Factors:**
- No formal SLAs with third parties for complaint investigation response
- No integrated case management system with third parties
- Relationship management varies by provider (some responsive, others not)
- Bank's contracts with third parties may not include complaint handling provisions
- No dedicated third-party liaison role (investigation owners handle ad hoc)

#### Improvement Opportunities

> *How could this exception be prevented, detected earlier, or handled more efficiently?*

**Prevention:**
- Not preventable (third-party relationships necessary for business model), but can be mitigated:
- Negotiate SLAs with major third-party providers for complaint investigation response (e.g., 10 business days)
- Include complaint handling requirements in new/renewed third-party contracts

**Earlier Detection:**
- Automated flagging at complaint registration: if product/service = [third-party category], flag as third-party case
- Assign extended SLA from start (e.g., 45 days vs. 30 days)

**More Efficient Handling:**
- Establish dedicated Third-Party Liaison role in Complaints team (centralized third-party relationships and escalation)
- Create third-party contact directory with escalation paths
- Implement shared case management platform or API integration with major third parties (e.g., card schemes have complaint portals)
- Template holding letters and client update messages for common third-party scenarios
- Monthly performance review meetings with third parties to discuss complaint handling effectiveness

**Estimated Improvement:**
- 30-40% reduction in resolution time if formal SLAs and dedicated liaison role implemented
- Improved client experience even if timeframe similar (better communication)

#### Related Exceptions

> *Other exceptions that commonly occur together or have similar root causes*

- **EX02 (SLA Breach):** Third-party delays frequently cause SLA breaches
- **EX05 (Legal Action):** Third-party liability disputes may escalate to legal action

---

### EX04: Vulnerable Customer

#### Overview

| Attribute | Value |
|-----------|-------|
| **Exception ID** | EX04 |
| **Exception Name** | Vulnerable Customer |
| **Category** | Regulatory Requirement / Special Handling |
| **Affected Process Steps** | All steps (entire complaint process adjusted) |
| **Frequency** | 40-50 times per month (20-25% of complaints) |
| **Business Impact** | High (regulatory scrutiny, reputational risk) |
| **Handling Owner** | Senior Handler (experienced investigation owner) |
| **Average Resolution Time** | Similar to standard (30 days) but with enhanced care |

#### Trigger Conditions

> *What causes this exception to occur?*

Vulnerable customer identified through:
- **Salesforce CRM flag:** Client previously identified as vulnerable (permanent or temporary) with vulnerability type documented (elderly, disabled, mental health, financial difficulty, bereavement, serious illness, etc.)
- **Self-identification:** Client mentions vulnerability during complaint submission ("I'm struggling with depression and this has made it worse")
- **Staff observation:** Customer Service or investigation owner identifies vulnerability indicators (confusion, distress, comprehension difficulties)
- **Third-party notification:** Power of Attorney, family member, or support worker contacts bank on client's behalf

**Consumer Duty Context:** FCA Consumer Duty requires banks to identify and support vulnerable customers, ensuring fair outcomes tailored to their needs.

#### Detection Method

> *How is this exception identified? (System alert, manual review, client complaint, etc.)*

**Automated Detection:** ServiceNow checks Salesforce CRM for vulnerability flag when complaint registered (API lookup). If flag present, vulnerability alert displayed on ServiceNow case.

**Manual Detection:** Investigation owner reviews CRM during investigation, or identifies vulnerability through client communication.

**Detection Rate:** Estimated 80-90% of vulnerable customers identified (high due to automated flag check). Gap: vulnerabilities not previously flagged in CRM may be missed unless staff observant.

#### Business Impact Analysis

> *What happens when this exception occurs? Quantify where possible.*

**Immediate Impact:**
- Case automatically escalated to senior handler (workload rebalancing required)
- Enhanced communication approach required (more frequent updates, clearer language, phone vs. email preference)
- Additional management oversight and quality review

**Downstream Effects:**
- Positive: Better client outcomes, fairer treatment, reduced ombudsman escalations from vulnerable clients
- Neutral: Slightly longer handling time per case (more careful communication) offset by fewer escalations

**Client Impact:**
- **Positive:** Enhanced support, appropriate communication method, faster escalation if needed, fair outcome considering vulnerability
- **Protection:** Prevents vulnerable clients from being disadvantaged by standard process

**Financial Impact (if applicable):**
- Minimal direct cost (senior handler time similar to junior handler)
- Risk mitigation: Prevents costly ombudsman escalations and regulatory fines for vulnerable customer mistreatment

**Regulatory/Compliance Risk:**
- **Critical Importance:** Consumer Duty makes vulnerable customer treatment a top regulatory priority
- Failure to identify or appropriately handle vulnerable customer complaints = serious regulatory breach
- FCA conducts thematic reviews of vulnerable customer treatment
- Positive: Robust vulnerable customer process demonstrates Consumer Duty compliance

#### Current Handling Procedure

> *Step-by-step: What happens today when this exception is triggered?*

1. **Detection:** Vulnerability flag identified (automated CRM check or manual identification)
2. **Immediate Actions:**
   - Case tagged "Vulnerable Customer" in ServiceNow
   - Automatically assigned to senior handler (not junior staff)
   - Complaints Manager notified for oversight
3. **Communication Approach Adjustment:**
   - Review client's communication preferences in CRM (phone vs. email, best time to call, supporter contact details)
   - Use clearer, simpler language in all communications
   - Offer phone call instead of written communication if appropriate
   - More frequent updates (don't leave client waiting maximum SLA time if resolution possible sooner)
4. **Investigation:**
   - Same thorough investigation as standard case
   - Consider vulnerability context when assessing bank's actions (e.g., was client's vulnerability considered in original service delivery?)
   - Identify if client's vulnerability contributed to complaint occurrence (process failing to accommodate needs)
5. **Resolution:**
   - Consider fair outcome in light of vulnerability (may be more generous redress or accommodation than standard case)
   - Ensure resolution addresses vulnerability-related needs (e.g., process adjustment going forward)
6. **Final Response:**
   - Tailored communication approach
   - Follow-up phone call to explain outcome in addition to written response
   - Signpost support services (e.g., debt advice if financially vulnerable)
7. **Quality Review:**
   - Manager reviews all vulnerable customer final responses before sending (additional quality check beyond standard sample review)
8. **Lessons Learned:**
   - Identify if bank's processes/systems adequately accommodate vulnerability
   - Escalate systemic vulnerability-related issues to senior management

**Average Additional Time:** +1-2 hours per case (more careful communication and management oversight)

#### Escalation Path

> *When and to whom does this exception escalate?*

| Escalation Level | Trigger | Owner | SLA |
|------------------|---------|-------|-----|
| Level 1 (Automatic) | Vulnerability flag detected | Senior Handler | Immediate assignment |
| Level 2 (Manager) | All vulnerable customer final responses | Complaints Manager (quality review) | Before sending |
| Level 3 (Senior) | Vulnerable customer threatens escalation or requests executive contact | Head of Customer Service | Within 1 day |
| Level 4 (Board) | Serious vulnerable customer mistreatment or media risk | CEO / Board Consumer Duty Champion | Immediate |

#### System Behavior

> *How do systems respond to this exception?*

**ServiceNow:** Automated API check of Salesforce CRM for vulnerability flag at case creation. If flag present, case auto-tagged "Vulnerable Customer" and assignment rules route to senior handler pool only. Visual alert displayed prominently on case record.

**Salesforce CRM:** Vulnerability flag displayed in customer record with vulnerability type and notes (e.g., "Client has depression - prefers phone contact, speak slowly and clearly"). Flag can be permanent or temporary with expiry date (e.g., bereavement vulnerability may be temporary).

**Integration Success:** This is one of few working integrations between ServiceNow and Salesforce (API lookup functional).

#### Documentation & Evidence

> *What documentation exists for this exception? What audit trail is captured?*

- **Existing Procedures:** Comprehensive Vulnerable Customer Complaints Handling Procedure (separate policy document). Aligns with Consumer Duty requirements.
- **Audit Trail Captured:** Vulnerability flag recorded on case. All communications saved with notes explaining vulnerable customer considerations. Manager quality review approval tracked.
- **Evidence Retained:** Complete case file demonstrating appropriate handling. Regular audits by Compliance Officer to ensure vulnerable customer process followed.

#### Root Cause Analysis

> *Why does this exception occur? (5-Whys or similar analysis)*

**Note:** This is not a true "exception" caused by process failure - it's a regulatory requirement and customer characteristic. Analysis focuses on ensuring robust identification and handling.

**Why is vulnerable customer identification critical?**
- Consumer Duty legal obligation
- Vulnerable customers at higher risk of poor outcomes if standard process doesn't accommodate needs
- Early identification allows appropriate handling from the start

**Why do some vulnerabilities go undetected?**
- Client hasn't disclosed vulnerability previously (not flagged in CRM)
- Staff not trained to recognize vulnerability indicators
- Client reluctant to disclose (stigma, privacy concerns)

**Improvement Focus:** Enhance detection rate, ensure consistent handling quality.

#### Improvement Opportunities

> *How could this exception be prevented, detected earlier, or handled more efficiently?*

**Better Detection:**
- Proactive vulnerability identification during all client interactions (not just complaints)
- Enhanced staff training on vulnerability indicators
- Annual vulnerability review: contact clients to update vulnerability flags (circumstances change)
- Third-party data sources: credit reference agencies may indicate financial vulnerability

**More Efficient Handling:**
- Vulnerability-specific templates for communication (clear language, supportive tone)
- Checklist for senior handlers: "Vulnerable Customer Handling Checklist" ensures consistent approach
- Dedicated Vulnerable Customer Specialist role (subject matter expert for complex cases)
- Enhanced reporting: track vulnerable customer complaint themes to identify systemic issues

**Process Enhancement:**
- Link vulnerable customer complaints to product/service design: if multiple vulnerable customers complain about same product feature, redesign may be needed
- Proactive outreach to known vulnerable customers if systemic issue identified (protect vulnerable clients first)

**Estimated Impact:**
- Current process already strong (good practice example)
- Enhancements would improve detection rate from 80-90% to 95%+ and reduce handling variability

#### Related Exceptions

> *Other exceptions that commonly occur together or have similar root causes*

- **No direct exception relationship** - vulnerable customer status can co-occur with any other exception (e.g., vulnerable customer + SLA breach, vulnerable customer + third-party involvement)
- When co-occurring, vulnerable customer needs take priority in handling approach

---

### EX05: Legal Action Threatened

#### Overview

| Attribute | Value |
|-----------|-------|
| **Exception ID** | EX05 |
| **Exception Name** | Legal Action Threatened |
| **Category** | Legal Risk / Escalation |
| **Affected Process Steps** | PS05 (Investigation), PS07 (Resolution), PS08 (Final Response) |
| **Frequency** | 5-8 times per month (2-4% of complaints) |
| **Business Impact** | High (legal costs, reputational risk, litigation risk) |
| **Handling Owner** | Investigation Owner + Legal Team |
| **Average Resolution Time** | 45-60 days (legal review adds time) |

#### Trigger Conditions

> *What causes this exception to occur?*

Legal action threatened when client:
- Explicitly mentions "solicitor," "lawyer," "legal advice," "sue," "court action" in complaint
- Submits complaint via solicitor rather than directly
- Indicates formal legal proceedings initiated or intended
- References specific legal grounds (e.g., breach of contract, negligence, data protection breach)

Typically occurs when:
- Client believes significant financial loss caused by bank's action/inaction
- Client believes bank acted unlawfully or negligently
- Complaint involves complex legal interpretation (e.g., contract terms, fiduciary duty)
- Client dissatisfied with initial complaint response and escalating

#### Detection Method

> *How is this exception identified? (System alert, manual review, client complaint, etc.)*

**Detection:** Manual identification by staff reviewing complaint correspondence. Keywords trigger attention: "solicitor," "legal action," "lawyer," "sue." Complaint submitted on solicitor's letterhead obvious indicator.

**Detection Timing:** Usually apparent from initial complaint submission or early correspondence.

**Challenge:** No automated keyword detection in ServiceNow. Relies on staff vigilance.

#### Business Impact Analysis

> *What happens when this exception occurs? Quantify where possible.*

**Immediate Impact:**
- Complaint investigation approach changes (more careful evidence gathering, legal considerations)
- Legal team involvement required (internal legal resource time or external counsel costs)
- Standard complaint timeframes may not apply if litigation commenced (different process)

**Downstream Effects:**
- Higher resolution costs: legal review adds time and expense
- Potential litigation costs if matter proceeds to court (tens of thousands in legal fees)
- Reputational risk if matter becomes public
- Management time diverted to legal matter oversight

**Client Impact:**
- Relationship breakdown: adversarial stance replaces service recovery
- Client unlikely to remain customer regardless of outcome
- Extended timeframe for resolution (legal process slower than complaint process)

**Financial Impact (if applicable):**
- Internal legal review: 3-10 hours per case @ £150/hour = £450-1,500 per case
- External counsel (if required): £5,000-20,000+ depending on complexity
- Settlement/judgment (if unfavorable): varies widely, potentially £10,000-100,000+
- Monthly aggregate exposure: ~£10,000-30,000 in legal costs for 5-8 cases

**Regulatory/Compliance Risk:**
- Medium: FCA expects complaints to be resolved fairly regardless of legal threats
- Bank cannot use legal threat as reason to treat complaint differently (must still investigate fairly)
- If complaint has merit, bank should resolve without forcing client to litigation

#### Current Handling Procedure

> *Step-by-step: What happens today when this exception is triggered?*

1. **Immediate Notification:**
   - Investigation owner immediately notifies Complaints Manager and Department Manager
   - Complaints Manager notifies Legal Team same day
   - Case tagged "Legal Threat" in ServiceNow
2. **Legal Team Assessment:**
   - Legal Team reviews complaint details and client's legal assertions
   - Assess litigation risk (low/medium/high)
   - Provide guidance on investigation approach and communication strategy
3. **Investigation Coordination:**
   - Investigation continues under Legal Team oversight
   - Evidence gathering more thorough (anticipating potential court disclosure)
   - All communications reviewed by Legal Team before sending
   - Preserve all evidence (email chains, system logs, call recordings, etc.)
4. **Communication Approach:**
   - If client now represented by solicitor, all communication directed to solicitor (not client directly)
   - Responses more formal and legally precise (less "customer service" tone)
   - Avoid admissions of liability without legal approval
5. **Resolution Decision:**
   - Legal Team advises on settlement vs. defense posture
   - If complaint has merit: offer fair resolution (may be more generous to avoid litigation costs)
   - If complaint lacks merit: defend position but offer alternative dispute resolution (mediation, Financial Ombudsman)
6. **Final Response:**
   - Legal Team reviews and approves final response before sending
   - Response addresses legal points raised by client/solicitor
   - Clear statement of bank's position and next steps (FOS referral available)
7. **Post-Resolution:**
   - If litigation proceeds, case transferred to Legal Team (no longer complaint process)
   - If settled, document lessons learned for process improvement

**Average Timeline:** 45-60 days (legal review adds 2-4 weeks vs. standard process)

#### Escalation Path

> *When and to whom does this exception escalate?*

| Escalation Level | Trigger | Owner | SLA |
|------------------|---------|-------|-----|
| Level 1 (Legal Team) | Legal threat identified | In-House Legal Counsel | Same-day notification, initial assessment within 2 days |
| Level 2 (Senior Legal) | High litigation risk or significant financial exposure | Head of Legal / General Counsel | Within 1 day |
| Level 3 (Executive) | Litigation commenced or significant reputational risk | CEO / Board Risk Committee | Immediate |
| Level 4 (External Counsel) | Complex legal matter requiring specialist expertise | External Law Firm | As needed |

#### System Behavior

> *How do systems respond to this exception?*

**ServiceNow:** Manual tagging "Legal Threat." No automated detection or workflow changes. Legal Team does not have direct access to ServiceNow (investigation owner forwards information via email).

**Legal Matter Management:** Legal Team may track in separate legal case management system (not integrated with ServiceNow). Potential for information silos and version control issues.

**Gap:** No system integration between complaints and legal. No automated legal review workflow. Communication via email (inefficient, risk of missing updates).

#### Documentation & Evidence

> *What documentation exists for this exception? What audit trail is captured?*

- **Existing Procedures:** Brief guidance in Complaints Handling Policy: "Notify Legal Team immediately if legal action threatened." No detailed procedure for investigation coordination or communication protocols.
- **Audit Trail Captured:** Case tagged in ServiceNow. Legal Team correspondence saved. Legal review approvals documented (email trail). If litigation proceeds, full case file transferred to Legal Team.
- **Evidence Retained:** Enhanced evidence retention for legal threat cases (preserve all emails, call recordings, system logs). Standard document retention policy (7 years) applies, but litigation may require extended retention.

#### Root Cause Analysis

> *Why does this exception occur? (5-Whys or similar analysis)*

**Why do clients threaten legal action?**
- Believe significant financial loss caused by bank
- Dissatisfied with bank's initial complaint response
- Solicitor advises litigation based on legal merits
- Emotional response to frustration (threat may not proceed to actual litigation)

**Why do clients feel need to involve solicitors?**
- Lack of confidence in complaint process delivering fair outcome
- Complexity of legal issues requires expert advice
- Previous negative experience with bank's complaint handling

**Root Cause:** Complaint represents significant financial loss or complex legal issue; client lacks confidence in complaint process; or bank's initial response inadequate (fueling escalation).

**Contributing Factors:**
- Some legal threats preventable if complaint handled better initially (faster resolution, more generous offer, better communication)
- Complex banking products/services create legal ambiguity (e.g., contract interpretation disputes)
- Financial stress motivates clients to pursue legal remedies aggressively

#### Improvement Opportunities

> *How could this exception be prevented, detected earlier, or handled more efficiently?*

**Prevention:**
- Better initial complaint handling reduces escalation to legal threats (address PP05 - inconsistent final response quality)
- Early intervention for high-value complaints: senior handler involvement from start
- Proactive settlement offers when bank clearly at fault (before client seeks legal advice)

**Earlier Detection:**
- Automated keyword detection in ServiceNow: flag cases containing "solicitor," "lawyer," "legal action," etc.
- Early legal team consultation for complex/high-value complaints (before client threatens legal action)

**More Efficient Handling:**
- Integrated complaint-legal workflow in ServiceNow: Legal Team has read/write access to complaint cases
- Pre-approved settlement authority: investigation owners authorized to settle up to £X without legal review (faster resolution for low-value cases)
- Alternative Dispute Resolution (ADR) pathway: offer mediation before litigation (faster and cheaper than court)
- Template legal responses for common scenarios (reduce legal review time)

**Estimated Improvement:**
- 20-30% reduction in legal threats if initial complaint handling improved
- 40-50% reduction in handling time if integrated workflow implemented
- Significant cost savings if more cases settled early vs. proceeding to litigation

#### Related Exceptions

> *Other exceptions that commonly occur together or have similar root causes*

- **EX02 (SLA Breach):** Legal review adds time, increasing SLA breach risk
- **EX03 (Third-Party Involvement):** Third-party liability disputes may escalate to legal action
- **PP05 (Inconsistent Final Response Quality):** Poor initial responses fuel legal escalation

---

### EX06: Systemic Issue Identified

#### Overview

| Attribute | Value |
|-----------|-------|
| **Exception ID** | EX06 |
| **Exception Name** | Systemic Issue Identified |
| **Category** | Critical Escalation / Regulatory Reportable Event |
| **Affected Process Steps** | PS06 (Root Cause), PS10 (Lessons Learned) |
| **Frequency** | 2-3 per quarter (rare but critical) |
| **Business Impact** | Critical (affects multiple clients, regulatory risk, potential mass redress) |
| **Handling Owner** | Senior Management + Compliance Officer |
| **Average Resolution Time** | 3-6 months (systemic fix + client remediation) |

#### Trigger Conditions

> *What causes this exception to occur?*

Systemic issue identified when complaint reveals:
- **Process failure affecting multiple clients:** E.g., incorrect fee charging due to system calculation error
- **System error with widespread impact:** E.g., banking platform processing error affecting transaction category
- **Product design flaw:** E.g., loan product terms unclear or unfair to customer segment
- **Staff training gap:** E.g., multiple complaints about same service failure across branches
- **Third-party provider failure:** E.g., outsourced call center mishandling customer authentication across all clients

Identified through:
- **Single complaint revealing wider issue:** Investigation uncovers that issue affects more than just complainant
- **Pattern analysis:** Multiple complaints about same issue within short timeframe
- **Root cause analysis:** Investigation identifies systemic process/system failure rather than one-off error

#### Detection Method

> *How is this exception identified? (System alert, manual review, client complaint, etc.)*

**Detection:** Manual identification by investigation owner during root cause analysis (PS06) or by Complaints Manager during monthly pattern analysis (PS10).

**Detection Indicators:**
- Investigation reveals system error or process flaw applicable to multiple clients
- Sudden spike in complaints about specific issue (from monthly MI review)
- Investigation owner recognizes complaint similar to recent others

**Detection Rate:** Variable - depends on investigation owner's diligence in root cause analysis and Complaints Manager's pattern analysis. Estimated 80-90% of systemic issues eventually detected, but timing varies (some caught on first complaint, others after multiple complaints).

**Detection Gap:** No automated pattern detection in ServiceNow. Inadequate root cause tracking (PP04) makes pattern analysis difficult.

#### Business Impact Analysis

> *What happens when this exception occurs? Quantify where possible.*

**Immediate Impact:**
- Initial complaint investigation becomes systemic issue investigation (scope expands significantly)
- Urgent investigation required to determine scope (how many clients affected, when did issue start, what's the financial impact)
- Immediate action required to stop ongoing harm (fix system error, halt process, recall product, etc.)

**Downstream Effects:**
- **Proactive client contact:** Bank must identify and contact all affected clients (not just those who complained)
- **Mass redress program:** Compensate all affected clients (not just complainants)
- **Regulatory notification:** FCA must be notified of systemic issues (reportable event)
- **Regulatory investigation risk:** FCA may launch investigation, request detailed reports, impose requirements
- **Reputational damage:** If issue becomes public (media, social media), significant brand damage
- **Process/system remediation:** Fix root cause (system change, process redesign, staff retraining)

**Client Impact:**
- **Complainant:** Resolution of individual complaint, likely enhanced compensation for identifying systemic issue
- **Other affected clients:** Proactive contact from bank, apology, redress (better outcome than if they'd had to complain individually)
- **All clients:** Confidence impacted if systemic issue publicized

**Financial Impact (if applicable):**
- **Redress costs:** Can range from £10,000 (small-scale issue, minimal redress per client) to £1,000,000+ (large-scale issue with significant per-client redress)
- **Investigation costs:** Internal resources (hundreds of hours) + external consultants/auditors if complex
- **Remediation costs:** System fixes, process changes (can be £50,000-500,000 depending on complexity)
- **Regulatory fines:** If FCA determines bank failed to identify/address systemic issue promptly, fines can be £100,000-£10,000,000+ depending on severity
- **Reputational costs:** Lost business, client attrition (difficult to quantify but potentially millions)

**Regulatory/Compliance Risk:**
- **Critical:** Systemic issues are FCA's highest concern (indicate poor governance, risk management, customer outcomes)
- Failure to identify, report, and remediate promptly = serious regulatory breach
- Senior management accountability under SMCR (Senior Managers Certification Regime) - individuals can be fined or banned
- Board-level issue: requires CEO/Board oversight and attestation

#### Current Handling Procedure

> *Step-by-step: What happens today when this exception is triggered?*

1. **Initial Recognition:**
   - Investigation owner or Complaints Manager identifies potential systemic issue
   - Immediately escalate to Head of Customer Service and Compliance Officer
2. **Urgent Assessment (within 24 hours):**
   - Senior management team convenes
   - Assess scope: How many clients potentially affected? What's the timeframe? What's the financial exposure?
   - Assess root cause: Process failure, system error, product flaw, third-party failure?
   - Assess regulatory implications: Is this FCA reportable? How urgent?
3. **Immediate Containment:**
   - Stop ongoing harm: Fix system error, halt process, suspend product, recall materials, etc.
   - Preserve evidence: Freeze system logs, retain all documentation
4. **Regulatory Notification:**
   - If material issue, notify FCA within 24-48 hours (initial notification, detailed report to follow)
   - FCA may impose requirements (e.g., independent review, regular progress updates)
5. **Scope Determination:**
   - Data analysis to identify all affected clients (may require IT team to query databases)
   - Financial impact calculation (total redress liability)
   - Timeline analysis (when did issue start, when was it fixed)
6. **Redress Program Design:**
   - Calculate appropriate redress per client
   - Design proactive contact approach (letter, phone call, etc.)
   - Obtain board approval for redress program budget
7. **Client Contact:**
   - Proactive contact to all affected clients (not waiting for them to complain)
   - Apologize, explain issue, offer redress
   - Provide complaint escalation option if client dissatisfied with redress
8. **Root Cause Remediation:**
   - Fix underlying system/process issue
   - Implement controls to prevent recurrence
   - Staff retraining if needed
9. **Lessons Learned:**
   - Board-level review: Why wasn't this caught earlier? What control failures occurred?
   - Process improvements to enhance early detection
   - Documentation for audit and regulatory review
10. **Regulatory Reporting:**
    - Final report to FCA with remediation details, client outcomes, lessons learned
    - Ongoing monitoring and reporting if FCA requires

**Average Timeline:** 3-6 months from identification to full remediation (varies widely by complexity)

#### Escalation Path

> *When and to whom does this exception escalate?*

| Escalation Level | Trigger | Owner | SLA |
|------------------|---------|-------|-----|
| Level 1 (Immediate) | Systemic issue suspected | Head of Customer Service + Compliance Officer | Within 4 hours |
| Level 2 (Executive) | Systemic issue confirmed | CEO + Board Risk Committee | Within 24 hours |
| Level 3 (Regulatory) | Material systemic issue | FCA notification (reportable event) | Within 24-48 hours |
| Level 4 (Board) | Significant financial/reputational impact | Full Board briefing | Next scheduled board meeting (or emergency meeting if critical) |

#### System Behavior

> *How do systems respond to this exception?*

**ServiceNow:** No automated systemic issue detection. Manual tagging "Systemic Issue." Original complaint case links to systemic issue project, but no formal project management workflow in ServiceNow.

**Data Analysis Systems:** IT team uses database queries to identify affected clients (not integrated with complaint system). Manual process, time-consuming.

**Gap:** No pattern detection AI or automated alerts for complaint clustering. No integrated workflow for systemic issue management (complaint system separate from project management).

#### Documentation & Evidence

> *What documentation exists for this exception? What audit trail is captured?*

- **Existing Procedures:** High-level guidance in Complaints Handling Policy: "Systemic issues must be escalated to senior management and FCA immediately." No detailed procedure for systemic issue investigation, redress program design, or client contact approach.
- **Audit Trail Captured:** Original complaint case detailed. Systemic issue investigation documented in board papers, FCA notifications, project plans (outside ServiceNow). Client redress program tracking (spreadsheet or dedicated project system).
- **Evidence Retained:** Comprehensive documentation for regulatory review: root cause analysis, scope determination data, redress calculations, client contact records, remediation evidence, FCA correspondence.

#### Root Cause Analysis

> *Why does this exception occur? (5-Whys or similar analysis)*

**Note:** Each systemic issue has its own specific root cause (process failure, system error, etc.). This analysis focuses on why systemic issues aren't detected earlier.

**Why are systemic issues not caught before clients complain?**
- Lack of proactive control monitoring (controls detect issues after they occur, not before)
- Inadequate testing before deploying system/process changes
- Poor root cause tracking prevents pattern identification (PP04)

**Why isn't pattern analysis more effective?**
- Root cause data captured as free text (not structured), making pattern analysis difficult
- Monthly pattern analysis timing too slow (systemic issues should be detected weekly or real-time)
- No automated pattern detection or clustering algorithms

**Root Cause of Detection Delays:**
- Reactive complaint handling (wait for clients to complain rather than proactive monitoring)
- Inadequate root cause taxonomy (PP04)
- No real-time pattern detection
- Control gaps in change management and testing

**Contributing Factors:**
- Complex banking systems make systemic issues difficult to predict
- Change management processes may not include adequate testing or impact analysis
- Staff may not recognize individual complaint as part of wider pattern

#### Improvement Opportunities

> *How could this exception be prevented, detected earlier, or handled more efficiently?*

**Prevention:**
- Enhanced change management: Rigorous testing and impact analysis before deploying system/process changes
- Proactive control monitoring: Controls detect anomalies before clients affected (e.g., automated alerts for unusual transaction patterns)
- Product design reviews: Customer fairness assessment before launching new products

**Earlier Detection:**
- **Structured root cause taxonomy** (addresses PP04): Enables automated pattern detection
- **Automated clustering analysis:** AI identifies complaint patterns in real-time ("5 complaints about [issue] in last 48 hours - investigate systemic cause")
- **Weekly pattern analysis** (vs. monthly): Faster detection, limits client impact
- **Proactive monitoring dashboards:** Real-time system/process performance metrics identify issues before complaints

**More Efficient Handling:**
- **Systemic Issue Response Playbook:** Standardized approach to scope determination, redress calculation, client contact, regulatory notification
- **Integrated systemic issue workflow:** Project management system linked to complaint system for seamless case tracking
- **Pre-approved redress frameworks:** Board-approved redress calculation methodologies (speeds up redress program design)
- **Third-party specialists:** Retain consulting firms for complex systemic issue investigations (faster than internal resources)

**Estimated Improvement:**
- 50-70% faster detection if automated pattern analysis implemented
- 30-40% reduction in client impact if detected earlier (fewer clients affected before issue stopped)
- 25-30% reduction in handling time if standardized playbook used

#### Related Exceptions

> *Other exceptions that commonly occur together or have similar root causes*

- **PP04 (Inadequate Root Cause Tracking):** Major barrier to early systemic issue detection
- **PP08 (No Systematic Lessons Learned):** Failure to implement lessons learned from previous systemic issues increases recurrence risk
- Multiple individual complaints may be related to undetected systemic issue

---

## Exception Patterns & Insights

### Clustering Analysis

> *Are there patterns in when/why exceptions occur?*

**Temporal Patterns:**
- **SLA breaches (EX02)** increase in Q4 (November-December) due to staff annual leave and holiday volume pressures
- **Duplicate complaints (EX01)** increase when acknowledgment letters delayed (clients resubmit thinking original not received)
- **Third-party involvement (EX03)** spikes around holiday periods (card transaction disputes from travel/shopping)

**Causality Patterns:**
- System fragmentation (PP03) is root cause of multiple exceptions: EX02 (SLA breaches due to slow investigations), EX01 (duplicate detection failures)
- Inadequate root cause tracking (PP04) delays systemic issue detection (EX06)
- Lack of real-time SLA visibility (PP07) prevents proactive intervention for SLA breaches (EX02)

**Co-Occurrence Patterns:**
- Third-party involvement (EX03) + SLA breach (EX02) = 60% co-occurrence rate (third-party delays cause SLA breaches)
- Vulnerable customer (EX04) + any other exception = requires especially careful handling (vulnerability needs + exception complexity)

### High-Impact Exception Summary

> *Exceptions requiring priority attention in transformation planning*

**Priority 1 - Critical:**
- **EX06 (Systemic Issue):** Rare but highest impact. Requires automated pattern detection and faster response capability.

**Priority 2 - High:**
- **EX02 (SLA Breach):** Most frequent high-impact exception. Addresses PP03 (system integration) and PP07 (real-time SLA visibility) to reduce occurrence.
- **EX04 (Vulnerable Customer):** Regulatory critical. Current process strong but requires ongoing vigilance and staff training.

**Priority 3 - Medium:**
- **EX03 (Third-Party Involvement):** Requires formal SLAs with third parties and dedicated liaison role.
- **EX05 (Legal Action):** Better initial complaint handling reduces legal escalations. Integrated legal-complaint workflow improves efficiency.

**Priority 4 - Low:**
- **EX01 (Duplicate Complaint):** Automated detection is quick win, minimal complexity.

### Exception-to-Pain-Point Mapping

> *How do exceptions relate to identified pain points?*

| EX# | Related Pain Points (PP#) | Connection |
|-----|---------------------------|------------|
| EX01 | PP02 (Lack of Automated Duplicate Detection) | Pain point is root cause of exception |
| EX02 | PP03 (System Fragmentation), PP07 (Limited SLA Visibility) | Pain points are major contributors to SLA breaches |
| EX03 | (No direct pain point link - external dependency) | New pain point could be identified: "Third-party coordination inefficiency" |
| EX04 | (No pain point link - regulatory requirement) | Process strength, not weakness |
| EX05 | PP05 (Inconsistent Final Response Quality) | Poor initial responses fuel legal escalation |
| EX06 | PP04 (Inadequate Root Cause Tracking), PP08 (No Systematic Lessons Learned) | Pain points delay systemic issue detection |

---

## Recommendations for TO-BE Design

> *Key considerations for the Transformation Agent when addressing exceptions*

### Design Principles

1. **Automate Exception Detection:** System should automatically identify and flag exceptions at case creation or during investigation (duplicates, third-party involvement, SLA risk, legal threats, systemic patterns).

2. **Differentiated Workflows:** TO-BE process should have distinct workflows for exception types (not one-size-fits-all). Example: Third-party cases automatically assigned extended SLA and routed to specialist handler.

3. **Proactive vs. Reactive:** Shift from reactive exception handling (wait for problem to occur, then escalate) to proactive (predict and prevent). Example: SLA breach prediction model identifies at-risk cases before deadline.

4. **Integration & Visibility:** Integrate complaint system with related systems (legal, third-party portals, CRM) for seamless exception coordination. Real-time dashboards for SLA, systemic patterns, etc.

5. **Standardized Playbooks:** Develop exception-specific playbooks with clear escalation paths, required actions, and quality gates. Reduces variability in exception handling quality.

### Specific Recommendations by Exception

**EX01 (Duplicate):**
- Implement automated duplicate detection at case creation (fuzzy matching on client + issue + date)
- One-click merge functionality
- Estimated impact: 80% reduction in duplicate occurrence

**EX02 (SLA Breach):**
- Real-time SLA dashboard with predictive alerts (flag at-risk cases before deadline)
- System integration to reduce investigation time (addresses PP03)
- Case complexity triage at intake (assign tiered SLAs based on complexity)
- Estimated impact: 50-60% reduction in SLA breaches

**EX03 (Third-Party):**
- Formal SLAs with third-party providers (10-day investigation response)
- Dedicated Third-Party Liaison role
- API integration with major third parties for shared case management
- Auto-assign extended SLA (45 days) at case creation if third-party flagged
- Estimated impact: 30-40% reduction in resolution time

**EX04 (Vulnerable Customer):**
- Continue current strong process
- Enhance detection through proactive vulnerability identification (all interactions, not just complaints)
- AI-assisted communication tailoring (suggest appropriate language/channel based on vulnerability type)
- Estimated impact: Maintain current high standard, improve detection rate 5-10%

**EX05 (Legal Threat):**
- Automated keyword detection for legal threats (flag cases containing trigger words)
- Integrated complaint-legal workflow (legal team direct access to complaint system)
- Pre-approved settlement authority for low-value cases (faster resolution without legal review)
- Alternative Dispute Resolution pathway (offer mediation before litigation)
- Estimated impact: 20-30% reduction in legal escalations; 40-50% reduction in handling time

**EX06 (Systemic Issue):**
- Structured root cause taxonomy for pattern analysis (addresses PP04)
- Automated clustering/pattern detection (AI identifies complaint themes in real-time)
- Weekly pattern analysis (vs. monthly) for faster detection
- Systemic Issue Response Playbook (standardized approach to scope, redress, regulatory notification)
- Estimated impact: 50-70% faster detection; 30-40% reduction in client impact

### Technology Enablers

- **ServiceNow Configuration:** Duplicate detection rules, SLA dashboards, automated escalation workflows, exception-specific case routing
- **AI/ML Models:** Duplicate detection, SLA breach prediction, systemic pattern clustering, legal threat keyword detection
- **Integration APIs:** ServiceNow-Salesforce (enhanced), ServiceNow-Legal system, third-party complaint portals
- **Reporting & Analytics:** Real-time exception dashboards, predictive analytics, automated regulatory reporting

### Success Metrics for Exception Handling

| Exception | Current State | TO-BE Target | Measurement |
|-----------|---------------|--------------|-------------|
| EX01 Duplicate Rate | 10% | <2% | % of complaints identified as duplicates |
| EX02 SLA Breach Rate | 15-20% | <8% | % of complaints exceeding 30-day SLA |
| EX03 Third-Party Resolution Time | 45-60 days | <35 days | Average days from receipt to final response |
| EX04 Vulnerable Detection Rate | 80-90% | >95% | % of vulnerable customers correctly identified |
| EX05 Legal Threat Cases | 2-4% | <2% | % of complaints escalating to legal threats |
| EX06 Systemic Issue Detection Time | Weeks | Days | Average time from first complaint to systemic issue identification |

---

## Change Log

| Date | Contributor | Role | Changes |
|------|-------------|------|---------|
| 2025-12-04 | Orchestration Test | Process Owner - Compliance Officer | Initial exception detail analysis - documented 6 exception scenarios with handling procedures, root cause analysis, and improvement opportunities |

---

_Generated by ProcessMiner Process Documentation Analyst_
_Document ID: P005-EXCEPTIONS-20251204_
