# Exception Paths & Variations: SEPA Mandate Capture

**Process ID:** P-SEPA-MC-001
**Document Type:** Exception Detail Analysis
**Last Updated:** 2025-12-04
**Related Document:** [AS-IS Process Documentation](./as-is-process-documentation.md)

---

## Executive Summary

The SEPA Mandate Capture process encounters 8 documented exception types, handling an average of 105 exceptions per month (4.2% of mandate volume). The most frequent exceptions relate to data quality issues: incomplete forms (15%), invalid IBANs (12%), and invalid creditors (8%). High-impact exceptions include sanctions screening hits (0.3% but requiring immediate escalation) and signature validation failures (6%).

Exception handling adds an average of 1.8 days to cycle time when triggered. The current exception management approach is reactive and manual, with limited root cause analysis feeding back to prevention. Estimated annual cost of exception handling is €87,000 in direct labor, plus indirect costs from client delays and relationship impact.

---

## Exception Summary Table

> **Quick Reference:** All identified exceptions with impact and frequency at a glance. Click any EX# for full details below.

| EX# | Exception Name | Trigger Condition | Affected Steps | Frequency | Business Impact | Handling Owner |
|-----|----------------|-------------------|----------------|-----------|-----------------|----------------|
| EX01 | Invalid Creditor | Creditor ID not found or inactive | PS04 | 8% (~200/month) | High | Payment Ops |
| EX02 | Invalid IBAN | IBAN fails validation checks | PS05 | 12% (~300/month) | Medium | Payment Ops |
| EX03 | Duplicate Mandate | Matching mandate exists in system | PS07 | 5% (~125/month) | Low | Payment Ops |
| EX04 | Sanctions Hit | Party matches sanctions/PEP list | PS08 | 0.3% (~8/month) | Critical | Compliance |
| EX05 | Approval Rejected | Four-eyes reviewer rejects | PS09 | 3% (~75/month) | Medium | Payment Ops |
| EX06 | Incomplete Form | Mandatory fields missing | PS03, PS06 | 15% (~375/month) | Medium | Payment Ops |
| EX07 | Signature Invalid | Missing or unverifiable signature | PS03 | 6% (~150/month) | High | Payment Ops |
| EX08 | Expired Mandate | Signature date >12 months ago | PS06 | 2% (~50/month) | Low | Payment Ops |

---

## Exception Statistics

| Metric | Value |
|--------|-------|
| Total Exceptions Identified | 8 |
| High-Impact Exceptions | 3 |
| Frequently Occurring (>10% of cases) | 2 |
| Exceptions Requiring Manual Intervention | 8 (100%) |
| Exceptions with Documented Procedures | 6 (75%) |
| Exceptions Lacking Clear Ownership | 1 |

---

## Detailed Exception Analysis

### EX01: Invalid Creditor

#### Overview

| Attribute | Value |
|-----------|-------|
| **Exception ID** | EX01 |
| **Exception Name** | Invalid Creditor |
| **Category** | Validation Failure |
| **Affected Process Steps** | PS04 (Creditor Validation) |
| **Frequency** | 8% of cases (200/month) |
| **Business Impact** | High |
| **Handling Owner** | Payment Operations Team |
| **Average Resolution Time** | 2-5 business days |

#### Trigger Conditions

> *What causes this exception to occur?*

This exception is triggered when:
1. Creditor ID in mandate does not exist in Creditor Registry
2. Creditor ID exists but status is "Inactive" or "Suspended"
3. Creditor has exceeded collection limits
4. Creditor type mismatch (e.g., B2B mandate from Core-only creditor)
5. Creditor ID format is invalid (checksum failure)

#### Detection Method

> *How is this exception identified? (System alert, manual review, client complaint, etc.)*

Automated detection during PS04:
- Real-time lookup against Creditor Registry returns "Not Found" or "Invalid Status"
- System automatically flags mandate and routes to exception queue
- Staff notification via MMS dashboard alert

#### Business Impact Analysis

> *What happens when this exception occurs? Quantify where possible.*

**Immediate Impact:**
- Mandate processing halted at PS04
- Mandate placed in "Pending Investigation" status
- Creditor not notified automatically (manual process)

**Downstream Effects:**
- Collection cannot be initiated until resolved
- May cascade to multiple mandates from same creditor
- Creates backlog in exception queue

**Client Impact:**
- Creditor cannot collect from their customers
- Average 3-day delay while creditor status is resolved
- May affect creditor's cash flow planning

**Financial Impact (if applicable):**
- Direct cost: ~€35/exception (investigation time)
- Annual cost: €7,000 (200/month × €35)
- Indirect: Client relationship strain

**Regulatory/Compliance Risk:**
- Low - validation control working as designed
- However, slow resolution may indicate onboarding process issues

#### Current Handling Procedure

> *Step-by-step: What happens today when this exception is triggered?*

1. System flags mandate in MMS exception queue
2. Payment Ops staff reviews within 4 hours
3. Lookup creditor in CRM to verify relationship status
4. If creditor exists but inactive:
   - Contact creditor RM for status clarification
   - If reactivation needed, escalate to Onboarding team
   - Hold mandate until resolved
5. If creditor ID typo suspected:
   - Contact submitting creditor for correction
   - Await corrected mandate
6. If creditor not bank client:
   - Reject mandate with explanation
   - Inform submitting party of onboarding requirement
7. Update exception log with resolution
8. Either resume processing or close as rejected

#### Escalation Path

> *When and to whom does this exception escalate?*

| Escalation Level | Trigger | Owner | SLA |
|------------------|---------|-------|-----|
| Level 1 | Initial detection | Payment Ops Staff | 4 hours |
| Level 2 | No resolution in 24h | Payment Ops Team Lead | 24 hours |
| Level 3 | Creditor reactivation needed | Creditor Onboarding | 48 hours |
| Level 4 | Commercial dispute | Relationship Manager | 5 days |

#### System Behavior

> *How do systems respond to this exception?*

- MMS: Mandate status = "Exception - Creditor Validation"
- Dashboard: Red flag indicator, aging counter starts
- Email: Auto-notification to assigned staff
- No external notification until manual decision

#### Documentation & Evidence

> *What documentation exists for this exception? What audit trail is captured?*

- **Existing Procedures:** DTP-MMS-003 (Creditor Setup Verification)
- **Audit Trail Captured:** All lookup attempts, staff actions, timestamps
- **Evidence Retained:** Exception log entry, communication records

#### Root Cause Analysis

> *Why does this exception occur? (5-Whys or similar analysis)*

**Primary Root Causes:**
1. Creditor submitting mandates before onboarding complete (35%)
2. Creditor ID transcription error on mandate form (25%)
3. Creditor account suspended due to unpaid fees (20%)
4. Legacy creditor IDs not migrated correctly (15%)
5. Creditor type configuration mismatch (5%)

**5-Whys Example (Premature Submission):**
1. Why invalid? Creditor not in registry
2. Why not in registry? Onboarding incomplete
3. Why incomplete? Multi-day onboarding process
4. Why mandates submitted early? Creditor eager to start collections
5. Why allowed? No validation at submission time

#### Improvement Opportunities

> *How could this exception be prevented, detected earlier, or handled more efficiently?*

1. **Prevention:** Pre-submission creditor ID validation on portal
2. **Earlier Detection:** Real-time validation API for creditor systems
3. **Efficient Handling:** Auto-notification to creditor with status and next steps
4. **Process Improvement:** Fast-track onboarding for creditors with pending mandates

#### Related Exceptions

> *Other exceptions that commonly occur together or have similar root causes*

- Often coincides with EX06 (Incomplete Form) - same creditors submit incomplete mandates
- May lead to EX03 (Duplicate) if corrected mandate re-submitted

---

### EX02: Invalid IBAN

#### Overview

| Attribute | Value |
|-----------|-------|
| **Exception ID** | EX02 |
| **Exception Name** | Invalid IBAN |
| **Category** | Validation Failure |
| **Affected Process Steps** | PS05 (IBAN Validation) |
| **Frequency** | 12% of cases (300/month) |
| **Business Impact** | Medium |
| **Handling Owner** | Payment Operations Team |
| **Average Resolution Time** | 1-3 business days |

#### Trigger Conditions

This exception is triggered when:
1. IBAN fails ISO 13616 format validation (check digit error)
2. IBAN country code invalid or unsupported
3. Internal account lookup fails (account not found)
4. Internal account status is "Closed" or "Blocked"
5. BIC mismatch with IBAN (where BIC provided)

#### Detection Method

Automated validation at PS05:
- Format validation (algorithm-based)
- Internal account lookup (real-time Core Banking query)
- External IBAN directory check (where available)

#### Business Impact Analysis

**Immediate Impact:**
- Mandate cannot proceed without valid IBAN
- Creates re-work loop with creditor/debtor

**Downstream Effects:**
- Collection would fail if registered with bad IBAN
- R-transactions and associated fees if not caught

**Client Impact:**
- Creditor must obtain corrected IBAN from debtor
- Delays collection start date
- Client effort to chase debtor for correct details

**Financial Impact:**
- Direct cost: ~€25/exception
- Annual cost: €90,000 (300/month × €25)
- Avoided cost: R-transaction fees (€5-15 each)

**Regulatory/Compliance Risk:**
- Low - validation working correctly
- SEPA Rulebook requires valid IBAN

#### Current Handling Procedure

1. System rejects mandate at validation
2. Staff reviews IBAN error type
3. If typo suspected:
   - Attempt correction using check digit reconstruction
   - If correctable, update and revalidate
4. If account closed:
   - Contact creditor to obtain new IBAN from debtor
5. If format completely invalid:
   - Reject mandate, notify creditor
6. Document resolution in exception log

#### Escalation Path

| Escalation Level | Trigger | Owner | SLA |
|------------------|---------|-------|-----|
| Level 1 | Detection | Payment Ops Staff | Same day |
| Level 2 | Cannot correct | Payment Ops Team Lead | 24 hours |
| Level 3 | Repeated issues same creditor | Customer Service | 48 hours |

#### Root Cause Analysis

**Primary Root Causes:**
1. Transcription errors (handwritten IBAN) - 45%
2. Debtor provided outdated IBAN - 25%
3. Account closed between mandate signing and submission - 15%
4. OCR extraction error - 10%
5. Debtor deliberately provided wrong IBAN - 5%

#### Improvement Opportunities

1. **Prevention:** Real-time IBAN validation on digital submission forms
2. **Earlier Detection:** IBAN checksum validation before full processing
3. **Efficient Handling:** Auto-suggest IBAN correction for common typo patterns
4. **Client Tools:** Self-service correction in creditor portal

#### Related Exceptions

- Linked to PP02 (OCR Accuracy) - OCR causes some IBAN errors
- May cause EX03 (Duplicate) if corrected mandate re-submitted

---

### EX03: Duplicate Mandate

#### Overview

| Attribute | Value |
|-----------|-------|
| **Exception ID** | EX03 |
| **Exception Name** | Duplicate Mandate |
| **Category** | Data Integrity |
| **Affected Process Steps** | PS07 (Duplicate Check) |
| **Frequency** | 5% of cases (125/month) |
| **Business Impact** | Low |
| **Handling Owner** | Payment Operations Team |
| **Average Resolution Time** | 15-60 minutes |

#### Trigger Conditions

This exception is triggered when:
1. Matching Creditor ID + Debtor IBAN + UMR found in system
2. Potential duplicate based on fuzzy matching (similar UMR)
3. Same debtor + creditor with different UMR (warning only)
4. Re-submission of previously rejected mandate

#### Detection Method

Automated detection at PS07:
- Exact match on key fields
- Fuzzy matching algorithm for near-duplicates
- Historical rejected mandate check

#### Business Impact Analysis

**Immediate Impact:**
- Processing paused for manual review
- 15-20 minutes investigation per case

**Downstream Effects:**
- Risk of double-charging debtor if true duplicate registered
- Administrative burden

**Client Impact:**
- Minor delay if false positive
- Protection against double collection if true duplicate

**Financial Impact:**
- Investigation cost: ~€20/case
- Annual cost: €30,000

**Regulatory/Compliance Risk:**
- Medium - duplicate mandates could enable fraud or error
- SEPA Rulebook requires unique UMR per mandate

#### Current Handling Procedure

1. System flags potential duplicate with match details
2. Staff reviews both mandates side-by-side
3. Determination:
   - **True Duplicate:** Reject new submission, notify creditor
   - **Amendment:** Process as update to existing mandate
   - **False Positive:** Clear flag, continue processing
4. Document decision and rationale

#### Root Cause Analysis

**Primary Root Causes:**
1. Client re-submission due to status uncertainty - 35%
2. Mandate amendment submitted as new - 30%
3. System retry after timeout - 15%
4. True duplicate (client error) - 15%
5. Fuzzy match false positive - 5%

#### Improvement Opportunities

1. **Prevention:** Real-time status updates (PP03) to reduce re-submissions
2. **Efficient Handling:** Rules engine for auto-resolution (PP06)
3. **Client Tools:** Clear guidance on amendment vs new mandate

#### Related Exceptions

- Directly related to PP06 (Duplicate Handling Complexity)
- Often follows EX01, EX02 (re-submission after correction)

---

### EX04: Sanctions Hit

#### Overview

| Attribute | Value |
|-----------|-------|
| **Exception ID** | EX04 |
| **Exception Name** | Sanctions Hit |
| **Category** | Compliance |
| **Affected Process Steps** | PS08 (Compliance Screening) |
| **Frequency** | 0.3% of cases (8/month) |
| **Business Impact** | Critical |
| **Handling Owner** | Compliance Team |
| **Average Resolution Time** | 1-10 business days |

#### Trigger Conditions

This exception is triggered when:
1. Creditor name matches sanctions list entry
2. Debtor name matches sanctions list entry
3. Either party matches PEP database
4. Creditor/debtor address in sanctioned jurisdiction
5. Related party connection to sanctioned entity

#### Detection Method

Automated screening at PS08:
- Real-time API call to Sanctions Screening Platform
- Match against EU, UN, OFAC lists
- PEP database check
- Fuzzy name matching algorithm

#### Business Impact Analysis

**Immediate Impact:**
- Mandate processing immediately halted
- Automatic escalation to Compliance team
- No external communication until investigation complete

**Downstream Effects:**
- Potential regulatory reporting obligation
- May trigger broader client relationship review
- Could impact other mandates from same creditor

**Client Impact:**
- Significant delay if false positive
- Mandate rejection if true hit confirmed
- Possible relationship termination

**Financial Impact:**
- Investigation cost: €200-500 per case
- Annual cost: €2,400-€4,800
- Potential regulatory fines if mishandled: €100K+

**Regulatory/Compliance Risk:**
- Critical - failure to screen is regulatory violation
- EU AML Directive, national sanctions laws

#### Current Handling Procedure

1. System immediately escalates to Compliance queue
2. Mandate locked - no further processing
3. Compliance analyst reviews within 4 hours:
   - Match quality assessment
   - Additional data gathering
   - Determination: True Hit / False Positive / Inconclusive
4. If True Hit:
   - Regulatory reporting initiated
   - Mandate rejected
   - Client relationship review triggered
5. If False Positive:
   - Document rationale thoroughly
   - Clear mandate for processing
   - Add to whitelist for future (with controls)
6. If Inconclusive:
   - Escalate to Compliance Manager
   - Enhanced due diligence
   - Decision within 5 business days

#### Escalation Path

| Escalation Level | Trigger | Owner | SLA |
|------------------|---------|-------|-----|
| Level 1 | Any hit | Compliance Analyst | 4 hours |
| Level 2 | Inconclusive or True Hit | Compliance Manager | 24 hours |
| Level 3 | Confirmed True Hit | MLRO | 48 hours |
| Level 4 | Regulatory reporting | Legal/External | As required |

#### Root Cause Analysis

**Primary Root Causes:**
1. Common name matches (false positives) - 75%
2. Outdated client data causing partial match - 15%
3. Actual sanctions concerns (true hits) - 5%
4. PEP status of legitimate clients - 5%

#### Improvement Opportunities

1. **False Positive Reduction:** Improved screening algorithms with context
2. **Efficiency:** Pre-cleared creditor list for known entities
3. **Speed:** Parallel screening during data entry (PP07)

#### Related Exceptions

- May lead to EX05 (Approval Rejected) if concerns raised at four-eyes
- Related to PP07 (Sanctions Screening Latency)

---

### EX05: Approval Rejected

#### Overview

| Attribute | Value |
|-----------|-------|
| **Exception ID** | EX05 |
| **Exception Name** | Approval Rejected |
| **Category** | Control Failure |
| **Affected Process Steps** | PS09 (Four-Eyes Approval) |
| **Frequency** | 3% of cases (75/month) |
| **Business Impact** | Medium |
| **Handling Owner** | Payment Operations Team |
| **Average Resolution Time** | 30 minutes - 2 hours |

#### Trigger Conditions

This exception is triggered when:
1. Approver identifies data entry error
2. Approver notes suspicious mandate characteristics
3. Approver requires additional documentation
4. Mandate data inconsistent with creditor profile
5. Approval criteria not met (limits, authorization)

#### Detection Method

Manual detection at PS09:
- Human review of mandate details
- Cross-check against creditor profile
- Verification of supporting documentation

#### Business Impact Analysis

**Immediate Impact:**
- Mandate returned to data entry for correction
- Creates re-work loop
- Delays mandate activation

**Downstream Effects:**
- Quality control working - prevents errors reaching production
- May indicate training needs if same errors repeat

**Client Impact:**
- Minor delay (usually same-day resolution)
- No external visibility into internal rejection

**Financial Impact:**
- Re-work cost: ~€15/rejection
- Annual cost: €13,500
- Avoided cost: Error correction post-registration much more expensive

#### Current Handling Procedure

1. Approver rejects with documented reason
2. Mandate returned to original processor
3. Processor reviews rejection reason
4. Correction made and re-submitted for approval
5. Different approver reviews (where possible)
6. If approved, processing continues
7. Rejection patterns logged for quality tracking

#### Root Cause Analysis

**Primary Root Causes:**
1. Data entry transcription error - 40%
2. Missing or incorrect supporting documentation - 25%
3. Creditor limit would be exceeded - 15%
4. Mandate type mismatch - 10%
5. Approver over-cautious (subjective) - 10%

#### Improvement Opportunities

1. **Prevention:** Enhanced validation at data entry (before approval)
2. **Efficiency:** Clear rejection reason codes for faster correction
3. **Quality:** Feedback loop to training program

---

### EX06: Incomplete Form

#### Overview

| Attribute | Value |
|-----------|-------|
| **Exception ID** | EX06 |
| **Exception Name** | Incomplete Form |
| **Category** | Data Quality |
| **Affected Process Steps** | PS03 (Data Extraction), PS06 (Data Entry) |
| **Frequency** | 15% of cases (375/month) |
| **Business Impact** | Medium |
| **Handling Owner** | Payment Operations Team |
| **Average Resolution Time** | 2-5 business days |

#### Trigger Conditions

This exception is triggered when:
1. Mandatory field not populated (UMR, signature date, etc.)
2. Field populated but illegible/unreadable
3. Multiple choice not clearly selected
4. Amendment indicator missing
5. Debtor/Creditor identification incomplete

#### Detection Method

Mixed detection:
- Automated: System validation of mandatory fields
- Manual: Staff review of OCR confidence scores
- OCR: Low confidence flag on extracted fields

#### Business Impact Analysis

**Immediate Impact:**
- Mandate cannot proceed with missing data
- Must contact submitter for missing information

**Downstream Effects:**
- Most common exception type - significant volume
- Creates outbound communication burden

**Client Impact:**
- Creditor must provide missing information
- May need to obtain new mandate from debtor
- Delays collection start

**Financial Impact:**
- Handling cost: ~€30/exception (including client contact)
- Annual cost: €135,000

#### Current Handling Procedure

1. System or staff identifies missing/incomplete fields
2. Exception logged with specific fields missing
3. Contact creditor via email/phone for information
4. If information obtainable, update mandate
5. If new mandate required, reject and request re-submission
6. Track creditor completion rates for feedback

#### Root Cause Analysis

**Primary Root Causes:**
1. Form design not clear to signatories - 30%
2. Handwriting illegible - 25%
3. OCR failed to extract - 20%
4. Creditor submitted draft/unsigned version - 15%
5. Scanning quality poor - 10%

#### Improvement Opportunities

1. **Prevention:** Mandatory field validation on digital submission
2. **Form Design:** Clearer mandate form with field guidance
3. **Creditor Education:** Best practices for mandate collection
4. **OCR:** Improved extraction with confidence scoring

---

### EX07: Signature Invalid

#### Overview

| Attribute | Value |
|-----------|-------|
| **Exception ID** | EX07 |
| **Exception Name** | Signature Invalid |
| **Category** | Authorization |
| **Affected Process Steps** | PS03 (Data Extraction) |
| **Frequency** | 6% of cases (150/month) |
| **Business Impact** | High |
| **Handling Owner** | Payment Operations Team |
| **Average Resolution Time** | 3-7 business days |

#### Trigger Conditions

This exception is triggered when:
1. Signature field empty on mandate form
2. Signature illegible or unclear
3. Digital mandate missing e-signature
4. Signature date missing or invalid
5. Corporate mandate missing authorized signatory
6. Signature appears to be stamp/facsimile (not permitted)

#### Detection Method

Manual review at PS03:
- Visual inspection of signature field
- Cross-reference signature date with mandate date
- Corporate mandate: Verify signatory authorization

#### Business Impact Analysis

**Immediate Impact:**
- Mandate lacks legal authorization - cannot be registered
- Must obtain valid signature

**Downstream Effects:**
- Risk of unauthorized collection if processed
- Potential refund liability
- Compliance risk

**Client Impact:**
- Debtor must re-sign mandate
- Creditor must re-collect signed form
- Significant delay and effort

**Financial Impact:**
- Handling cost: ~€40/exception (including client communication)
- Annual cost: €72,000

**Regulatory/Compliance Risk:**
- High - mandates must be properly authorized per SEPA Rulebook
- Collecting without valid mandate is scheme violation

#### Current Handling Procedure

1. Staff identifies signature issue during review
2. Mandate flagged with specific signature concern
3. Contact creditor with issue explanation
4. Creditor must obtain new signature from debtor
5. Re-submit mandate with valid signature
6. Verify signature on re-submitted form

#### Root Cause Analysis

**Primary Root Causes:**
1. Debtor simply forgot to sign - 40%
2. Signature field location unclear on form - 20%
3. Signature date omitted - 20%
4. Corporate authorization documentation missing - 10%
5. Intentional attempt to avoid authorization - 10%

#### Improvement Opportunities

1. **Prevention:** e-Signature mandates with enforced signature capture
2. **Form Design:** Prominent signature field with clear instructions
3. **Digital Validation:** Signature presence detection before submission

---

### EX08: Expired Mandate

#### Overview

| Attribute | Value |
|-----------|-------|
| **Exception ID** | EX08 |
| **Exception Name** | Expired Mandate |
| **Category** | Validity |
| **Affected Process Steps** | PS06 (Mandate Data Entry) |
| **Frequency** | 2% of cases (50/month) |
| **Business Impact** | Low |
| **Handling Owner** | Payment Operations Team |
| **Average Resolution Time** | 3-7 business days |

#### Trigger Conditions

This exception is triggered when:
1. Signature date is more than 12 months before submission
2. Mandate explicitly states validity period that has passed
3. Future-dated signature (fraud indicator)

#### Detection Method

Automated validation at PS06:
- Date comparison: Signature date vs current date
- Business rule: >12 months = expired
- Future date check: Flag if signature date > submission date

#### Business Impact Analysis

**Immediate Impact:**
- Mandate cannot be registered as-is
- Must obtain fresh authorization

**Downstream Effects:**
- Minor - relatively rare exception

**Client Impact:**
- Creditor must obtain new mandate from debtor
- Original mandate becomes documentation only

**Financial Impact:**
- Handling cost: ~€20/exception
- Annual cost: €12,000

**Regulatory/Compliance Risk:**
- Low - SEPA Rulebook does not mandate signature date limit
- Internal policy for mandate freshness

#### Current Handling Procedure

1. System flags mandate with old signature date
2. Staff reviews date calculation
3. If policy exception warranted:
   - Escalate to Team Lead for approval
4. If no exception:
   - Notify creditor of expiration
   - Request new mandate with fresh signature
5. Document resolution

#### Root Cause Analysis

**Primary Root Causes:**
1. Creditor backlog - mandates collected but not submitted promptly - 60%
2. Migration from paper archive - old mandates newly digitized - 25%
3. Date transcription error - 10%
4. Deliberate submission of old mandates - 5%

#### Improvement Opportunities

1. **Prevention:** Warning at submission if signature date >6 months
2. **Policy Review:** Assess if 12-month limit appropriate
3. **Creditor Guidance:** Best practices for timely submission

---

## Exception Patterns & Insights

### Clustering Analysis

> *Are there patterns in when/why exceptions occur?*

**Temporal Patterns:**
- Month-end: +40% exception volume due to rushed submissions
- Monday mornings: Higher incomplete forms (weekend scanning backlog)
- Post-holiday: Expired mandates spike (submission delays)

**Channel Patterns:**
- Paper mandates: 70% of exceptions originate from paper channel (vs 45% volume share)
- Digital portal: Lowest exception rate (2% vs overall 4.2%)
- Email submissions: Highest incomplete form rate

**Creditor Patterns:**
- Top 5% of creditors by volume generate 35% of exceptions
- New creditors (onboarded <6 months): 3x exception rate
- Large volume creditors have better quality

### High-Impact Exception Summary

> *Exceptions requiring priority attention in transformation planning*

| Priority | Exception | Impact | Recommendation |
|----------|-----------|--------|----------------|
| 1 | EX04 - Sanctions Hit | Critical | Streamline false positive handling |
| 2 | EX07 - Signature Invalid | High | Implement e-signature to prevent |
| 3 | EX01 - Invalid Creditor | High | Pre-validation at submission |
| 4 | EX06 - Incomplete Form | Medium | Mandatory field validation |

### Exception-to-Pain-Point Mapping

> *How do exceptions relate to identified pain points?*

| EX# | Related Pain Points (PP#) | Connection |
|-----|---------------------------|------------|
| EX01 | PP04 | Creditor validation delays compound invalid creditor handling |
| EX02 | PP05 | External IBAN validation gaps lead to undetected errors |
| EX03 | PP06, PP03 | Duplicate handling complexity; status uncertainty causes re-submission |
| EX04 | PP07 | Sanctions screening latency impacts overall cycle time |
| EX05 | PP08 | Four-eyes bottleneck delays exception resolution |
| EX06 | PP01, PP02 | Paper mandates and OCR issues drive incomplete forms |
| EX07 | PP01 | Paper process cannot enforce signature capture |
| EX08 | PP10 | Amendment friction causes mandate re-collection |

---

## Recommendations for TO-BE Design

> *Key considerations for the Transformation Agent when addressing exceptions*

### Prevention Focus

1. **Digital-First (EX06, EX07):** Mandatory field validation and e-signature eliminate 50%+ of exceptions
2. **Pre-Submission Validation (EX01, EX02):** Real-time validation before mandate enters processing
3. **Status Transparency (EX03):** Clear status updates reduce uncertainty-driven duplicates

### Detection Enhancement

1. **Improved OCR (EX06):** ML-based extraction reduces data quality exceptions
2. **Smart Duplicate Detection (EX03):** Context-aware duplicate handling with auto-resolution
3. **Sanctions Optimization (EX04):** Parallel processing, better false positive management

### Resolution Efficiency

1. **Self-Service Correction (EX02, EX06):** Creditor portal for fixing simple errors
2. **Automated Workflows (EX01, EX05):** Rules-based routing and resolution
3. **Clear SLAs:** Published resolution times for each exception type

### Compliance Safeguards

1. **Maintain Control Integrity:** Any automation must preserve four-eyes and sanctions screening
2. **Audit Trail:** All exception handling actions must be fully logged
3. **Escalation Paths:** Clear escalation for compliance-critical exceptions

---

## Change Log

| Date | Contributor | Role | Changes |
|------|-------------|------|---------|
| 2025-12-04 | ProcessMiner Analyst | Process Documentation Analyst | Initial exception analysis |

---

_Generated by ProcessMiner Process Documentation Analyst_
_Document ID: P-SEPA-MC-001-exceptions_
