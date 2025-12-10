# Exception Paths & Variations: Client Onboarding

**Process ID:** COB-003
**Document Type:** Exception Detail Analysis
**Last Updated:** 2025-12-09
**Related Document:** [AS-IS Process Documentation](./as-is-process-documentation.md)

---

## Executive Summary

The BizBanking Client Onboarding process has 5 documented exception paths that deviate from standard flow. Incomplete Documentation is the highest-frequency exception (~30% of applications), while KYC Screening Hits and System Downtime carry the highest impact due to regulatory and operational implications respectively.

Exception handling is well-defined with clear ownership, though manual intervention is required for all exceptions. The documentation-related exception drives the majority of processing delays, representing a key opportunity for automation and process improvement.

---

## Exception Summary Table

| EX# | Exception Name | Trigger Condition | Affected Steps | Frequency | Business Impact | Handling Owner |
|-----|----------------|-------------------|----------------|-----------|-----------------|----------------|
| EX-COB-001 | Incomplete Documentation | Required docs missing after submission | PS-COB-001, PS-COB-002 | HIGH (~30%) | MEDIUM | Operations Officer |
| EX-COB-002 | KYC Screening Hit | World-Check match on director/UBO | PS-COB-002 | LOW (~5%) | HIGH | Compliance Officer |
| EX-COB-003 | Credit Decline | Credit assessment fails scorecard | PS-COB-003 | MEDIUM (~15%) | MEDIUM | Relationship Manager |
| EX-COB-004 | System Downtime | CBS unavailable >4 hours | PS-COB-004 | LOW (rare) | HIGH | IT Service Desk |
| EX-COB-005 | Complex Ownership Structure | >3 layers, foreign shareholders, trusts | PS-COB-002 | MEDIUM (~20%) | MEDIUM | Senior KYC Analyst |

---

## Exception Statistics

| Metric | Value |
|--------|-------|
| Total Exceptions Identified | 5 |
| High-Impact Exceptions | 2 |
| Frequently Occurring (>10% of cases) | 3 |
| Exceptions Requiring Manual Intervention | 5 |
| Exceptions with Documented Procedures | 5 |
| Exceptions Lacking Clear Ownership | 0 |

---

## Detailed Exception Analysis

### EX-COB-001: Incomplete Documentation

| Attribute | Value |
|-----------|-------|
| **Exception ID** | EX-COB-001 |
| **Category** | Documentation |
| **Affected Steps** | PS-COB-001: Application Receipt, PS-COB-002: KYC Verification |
| **Frequency** | HIGH (~30% of applications) |
| **Impact** | MEDIUM — Delays processing by 2-3 days on average |
| **Handling Owner** | Operations Officer |

#### Description

This exception occurs when a client application cannot proceed through verification due to missing or incomplete documentation. Common missing items include CRO company documents, certified copies of director identification, proof of address dated within 3 months, and beneficial ownership declarations for corporate clients.

The exception is most prevalent in self-service channel applications where clients submit without relationship manager guidance. It results in the application being placed on hold while the client is contacted for additional documentation.

#### Trigger Conditions

- Client submits application without all required KYC documents
- Documents provided are expired, illegible, or do not meet certification requirements
- Corporate structure documentation is incomplete or missing beneficial owner information
- Business plan not provided for companies trading <2 years

#### Current Handling Procedure

1. Operations Officer identifies missing documentation during triage (PS-COB-001)
2. Case status updated to "Pending Documentation" in OWS
3. "Missing Documents" email template (TPL-BB-001) sent to client
4. Case placed in 5-day follow-up queue
5. If no response after 10 business days, escalate to Relationship Manager
6. If no response after 20 business days, application auto-expires

#### Root Cause Analysis

The primary root cause is insufficient upfront guidance to clients on documentation requirements. The online application portal lists requirements but does not prevent submission of incomplete applications. Additionally, document requirements vary by client type (sole trader vs. limited company), creating confusion for clients unfamiliar with the process.

#### Improvement Opportunities

- Implement mandatory document upload validation in the online portal before submission
- Create segment-specific document checklists with visual examples
- Add automated document completeness checking with real-time feedback
- Consider document collection service integration for high-value clients

---

### EX-COB-002: KYC Screening Hit

| Attribute | Value |
|-----------|-------|
| **Exception ID** | EX-COB-002 |
| **Category** | Compliance |
| **Affected Steps** | PS-COB-002: KYC Verification |
| **Frequency** | LOW (~5% of applications) |
| **Impact** | HIGH — Requires Compliance escalation, potential MLRO involvement |
| **Handling Owner** | Compliance Officer |

#### Description

This exception occurs when a director or Ultimate Beneficial Owner triggers a match in World-Check screening for PEP status, sanctions listing, or adverse media. All screening hits require manual review by the Compliance Officer to determine if the match is a true positive or false positive.

True positive PEP matches require Enhanced Due Diligence (EDD) procedures. True positive Sanctions matches require immediate escalation to the MLRO and process halt.

#### Trigger Conditions

- Director or UBO name matches PEP database entry
- Director or UBO name matches sanctions list
- Adverse media search returns relevant negative results
- Internal watchlist match identified

#### Current Handling Procedure

1. KYC Analyst identifies screening hit during verification (PS-COB-002)
2. Case immediately escalated to Compliance Officer
3. Compliance Officer reviews match details and source data
4. False positive: Document rationale, clear case, return to KYC queue
5. True positive PEP: Initiate EDD procedures, senior management approval required
6. True positive Sanctions: Escalate to MLRO immediately, do not proceed

#### Root Cause Analysis

World-Check screening generates a high volume of false positives (~40%) due to common name matches, particularly for Irish names like Murphy, O'Brien, and Kelly. The screening algorithm does not effectively filter by geography or date of birth, resulting in excessive manual review workload.

#### Improvement Opportunities

- Implement pre-screening name disambiguation using date of birth and address
- Configure World-Check with tighter matching parameters for common names
- Develop automated false positive resolution for repeat clear cases
- Consider supplementary screening tool with better precision

---

### EX-COB-003: Credit Decline

| Attribute | Value |
|-----------|-------|
| **Exception ID** | EX-COB-003 |
| **Category** | Credit |
| **Affected Steps** | PS-COB-003: Credit Assessment |
| **Frequency** | MEDIUM (~15% of overdraft applications) |
| **Impact** | MEDIUM — Revenue impact, client experience impact |
| **Handling Owner** | Relationship Manager |

#### Description

This exception occurs when a credit assessment for an overdraft facility fails the scorecard or policy criteria. Declines may result from poor credit bureau scores, inadequate financial history, insufficient trading history, or policy breaches (e.g., director with previous insolvency).

The decline does not terminate the onboarding — clients are offered an account-only product as an alternative.

#### Trigger Conditions

- Credit bureau score below threshold
- Financial ratios (DSCR, gearing) outside policy limits
- Director has adverse credit history or previous insolvency
- Insufficient trading history for requested facility size

#### Current Handling Procedure

1. Credit Analyst completes assessment and generates decline recommendation
2. Decline reviewed by Credit Manager (if within policy) or Credit Committee (if exception)
3. Relationship Manager notified of decline with rationale (where permissible)
4. RM contacts client to explain outcome and offer account-only alternative
5. Decline documented in CRM for future reference

#### Root Cause Analysis

Credit declines primarily result from early-stage businesses with insufficient trading history or directors with prior adverse credit events. The scorecard is appropriately calibrated for risk but may be overly conservative for new businesses with strong prospects.

#### Improvement Opportunities

- Develop alternative assessment criteria for startup businesses
- Consider guarantor/security options to enable marginal cases
- Implement credit appetite tiers based on RM relationship strength
- Build automated decline prediction to set expectations earlier

---

### EX-COB-004: System Downtime

| Attribute | Value |
|-----------|-------|
| **Exception ID** | EX-COB-004 |
| **Category** | System |
| **Affected Steps** | PS-COB-004: Account Setup |
| **Frequency** | LOW (rare — estimated 2-3 times per year) |
| **Impact** | HIGH — SLA breach, BCP activation, operational disruption |
| **Handling Owner** | IT Service Desk |

#### Description

This exception occurs when the Core Banking System (CBS - Temenos T24) is unavailable for more than 4 hours, preventing account creation and configuration. This triggers Business Continuity Planning (BCP) procedures and manual workarounds.

#### Trigger Conditions

- CBS system outage exceeding 4 hours
- Scheduled maintenance extending beyond planned window
- Network connectivity issues to CBS environment
- CBS database performance degradation causing timeouts

#### Current Handling Procedure

1. IT Service Desk declares CBS unavailability incident
2. Operations Team Lead activates BCP manual process
3. Applications queued manually in spreadsheet tracker
4. Client notifications sent regarding potential delays
5. When CBS restored, manual entries reconciled and processed
6. Post-incident review conducted

#### Root Cause Analysis

System downtime incidents are typically caused by infrastructure issues (hardware failures, network problems) or unplanned maintenance activities. The CBS platform (T24) is aging and scheduled for replacement in the next 2-3 years.

#### Improvement Opportunities

- Implement real-time system health monitoring with predictive alerts
- Develop automated failover capabilities for critical functions
- Accelerate CBS modernization program
- Create streamlined BCP procedures to minimize manual effort

---

### EX-COB-005: Complex Ownership Structure

| Attribute | Value |
|-----------|-------|
| **Exception ID** | EX-COB-005 |
| **Category** | Compliance |
| **Affected Steps** | PS-COB-002: KYC Verification |
| **Frequency** | MEDIUM (~20% of applications) |
| **Impact** | MEDIUM — Extended timeline (5-10 additional days), specialist resource required |
| **Handling Owner** | Senior KYC Analyst |

#### Description

This exception occurs when a client's ownership structure exceeds standard complexity thresholds, requiring specialist review and potentially legal consultation. Complex structures include multiple corporate layers, foreign-registered entities in the ownership chain, or trust arrangements.

#### Trigger Conditions

- Ownership structure with more than 3 corporate layers
- Foreign-registered companies in ownership chain
- Trust structures as shareholders or beneficial owners
- Nominee arrangements or bearer shares
- Multiple UBOs with combined ownership triggering threshold

#### Current Handling Procedure

1. KYC Analyst identifies complex structure during verification
2. Case escalated to Senior KYC Analyst for specialist review
3. Additional documentation requested (trust deeds, foreign company extracts)
4. If trust involved, Legal review required before proceeding
5. Enhanced ownership diagram created and documented
6. Senior KYC Analyst completes verification and risk assessment

#### Root Cause Analysis

Complex ownership structures are inherent to certain business types (family businesses, investment vehicles, cross-border operations) and cannot be eliminated. The challenge is ensuring adequate due diligence without creating excessive delays or client friction.

#### Improvement Opportunities

- Develop pre-qualification questionnaire to identify complexity upfront
- Create specialist KYC track for complex structures from initial triage
- Build automated structure visualization tools
- Establish panel of pre-approved legal advisors for faster turnaround

---

## Exception Patterns & Insights

### Clustering Analysis

Exceptions cluster around two process phases:
1. **Documentation/Verification Phase (PS-COB-001, PS-COB-002)**: 3 of 5 exceptions occur here, accounting for ~55% of exception volume
2. **Credit/Setup Phase (PS-COB-003, PS-COB-004)**: 2 exceptions, less frequent but higher individual impact

### High-Impact Exception Summary

| EX# | Exception | Why High Impact | Priority |
|-----|-----------|-----------------|----------|
| EX-COB-002 | KYC Screening Hit | Regulatory risk, potential sanctions breach | Critical |
| EX-COB-004 | System Downtime | Operational disruption, SLA breach | High |

### Exception-to-Pain-Point Mapping

| EX# | Related Pain Points (PP#) | Connection |
|-----|---------------------------|------------|
| EX-COB-001 | PP-COB-001 (Manual document chasing) | Incomplete docs trigger manual follow-up cycle |
| EX-COB-002 | PP-COB-003 (KYC screening false positives) | 40% false positive rate increases exception volume |
| EX-COB-004 | PP-COB-002 (System switching) | Multiple systems increases failure points |
| EX-COB-005 | PP-COB-002 (System switching) | Complex structures require more system interaction |

---

## Recommendations for TO-BE Design

1. **Preventive Controls**: Implement front-end validation to prevent incomplete applications entering the pipeline (addresses EX-COB-001)

2. **Screening Optimization**: Tune World-Check parameters and implement pre-screening disambiguation to reduce false positive rate (addresses EX-COB-002)

3. **Alternative Credit Paths**: Develop startup-friendly credit products with alternative assessment criteria (addresses EX-COB-003)

4. **System Resilience**: Prioritize CBS modernization and implement automated failover (addresses EX-COB-004)

5. **Specialist Track**: Create dedicated complex structure processing track with specialist resources and SLAs (addresses EX-COB-005)

---

## Change Log

| Date | Contributor | Role | Changes |
|------|-------------|------|---------|
| 2025-12-09 | Markus | RTM | Initial exception analysis - 5 exceptions documented |

---

_Generated by ProcessMiner Process Documentation Analyst_
_Document ID: COB-003-exceptions_
