# Gap Resolution Log: Onboarding

**Document Type:** Validation Gap Tracking
**Process ID:** ONB-001
**Transformation ID:** TRX-ONB-001
**Last Updated:** 2025-12-09
**Version:** 1.0

---

## Summary

| Metric | Value |
|--------|-------|
| Total Gaps Raised | 12 |
| Resolved | 12 |
| Deferred | 0 |
| Open | 0 |
| Validation Iterations | 1 |

---

## Gap Resolution Table

| VG# | Source | Description | Severity | Resolution Type | Status |
|-----|--------|-------------|----------|-----------------|--------|
| VG-ONB-001 | Control Analyst | SOD implementation lacks human intervention criteria | High | Documentation Update | Resolved |
| VG-ONB-002 | Control Analyst | Data retention hybrid reintroduces manual risk | High | Design Change | Resolved |
| VG-ONB-003 | Control Analyst | Consent propagation detail missing | Medium | Documentation Update | Resolved |
| VG-ONB-004 | Control Analyst | Biometrics regulatory framework missing | Medium | Documentation Update | Resolved |
| VG-ONB-005 | Control Analyst | EU AI Act compliance detail insufficient | High | Documentation Update | Resolved |
| VG-ONB-006 | Control Analyst | Audit trail transition continuity | Medium | Documentation Update | Resolved |
| VG-ONB-007 | Control Analyst | Effectiveness KPIs not defined | Medium | Documentation Update | Resolved |
| VG-ONB-008 | CX Analyst | Day 5 vs fintech benchmark gap | Medium | Documentation Update | Resolved |
| VG-ONB-009 | CX Analyst | Portal deflection targets missing | High | Documentation Update | Resolved |
| VG-ONB-010 | CX Analyst | CES baseline and adoption curve missing | High | Documentation Update | Resolved |
| VG-ONB-011 | Innovation Analyst | RPA scope change benefit impact | Medium | Documentation Update | Resolved |
| VG-ONB-012 | Innovation Analyst | eIDAS architecture prep detail | Low | Documentation Update | Resolved |

---

## Detailed Resolution Records

### VG-ONB-001: SOD Human Intervention Criteria

| Attribute | Value |
|-----------|-------|
| **Source** | Control Analyst |
| **Severity** | High |
| **TO-BE Reference** | TC-ONB-001 to TC-ONB-005 |
| **Resolution Type** | Documentation Update |
| **Status** | Resolved |
| **Resolved Date** | 2025-12-09 |

**Gap Description:**
The design states "AI = maker, Human = checker" but lacks explicit criteria for when human override is mandatory, AI confidence thresholds, and reviewer qualification requirements.

**Resolution:**
Added explicit SOD implementation criteria:
- AI confidence score <85% triggers mandatory human detailed review
- AI confidence 85-95% requires human confirmation
- AI confidence >95% requires human spot-check (10% sample)
- Human reviewers must hold AML certification
- Daily audit of approval patterns to detect rubber-stamping
- Quarterly review of AI confidence calibration

---

### VG-ONB-002: Data Retention Hybrid Risk

| Attribute | Value |
|-----------|-------|
| **Source** | Control Analyst |
| **Severity** | High |
| **TO-BE Reference** | TC-ONB-008 |
| **Resolution Type** | Design Change |
| **Status** | Resolved |
| **Resolved Date** | 2025-12-09 |
| **New Decision** | TD-ONB-009 |

**Gap Description:**
TC-ONB-008 hybrid approach requiring human confirmation reintroduces the manual risk that automation was meant to eliminate.

**Resolution:**
Redesigned TC-ONB-008 from confirmation-based to exception-based:
- System automatically executes retention policies
- Human review limited to exceptions, disputes, policy changes
- SLA-based monitoring ensures GDPR compliance
- Full automation logging with human oversight dashboard

---

### VG-ONB-003: Consent Propagation Detail

| Attribute | Value |
|-----------|-------|
| **Source** | Control Analyst |
| **Severity** | Medium |
| **TO-BE Reference** | TC-ONB-006, TC-ONB-007 |
| **Resolution Type** | Documentation Update |
| **Status** | Resolved |
| **Resolved Date** | 2025-12-09 |

**Gap Description:**
Missing specifics on consent withdrawal propagation, in-flight handling, and granularity model.

**Resolution:**
Added consent architecture detail:
- Real-time propagation via event bus (<1 second latency)
- In-flight transactions: complete current, block future
- Purpose-specific consent model (marketing, analytics, third-party)
- Consent withdrawal SLAs: immediate for new, 24h for in-flight

---

### VG-ONB-004: Biometrics Regulatory Framework

| Attribute | Value |
|-----------|-------|
| **Source** | Control Analyst |
| **Severity** | Medium |
| **TO-BE Reference** | TC-ONB-010 |
| **Resolution Type** | Documentation Update |
| **Status** | Resolved |
| **Resolved Date** | 2025-12-09 |

**Gap Description:**
TC-ONB-010 lacks regulatory approval framework, fallback controls, and jurisdiction handling.

**Resolution:**
Added regulatory framework:
- Required approvals: GDPR DPA notification, national biometric law compliance
- Fallback: TC-ONB-002 (standard identity verification) if biometrics not approved
- Jurisdiction plan: EU-wide first, extend based on local approval
- Regulatory tracking: quarterly review of approval status changes

---

### VG-ONB-005: EU AI Act Compliance

| Attribute | Value |
|-----------|-------|
| **Source** | Control Analyst |
| **Severity** | High |
| **TO-BE Reference** | TC-ONB-009 |
| **Resolution Type** | Documentation Update |
| **Status** | Resolved |
| **Resolved Date** | 2025-12-09 |

**Gap Description:**
TC-ONB-009 lacks EU AI Act specifics for high-risk AI systems (Art. 9, 11, 13, 14).

**Resolution:**
Expanded TC-ONB-009 to include:
- Art. 9: Risk management system with quarterly risk assessment
- Art. 11: Technical documentation of AI model, training data, performance
- Art. 13: User notification that AI assists KYC decision
- Art. 14: Human oversight procedures (linked to VG-ONB-001 resolution)
- Ongoing monitoring of AI performance and bias

---

### VG-ONB-006: Audit Trail Transition

| Attribute | Value |
|-----------|-------|
| **Source** | Control Analyst |
| **Severity** | Medium |
| **TO-BE Reference** | All TC-ONB-* |
| **Resolution Type** | Documentation Update |
| **Status** | Resolved |
| **Resolved Date** | 2025-12-09 |

**Gap Description:**
No plan for audit trail continuity between AS-IS (CP#) and TO-BE (TC#) during transition.

**Resolution:**
Added transition plan:
- CP# to TC# mapping table for auditor reference
- Legacy audit trail preservation (5-year retention)
- Cross-reference documentation for regulatory audits
- Parallel logging during transition period

---

### VG-ONB-007: Effectiveness KPIs

| Attribute | Value |
|-----------|-------|
| **Source** | Control Analyst |
| **Severity** | Medium |
| **TO-BE Reference** | Section 4 (Control Design) |
| **Resolution Type** | Documentation Update |
| **Status** | Resolved |
| **Resolved Date** | 2025-12-09 |

**Gap Description:**
Effectiveness target of 4.8/5 lacks measurable KPIs and validation methodology.

**Resolution:**
Added effectiveness measurement framework:
- Per-control KPIs defined (detection rate, false positive rate, audit completeness)
- Baseline measurement at go-live
- Quarterly effectiveness assessment
- Annual third-party control audit

---

### VG-ONB-008: Day 5 vs Fintech Benchmark

| Attribute | Value |
|-----------|-------|
| **Source** | CX Analyst |
| **Severity** | Medium |
| **TO-BE Reference** | Section 5.2, TJ-ONB-003 |
| **Resolution Type** | Documentation Update |
| **Status** | Resolved |
| **Resolved Date** | 2025-12-09 |

**Gap Description:**
Day 5 timeline not benchmarked against fintech 10-minute competitor standard.

**Resolution:**
Added competitive positioning:
- Regulatory constraints (KYC, AML) prevent 10-minute banking onboarding
- Day 5 is best-in-class for regulated full-service banks
- Micro-wins strategy: instant account number (Day 1), basic features enabled (Day 2)
- Track 1 "done" messaging compensates for absolute timeline difference

---

### VG-ONB-009: Portal Deflection Targets

| Attribute | Value |
|-----------|-------|
| **Source** | CX Analyst |
| **Severity** | High |
| **TO-BE Reference** | TJ-ONB-010, Section 5.3 |
| **Resolution Type** | Documentation Update |
| **Status** | Resolved |
| **Resolved Date** | 2025-12-09 |

**Gap Description:**
Self-service portal lacks deflection rate targets and escalation quality metrics.

**Resolution:**
Added portal metrics:
- Deflection target: 70% queries resolved without human contact
- Escalation quality: 100% context transfer (no re-explanation)
- Repeat contact rate: <10% (measure resolution quality)
- Portal CES target: ≤2 (low effort)

---

### VG-ONB-010: CES Baseline Missing

| Attribute | Value |
|-----------|-------|
| **Source** | CX Analyst |
| **Severity** | High |
| **TO-BE Reference** | Section 5.4 |
| **Resolution Type** | Documentation Update |
| **Status** | Resolved |
| **Resolved Date** | 2025-12-09 |

**Gap Description:**
CES 50-60% reduction target lacks AS-IS baseline and portal adoption curve.

**Resolution:**
Added CES framework:
- Pre-launch: Measure AS-IS CES baseline across current touchpoints
- Target reframed: "50-60% reduction by Month 12" (not Day 1)
- Portal adoption curve: expect Year 1 learning effort, benefits realize Month 6+
- Leading indicator: Portal usage rate as proxy for effort shifting

---

### VG-ONB-011: RPA Scope Change Impact

| Attribute | Value |
|-----------|-------|
| **Source** | Innovation Analyst |
| **Severity** | Medium |
| **TO-BE Reference** | Section 6.2, II-ONB-005 |
| **Resolution Type** | Documentation Update |
| **Status** | Resolved |
| **Resolved Date** | 2025-12-09 |

**Gap Description:**
RPA scope reduction (TD-ONB-006) not documented with impact on €500K benefit target.

**Resolution:**
Added scope change documentation:
- Original: RPA across all 7 systems (€500K benefit)
- Revised: RPA for legacy gaps only (20% scope)
- Benefit reallocation: AI agents absorb efficiency gains
- €500K target maintained through AI-powered automation (different mechanism)

---

### VG-ONB-012: eIDAS Architecture Prep

| Attribute | Value |
|-----------|-------|
| **Source** | Innovation Analyst |
| **Severity** | Low |
| **TO-BE Reference** | Section 6.4, II-ONB-007 |
| **Resolution Type** | Documentation Update |
| **Status** | Resolved |
| **Resolved Date** | 2025-12-09 |

**Gap Description:**
II-ONB-007 "architecture prepared" lacks specific readiness steps.

**Resolution:**
Added readiness steps:
- Identity workflow designed to accept wallet credentials
- API endpoints stubbed for eIDAS 2.0 integration
- Data mapping: wallet attributes → KYC requirements
- Regulatory monitoring: 0.25 FTE tracking eIDAS 2.0 specs
- Trigger: Begin implementation when specs finalized (est. 2026)

---

## Deferred Gaps

None — all gaps resolved in iteration 1.

---

## Change Log

| Date | Action | By |
|------|--------|-----|
| 2025-12-09 | Initial gap log created | Transformation Agent |
| 2025-12-09 | 12 gaps raised in validation iteration 1 | Specialist Agents |
| 2025-12-09 | All 12 gaps resolved | Peter (SME) |

---

_Generated by ProcessMiner Transformation Agent_
