# Friction Points Detail: Client Onboarding

**Document Type:** Friction Point Analysis
**Process ID:** COB-003
**Business Unit:** BizBanking
**Last Updated:** 2025-12-09
**Version:** 1.0.0

---

## Overview

This document provides detailed analysis of each friction point in the Client Onboarding journey. For summary view, see [CX Journey Documentation](./cx-journey-documentation.md).

---

## FP-COB-001: Unclear Document Requirements

| Attribute | Value |
|-----------|-------|
| **Stage** | Initiation |
| **Touchpoint** | JT-COB-001 (Application Submission) |
| **Severity** | HIGH |
| **CES Impact** | +3 |
| **Frequency** | 30% of applications |

### Description

Clients are presented with a document checklist that appears comprehensive but lacks context-specific guidance. Standard vs. complex requirements are not differentiated, leading to confusion about what's actually needed. Examples and acceptable formats are missing.

### Root Cause Analysis

1. **Single checklist for all scenarios** — No differentiation between sole trader, partnership, limited company
2. **Generic document names** — "Proof of address" without specifying acceptable documents
3. **No examples provided** — Clients guess at what's acceptable
4. **No real-time validation** — Errors only discovered after submission

### Client Impact

| Impact Area | Description |
|-------------|-------------|
| **Emotional** | Confusion at start, frustration when told incomplete |
| **Time** | 1-3 additional days gathering correct documents |
| **Trust** | Early erosion of confidence in process |

### Pain Point Link
- PP-COB-001: Manual document chasing

### Enhancement Ideas

| EI# | Enhancement | Est. CES Reduction | Complexity |
|-----|-------------|-------------------|------------|
| EI-COB-001 | Smart document checklist with real-time validation | -6 | MEDIUM |

---

## FP-COB-002: Repeated Document Chasing

| Attribute | Value |
|-----------|-------|
| **Stage** | Initiation |
| **Touchpoint** | JT-COB-002 (Document Request) |
| **Severity** | HIGH |
| **CES Impact** | +6 |
| **Frequency** | 30% of applications, 2-3 cycles each |

### Description

After submitting what they believe is a complete application, clients receive emails requesting additional documents. This often happens multiple times, with new items requested in subsequent emails rather than all at once. The experience feels like "death by a thousand cuts."

### Root Cause Analysis

1. **Incomplete initial triage** — Operations officers miss items on first review
2. **Sequential discovery** — KYC finds more issues after Ops review
3. **No consolidated request** — Each team sends separate requests
4. **Manual email process** — No automated tracking or reminder system

### Client Impact

| Impact Area | Description |
|-------------|-------------|
| **Emotional** | Annoyed → Frustrated → Distrustful |
| **Time** | 2-5 additional days per application |
| **Effort** | 4-6 email exchanges, document scanning |
| **Relationship** | Trust eroded before relationship begins |

### Pain Point Link
- PP-COB-001: Manual document chasing

### Enhancement Ideas

| EI# | Enhancement | Est. CES Reduction | Complexity |
|-----|-------------|-------------------|------------|
| EI-COB-001 | Smart document checklist with real-time validation | -6 | MEDIUM |
| EI-COB-002 | Automated document reminder with escalation | -3 | LOW |

---

## FP-COB-003: Paper Signature Requirement

| Attribute | Value |
|-----------|-------|
| **Stage** | Initiation |
| **Touchpoint** | JT-COB-001 (Application Submission) |
| **Severity** | MEDIUM |
| **CES Impact** | +2 |
| **Frequency** | 40% of applications |

### Description

Despite digital application options, 40% of applications still require paper signatures — either because the channel doesn't support e-sign (RM/branch) or clients aren't offered the digital option. Paper applications require scanning, which adds 1-2 days and introduces quality issues.

### Root Cause Analysis

1. **Channel inconsistency** — Portal has e-sign, branch/RM don't
2. **Legacy process** — Paper still "feels more official" to some RMs
3. **No mandate for digital** — Optional rather than default
4. **Scanning burden** — Client must scan or Operations must digitize

### Client Impact

| Impact Area | Description |
|-------------|-------------|
| **Emotional** | Inconvenience, feels outdated |
| **Time** | 1-2 days for scanning/posting |
| **Effort** | Physical effort to print, sign, scan |

### Pain Point Link
- PP-COB-004: Paper-based signatures

### Enhancement Ideas

| EI# | Enhancement | Est. CES Reduction | Complexity |
|-----|-------------|-------------------|------------|
| EI-COB-003 | E-signature implementation (DocuSign/Adobe Sign) | -2 | MEDIUM |

---

## FP-COB-004: Complex Ownership Questions

| Attribute | Value |
|-----------|-------|
| **Stage** | Verification |
| **Touchpoint** | JT-COB-004 (Information Request) |
| **Severity** | MEDIUM |
| **CES Impact** | +4 |
| **Frequency** | 20% of applications |

### Description

For complex ownership structures (>3 layers, foreign shareholders, trusts), clients receive technical KYC questions they often cannot answer without professional help. The language is regulatory, not client-friendly, and clients don't understand why this information is needed.

### Root Cause Analysis

1. **Regulatory complexity** — CDD/AML requirements are genuinely complex
2. **No explanation** — Clients don't understand purpose
3. **Technical language** — "Ultimate Beneficial Owner" vs "Who owns your company"
4. **No self-help** — Clients must engage accountant/solicitor

### Client Impact

| Impact Area | Description |
|-------------|-------------|
| **Emotional** | Confused, stressed, intimidated |
| **Time** | 2-5 days to consult professionals |
| **Cost** | €200-500 professional fees |
| **Trust** | Bank perceived as bureaucratic |

### Exception Link
- EX-COB-005: Complex Ownership Structure

### Enhancement Ideas

| EI# | Enhancement | Est. CES Reduction | Complexity |
|-----|-------------|-------------------|------------|
| EI-COB-004 | Interactive ownership structure wizard | -2 | HIGH |

---

## FP-COB-005: No Status Visibility

| Attribute | Value |
|-----------|-------|
| **Stage** | All Stages |
| **Touchpoint** | All Touchpoints |
| **Severity** | HIGH |
| **CES Impact** | +4 |
| **Frequency** | 100% of applications |

### Description

After submitting an application, clients enter a "black hole" with no visibility into progress. They don't know what stage they're at, what's happening, or when to expect updates. The only communication is when the bank needs something from them.

### Root Cause Analysis

1. **No status portal** — Clients can't self-serve status
2. **Reactive communication** — Only contact when bank needs input
3. **Internal focus** — Systems designed for bank, not client
4. **No proactive updates** — "Still processing" messages not sent

### Client Impact

| Impact Area | Description |
|-------------|-------------|
| **Emotional** | Anxious, uncertain, frustrated |
| **Behavior** | Calls RM/branch for updates |
| **Trust** | Bank perceived as uncommunicative |

### Pain Point Link
- PP-COB-002: System switching / No single client view (internal parallel)

### Enhancement Ideas

| EI# | Enhancement | Est. CES Reduction | Complexity |
|-----|-------------|-------------------|------------|
| EI-COB-005 | Real-time status tracker with proactive notifications | -4 | MEDIUM |
| EI-COB-007 | Expected timeline communication at each stage | -2 | LOW |

---

## FP-COB-006: Missed Welcome Calls

| Attribute | Value |
|-----------|-------|
| **Stage** | Relationship |
| **Touchpoint** | JT-COB-008 (Welcome Call) |
| **Severity** | MEDIUM |
| **CES Impact** | +3 |
| **Frequency** | 70% require 3+ attempts |

### Description

The welcome call — intended as a positive relationship-building moment — becomes a friction point because clients don't answer unknown numbers, RMs call during business hours when clients are working, and there's no way for clients to schedule a convenient time.

### Root Cause Analysis

1. **Unknown caller** — Clients screen calls from unrecognized numbers
2. **Business hours only** — RM calls 9-5 when clients are working
3. **No scheduling option** — Client cannot pick their time
4. **Multiple attempts** — Creates chase dynamic, not welcome dynamic

### Client Impact

| Impact Area | Description |
|-------------|-------------|
| **Emotional** | Annoyed, feels chased rather than welcomed |
| **Time** | 3-5 days to finally connect |
| **Behavior** | Avoidance, delayed relationship establishment |

### Pain Point Link
- PP-COB-006: Welcome call scheduling

### Enhancement Ideas

| EI# | Enhancement | Est. CES Reduction | Complexity |
|-----|-------------|-------------------|------------|
| EI-COB-006 | Self-service welcome call scheduling | -3 | LOW |

---

## FP-COB-007: Wait Time Uncertainty

| Attribute | Value |
|-----------|-------|
| **Stage** | Decision |
| **Touchpoint** | JT-COB-005 (Credit Decision) |
| **Severity** | MEDIUM |
| **CES Impact** | +2 |
| **Frequency** | 100% of overdraft applications |

### Description

Clients waiting for credit decisions don't know how long to expect. SLAs exist internally (3 days) but aren't communicated to clients. The wait feels longer than it is because of uncertainty.

### Root Cause Analysis

1. **No timeline communication** — Clients not told expected duration
2. **Variable processing** — Actual times vary significantly
3. **No interim updates** — Silence during processing
4. **Anxiety amplification** — Uncertainty extends perceived wait

### Client Impact

| Impact Area | Description |
|-------------|-------------|
| **Emotional** | Anxious, uncertain |
| **Behavior** | Calls RM for updates |
| **Trust** | Bank perceived as slow/unresponsive |

### Enhancement Ideas

| EI# | Enhancement | Est. CES Reduction | Complexity |
|-----|-------------|-------------------|------------|
| EI-COB-007 | Expected timeline communication at each stage | -2 | LOW |

---

## Summary Statistics

| Metric | Value |
|--------|-------|
| **Total Friction Points** | 7 |
| **Total CES Impact** | +24 points |
| **High Severity** | 3 |
| **Medium Severity** | 4 |
| **Documentation Related** | 3 |
| **Communication Related** | 2 |
| **Visibility Related** | 2 |

---

## Cross-Reference Summary

### Friction to Touchpoint Mapping

| Friction Point | Touchpoint |
|----------------|------------|
| FP-COB-001 | JT-COB-001 |
| FP-COB-002 | JT-COB-002 |
| FP-COB-003 | JT-COB-001 |
| FP-COB-004 | JT-COB-004 |
| FP-COB-005 | All |
| FP-COB-006 | JT-COB-008 |
| FP-COB-007 | JT-COB-005 |

### Friction to Pain Point Mapping

| Friction Point | Pain Point |
|----------------|------------|
| FP-COB-001 | PP-COB-001 |
| FP-COB-002 | PP-COB-001 |
| FP-COB-003 | PP-COB-004 |
| FP-COB-004 | (via EX-COB-005) |
| FP-COB-005 | PP-COB-002 |
| FP-COB-006 | PP-COB-006 |
| FP-COB-007 | - |

---

_Generated by ProcessMiner Client Journey Analyst_
_Document ID: COB-003-friction_
