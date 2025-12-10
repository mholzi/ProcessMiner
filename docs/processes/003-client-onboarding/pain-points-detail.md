# Pain Points & Improvement Opportunities: Client Onboarding

**Process ID:** COB-003
**Document Type:** Pain Point Detail Analysis
**Last Updated:** 2025-12-09
**Related Document:** [AS-IS Process Documentation](./as-is-process-documentation.md)

---

## Executive Summary

The BizBanking Client Onboarding process has 6 identified pain points affecting operational efficiency and client experience. Two pain points (PP-COB-001, PP-COB-002) are rated HIGH severity and represent the primary transformation opportunities.

System fragmentation is the dominant theme — staff navigate 6+ systems with no unified client view, leading to data re-entry, errors, and frustration. Process inefficiencies around document handling and client communication compound these system issues. Three pain points qualify as quick wins with low effort and meaningful impact.

---

## Pain Point Summary Table

| PP# | Pain Point | Category | Affected Steps | Impact | Frequency | Priority | Quick Win? |
|-----|------------|----------|----------------|--------|-----------|----------|------------|
| PP-COB-001 | Manual document chasing | PROCESS | PS-COB-001, PS-COB-002 | HIGH | HIGH (~30%) | P1 | Yes |
| PP-COB-002 | System switching / No single view | SYSTEM | All steps | HIGH | HIGH (100%) | P1 | No |
| PP-COB-003 | KYC screening false positives | SYSTEM | PS-COB-002 | MEDIUM | HIGH | P2 | No |
| PP-COB-004 | Paper-based signatures | PROCESS | PS-COB-001 | MEDIUM | MEDIUM (~40%) | P2 | Yes |
| PP-COB-005 | Credit bureau delays | SYSTEM | PS-COB-003 | LOW | MEDIUM | P3 | No |
| PP-COB-006 | Welcome call scheduling | PROCESS | PS-COB-005 | MEDIUM | HIGH (~70%) | P2 | Yes |

---

## Pain Point Statistics

| Metric | Value |
|--------|-------|
| Total Pain Points Identified | 6 |
| High-Impact Pain Points | 2 |
| Frequently Occurring (Daily+) | 4 |
| Client-Facing Pain Points | 4 |
| Staff/Operational Pain Points | 2 |
| Compliance/Risk Pain Points | 1 |
| Quick Win Opportunities | 3 |
| Automation Candidates | 4 |

---

## Pain Point Categories

| Category | Count | Combined Impact | Top Priority |
|----------|-------|-----------------|--------------|
| PROCESS | 3 | HIGH | PP-COB-001 |
| SYSTEM | 3 | HIGH | PP-COB-002 |

---

## Detailed Pain Point Analysis

### PP-COB-001: Manual document chasing

| Attribute | Value |
|-----------|-------|
| **Pain Point ID** | PP-COB-001 |
| **Category** | PROCESS |
| **Affected Steps** | PS-COB-001: Application Receipt, PS-COB-002: KYC Verification |
| **Severity** | HIGH |
| **Impact** | 2-3 follow-ups per application, delays onboarding by 2-5 days |
| **Frequency** | HIGH (~30% of applications) |
| **Priority** | P1 — Quick win with automation |

#### Description

Operations Officers must manually track and chase missing documents with no automated reminder system. When an application arrives incomplete, staff manually send email reminders, track responses in spreadsheets, and follow up multiple times. On average, each incomplete application requires 2-3 follow-up cycles before documents are received.

This pain point affects approximately 30% of all applications and is the primary driver of onboarding delays. Staff time is consumed by repetitive administrative tasks rather than value-added verification work.

#### Root Cause Analysis

1. No automated document tracking or reminder system in OWS
2. Online portal allows submission without complete documents
3. Document requirements vary by client type, causing confusion
4. No real-time document validation or feedback to clients

#### Current Workarounds

- Staff maintain personal Excel trackers for follow-ups
- Calendar reminders set manually for each case
- Email templates used but manually triggered
- Escalation to RM after 10 days (manual process)

#### Improvement Opportunities

- **Quick Win**: Implement automated email reminders at 3, 7, and 14 days
- **Medium-term**: Add document upload validation to online portal
- **Long-term**: Client portal with real-time document status and upload capability

#### Estimated Impact of Fix

Automated reminders would reduce staff time by approximately 30 minutes per incomplete case. With ~30 incomplete applications per month, this saves 15+ hours monthly. More importantly, automated reminders typically improve document response rates by 40%, reducing overall cycle time.

---

### PP-COB-002: System switching / No single client view

| Attribute | Value |
|-----------|-------|
| **Pain Point ID** | PP-COB-002 |
| **Category** | SYSTEM |
| **Affected Steps** | All process steps (PS-COB-001 through PS-COB-006) |
| **Severity** | HIGH |
| **Impact** | 6+ systems, data entry errors, staff frustration |
| **Frequency** | HIGH (100% of applications) |
| **Priority** | P1 — Strategic initiative |

#### Description

Staff must access and switch between 6+ systems during onboarding: CRM (Salesforce), OWS, Fenergo, World-Check, T24 (CBS), CDS, DMS, and Card Management. There is no unified client view — staff copy-paste data between systems, leading to errors and inefficiency. The same client information is entered multiple times across different screens.

This is the most pervasive pain point, affecting every single application. Staff consistently cite this as their top frustration, particularly during high-volume periods when fatigue increases error rates.

#### Root Cause Analysis

1. Systems implemented at different times by different vendors
2. No integration layer or API orchestration between systems
3. Each system has its own client data model
4. Historical IT investment decisions prioritized features over integration

#### Current Workarounds

- Copy-paste between system screens
- Personal data staging templates in Excel
- Dual monitors to view multiple systems simultaneously
- Checker role includes cross-system data verification

#### Improvement Opportunities

- **Quick Win**: Create unified view dashboard pulling from existing APIs
- **Medium-term**: Implement API integration for core data fields
- **Long-term**: Unified client data platform or system consolidation

#### Estimated Impact of Fix

Full integration would eliminate an estimated 2 hours of manual data entry per application. With 100 applications per month, this represents 200+ hours of productivity gains. Error rates would drop from ~5% to near-zero, eliminating 20+ hours of monthly rework.

---

### PP-COB-003: KYC screening false positives

| Attribute | Value |
|-----------|-------|
| **Pain Point ID** | PP-COB-003 |
| **Category** | SYSTEM |
| **Affected Steps** | PS-COB-002: KYC Verification |
| **Severity** | MEDIUM |
| **Impact** | ~40% false positive rate, manual review burden |
| **Frequency** | HIGH |
| **Priority** | P2 — System optimization |

#### Description

World-Check screening generates approximately 40% false positives, requiring manual Compliance Officer review for each hit. Common Irish names (Murphy, O'Brien, Kelly) are particularly problematic, triggering matches that are almost always false positives. Each false positive takes 15-30 minutes to investigate and clear.

#### Root Cause Analysis

1. World-Check matching algorithm is overly broad
2. No pre-screening using date of birth or address
3. Common name disambiguation not implemented
4. Configuration has not been optimized for Irish market

#### Current Workarounds

- Compliance maintains "cleared names" reference list
- Experienced analysts recognize repeat false positives quickly
- Batch processing of obvious false positives

#### Improvement Opportunities

- **Quick Win**: Configure tighter matching parameters for common names
- **Medium-term**: Implement pre-screening using DOB and address
- **Long-term**: Evaluate alternative screening tools with better precision

#### Estimated Impact of Fix

Reducing false positive rate from 40% to 15% would eliminate approximately 25 manual reviews per month, saving 8-12 hours of Compliance Officer time and reducing KYC cycle time.

---

### PP-COB-004: Paper-based signatures

| Attribute | Value |
|-----------|-------|
| **Pain Point ID** | PP-COB-004 |
| **Category** | PROCESS |
| **Affected Steps** | PS-COB-001: Application Receipt |
| **Severity** | MEDIUM |
| **Impact** | 1-2 day delay for digitization |
| **Frequency** | MEDIUM (~40% of applications) |
| **Priority** | P2 — Quick win |

#### Description

Approximately 40% of applications still arrive as paper documents requiring manual digitization. Paper applications must be scanned, indexed, and uploaded to DMS before processing can begin. This creates a 1-2 day delay compared to digital submissions and increases risk of document loss or quality issues.

#### Root Cause Analysis

1. Some clients prefer paper processes
2. Partner channel (accountants, solicitors) often submit paper
3. Walk-in clients at branches complete paper forms
4. E-signature not yet implemented for all document types

#### Current Workarounds

- Dedicated scanning station in operations area
- Same-day scanning target (not always achieved)
- Manual indexing and quality checks

#### Improvement Opportunities

- **Quick Win**: Implement e-signature solution (DocuSign, Adobe Sign)
- **Medium-term**: Partner portal for digital submission
- **Long-term**: Eliminate paper channel entirely

#### Estimated Impact of Fix

E-signature implementation would eliminate 1-2 day delay for 40% of applications, improving overall cycle time and client experience. Annual cost savings from reduced printing, postage, and scanning estimated at €15,000-20,000.

---

### PP-COB-005: Credit bureau delays

| Attribute | Value |
|-----------|-------|
| **Pain Point ID** | PP-COB-005 |
| **Category** | SYSTEM |
| **Affected Steps** | PS-COB-003: Credit Assessment |
| **Severity** | LOW |
| **Impact** | Variable response times (instant to 24hrs), no visibility |
| **Frequency** | MEDIUM |
| **Priority** | P3 — Monitor |

#### Description

Credit bureau response times are inconsistent, ranging from instant to 24+ hours. Credit Analysts have no visibility into when data will be available, making workload planning difficult. During bureau system issues, applications queue without clear expected resolution time.

#### Root Cause Analysis

1. Bureau system capacity varies by time of day
2. Complex queries (multiple directors) take longer
3. No SLA enforcement or visibility mechanism
4. Legacy integration without status tracking

#### Current Workarounds

- Analysts check periodically for bureau data
- Work on other cases while waiting
- Escalate to IT if delays exceed 24 hours

#### Improvement Opportunities

- **Medium-term**: Implement webhook notification when data ready
- **Long-term**: Real-time bureau integration or caching layer

#### Estimated Impact of Fix

Webhook notifications would improve analyst efficiency by eliminating periodic checking. Impact is relatively low compared to other pain points.

---

### PP-COB-006: Welcome call scheduling

| Attribute | Value |
|-----------|-------|
| **Pain Point ID** | PP-COB-006 |
| **Category** | PROCESS |
| **Affected Steps** | PS-COB-005: Client Communication |
| **Severity** | MEDIUM |
| **Impact** | Average 3 attempts to reach client |
| **Frequency** | HIGH (~70% of clients require multiple attempts) |
| **Priority** | P2 — Quick win |

#### Description

Relationship Managers struggle to reach clients for welcome calls, averaging 3 attempts before successful contact. There is no self-service scheduling option — RMs call clients at various times hoping to connect. This creates frustration for both RMs and clients, and delays the relationship-building objective of the welcome call.

#### Root Cause Analysis

1. No self-service scheduling option for clients
2. RMs call during business hours when clients are busy
3. No callback scheduling or voicemail coordination
4. Mobile numbers often go to voicemail

#### Current Workarounds

- Multiple call attempts at different times
- Email follow-up requesting callback
- Some RMs use personal Calendly for scheduling

#### Improvement Opportunities

- **Quick Win**: Implement self-service scheduling (Calendly or similar)
- **Medium-term**: Integrate scheduling with CRM
- **Long-term**: Offer video call option for convenience

#### Estimated Impact of Fix

Self-service scheduling typically reduces attempts from 3 to 1, saving 15-20 minutes per onboarding. With 100 onboardings per month, this saves 25-33 hours monthly and improves client experience.

---

## Pain Point Patterns & Themes

### Theme Analysis

> *What patterns emerge across pain points?*

*[To be completed]*

### Automation Opportunities

> *Pain points that are strong candidates for automation*

| PP# | Pain Point | Automation Type | Feasibility | Impact |
|-----|------------|-----------------|-------------|--------|
*[To be completed]*

### Quick Wins

> *Pain points that can be addressed with minimal effort/risk*

| PP# | Pain Point | Proposed Solution | Effort | Timeline |
|-----|------------|-------------------|--------|----------|
*[To be completed]*

### High-Complexity Transformations

> *Pain points requiring significant change - strategic initiatives*

*[To be completed]*

---

## Prioritized Recommendations

### Priority 1: Critical (Address Immediately)

*[To be completed]*

### Priority 2: High (Address in 0-6 months)

*[To be completed]*

### Priority 3: Medium (Address in 6-12 months)

*[To be completed]*

### Priority 4: Low (Backlog / Future Consideration)

*[To be completed]*

---

## Input for Downstream Agents

### For Transformation Agent

> *Key pain points to address in TO-BE design*

*[To be completed]*

### For Client Journey Analyst

> *Pain points with client experience impact*

*[To be completed]*

### For Control Analyst

> *Pain points affecting compliance/controls*

*[To be completed]*

### For Innovation Analyst

> *Pain points that might benefit from emerging technologies*

*[To be completed]*

---

## Change Log

| Date | Contributor | Role | Changes |
|------|-------------|------|---------|
| 2025-12-09 | Markus | RTM | Initial pain point analysis |

---

_Generated by ProcessMiner Process Documentation Analyst_
_Document ID: COB-003-pain-points_
