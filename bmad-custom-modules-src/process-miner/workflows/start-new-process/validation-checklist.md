# Start New Process - Validation Checklist

## Session Completeness

- [ ] Process metadata captured (name, business unit, SME details)
- [ ] Process overview completed (purpose, trigger, frequency, volume)
- [ ] Minimum 5 process steps documented
- [ ] Each process step has unique PS# ID
- [ ] Each process step has rationale (banking compliance requirement)
- [ ] Each process step has assigned owner

## Pain Points Validation

- [ ] Pain points identified (or confirmed none exist)
- [ ] Each pain point has unique PP# ID
- [ ] Each pain point has severity (HIGH/MEDIUM/LOW)
- [ ] Each pain point has impact assessment
- [ ] Each pain point linked to relevant PS# ID(s)

## Exceptions Validation

- [ ] Exceptions identified (or confirmed none exist)
- [ ] Each exception has unique EX# ID
- [ ] Each exception has frequency (RARE/OCCASIONAL/FREQUENT)
- [ ] Each exception has handling procedure
- [ ] Each exception linked to relevant PS# ID(s)

## Controls & Compliance

- [ ] Compliance controls identified (or confirmed standard only)
- [ ] Each control has unique CP# ID
- [ ] Each control has control_type (PREVENTIVE/DETECTIVE/CORRECTIVE)
- [ ] Each control traced to regulatory requirement
- [ ] Each control linked to relevant PS# ID(s)
- [ ] Control owner assigned for each control

## Systems & Tools

- [ ] Systems/tools identified (or confirmed none used)
- [ ] Each system has unique SYS# ID
- [ ] Each system has system_type (CORE/SUPPORTING/EXTERNAL)
- [ ] System purpose and integration status captured
- [ ] Each system linked to relevant PS# ID(s)

## Cross-Referencing

- [ ] Traceability matrix established (PS↔EX, PS↔PP, PS↔CP, PS↔SYS)
- [ ] All IDs follow naming convention (PS-XX-###, EX-XX-###, PP-XX-###, CP-XX-###, SYS-XX-###)
- [ ] No orphaned elements (all items linked to process steps)

## JSON Schema Compliance (v1.0.0)

- [ ] `$schema` field present: "process-miner-structured-data-v1"
- [ ] `schema_version` field present: "1.0.0"
- [ ] `session.checkpoint` updated correctly
- [ ] `validation.status` set to COMPLETE/PARTIAL/DRAFT
- [ ] All items have `confidence` field (HIGH/MEDIUM/LOW)
- [ ] All items have `links` object with `process_steps` array

## Output Files Synchronized

- [ ] structured-data.json - Machine-readable data
- [ ] as-is-process-documentation.md - Main document
- [ ] exceptions-detail.md - Exception details
- [ ] pain-points-detail.md - Pain point details
- [ ] control-points-detail.md - Control details
- [ ] All 5 files contain consistent data

## Session State Management

- [ ] Session state saved successfully
- [ ] Checkpoint granularity: per-item (not per-step)
- [ ] Session resumable if needed
- [ ] SME confirmed completeness of captured data

## Principles Adherence

- [ ] **Import Before Interview**: Checked for existing docs first
- [ ] **Progressive Elicitation**: Started broad, drilled down adaptively
- [ ] **Y/E/R Approval**: Used [Y] Accept / [E] Edit / [R] Rewrite pattern
- [ ] **Rewrite Sub-menu**: [R] opens Advanced Elicitation, Party Mode, Brainstorming, Quick Questions
- [ ] **Banking Compliance**: Captured rationale and requirements for all elements

## Quality Checks

- [ ] AI gap analysis performed before completion
- [ ] All clarification questions addressed
- [ ] No placeholder text in captured data
- [ ] Dates and timestamps properly formatted
- [ ] SME expressed satisfaction with captured content

## Handoff Readiness

- [ ] Structured data ready for downstream agents (Transformation Agent, Control Analyst, etc.)
- [ ] Session resumable if needed (state preserved)
- [ ] Clear next steps communicated to SME
