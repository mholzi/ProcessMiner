# Process Miner Agent Alignment Design

## Executive Summary

This document proposes structural alignment across four ProcessMiner analyst agents to establish consistent capabilities, shared workflows, and unified patterns. The goal is to enable each agent to perform six standardized capabilities while maintaining their domain-specific expertise.

---

## 1. Current State Analysis

### 1.1 Agent Overview

| Agent | Icon | Primary Domain | Invocation Pattern | Menu Sections |
|-------|------|----------------|-------------------|---------------|
| Process Documentation Analyst (PDA) | 📋 | Process knowledge extraction | Single (AS-IS only) | None |
| Client Journey Analyst (CJA) | 🎯 | Client experience mapping | Dual (AS-IS + TO-BE) | Yes |
| Control Analyst (CA) | 🛡️ | Compliance & control validation | Dual (AS-IS + TO-BE) | Yes |
| Innovation Analyst (IA) | 💡 | Market trends & innovation | Dual (AS-IS + TO-BE) | None |

### 1.2 Structural Inconsistencies Identified

| Aspect | PDA | CJA | CA | IA |
|--------|-----|-----|----|----|
| Section-based menu | ❌ | ✅ | ✅ | ❌ |
| Uses workflow references | ✅ | ✅ | ✅ | ⚠️ Mixed |
| Uses `action="#prompt"` pattern | ❌ | ❌ | ❌ | ✅ |
| Capture-item workflow | ✅ | ✅ | ❌ | ❌ |
| Continue-session workflow | ✅ | ✅ | ❌ | ❌ |
| QA check capability | ❌ | ❌ | ❌ | ❌ |
| YAML export capability | ❌ | ❌ | ❌ | ❌ |
| Executive summary | ❌ | ✅ | ✅ | ✅ |
| Workflow file extension | `.md` | Mixed | Mixed | `.yaml` |

### 1.3 Current Item Types by Agent

| Agent | Capturable Items | Current Workflow |
|-------|-----------------|------------------|
| PDA | Pain Points (PP#), Exceptions (EX#), Control Points (CP#) | `capture-item/workflow.md` |
| CJA | Enhancement Ideas (EI#) | `capture-item/workflow.md` |
| CA | Control Points (CP#) | None (missing) |
| IA | Innovation Ideas (II#) | None (uses inline prompts) |

---

## 2. Target State: Unified Agent Capability Model

### 2.1 Six Standard Capabilities per Agent

Each agent MUST support these six capabilities in a consistent manner:

```
┌─────────────────────────────────────────────────────────────────┐
│                    STANDARD AGENT CAPABILITIES                  │
├─────────────────────────────────────────────────────────────────┤
│  (A) Initial Analysis      - Domain-specific analysis workflow  │
│  (B) Capture/Amend Items   - Add/edit key input factors         │
│  (C) Compose/Edit Document - Create/update main deliverable     │
│  (D) QA Check              - Validate document integrity        │
│  (E) Export to YAML        - Generate structured AI-consumable  │
│  (F) Executive Summary     - Generate stakeholder summary       │
└─────────────────────────────────────────────────────────────────┘
```

### 2.2 Capability Mapping by Agent

| Capability | PDA | CJA | CA | IA |
|------------|-----|-----|----|----|
| **(A) Initial Analysis** | Elicit Process Knowledge | CX AS-IS Analysis | Regulatory Framework Mapping + Control Inventory | Market Research + Innovation Backlog |
| **(B) Capture/Amend Items** | PP#, EX#, CP# | EI# (Enhancement Ideas) | CP# (Control Points), RG# (Regulations) | II# (Innovation Ideas), TR# (Trends) |
| **(C) Compose/Edit Document** | AS-IS Process Documentation | CX Journey Report | Compliance Assessment Report | Innovation Analysis Report |
| **(D) QA Check** | Validate all sections aligned | Validate journey vs process | Validate controls vs regulations | Validate ideas vs priorities |
| **(E) Export to YAML** | process-asis.yaml | cx-journey.yaml | compliance-controls.yaml | innovation-priorities.yaml |
| **(F) Executive Summary** | Process Summary | CX Summary | Compliance Summary | Innovation Summary |

---

## 3. Shared Workflow Architecture

### 3.1 Recommended Shared Workflows

These workflows should be parameterized and reused across all agents:

```
.bmad/custom/modules/process-miner/workflows/
├── shared/
│   ├── capture-item/workflow.md          # Parameterized by item_type
│   ├── continue-session/workflow.md      # Generic session resume
│   ├── compose-document/workflow.md      # Parameterized by doc_type
│   ├── qa-check/workflow.md              # Parameterized by validation_rules
│   ├── export-to-yaml/workflow.md        # Parameterized by schema
│   └── executive-summary/workflow.md     # Parameterized by summary_template
```

### 3.2 Workflow Parameter Definitions

#### 3.2.1 capture-item/workflow.md

| Parameter | PDA Values | CJA Values | CA Values | IA Values |
|-----------|------------|------------|-----------|-----------|
| `item_type` | `pain_point`, `exception`, `control_point` | `enhancement_idea` | `control_point`, `regulation` | `innovation_idea`, `market_trend` |
| `id_prefix` | PP#, EX#, CP# | EI# | CP#, RG# | II#, TR# |
| `required_fields` | description, severity, process_step | description, benefit, effort | requirement_ref, effectiveness, evidence | feasibility_score, strategic_fit, roi_estimate |
| `validation_rules` | Must link to PS# | Must link to journey_stage | Must link to regulation | Must have feasibility assessment |

#### 3.2.2 compose-document/workflow.md

| Parameter | PDA | CJA | CA | IA |
|-----------|-----|-----|----|----|
| `doc_type` | `process-asis` | `cx-journey` | `compliance-assessment` | `innovation-analysis` |
| `template` | process-asis-template.md | cx-journey-template.md | compliance-template.md | innovation-template.md |
| `required_sections` | Overview, Steps, Exceptions, Pain Points, Controls | Journey Map, Touchpoints, CES Scores, Enhancement Ideas | Regulatory Framework, Control Inventory, Gap Analysis | Market Research, Innovation Backlog, Priorities |

#### 3.2.3 qa-check/workflow.md

| Parameter | PDA | CJA | CA | IA |
|-----------|-----|-----|----|----|
| `validation_type` | `process-integrity` | `cx-alignment` | `compliance-coverage` | `innovation-viability` |
| `cross_references` | Steps ↔ Controls ↔ Pain Points | Journey ↔ Process Steps ↔ Enhancements | Controls ↔ Regulations ↔ Evidence | Ideas ↔ Feasibility ↔ Priorities |
| `completeness_checks` | All steps have controls | All touchpoints scored | All regulations mapped | All ideas assessed |

#### 3.2.4 export-to-yaml/workflow.md

| Parameter | PDA | CJA | CA | IA |
|-----------|-----|-----|----|----|
| `schema` | process-asis-schema.yaml | cx-journey-schema.yaml | compliance-schema.yaml | innovation-schema.yaml |
| `output_file` | {process_id}-asis.yaml | {process_id}-cx.yaml | {process_id}-compliance.yaml | {process_id}-innovation.yaml |
| `nested_entities` | steps, controls, pain_points | touchpoints, enhancements | controls, regulations, gaps | ideas, trends, priorities |

---

## 4. Proposed Agent Menu Structure

### 4.1 Standardized Menu Template

Each agent should follow this menu structure:

```yaml
menu:
  # Section: Initial Analysis
  - trigger: run-{domain}-analysis
    workflow: '{project-root}/.bmad/custom/modules/process-miner/workflows/{domain}-analysis/workflow.md'
    description: 'Run full {Domain} analysis workflow'
    section: 'Initial Analysis'

  - trigger: continue-session
    workflow: '{project-root}/.bmad/custom/modules/process-miner/workflows/shared/continue-session/workflow.md'
    description: 'Continue existing analysis session'
    section: 'Initial Analysis'

  # Section: Capture & Amend
  - trigger: add-{item_type}
    workflow: '{project-root}/.bmad/custom/modules/process-miner/workflows/shared/capture-item/workflow.md'
    item_type: '{item_type}'
    mode: 'add'
    description: 'Add new {Item Type}'
    section: 'Capture & Amend'

  - trigger: edit-{item_type}
    workflow: '{project-root}/.bmad/custom/modules/process-miner/workflows/shared/capture-item/workflow.md'
    item_type: '{item_type}'
    mode: 'edit'
    description: 'Edit existing {Item Type}'
    section: 'Capture & Amend'

  # Section: Document Management
  - trigger: compose-document
    workflow: '{project-root}/.bmad/custom/modules/process-miner/workflows/shared/compose-document/workflow.md'
    doc_type: '{doc_type}'
    description: 'Compose/Edit {Document Name}'
    section: 'Document Management'

  - trigger: qa-check
    workflow: '{project-root}/.bmad/custom/modules/process-miner/workflows/shared/qa-check/workflow.md'
    validation_type: '{validation_type}'
    description: 'Run QA validation check'
    section: 'Document Management'

  # Section: Outputs
  - trigger: export-yaml
    workflow: '{project-root}/.bmad/custom/modules/process-miner/workflows/shared/export-to-yaml/workflow.md'
    schema: '{schema}'
    description: 'Export to structured YAML for AI consumption'
    section: 'Outputs'

  - trigger: executive-summary
    workflow: '{project-root}/.bmad/custom/modules/process-miner/workflows/shared/executive-summary/workflow.md'
    summary_template: '{template}'
    description: 'Generate Executive Summary'
    section: 'Outputs'
```

### 4.2 Agent-Specific Menu Configurations

#### Process Documentation Analyst (PDA)

```yaml
menu:
  # Section: Initial Analysis
  - trigger: start-new
    workflow: '...elicit-process-knowledge/workflow.md'
    section: 'Initial Analysis'

  - trigger: continue-session
    workflow: '...shared/continue-session/workflow.md'
    section: 'Initial Analysis'

  # Section: Capture & Amend
  - trigger: add-pain-point
    workflow: '...shared/capture-item/workflow.md'
    item_type: 'pain_point'
    section: 'Capture & Amend'

  - trigger: add-exception
    workflow: '...shared/capture-item/workflow.md'
    item_type: 'exception'
    section: 'Capture & Amend'

  - trigger: add-control-point
    workflow: '...shared/capture-item/workflow.md'
    item_type: 'control_point'
    section: 'Capture & Amend'

  # Section: Document Management
  - trigger: compose-document
    workflow: '...shared/compose-document/workflow.md'
    doc_type: 'process-asis'
    section: 'Document Management'

  - trigger: qa-check
    workflow: '...shared/qa-check/workflow.md'
    validation_type: 'process-integrity'
    section: 'Document Management'

  # Section: Outputs
  - trigger: export-yaml
    workflow: '...shared/export-to-yaml/workflow.md'
    schema: 'process-asis-schema'
    section: 'Outputs'

  - trigger: executive-summary
    workflow: '...shared/executive-summary/workflow.md'
    section: 'Outputs'
```

#### Client Journey Analyst (CJA)

```yaml
menu:
  # Section: Flow 1 - AS-IS Analysis
  - trigger: run-cx-analysis
    workflow: '...cx-asis-analysis/workflow.md'
    section: 'Flow 1: AS-IS Journey'

  - trigger: continue-session
    workflow: '...shared/continue-session/workflow.md'
    section: 'Flow 1: AS-IS Journey'

  # Section: Flow 2 - Target Validation (existing)
  - trigger: run-cx-validation
    workflow: '...cx-target-validation/workflow.md'
    section: 'Flow 2: Target Validation'

  # Section: Capture & Amend
  - trigger: add-enhancement
    workflow: '...shared/capture-item/workflow.md'
    item_type: 'enhancement_idea'
    section: 'Capture & Amend'

  - trigger: edit-enhancement
    workflow: '...shared/capture-item/workflow.md'
    item_type: 'enhancement_idea'
    mode: 'edit'
    section: 'Capture & Amend'

  # Section: Document Management
  - trigger: compose-document
    workflow: '...shared/compose-document/workflow.md'
    doc_type: 'cx-journey'
    section: 'Document Management'

  - trigger: qa-check
    workflow: '...shared/qa-check/workflow.md'
    validation_type: 'cx-alignment'
    section: 'Document Management'

  # Section: Outputs
  - trigger: export-yaml
    workflow: '...shared/export-to-yaml/workflow.md'
    schema: 'cx-journey-schema'
    section: 'Outputs'

  - trigger: executive-summary
    workflow: '...shared/executive-summary/workflow.md'
    section: 'Outputs'
```

#### Control Analyst (CA)

```yaml
menu:
  # Section: Flow 1 - AS-IS Analysis
  - trigger: run-control-analysis
    workflow: '...control-analysis/workflow.md'  # Combines regulatory-framework-mapping + control-point-inventory
    section: 'Flow 1: AS-IS Controls'

  - trigger: continue-session
    workflow: '...shared/continue-session/workflow.md'
    section: 'Flow 1: AS-IS Controls'

  # Section: Flow 2 - Target Validation (existing)
  - trigger: validate-target-controls
    workflow: '...validate-target-controls/workflow.md'
    section: 'Flow 2: Target Validation'

  # Section: Capture & Amend
  - trigger: add-control-point
    workflow: '...shared/capture-item/workflow.md'
    item_type: 'control_point'
    section: 'Capture & Amend'

  - trigger: add-regulation
    workflow: '...shared/capture-item/workflow.md'
    item_type: 'regulation'
    section: 'Capture & Amend'

  - trigger: edit-control
    workflow: '...shared/capture-item/workflow.md'
    item_type: 'control_point'
    mode: 'edit'
    section: 'Capture & Amend'

  # Section: Document Management
  - trigger: compose-document
    workflow: '...shared/compose-document/workflow.md'
    doc_type: 'compliance-assessment'
    section: 'Document Management'

  - trigger: qa-check
    workflow: '...shared/qa-check/workflow.md'
    validation_type: 'compliance-coverage'
    section: 'Document Management'

  # Section: Outputs
  - trigger: export-yaml
    workflow: '...shared/export-to-yaml/workflow.md'
    schema: 'compliance-schema'
    section: 'Outputs'

  - trigger: executive-summary
    workflow: '...shared/executive-summary/workflow.md'
    section: 'Outputs'
```

#### Innovation Analyst (IA)

```yaml
menu:
  # Section: Flow 1 - Innovation Research
  - trigger: run-innovation-analysis
    workflow: '...innovation-analysis/workflow.md'  # Replaces action="#prompt" pattern
    section: 'Flow 1: Innovation Research'

  - trigger: continue-session
    workflow: '...shared/continue-session/workflow.md'
    section: 'Flow 1: Innovation Research'

  # Section: Flow 2 - Target Validation (existing)
  - trigger: compare-innovation-vs-target
    workflow: '...innovation-target-validation/workflow.md'
    section: 'Flow 2: Target Validation'

  # Section: Capture & Amend
  - trigger: add-innovation-idea
    workflow: '...shared/capture-item/workflow.md'
    item_type: 'innovation_idea'
    section: 'Capture & Amend'

  - trigger: add-market-trend
    workflow: '...shared/capture-item/workflow.md'
    item_type: 'market_trend'
    section: 'Capture & Amend'

  - trigger: edit-idea
    workflow: '...shared/capture-item/workflow.md'
    item_type: 'innovation_idea'
    mode: 'edit'
    section: 'Capture & Amend'

  # Section: Document Management
  - trigger: compose-document
    workflow: '...shared/compose-document/workflow.md'
    doc_type: 'innovation-analysis'
    section: 'Document Management'

  - trigger: qa-check
    workflow: '...shared/qa-check/workflow.md'
    validation_type: 'innovation-viability'
    section: 'Document Management'

  # Section: Outputs
  - trigger: export-yaml
    workflow: '...shared/export-to-yaml/workflow.md'
    schema: 'innovation-schema'
    section: 'Outputs'

  - trigger: executive-summary
    workflow: '...shared/executive-summary/workflow.md'
    section: 'Outputs'
```

---

## 5. New Shared Workflows to Create

### 5.1 qa-check/workflow.md (NEW)

**Purpose:** Validates document integrity by checking cross-references, completeness, and alignment between sections.

**Input Parameters:**
- `validation_type`: Type of validation to perform
- `document_path`: Path to document being validated
- `process_id`: Current process identifier

**Validation Rules by Type:**

| Type | Checks |
|------|--------|
| `process-integrity` | All PS# referenced, all CP# linked to PS#, all PP# have severity |
| `cx-alignment` | All touchpoints map to PS#, CES scores complete, EI# linked to pain points |
| `compliance-coverage` | All regulations mapped, all CP# have effectiveness rating, evidence documented |
| `innovation-viability` | All II# have feasibility score, priorities use MoSCoW, ROI estimates present |

**Output:**
- QA Report with PASS/WARN/FAIL status
- List of issues found
- Recommendations for remediation

### 5.2 export-to-yaml/workflow.md (NEW)

**Purpose:** Converts markdown documents into structured YAML files optimized for AI agent consumption.

**Input Parameters:**
- `schema`: Schema definition to use
- `document_path`: Source document
- `output_path`: Destination YAML file

**Schema Definitions Required:**

```yaml
# process-asis-schema.yaml
process:
  id: string
  name: string
  bank: string
  steps:
    - id: string (PS#)
      name: string
      description: string
      controls: [CP#]
      pain_points: [PP#]
  pain_points:
    - id: string (PP#)
      description: string
      severity: high|medium|low
      step_ref: PS#
  controls:
    - id: string (CP#)
      description: string
      type: preventive|detective|corrective
      regulation_ref: [RG#]
```

```yaml
# cx-journey-schema.yaml
journey:
  process_id: string
  touchpoints:
    - id: string
      channel: string
      step_ref: PS#
      ces_score: number
      pain_points: [PP#]
  enhancements:
    - id: string (EI#)
      description: string
      benefit: string
      effort: low|medium|high
      touchpoint_ref: string
```

```yaml
# compliance-schema.yaml
compliance:
  process_id: string
  regulations:
    - id: string (RG#)
      name: string
      requirement: string
      controls: [CP#]
  controls:
    - id: string (CP#)
      description: string
      effectiveness: effective|partially_effective|ineffective
      evidence: string
      regulation_refs: [RG#]
  gaps:
    - id: string
      regulation_ref: RG#
      description: string
      risk_level: critical|high|medium|low
```

```yaml
# innovation-schema.yaml
innovation:
  process_id: string
  market_trends:
    - id: string (TR#)
      name: string
      relevance: high|medium|low
      source: string
  ideas:
    - id: string (II#)
      name: string
      description: string
      feasibility:
        technical: number
        regulatory: number
        financial: number
        complexity: number
        adoption: number
        competitive: number
        weighted_score: number
      priority: must|should|could|defer
      trend_refs: [TR#]
```

### 5.3 compose-document/workflow.md (NEW)

**Purpose:** Creates or updates the main deliverable document from captured items and analysis data.

**Input Parameters:**
- `doc_type`: Type of document to compose
- `template`: Template to use
- `process_id`: Current process identifier

**Workflow Steps:**
1. Load existing document or create from template
2. Aggregate all captured items (PP#, CP#, EI#, etc.)
3. Generate/update each section
4. Apply formatting standards
5. Update change log
6. Save document

### 5.4 executive-summary/workflow.md (ENHANCED)

**Purpose:** Generates stakeholder-ready executive summary from detailed analysis.

**Input Parameters:**
- `summary_type`: Type of summary (process|cx|compliance|innovation)
- `process_id`: Current process identifier
- `audience`: Target audience (executive|technical|compliance)

**Output Sections:**
- Key Findings (3-5 bullet points)
- Metrics Dashboard
- Critical Issues
- Recommendations
- Next Steps

---

## 6. Item Type Definitions

### 6.1 Unified Item Type Registry

| ID Prefix | Item Type | Agent Owner | Required Fields |
|-----------|-----------|-------------|-----------------|
| PS# | Process Step | PDA | id, name, description, sequence, actor, system |
| PP# | Pain Point | PDA | id, description, severity, step_ref, impact |
| EX# | Exception | PDA | id, description, frequency, handling, step_ref |
| CP# | Control Point | PDA, CA | id, description, type, step_ref, regulation_ref |
| RG# | Regulation | CA | id, name, requirement, jurisdiction |
| EI# | Enhancement Idea | CJA | id, description, benefit, effort, touchpoint_ref |
| II# | Innovation Idea | IA | id, name, description, feasibility_score, priority |
| TR# | Market Trend | IA | id, name, relevance, source, date_identified |
| SYS# | System | PDA | id, name, type, integration_points |

### 6.2 Cross-Reference Matrix

```
           PS#   PP#   EX#   CP#   RG#   EI#   II#   TR#   SYS#
PS#        -     ←     ←     ←     -     -     -     -     ←
PP#        →     -     -     -     -     ←     ←     -     -
EX#        →     -     -     -     -     -     -     -     -
CP#        →     -     -     -     ←     -     -     -     -
RG#        -     -     -     →     -     -     -     -     -
EI#        -     →     -     -     -     -     -     -     -
II#        -     →     -     -     -     -     -     ←     -
TR#        -     -     -     -     -     -     →     -     -
SYS#       →     -     -     -     -     -     -     -     -

Legend: → references, ← referenced by
```

---

## 7. Implementation Roadmap

### Phase 1: Structural Alignment

1. Add `section` attribute to all menu items across all agents
2. Remove `action="#prompt"` pattern from Innovation Analyst
3. Standardize workflow file extensions to `.md`
4. Add `continue-session` workflow to CA and IA

### Phase 2: Shared Workflow Creation

1. Create `shared/` workflow directory
2. Implement `capture-item/workflow.md` with full parameterization
3. Implement `qa-check/workflow.md`
4. Implement `export-to-yaml/workflow.md`
5. Implement `compose-document/workflow.md`
6. Enhance `executive-summary/workflow.md`

### Phase 3: Agent Menu Updates

1. Update PDA menu with new sections and workflows
2. Update CJA menu with new shared workflows
3. Update CA menu with capture-item and new workflows
4. Update IA menu to use workflows instead of prompts

### Phase 4: Schema & Template Creation

1. Create YAML schemas for each document type
2. Create/update document templates
3. Create QA validation rule definitions
4. Create executive summary templates per audience

### Phase 5: Testing & Validation

1. Test each workflow independently
2. Test cross-agent workflow consistency
3. Validate YAML export against schemas
4. User acceptance testing

---

## 8. File Structure After Alignment

```
.bmad/custom/modules/process-miner/
├── agents/
│   ├── process-documentation-analyst.agent.yaml
│   ├── client-journey-analyst.agent.yaml
│   ├── control-analyst.agent.yaml
│   └── innovation-analyst.agent.yaml
├── workflows/
│   ├── shared/                              # NEW: Shared workflows
│   │   ├── capture-item/workflow.md
│   │   ├── continue-session/workflow.md
│   │   ├── compose-document/workflow.md
│   │   ├── qa-check/workflow.md
│   │   ├── export-to-yaml/workflow.md
│   │   └── executive-summary/workflow.md
│   ├── elicit-process-knowledge/            # PDA-specific
│   ├── cx-asis-analysis/                    # CJA-specific
│   ├── cx-target-validation/                # CJA-specific
│   ├── control-analysis/                    # CA-specific (consolidate existing)
│   ├── validate-target-controls/            # CA-specific
│   ├── innovation-analysis/                 # IA-specific
│   └── innovation-target-validation/        # IA-specific
├── schemas/                                  # NEW: YAML schemas
│   ├── process-asis-schema.yaml
│   ├── cx-journey-schema.yaml
│   ├── compliance-schema.yaml
│   └── innovation-schema.yaml
├── templates/
│   ├── process-asis-template.md
│   ├── cx-journey-template.md
│   ├── compliance-assessment-template.md
│   ├── innovation-analysis-template.md
│   └── executive-summary/
│       ├── executive-template.md
│       ├── technical-template.md
│       └── compliance-template.md
├── validation-rules/                         # NEW: QA check rules
│   ├── process-integrity-rules.yaml
│   ├── cx-alignment-rules.yaml
│   ├── compliance-coverage-rules.yaml
│   └── innovation-viability-rules.yaml
└── tasks/
    └── module-activation.xml
```

---

## 9. Summary of Changes by Agent

### Process Documentation Analyst (PDA)

| Change | Type | Description |
|--------|------|-------------|
| Add section grouping | Enhancement | Group menu items into sections |
| Add qa-check | New capability | Document integrity validation |
| Add export-yaml | New capability | Structured YAML output |
| Add executive-summary | New capability | Stakeholder summary |
| Refactor compose-document | Enhancement | Use shared workflow |

### Client Journey Analyst (CJA)

| Change | Type | Description |
|--------|------|-------------|
| Standardize workflow paths | Cleanup | Use shared workflows |
| Add qa-check | New capability | CX alignment validation |
| Add export-yaml | New capability | Structured YAML output |
| Refactor capture-item | Enhancement | Use shared workflow with params |

### Control Analyst (CA)

| Change | Type | Description |
|--------|------|-------------|
| Add capture-item workflows | New capability | Add/edit controls and regulations |
| Add continue-session | New capability | Resume analysis sessions |
| Add qa-check | New capability | Compliance coverage validation |
| Add export-yaml | New capability | Structured YAML output |
| Consolidate initial analysis | Enhancement | Single workflow for regulatory mapping + inventory |

### Innovation Analyst (IA)

| Change | Type | Description |
|--------|------|-------------|
| Remove action="#prompt" pattern | Refactor | Convert to workflow references |
| Add section grouping | Enhancement | Group menu items into sections |
| Add capture-item workflows | New capability | Add/edit ideas and trends |
| Add continue-session | New capability | Resume analysis sessions |
| Add qa-check | New capability | Innovation viability validation |
| Add export-yaml | New capability | Structured YAML output |

---

## 10. Benefits of Alignment

1. **Consistency**: Users learn one pattern, apply across all agents
2. **Maintainability**: Shared workflows reduce duplication
3. **Extensibility**: New agents can adopt standard capability model
4. **AI Integration**: Structured YAML enables downstream automation
5. **Quality Assurance**: Built-in validation across all deliverables
6. **Traceability**: Cross-references enable impact analysis

---

*Document generated by BMad Builder for ProcessMiner*
*Version: 1.0.0*
*Date: 2025-12-06*
