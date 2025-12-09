# Transformation Decisions Detail: Onboarding

**Document Type:** Transformation Decision Log (Detail)
**Process ID:** ONB-001
**Transformation ID:** TRX-ONB-001
**Document Owner:** Peter (SME)
**Last Updated:** 2025-12-09
**Version:** 1.0

---

## Executive Summary

This document provides detailed analysis of all 8 transformation decisions (TD#) made during the TO-BE design for the Onboarding process. Decisions span process design, control enhancement, client experience, and innovation integration.

### Decision Statistics

| Metric | Value |
|--------|-------|
| Total Decisions Logged | 8 |
| Strategic Decisions | 3 (TD-004, TD-005, TD-006) |
| Tactical Decisions | 4 (TD-001, TD-002, TD-003, TD-007) |
| Trade-off Decisions | 1 (TD-008) |
| Deferred Decisions | 0 |

---

## How to Read This Document

> This document provides **detailed analysis** of all transformation decisions (TD#) made during TO-BE design. Each decision includes alternatives considered, evaluation criteria, rationale, and impact assessment.
>
> **Parent Document:** [Target State Documentation](./target-state-documentation.md)
>
> **Decision Categories:**
> - **Strategic** - Fundamental design direction affecting multiple areas
> - **Tactical** - Specific implementation choices within a design direction
> - **Trade-off** - Balancing competing demands (efficiency vs control, etc.)
> - **Deferred** - Decisions postponed for future consideration

---

## Decision Catalog

### Decision Summary Table

| TD# | Decision Title | Category | AS-IS Impact | Stakeholders | Status |
|-----|----------------|----------|--------------|--------------|--------|
| TD-ONB-001 | Layered DTP Documentation Strategy | Tactical | GAP-ONB-001 | Operations, Training, IT | Approved |
| TD-ONB-002 | Data Retention Hybrid Automation | Tactical | CP-ONB-008 | DPO, Compliance, IT | Approved |
| TD-ONB-003 | Real-Time Consent + Self-Service | Tactical | CP-ONB-006, CP-ONB-007 | Marketing, Compliance, Digital | Approved |
| TD-ONB-004 | KYC SOD: AI First-Eyes, Human Second-Eyes | Strategic | CP-ONB-001 to CP-ONB-005 | Compliance, KYC Team, IT | Approved |
| TD-ONB-005 | Two-Track Compressed Journey | Strategic | All PS#, Client Experience | CX, Marketing, Call Centre | Approved |
| TD-ONB-006 | AI-First Automation Strategy | Strategic | All automation | IT, Digital, IBM Partnership | Approved |
| TD-ONB-007 | Include All SHOULD HAVE Innovations | Tactical | Innovation portfolio | Product, IT, Finance | Approved |
| TD-ONB-008 | Include COULD HAVE/DEFER with Conditions | Trade-off | Innovation portfolio | Product, IT, Compliance | Approved |

---

## Detailed Decision Records

### TD-ONB-001: Layered DTP Documentation Strategy

#### Decision Overview

| Attribute | Value |
|-----------|-------|
| **Decision ID** | TD-ONB-001 |
| **Category** | Tactical |
| **Decision Date** | 2025-12-09 |
| **Decision Maker** | Peter (SME) |
| **Status** | Approved |

#### Context and Problem Statement

The AS-IS process has no documented Desktop Procedure (DTP) for staff executing the 180-day onboarding journey (GAP-ONB-001). New team members lack a standardised reference, and process consistency may vary between operators.

#### Decision Drivers

- **Training Efficiency:** New staff need clear guidance to execute consistently
- **Audit Compliance:** Regulators expect documented procedures
- **User Preferences:** Different staff prefer different formats (document vs system vs AI)
- **Maintenance Burden:** Traditional documents become outdated quickly

#### Alternatives Considered

| Option | Description | Pros | Cons |
|--------|-------------|------|------|
| A: Traditional DTP | Comprehensive desktop procedure manual | Familiar, audit-ready, works offline | Static, requires manual updates |
| B: Contextual System Help | Step-by-step guidance embedded in CRM/systems | Always current, point-of-need | Requires IT development |
| C: AI-Powered Assistant | Extend chatbot for internal staff guidance | Natural language, handles exceptions | Requires chatbot training |

#### Decision

**Selected Option:** All three (A + B + C) as complementary layers

**Rationale:**
Different staff have different needs and learning styles. Combining all three approaches creates a comprehensive support ecosystem:
- DTP document serves audit/compliance and offline reference needs
- Contextual help supports routine daily execution
- AI assistant handles exceptions and natural language queries

#### Impact Assessment

| Impact Area | Description | Severity |
|-------------|-------------|----------|
| IT Development | Contextual help requires system changes | Medium |
| Training | Reduced training time with layered support | Positive |
| Operations | Improved consistency across operators | Positive |
| Chatbot | Additional training for staff-facing queries | Low |

#### AS-IS References Affected

| Reference | Type | Change |
|-----------|------|--------|
| GAP-ONB-001 | Gap | Resolved |
| PS-ONB-004 | Process Step | Enhanced with AI support |

#### TO-BE References Created/Modified

| Reference | Type | Description |
|-----------|------|-------------|
| TS-ONB-004 | Process Step | Includes AI assistant for staff |

#### Trade-offs Accepted

Higher implementation effort for comprehensive solution vs. simpler single-approach implementation.

#### Risks and Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Three systems to maintain | Medium | Medium | Central content source; auto-sync |
| Staff confusion on which to use | Low | Low | Clear guidance on when to use each |

---

### TD-ONB-002: Data Retention Hybrid Automation

#### Decision Overview

| Attribute | Value |
|-----------|-------|
| **Decision ID** | TD-ONB-002 |
| **Category** | Tactical |
| **Decision Date** | 2025-12-09 |
| **Decision Maker** | Peter (SME) |
| **Status** | Approved |

#### Context and Problem Statement

CP-ONB-008 (Data Retention Compliance) has the lowest effectiveness score (3.2/5) due to manual processing at Day 180 close-out. Inconsistent timing and partial audit trail create compliance risk.

#### Decision Drivers

- **Control Effectiveness:** Current 3.2/5 is below standard
- **Audit Trail:** Partial documentation is compliance risk
- **Consistency:** Manual timing varies between operators
- **Oversight:** Complex retention decisions need human judgement

#### Alternatives Considered

| Option | Description | Pros | Cons |
|--------|-------------|------|------|
| A: Strengthen Manual | Add checklists, mandatory fields, sign-off | Low cost, quick | Still manual, still inconsistent |
| B: Full Automation | System-triggered, auto-classification, auto-execution | 100% consistent | Complex decisions need human judgement |
| C: Hybrid | Auto-trigger + auto-classify + human confirmation | Best of both | Requires some manual effort |

#### Decision

**Selected Option:** C - Hybrid approach

**Rationale:**
Balances automation benefits (consistency, audit trail) with human oversight for complex retention decisions. System handles the "when" and "what"; human confirms the "should we."

#### Impact Assessment

| Impact Area | Description | Severity |
|-------------|-------------|----------|
| Control Effectiveness | 3.2 → 4.5 improvement | Positive (High) |
| Audit Trail | Complete automation logging | Positive |
| Manual Effort | Reduced but not eliminated | Neutral |

#### AS-IS References Affected

| Reference | Type | Change |
|-----------|------|--------|
| CP-ONB-008 | Control | Enhanced → TC-ONB-008 |
| CIR-ONB-001 | Improvement | Addressed |

#### TO-BE References Created/Modified

| Reference | Type | Description |
|-----------|------|-------------|
| TC-ONB-008 | Target Control | Hybrid Automated Data Retention |
| TS-ONB-008 | Process Step | Includes automated retention trigger |

#### Dependencies

| Dependency | Type | Impact |
|------------|------|--------|
| II-ONB-005 (RPA) | Innovation | Provides automation capability |
| Data Retention System | System | Must support auto-classification |

---

### TD-ONB-003: Real-Time Consent + Self-Service

#### Decision Overview

| Attribute | Value |
|-----------|-------|
| **Decision ID** | TD-ONB-003 |
| **Category** | Tactical |
| **Decision Date** | 2025-12-09 |
| **Decision Maker** | Peter (SME) |
| **Status** | Approved |

#### Context and Problem Statement

CP-ONB-007 (Communication Opt-In Verification) has effectiveness 4.0/5 with detection capability dependent on consent database accuracy. CIR-ONB-002 recommends real-time validation.

#### Decision Drivers

- **Database Accuracy:** Root cause of verification weakness
- **Customer Empowerment:** GDPR promotes customer control
- **Marketing Compliance:** Risk of communications without valid consent
- **Self-Service Strategy:** Aligns with broader portal initiative

#### Alternatives Considered

| Option | Description | Pros | Cons |
|--------|-------------|------|------|
| A: Database Validation | Real-time consent database reconciliation | Addresses root cause | Backend only, no customer visibility |
| B: Secondary Check | Double-check at send time | Catches sync delays | Performance impact |
| C: Self-Service Portal | Customer manages own preferences | Always current, empowerment | Requires portal development |

#### Decision

**Selected Option:** A + C - Real-time validation AND customer self-service

**Rationale:**
Two-pronged approach: fix backend accuracy issues (A) while empowering customers to manage preferences directly (C). Addresses both root cause and customer experience.

#### Impact Assessment

| Impact Area | Description | Severity |
|-------------|-------------|----------|
| Control Effectiveness | 4.0 → 4.8 improvement | Positive |
| Customer Experience | Self-service empowerment | Positive |
| Marketing Operations | Reduced preference complaints | Positive |

#### AS-IS References Affected

| Reference | Type | Change |
|-----------|------|--------|
| CP-ONB-006 | Control | Enhanced → TC-ONB-006 |
| CP-ONB-007 | Control | Enhanced → TC-ONB-007 |
| CIR-ONB-002 | Improvement | Addressed |

#### TO-BE References Created/Modified

| Reference | Type | Description |
|-----------|------|-------------|
| TC-ONB-006 | Target Control | Self-Service Consent Management |
| TC-ONB-007 | Target Control | Real-Time Consent Validation |
| TS-ONB-010 | Process Step | Self-Service Portal includes consent |
| TJ-ONB-010 | Touchpoint | Consent management via portal |

#### Dependencies

| Dependency | Type | Impact |
|------------|------|--------|
| II-ONB-008 (Self-Service Portal) | Innovation | Enables customer-facing consent |

---

### TD-ONB-004: KYC SOD - AI First-Eyes, Human Second-Eyes

#### Decision Overview

| Attribute | Value |
|-----------|-------|
| **Decision ID** | TD-ONB-004 |
| **Category** | Strategic |
| **Decision Date** | 2025-12-09 |
| **Decision Maker** | Peter (SME) |
| **Status** | Approved |

#### Context and Problem Statement

All KYC controls (CP-ONB-001 to CP-ONB-005) require four-eyes principle (maker-checker). SME requested maximum automation of the "first eyes" while maintaining human oversight for the "second eyes."

#### Decision Drivers

- **Regulatory Compliance:** Four-eyes principle is non-negotiable
- **Processing Speed:** Manual first-review is bottleneck
- **Human Focus:** Reviewers should focus on exceptions, not routine
- **AI Capability:** AI can handle document verification, PEP screening effectively

#### Alternatives Considered

| Option | Description | Pros | Cons |
|--------|-------------|------|------|
| Keep As-Is | Human maker + Human checker | Proven, low risk | Slow, expensive |
| Full Automation | AI maker + AI checker | Fast, scalable | Regulatory risk, no human accountability |
| AI First + Human Second | AI performs first review, human approves | Speed + oversight | Requires AI audit trail |

#### Decision

**Selected Option:** AI First-Eyes + Human Second-Eyes

**Rationale:**
Maintains four-eyes principle (AI = maker, Human = checker) while maximizing automation benefits. Human reviewer focuses on AI-flagged exceptions and makes all final decisions. Requires full AI audit trail for EU AI Act compliance.

#### Impact Assessment

| Impact Area | Description | Severity |
|-------------|-------------|----------|
| KYC Processing Time | -60% estimated | Positive (High) |
| Reviewer Productivity | Focus on exceptions only | Positive |
| Regulatory Compliance | Four-eyes preserved | Maintained |
| AI Governance | New audit trail requirement | Medium effort |

#### AS-IS References Affected

| Reference | Type | Change |
|-----------|------|--------|
| CP-ONB-001 | Control | Enhanced → TC-ONB-001 |
| CP-ONB-002 | Control | Enhanced → TC-ONB-002 |
| CP-ONB-003 | Control | Enhanced → TC-ONB-003 |
| CP-ONB-004 | Control | Enhanced → TC-ONB-004 |
| CP-ONB-005 | Control | Enhanced → TC-ONB-005 |

#### TO-BE References Created/Modified

| Reference | Type | Description |
|-----------|------|-------------|
| TC-ONB-001 to TC-ONB-005 | Target Controls | AI-first with human approval |
| TC-ONB-009 | Target Control | NEW: AI Decision Audit Trail |
| TS-ONB-001 | Process Step | Includes AI instant verification |

#### Dependencies

| Dependency | Type | Impact |
|------------|------|--------|
| II-ONB-004 (AI-Assisted KYC) | Innovation | Provides AI capability |
| II-ONB-003 (Document Pre-population) | Innovation | Supports AI verification |

#### Validation Implications

Control Analyst must validate that SOD is preserved and EU AI Act requirements are met.

---

### TD-ONB-005: Two-Track Compressed Journey

#### Decision Overview

| Attribute | Value |
|-----------|-------|
| **Decision ID** | TD-ONB-005 |
| **Category** | Strategic |
| **Decision Date** | 2025-12-09 |
| **Decision Maker** | Peter (SME) |
| **Status** | Approved |

#### Context and Problem Statement

Client mental model differs from bank's 180-day journey view. Clients want to feel "done" quickly; bank sees ongoing engagement value. Fintechs offer 10-minute onboarding creating competitive pressure.

#### Decision Drivers

- **Competitive Pressure:** Fintechs set 10-minute expectation
- **Client Psychology:** Clients see setup "done" when account works
- **Bank Value:** 180-day engagement drives activation and loyalty
- **NPS Impact:** Perceived long journey hurts satisfaction

#### Alternatives Considered

| Option | Description | Pros | Cons |
|--------|-------------|------|------|
| A: Compress Early | Front-load activation to Day 1-5 | Faster perceived completion | Restructures communications |
| B: Transparency | Progress tracker shows where client is | Sets expectations | Doesn't shorten perception |
| C: Two-Track | Track 1 "Account Ready" (Day 5) + Track 2 "Relationship" | Best of both | Requires messaging reframe |

#### Decision

**Selected Option:** All three (A + B + C) combined

**Rationale:**
Comprehensive approach addressing client psychology from multiple angles:
- Actually compress activation (A) so Track 1 completes by Day 5
- Provide progress visibility (B) throughout both tracks
- Reframe Track 2 as relationship value-add, not onboarding burden (C)

#### Impact Assessment

| Impact Area | Description | Severity |
|-------------|-------------|----------|
| Perceived Completion | 180 days → 5 days | Positive (High) |
| NPS | Expected improvement +35 → +40+ | Positive |
| Communication Strategy | Full reframe required | Medium effort |
| Bank Engagement | Maintained via Track 2 positioning | Neutral |

#### AS-IS References Affected

| Reference | Type | Change |
|-----------|------|--------|
| All PS# | Process Steps | Reorganized into two tracks |
| Client Journey | CX | Fundamentally redesigned |

#### TO-BE References Created/Modified

| Reference | Type | Description |
|-----------|------|-------------|
| TS-ONB-009 | Process Step | Progress Dashboard (transparency) |
| All TJ# | Touchpoints | Reorganized by track |

#### Dependencies

| Dependency | Type | Impact |
|------------|------|--------|
| II-ONB-009 (Progress Tracker) | Innovation | Enables transparency |
| II-ONB-002 (AI Personalization) | Innovation | Enables Track 2 messaging |

---

### TD-ONB-006: AI-First Automation Strategy

#### Decision Overview

| Attribute | Value |
|-----------|-------|
| **Decision ID** | TD-ONB-006 |
| **Category** | Strategic |
| **Decision Date** | 2025-12-09 |
| **Decision Maker** | Peter (SME) |
| **Status** | Approved |

#### Context and Problem Statement

II-ONB-005 (RPA Automation) is a MUST HAVE innovation. However, SME indicated preference for AI agents over traditional RPA where possible.

#### Decision Drivers

- **AI Capability:** AI agents are more intelligent and adaptable
- **RPA Limitations:** RPA is brittle, maintenance-heavy
- **Legacy Reality:** Some systems lack APIs, need RPA
- **IBM Partnership:** Existing relationship for RPA

#### Alternatives Considered

| Option | Description | Pros | Cons |
|--------|-------------|------|------|
| RPA Primary | Traditional RPA for all automation | Proven, IBM partnership | Brittle, high maintenance |
| AI Primary | AI agents wherever possible | Intelligent, adaptable | Emerging technology |
| Hybrid | AI primary, RPA for legacy gaps | Best fit for each use case | Two skill sets needed |

#### Decision

**Selected Option:** AI-first, RPA secondary (for legacy integration only)

**Rationale:**
AI agents offer intelligent decision-making, natural language interaction, and adaptability. RPA is limited to legacy systems without modern API integration. Target ratio: 80% AI agent automation, 20% RPA for legacy gaps.

#### Impact Assessment

| Impact Area | Description | Severity |
|-------------|-------------|----------|
| Automation Capability | Higher intelligence | Positive |
| IBM Partnership | Reduced RPA scope | Neutral |
| IT Skills | AI/ML skills needed | Medium effort |
| Long-term Maintenance | Lower than RPA | Positive |

#### AS-IS References Affected

| Reference | Type | Change |
|-----------|------|--------|
| All automation | Systems | AI-first strategy |

#### TO-BE References Created/Modified

| Reference | Type | Description |
|-----------|------|-------------|
| All TS# | Process Steps | AI-first automation |

#### Trade-offs Accepted

- May require more custom development vs. packaged RPA
- Less leverage of existing IBM RPA partnership
- Higher initial AI development effort

---

### TD-ONB-007: Include All SHOULD HAVE Innovations

#### Decision Overview

| Attribute | Value |
|-----------|-------|
| **Decision ID** | TD-ONB-007 |
| **Category** | Tactical |
| **Decision Date** | 2025-12-09 |
| **Decision Maker** | Peter (SME) |
| **Status** | Approved |

#### Context and Problem Statement

4 SHOULD HAVE innovations identified: II-ONB-003 (Document Pre-population), II-ONB-008 (Self-Service Portal), II-ONB-009 (Progress Tracker), II-ONB-010 (AI Nudges).

#### Decision

**Selected Option:** Include all 4 SHOULD HAVEs in target state

**Rationale:**
All support decisions already made (TD-001 through TD-006). Creates coherent ecosystem of capabilities. No capability sacrificed.

#### TO-BE References Created/Modified

| Reference | Type | Description |
|-----------|------|-------------|
| II-ONB-003 | Innovation | Integrated at TS-ONB-001 |
| II-ONB-008 | Innovation | Integrated at TS-ONB-010 |
| II-ONB-009 | Innovation | Integrated at TS-ONB-009 |
| II-ONB-010 | Innovation | Integrated at TS-ONB-005 |

---

### TD-ONB-008: Include COULD HAVE/DEFER with Conditions

#### Decision Overview

| Attribute | Value |
|-----------|-------|
| **Decision ID** | TD-ONB-008 |
| **Category** | Trade-off |
| **Decision Date** | 2025-12-09 |
| **Decision Maker** | Peter (SME) |
| **Status** | Approved |

#### Context and Problem Statement

3 remaining innovations: II-ONB-004 (AI-Assisted KYC) - COULD HAVE, II-ONB-006 (Biometrics) - COULD HAVE, II-ONB-007 (EU Digital Wallet) - DEFER.

#### Decision

**Selected Option:** Include all with appropriate conditions

**Rationale:**
- II-ONB-004: Integral to TD-ONB-004 (KYC automation) - include unconditionally
- II-ONB-006: Include when regulatory approval obtained (trigger-based)
- II-ONB-007: Prepare architecture now; implement when eIDAS 2.0 specs finalized (2026)

Full innovation portfolio positions bank ahead of competitors; conditional items managed by triggers not timelines.

#### TO-BE References Created/Modified

| Reference | Type | Description |
|-----------|------|-------------|
| II-ONB-004 | Innovation | Integrated at TC-ONB-001 to TC-ONB-005 |
| II-ONB-006 | Innovation | TC-ONB-010 (conditional) |
| II-ONB-007 | Innovation | Architecture preparation |

---

## Trade-off Analysis

### Trade-off Summary

| Trade-off | Competing Demands | Decision | Rationale |
|-----------|-------------------|----------|-----------|
| Automation vs Human Oversight | Speed vs Safety | AI first-eyes + human second-eyes | Regulatory safety with efficiency |
| Speed vs Comprehensiveness | Quick wins vs Full solution | All innovations included | No capability sacrificed |
| AI Agents vs RPA | Emerging vs Proven | AI-first, RPA for gaps | AI more capable long-term |

### Trade-off Details

#### Trade-off 1: Automation Depth vs Human Oversight

**Competing Demands:**
- **Demand A:** Maximum automation for speed and cost reduction
- **Demand B:** Human oversight for compliance and judgement calls

**Analysis:**
Regulatory requirements (four-eyes, SOD) mandate human involvement in key decisions. However, the "what" of human involvement can be optimized: reviewing AI recommendations vs. performing initial analysis.

**Decision:**
AI performs all initial analysis (first-eyes); human makes all final decisions (second-eyes). Four-eyes preserved; human focus elevated to judgement and exceptions.

**Accepted Compromise:**
Some manual effort remains for final approvals; accepted for regulatory safety and accountability.

**Linked TD#:** TD-ONB-004

---

#### Trade-off 2: Speed to Market vs Comprehensive Solution

**Competing Demands:**
- **Demand A:** Quick wins (chatbot, personalization) deliver value fast
- **Demand B:** Full solution (all 10 innovations) takes longer to implement

**Analysis:**
Partial implementation creates technical debt and fragmented experience. Full implementation provides coherent ecosystem but requires higher investment.

**Decision:**
Include all innovations with phased implementation (MUST HAVEs first, then SHOULD HAVEs, then conditional COULD HAVEs).

**Accepted Compromise:**
Higher total investment; longer full implementation timeline; but no capability sacrificed.

**Linked TD#:** TD-ONB-007, TD-ONB-008

---

#### Trade-off 3: AI Agents vs RPA Investment

**Competing Demands:**
- **Demand A:** RPA is proven, lower risk, IBM partnership exists
- **Demand B:** AI agents are more capable but emerging technology

**Analysis:**
RPA excels at repetitive, rule-based tasks but is brittle and maintenance-heavy. AI agents offer intelligent adaptation and natural language capability. Legacy systems without APIs still need RPA.

**Decision:**
AI-first strategy; RPA limited to legacy system integration (target 80/20 split).

**Accepted Compromise:**
May require more custom development; less leverage of existing IBM partnership for RPA; but better long-term capability and lower maintenance.

**Linked TD#:** TD-ONB-006

---

## Decision Patterns and Themes

### Common Themes

1. **Layered Approaches:** Multiple decisions (TD-001, TD-005) chose layered solutions rather than single approaches
2. **Human-AI Collaboration:** Consistent pattern of AI handling routine work, humans handling exceptions and final decisions
3. **Customer Empowerment:** Self-service capabilities emphasized (portal, consent management, progress tracker)
4. **Comprehensive Over Quick:** Preference for full solutions over quick wins

### Design Principles Emerging

1. **AI-First:** Where automation is needed, prefer AI agents over traditional RPA
2. **Human-in-Loop:** Maintain human accountability for key decisions
3. **Self-Service:** Empower customers to manage their own experience
4. **Layered Solutions:** Address diverse user needs with complementary approaches
5. **Full Portfolio:** Include all innovations with appropriate conditions rather than excluding

### Consistency Check

| Principle | Decisions Aligned | Decisions Conflicting | Resolution |
|-----------|-------------------|----------------------|------------|
| AI-First | TD-004, TD-006 | None | Consistent |
| Human-in-Loop | TD-002, TD-004 | None | Consistent |
| Self-Service | TD-003, TD-005 | None | Consistent |
| Comprehensive | TD-001, TD-005, TD-007, TD-008 | None | Consistent |

---

## Decision Audit Trail

### Decision Timeline

| Date | TD# | Decision | Category | Outcome |
|------|-----|----------|----------|---------|
| 2025-12-09 | TD-ONB-001 | Layered DTP | Tactical | Approved |
| 2025-12-09 | TD-ONB-002 | Hybrid Data Retention | Tactical | Approved |
| 2025-12-09 | TD-ONB-003 | Consent + Self-Service | Tactical | Approved |
| 2025-12-09 | TD-ONB-004 | AI First-Eyes KYC | Strategic | Approved |
| 2025-12-09 | TD-ONB-005 | Two-Track Journey | Strategic | Approved |
| 2025-12-09 | TD-ONB-006 | AI-First Automation | Strategic | Approved |
| 2025-12-09 | TD-ONB-007 | All SHOULD HAVEs | Tactical | Approved |
| 2025-12-09 | TD-ONB-008 | Conditional COULD HAVEs | Trade-off | Approved |

### Decision Revisions

| TD# | Original Decision | Revision Date | Revised Decision | Reason |
|-----|-------------------|---------------|------------------|--------|
| — | — | — | — | No revisions |

---

## Document Metadata

**SME Contributors:** Peter (SME)
**Decision Sessions:** 1
**Review Date:** 2025-12-09

### Linked Documents

| Document | Purpose | Link |
|----------|---------|------|
| Target State Documentation | Parent document | [target-state-documentation.md](./target-state-documentation.md) |
| Gap Resolution Log | Validation gaps | [gap-resolution-log.md](./gap-resolution-log.md) |
| AS-IS Process Documentation | Source reference | [as-is-process-documentation.md](./as-is-process-documentation.md) |

---

## Change Log

| Date | Contributor | Role | Changes |
|------|-------------|------|---------|
| 2025-12-09 | Peter | SME | Initial decision log - 8 decisions |

---

## Glossary

| Term | Definition |
|------|------------|
| TD# | Transformation Decision reference |
| Strategic | Fundamental design direction decision |
| Tactical | Specific implementation choice |
| Trade-off | Decision balancing competing demands |
| Deferred | Decision postponed for future consideration |
| AI first-eyes | AI performs initial review/analysis |
| Human second-eyes | Human makes final approval decision |

---

_Generated by ProcessMiner Transformation Agent_
_Document ID: TRX-ONB-001-DECISIONS_
