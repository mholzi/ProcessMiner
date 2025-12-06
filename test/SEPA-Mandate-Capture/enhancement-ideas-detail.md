# Enhancement Ideas: SEPA Mandate Capture

**Process ID:** P-SEPA-MC-001
**Document Type:** Enhancement Ideas Catalog
**Last Updated:** 2025-12-04
**Related Document:** [Client Experience AS-IS Analysis](./Client-Experience-AS-IS-Analysis.md)

---

## Executive Summary

This catalog documents 14 enhancement ideas identified through Client Experience analysis, pain point assessment, and innovation research. The ideas target a collective CES reduction of 51 points (from 47 to target 28), bringing the bank from below-average to best-in-class performance. Enhancement ideas span self-service capabilities, digital-first mandate capture, real-time visibility, and intelligent automation.

Prioritization recommends 5 quick wins for immediate implementation (€100K, 3 months), 6 medium-complexity enhancements for near-term (€350K, 6-12 months), and 3 strategic initiatives for longer-term transformation (€500K+, 12-18 months).

---

## Enhancement Summary Table

> **Quick Reference:** All identified enhancement ideas linked to friction points. Click any EI# for full details below.

| EI# | Enhancement | Friction Point | Impact | Complexity | Est. CES Reduction | Source |
|-----|-------------|----------------|--------|------------|-------------------|--------|
| EI01 | Real-time Status Tracking | FP01 | High | Low | -8 | CX Analysis |
| EI02 | Digital Mandate with e-Signature | FP02 | High | Medium | -12 | CX + PDA |
| EI03 | Push Notifications at Milestones | FP03 | Medium | Low | -4 | CX Analysis |
| EI04 | Self-service Correction Portal | FP04 | Medium | Medium | -3 | CX Analysis |
| EI05 | Instant Confirmation Email | FP07 | Medium | Low | -2 | CX Analysis |
| EI06 | Multi-channel Acknowledgment | FP06 | Medium | Low | -2 | CX Analysis |
| EI07 | Estimated Completion Display | FP09 | Low | Low | -2 | CX Analysis |
| EI08 | Pre-filled Mandate from Data | FP05 | Medium | High | -4 | Innovation |
| EI09 | Bulk Mandate Upload | FP08 | Medium | Medium | -3 | PDA |
| EI10 | Debtor Mandate Portal | FP10 | Low | Medium | -2 | CX Analysis |
| EI11 | Mobile Mandate Submission | FP11 | Medium | Medium | -3 | Innovation |
| EI12 | WhatsApp/SMS Status Updates | FP12 | Low | Low | -2 | Innovation |
| EI13 | Express Processing Option | FP13 | Low | High | -1 | Innovation |
| EI14 | Conversational AI for Inquiries | Multiple | Medium | Medium | -3 | Innovation |

---

## Enhancement Statistics

| Metric | Value |
|--------|-------|
| Total Enhancement Ideas | 14 |
| High-Impact Enhancements | 3 |
| Low-Complexity (Quick Wins) | 5 |
| Medium-Complexity | 6 |
| High-Complexity | 3 |
| Total Est. CES Reduction | -51 points |
| From CX Analysis | 9 |
| From PDA/Pain Points | 3 |
| From Innovation Research | 5 |

---

## Enhancement Categories

> *Breakdown by category helps prioritize transformation themes*

| Category | Count | Combined CES Impact | Top Priority |
|----------|-------|---------------------|--------------|
| Visibility & Tracking | 4 | -16 | EI01 |
| Digital Experience | 3 | -18 | EI02 |
| Self-Service | 3 | -8 | EI04 |
| Communication | 3 | -8 | EI03 |
| Efficiency | 1 | -1 | EI13 |

---

## Detailed Enhancement Analysis

### EI01: Real-time Status Tracking

#### Overview

| Attribute | Value |
|-----------|-------|
| **Enhancement ID** | EI01 |
| **Enhancement Name** | Real-time Status Tracking in Portal |
| **Category** | Visibility & Tracking |
| **Source** | CX Analysis |
| **Linked Friction Point** | FP01 |
| **Linked Pain Point** | PP03 |
| **Impact Level** | High |
| **Complexity** | Low |
| **Est. CES Reduction** | -8 points |

#### Problem Being Addressed

> *What friction/pain point does this enhancement address?*

Clients currently see only "Submitted" and "Completed" status in the portal - nothing in between. The processing "black box" generates 180+ status inquiry calls monthly and significant client anxiety. Clients don't know if their mandate is stuck, progressing, or requiring action.

#### Proposed Solution

> *Detailed description of the enhancement*

Implement real-time mandate status visibility in the corporate portal and customer-facing channels:

1. **Status States:** Define client-visible status stages:
   - Received → Validating → Compliance Check → Approval → Registered → Active
2. **Progress Visualization:** Timeline or progress bar showing current stage
3. **Expected Completion:** Estimated completion date based on current position and historical data
4. **Activity Log:** Show recent activities (e.g., "Validation completed 10:15 AM")
5. **Next Steps:** If client action needed, show clear call-to-action

#### Expected Benefits

> *What improvements will this enhancement deliver?*

**Client Experience Benefits:**
- Eliminates "black box" anxiety
- Reduces need to call for status
- Builds trust through transparency
- Sets accurate expectations

**Operational Benefits:**
- 70% reduction in status inquiry calls (126 calls/month saved)
- Customer Service capacity freed for complex issues
- Reduced escalations to Payment Operations

**Quantified Impact:**
- Estimated CES reduction: 8 points
- Time savings per occurrence: 8 minutes × 126 calls = 16.8 hours/month
- Error reduction: 50% reduction in duplicate submissions from uncertainty

#### Implementation Considerations

> *What should the Transformation Agent consider when implementing?*

**Dependencies:**
- MMS must expose status via API (already available)
- Portal development capacity required
- UI/UX design for status visualization

**Prerequisites:**
- Define client-facing status taxonomy
- Map internal statuses to client-visible stages
- Test status update latency (<5 seconds)

**Constraints:**
- Some internal statuses shouldn't be exposed (e.g., "Sanctions Screening")
- Must handle edge cases (stuck mandates)
- Multi-language support required

**Risks:**
- Status exposure may reveal internal SLA breaches
- Initial implementation may have status lag

#### Complexity Assessment

| Factor | Assessment |
|--------|------------|
| Technical Complexity | Low - API exists, UI development only |
| Organizational Change | Low - No process change needed |
| Integration Required | Low - Single system (Portal ↔ MMS) |
| Timeline Estimate | 4-6 weeks |
| Resource Requirements | 1 FE developer, 0.5 BA, 0.5 QA |

#### Innovation Context

> *If sourced from innovation research or Party Mode*

**Source:** CX Analysis (client feedback), Industry benchmark
**Reference:** Amazon-style order tracking, ING mandate portal
**Adaptation Notes:** Simplify for banking context; fewer stages than e-commerce

#### Traceability

| Link Type | ID | Description |
|-----------|----|-----------|
| Friction Point | FP01 | Status Visibility Blackout |
| Pain Point | PP03 | No Real-time Status Updates |
| Exception | - | - |
| Control Point | CP11 | Must log status view access |

---

### EI02: Digital Mandate with e-Signature

#### Overview

| Attribute | Value |
|-----------|-------|
| **Enhancement ID** | EI02 |
| **Enhancement Name** | Digital Mandate with e-Signature |
| **Category** | Digital Experience |
| **Source** | CX Analysis + PDA |
| **Linked Friction Point** | FP02 |
| **Linked Pain Point** | PP01 |
| **Impact Level** | High |
| **Complexity** | Medium |
| **Est. CES Reduction** | -12 points |

#### Problem Being Addressed

45% of mandates arrive on paper, requiring creditors to physically collect signatures from debtors. This involves postal exchange, in-person meetings, or courier services - adding 1-7 days to the preparation phase and creating document quality issues.

#### Proposed Solution

Implement end-to-end digital mandate capture with qualified e-signature:

1. **Digital Form:** Web-based mandate form with field validation
2. **e-Signature Integration:** Qualified Electronic Signature (QES) per eIDAS
3. **Debtor Journey:**
   - Creditor initiates mandate request
   - Debtor receives email/SMS link
   - Debtor reviews and signs digitally
   - Mandate auto-submitted to bank
4. **Authentication:** Bank ID or video ID for debtor verification
5. **Storage:** Digital mandate stored with signature certificate

#### Expected Benefits

**Client Experience Benefits:**
- Zero paper handling for debtor
- Complete mandate in minutes, not days
- Sign anywhere, anytime (mobile-friendly)
- Automatic validation prevents errors

**Operational Benefits:**
- Eliminates scanning and OCR steps
- 100% STP for digital mandates
- Reduces signature validation exceptions (EX07) by 90%
- Processing time: minutes instead of days

**Quantified Impact:**
- Estimated CES reduction: 12 points
- Time savings per occurrence: 9 minutes processing × 45% volume
- Error reduction: 80% reduction in form-related exceptions

#### Implementation Considerations

**Dependencies:**
- e-Signature vendor selection and integration
- Legal/Compliance sign-off on e-signature validity
- Debtor identity verification solution

**Prerequisites:**
- eIDAS compliance assessment
- e-Signature vendor procurement
- Debtor communication templates

**Constraints:**
- QES requirement for full legal equivalence
- Some debtors may not have digital identity
- Paper fallback must remain available

**Risks:**
- Adoption rate uncertainty
- Identity verification friction for debtors
- Initial creditor education needed

#### Complexity Assessment

| Factor | Assessment |
|--------|------------|
| Technical Complexity | Medium - Third-party integration |
| Organizational Change | Medium - New channel, training |
| Integration Required | Medium - e-Sig vendor, identity, MMS |
| Timeline Estimate | 3-4 months |
| Resource Requirements | €80-120K (vendor + development) |

---

### EI03: Push Notifications at Milestones

#### Overview

| Attribute | Value |
|-----------|-------|
| **Enhancement ID** | EI03 |
| **Enhancement Name** | Push Notifications at Milestones |
| **Category** | Communication |
| **Source** | CX Analysis |
| **Linked Friction Point** | FP03 |
| **Linked Pain Point** | PP03, PP09 |
| **Impact Level** | Medium |
| **Complexity** | Low |
| **Est. CES Reduction** | -4 points |

#### Problem Being Addressed

Clients receive no communication during the 3.2-day average processing time. They must actively check the portal (assuming EI01 is implemented) or call for updates. Proactive communication would reduce anxiety and demonstrate responsiveness.

#### Proposed Solution

Implement event-driven notifications at key mandate processing milestones:

1. **Notification Events:**
   - Mandate received and queued
   - Validation complete (or issues found)
   - Approval granted
   - Mandate registered and active
   - Any action required from client

2. **Channels:**
   - Email (default)
   - Portal notification center
   - Optional: SMS, app push notification

3. **Personalization:** Client name, mandate reference, next expected step

#### Expected Benefits

**Client Experience Benefits:**
- Proactive communication builds trust
- Reduces need to check portal repeatedly
- Immediate awareness if action needed
- Sets clear expectations

**Operational Benefits:**
- Further reduces status inquiry calls
- Earlier client response to issues
- Improved perceived service quality

**Quantified Impact:**
- Estimated CES reduction: 4 points
- Additional call reduction: 30% beyond EI01
- Client satisfaction improvement: +0.3 NPS points

#### Complexity Assessment

| Factor | Assessment |
|--------|------------|
| Technical Complexity | Low - Event triggers exist |
| Organizational Change | Low - No process change |
| Integration Required | Low - Email gateway, templates |
| Timeline Estimate | 3-4 weeks |
| Resource Requirements | €20-30K |

---

### EI04: Self-service Correction Portal

#### Overview

| Attribute | Value |
|-----------|-------|
| **Enhancement ID** | EI04 |
| **Enhancement Name** | Self-service Correction Portal |
| **Category** | Self-Service |
| **Source** | CX Analysis |
| **Linked Friction Point** | FP04 |
| **Linked Pain Point** | PP10 |
| **Impact Level** | Medium |
| **Complexity** | Medium |
| **Est. CES Reduction** | -3 points |

#### Problem Being Addressed

When mandates fail validation (4.2% rate), creditors receive a rejection email and must re-engage debtors for corrections. Simple errors (typos, missing fields) require full re-collection cycle. No self-service correction option exists.

#### Proposed Solution

Enable creditors to correct certain mandate errors via self-service portal:

1. **Correction Scope:** Define correctable vs non-correctable fields
   - Correctable: IBAN typos (check digit recalculation), dates, creditor reference
   - Non-correctable: Signature, debtor name (requires new mandate)

2. **Workflow:**
   - Mandate flagged with specific error
   - Creditor accesses correction screen
   - Creditor updates field(s)
   - System re-validates and resubmits
   - Four-eyes approval may be waived for minor corrections

3. **Audit Trail:** All corrections logged with before/after values

#### Expected Benefits

**Client Experience Benefits:**
- Immediate correction for simple errors
- No debtor re-engagement for typos
- Faster mandate activation
- Reduced frustration

**Operational Benefits:**
- Reduces exception handling workload
- Faster cycle time for corrected mandates
- Less outbound communication

**Quantified Impact:**
- Estimated CES reduction: 3 points
- Exception handling time saved: 50% for correctable errors
- Cycle time reduction: 1-3 days for affected mandates

#### Complexity Assessment

| Factor | Assessment |
|--------|------------|
| Technical Complexity | Medium - Correction workflow |
| Organizational Change | Medium - Approval waiver policy |
| Integration Required | Medium - Portal, MMS, controls |
| Timeline Estimate | 6-8 weeks |
| Resource Requirements | €40-60K |

---

### EI05-EI07: Quick Win Communication Enhancements

#### EI05: Instant Confirmation Email

**Problem:** Confirmation emails batched, 1-3 day delay after activation
**Solution:** Real-time email trigger on mandate registration
**CES Reduction:** -2 | **Complexity:** Low | **Timeline:** 2-3 weeks

#### EI06: Multi-channel Submission Acknowledgment

**Problem:** Paper and email submissions get no instant acknowledgment
**Solution:** Auto-acknowledgment for all channels within 5 minutes
**CES Reduction:** -2 | **Complexity:** Low | **Timeline:** 2-3 weeks

#### EI07: Estimated Completion Time Display

**Problem:** Clients don't know when to expect mandate activation
**Solution:** Display estimated completion based on historical data
**CES Reduction:** -2 | **Complexity:** Low | **Timeline:** 2-3 weeks

---

### EI08: Pre-filled Mandate from Account Data

#### Overview

| Attribute | Value |
|-----------|-------|
| **Enhancement ID** | EI08 |
| **Enhancement Name** | Pre-filled Mandate from Account Data |
| **Category** | Digital Experience |
| **Source** | Innovation Research |
| **Linked Friction Point** | FP05 |
| **Linked Pain Point** | PP01 |
| **Impact Level** | Medium |
| **Complexity** | High |
| **Est. CES Reduction** | -4 points |

#### Problem Being Addressed

Creditors and debtors must manually complete mandate forms with data that the bank already knows (IBAN, name, address). This creates effort and error potential.

#### Proposed Solution

Leverage Open Banking (PSD2) to pre-populate mandate data:

1. **For Debtors (internal accounts):** Pre-fill from Core Banking data
2. **For External Debtors:** Use Account Information Services (AIS) with consent
3. **Workflow:**
   - Debtor initiates mandate via creditor portal
   - Authenticates with their bank (Open Banking)
   - Bank pre-fills account and identity data
   - Debtor reviews and confirms

#### Expected Benefits

- Eliminates manual data entry for debtors
- Near-zero form errors
- Faster completion time

#### Complexity Assessment

**High Complexity:** Requires Open Banking API integration, consent management, and multi-bank testing. Timeline: 4-6 months. Investment: €100-150K.

---

### EI09: Bulk Mandate Upload for Creditors

#### Overview

| Attribute | Value |
|-----------|-------|
| **Enhancement ID** | EI09 |
| **Enhancement Name** | Bulk Mandate Upload |
| **Category** | Efficiency |
| **Source** | PDA |
| **Linked Friction Point** | FP08 |
| **Linked Pain Point** | PP01 |
| **Impact Level** | Medium |
| **Complexity** | Medium |
| **Est. CES Reduction** | -3 points |

#### Problem Being Addressed

Large creditors with multiple mandates must submit each individually via portal. No batch upload capability exists, creating significant effort for high-volume creditors.

#### Proposed Solution

Enable bulk mandate submission via file upload:

1. **File Format:** CSV/XML template with all mandate fields
2. **Validation:** Pre-upload validation with error report
3. **Processing:** Bulk processing with individual status tracking
4. **Reporting:** Summary report of successful/failed mandates

#### Expected Benefits

- 90% effort reduction for batch submissions
- Standardized data quality
- Single submission for multiple mandates

#### Complexity Assessment

**Medium Complexity:** File parsing, bulk validation, status tracking. Timeline: 8-10 weeks. Investment: €50-70K.

---

### EI10-EI14: Additional Enhancement Ideas

#### EI10: Debtor Mandate Notification Portal

**Problem:** Debtors have no visibility into mandates authorized against their account
**Solution:** Self-service portal showing active mandates, with option to flag issues
**CES Reduction:** -2 | **Complexity:** Medium | **Timeline:** 8-10 weeks

#### EI11: Mobile Mandate Submission

**Problem:** Portal not optimized for mobile; no native app option
**Solution:** Mobile-responsive portal + native app for mandate management
**CES Reduction:** -3 | **Complexity:** Medium | **Timeline:** 3-4 months

#### EI12: WhatsApp/SMS Status Updates

**Problem:** Email may not be checked frequently; no instant channel
**Solution:** Opt-in WhatsApp/SMS notifications for status updates
**CES Reduction:** -2 | **Complexity:** Low | **Timeline:** 4-6 weeks

#### EI13: Express Processing Option

**Problem:** No option for urgent mandate activation
**Solution:** Premium "express" lane with guaranteed same-day activation (fee-based)
**CES Reduction:** -1 | **Complexity:** High | **Timeline:** 3-4 months

#### EI14: Conversational AI for Inquiries

**Problem:** Status inquiries handled by human agents
**Solution:** AI chatbot for mandate status, FAQs, and simple corrections
**CES Reduction:** -3 | **Complexity:** Medium | **Timeline:** 3-4 months

---

## Enhancement Patterns & Themes

### Theme Analysis

> *What patterns emerge across enhancement ideas?*

1. **Visibility Theme (EI01, EI03, EI07, EI12):** Clients want to see what's happening without asking
2. **Digital-First Theme (EI02, EI08, EI11):** Eliminate paper, enable anywhere access
3. **Self-Service Theme (EI04, EI10, EI14):** Empower clients to help themselves
4. **Efficiency Theme (EI05, EI06, EI09):** Reduce effort on both sides

### Quick Wins

> *Low-complexity enhancements with good impact*

| EI# | Enhancement | Friction | Complexity | CES Impact |
|-----|-------------|----------|------------|------------|
| EI01 | Status Tracking | FP01 | Low | -8 |
| EI03 | Push Notifications | FP03 | Low | -4 |
| EI05 | Instant Confirmation | FP07 | Low | -2 |
| EI06 | Multi-channel Ack | FP06 | Low | -2 |
| EI07 | Est. Completion | FP09 | Low | -2 |

**Total Quick Wins:** 5 enhancements, ~€100K investment, -18 CES points

### High-Impact Opportunities

> *Enhancements with significant CES reduction potential*

| EI# | Enhancement | Friction | Impact | Complexity | CES Impact |
|-----|-------------|----------|--------|------------|------------|
| EI02 | e-Signature Mandate | FP02 | High | Medium | -12 |
| EI01 | Status Tracking | FP01 | High | Low | -8 |
| EI08 | Pre-filled Mandate | FP05 | Medium | High | -4 |

### Complex Transformations

> *Enhancements requiring significant change - strategic initiatives*

**EI02 - Digital Mandate with e-Signature:** Flagship transformation initiative. Requires vendor selection, legal sign-off, creditor/debtor education, and parallel operation period. 3-4 months, €120K+.

**EI08 - Pre-filled Mandate via Open Banking:** Innovative but complex. Requires Open Banking certification, multi-bank testing, consent management. 4-6 months, €150K+.

**EI13 - Express Processing Option:** Requires process redesign, pricing model, capacity management. May cannibalize standard processing. 3-4 months, €80K+.

---

## Innovation-Sourced Ideas

### From Industry Research

| EI# | Enhancement | Source | Applicability |
|-----|-------------|--------|---------------|
| EI08 | Pre-filled Mandate | Open Banking trend | High - PSD2 enabler |
| EI11 | Mobile Submission | Mobile banking adoption | High - client expectation |
| EI12 | WhatsApp Updates | Messaging preference shift | Medium - younger demographic |
| EI14 | Conversational AI | AI/chatbot trend | Medium - emerging capability |

### From Party Mode Discussions

| EI# | Enhancement | Contributing Agents | Key Insight |
|-----|-------------|---------------------|-------------|
| EI02 | e-Signature | CX + Control Analyst | Legal framework now supports; control integrity maintained |
| EI04 | Self-service Correction | CX + PDA | Compliance-safe for defined field set |
| EI09 | Bulk Upload | PDA + Innovation | High-volume creditors requesting |

---

## Exclusions (Tried and Failed)

- **Video verification for mandate signing:** Tested in pilot; client friction too high, technical issues. Not proceeding.
- **Blockchain-based mandate registry:** Investigated; no clear benefit over current system. Deferred indefinitely.
- **AI-based signature validation:** Accuracy insufficient for compliance; manual review still required.

---

## Input for Downstream Agents

### For Transformation Agent

> *Enhancement ideas to consider for TO-BE design*

**Must Include (Quick Wins):**
- EI01: Status Tracking
- EI03: Push Notifications
- EI05: Instant Confirmation
- EI06: Multi-channel Acknowledgment

**Should Include (High Impact):**
- EI02: e-Signature Mandate (flagship)
- EI04: Self-service Correction

**Could Include (Value-Add):**
- EI09: Bulk Upload
- EI11: Mobile Submission
- EI14: Conversational AI

### For Control Analyst

> *Enhancements affecting compliance/controls*

- EI02: e-Signature impacts CP07 (Signature Validation) - must maintain control equivalence
- EI04: Self-service Correction impacts CP06 (Four-Eyes) - approval waiver policy needed
- EI13: Express Processing must maintain all controls despite speed

### For Innovation Analyst

> *Enhancements that leverage emerging technologies*

- EI08: Open Banking APIs
- EI14: Conversational AI / NLP
- EI11: Mobile native development
- EI02: e-Signature technology (QES)

---

## Change Log

| Date | Contributor | Role | Changes |
|------|-------------|------|---------|
| 2025-12-04 | ProcessMiner Analyst | Client Journey Analyst | Initial enhancement catalog |

---

_Generated by ProcessMiner Client Journey Analyst_
_Document ID: P-SEPA-MC-001-enhancement-ideas_
