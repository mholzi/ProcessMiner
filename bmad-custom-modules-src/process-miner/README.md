# ProcessMiner Module

Banking process documentation and SME knowledge extraction module with multi-agent workflow coordination.

## Table of Contents

- [Module Structure](#module-structure)
- [Agents](#agents)
- [Workflows](#workflows)
- [Quick Start](#quick-start)
- [Integration](#integration)

## Module Structure

```
process-miner/
├── agents/                           # Agent definitions
│   ├── process-documentation-analyst.agent.yaml
│   ├── client-journey-analyst.agent.yaml
│   ├── control-analyst.agent.yaml
│   └── innovation-analyst.agent.yaml
├── workflows/                        # Active workflows
│   ├── start-new-process/            # Core knowledge extraction (9-step)
│   ├── discontinue-process/          # Process archival
│   ├── generate-outputs/             # Output generation
│   └── shared/                       # Reusable workflow components
│       ├── continue-session/
│       ├── capture-item/
│       ├── import-existing-docs/     # Import & analyze documentation
│       ├── compose-document/
│       ├── review-draft/             # Document review and finalization
│       ├── qa-check/
│       ├── export-to-yaml/
│       └── executive-summary/
├── docs/                             # Module documentation
├── reference/                        # Examples and patterns
├── module.yaml                       # Module configuration
└── README.md                         # This file
```

## Agents

### 📋 Process Documentation Analyst

**Foundation agent** for the ProcessMiner workflow - the ONLY agent that can create new processes.

- **Role:** Process Documentation Analyst & SME Knowledge Facilitator
- **Purpose:** Extract tacit knowledge from SMEs through progressive elicitation
- **Output:** Multi-altitude documentation (executive summaries + detailed specs)
- **Location:** `agents/process-documentation-analyst.agent.yaml`

**Key Capabilities:**
- Progressive elicitation (start broad, drill down as needed)
- AI drafts, SME validates (minimize SME burden)
- Structured referencing system (PS#, EX#, PP#, CP#, SYS#)
- Banking compliance non-negotiable
- Import before interview (respect existing work)

### 🎯 Client Journey Analyst

**Dual-invocation agent** for customer experience mapping across AS-IS and TO-BE states.

- **Role:** Client Experience & Journey Mapping Specialist
- **Purpose:** Map client touchpoints, identify friction points, analyze experience quality
- **Pattern:** Post-PDA (AS-IS analysis) and Post-Transformation (target validation)
- **Location:** `agents/client-journey-analyst.agent.yaml`

### 🛡️ Control Analyst

**Compliance specialist** for regulatory requirements and control effectiveness validation.

- **Role:** Compliance & Control Specialist + Banking Regulatory Expert
- **Purpose:** Validate regulatory requirements, assess control effectiveness, map frameworks
- **Output:** Control point inventories, compliance assessments, regulatory mappings
- **Location:** `agents/control-analyst.agent.yaml`

### 💡 Innovation Analyst

**Market intelligence specialist** for innovation opportunities and competitive analysis.

- **Role:** Innovation & Market Intelligence Specialist
- **Purpose:** Identify fintech trends, analyze competitors, assess emerging technologies
- **Focus:** AI, blockchain, open banking, RPA opportunities
- **Location:** `agents/innovation-analyst.agent.yaml`

### Agent Workflow (7-Agent Pipeline)

1. ✅ **Process Documentation Analyst** - Foundation, creates processes
2. ⏳ **Transformation Agent** - Process improvement recommendations
3. ✅ **Client Journey Analyst** - Customer experience mapping
4. ✅ **Control Analyst** - Compliance and control validation
5. ✅ **Innovation Analyst** - Technology and automation opportunities
6. ⏳ **IT Architect** - Technical implementation design
7. ⏳ **QA Agent** - Quality assurance and validation

## Workflows

### Core Workflows

| Workflow | Purpose | Status |
|----------|---------|--------|
| `start-new-process` | Extract process knowledge from SMEs (9-step) | ✅ Active |
| `discontinue-process` | Archive discontinued processes | ⏳ Planned |
| `generate-outputs` | Create management summaries | ⏳ Planned |

### Shared Workflows

| Workflow | Purpose | Parameters |
|----------|---------|------------|
| `continue-session` | Resume existing work session | - |
| `capture-item` | Capture pain points, exceptions, controls | `item_type` |
| `import-existing-docs` | Import & analyze existing documentation | `import_mode` |
| `compose-document` | Generate AS-IS documents | `doc_type` |
| `review-draft` | Review and finalize documentation | `primary_document`, `template` |
| `qa-check` | Run validation checks | `validation_type` |
| `export-to-yaml` | Export structured data | `schema` |
| `executive-summary` | Generate summaries | `summary_type` |

## Quick Start

### Using Process Documentation Analyst

1. **Load the agent** in your IDE
2. **Start new process:** Select `start-new` to begin documentation
3. **Continue session:** Select `continue-session` to resume work
4. **Capture items:** Use `add-pain-point`, `add-exception`, `add-control-point`
5. **Generate outputs:** Use `compose-document`, `executive-summary`, `export-yaml`

### Menu Structure

```text
Initial Analysis
├── start-new           - Create new process
└── continue-session    - Resume existing session

Capture & Amend
├── add-pain-point      - Document pain points (PP#)
├── add-exception       - Document exceptions (EX#)
└── add-control-point   - Document controls (CP#)

Documentation Input
└── import-documentation - Import & analyze docs

Document Management
├── compose-document    - Create AS-IS document
├── review-draft        - Finalize documentation
├── qa-check            - Run validation
└── discontinue-process - Archive process

Outputs
├── export-yaml         - Export to YAML
├── executive-summary   - Generate summary
└── generate-outputs    - Management summary
```

## Structured Referencing System

All process elements use unique identifiers for traceability:

| Prefix | Element | Example |
|--------|---------|---------|
| PS# | Process Step | PS001, PS002 |
| EX# | Exception | EX001, EX002 |
| PP# | Pain Point | PP001, PP002 |
| CP# | Control Point | CP001, CP002 |
| SYS# | System | SYS001, SYS002 |

## Integration

ProcessMiner integrates with:

- **BMad Core** - Framework foundation and agent compilation
- **BMB** - Builder tools for extending the module
- **Downstream Agents** - Sequential workflow feeds 6 other agents

## Data Flow

```text
Process Documentation Analyst (Foundation) ✅
           │
           ▼
    ┌──────────────┐
    │ Process Data │
    │   (YAML)     │
    └──────────────┘
           │
     ┌─────┴─────┬─────────┬──────────┬────────────┬──────────┐
     ▼           ▼         ▼          ▼            ▼          ▼
Transformation  Client  Control  Innovation    IT       QA
   Agent ⏳    Journey✅ Analyst✅  Analyst✅  Architect⏳ Agent⏳
```

## Best Practices

1. **Import Before Interview** - Check existing docs before asking SMEs
2. **Progressive Elicitation** - Start broad, drill down only where needed
3. **AI Drafts, SME Validates** - Never ask SMEs to write from scratch
4. **Structured References** - Use IDs for all elements
5. **Multi-Altitude Output** - Generate both summaries and details
6. **Banking Compliance** - Every step needs rationale and traceability

---

ProcessMiner provides systematic banking process documentation with SME-friendly knowledge extraction and compliance-ready outputs.
