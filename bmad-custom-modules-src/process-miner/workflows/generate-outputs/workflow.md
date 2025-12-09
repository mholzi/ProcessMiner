---
name: Generate Management Summary
description: Creates or updates Amazon 6-Pager format management summaries from process documentation, with intelligent change detection for existing summaries.
web_bundle: false
---

# Generate Management Summary Workflow

**Goal:** Generate or update a management-level summary document following the Amazon 6-Pager format, tailored to the calling agent's domain, with intelligent detection of material changes when updating existing summaries.

**Your Role:** In addition to your name, communication_style, and persona, you are also a document synthesizer and executive communication specialist collaborating with a process owner. This is a partnership, not a client-vendor relationship. You bring expertise in executive communication, data synthesis, and the Amazon 6-Pager format, while the user brings their domain knowledge and understanding of what stakeholders need to know. Work together as equals to create decision-ready documentation.

---

## WORKFLOW ARCHITECTURE

This uses **step-file architecture** for disciplined execution:

### Core Principles

- **Micro-file Design**: Each step is a self contained instruction file that is a part of an overall workflow that must be followed exactly
- **Just-In-Time Loading**: Only the current step file is in memory - never load future step files until told to do so
- **Sequential Enforcement**: Sequence within the step files must be completed in order, no skipping or optimization allowed
- **State Tracking**: Document progress in output file frontmatter using `stepsCompleted` array when a workflow produces a document
- **Append-Only Building**: Build documents by appending content as directed to the output file

### Step Processing Rules

1. **READ COMPLETELY**: Always read the entire step file before taking any action
2. **FOLLOW SEQUENCE**: Execute all numbered sections in order, never deviate
3. **WAIT FOR INPUT**: If a menu is presented, halt and wait for user selection
4. **CHECK CONTINUATION**: If the step has a menu with Continue as an option, only proceed to next step when user selects 'C' (Continue)
5. **SAVE STATE**: Update `stepsCompleted` in frontmatter before loading next step
6. **LOAD NEXT**: When directed, load, read entire file, then execute the next step file

### Critical Rules (NO EXCEPTIONS)

- 🛑 **NEVER** load multiple step files simultaneously
- 📖 **ALWAYS** read entire step file before execution
- 🚫 **NEVER** skip steps or optimize the sequence
- 💾 **ALWAYS** update frontmatter of output files when writing the final output for a specific step
- 🎯 **ALWAYS** follow the exact instructions in the step file
- ⏸️ **ALWAYS** halt at menus and wait for user input
- 📋 **NEVER** create mental todo lists from future steps

---

## AMAZON 6-PAGER FORMAT

This workflow generates management summaries following the Amazon 6-Pager structure:

| Section | Pages | Purpose |
|---------|-------|---------|
| **1. Introduction** | ½–1 | Background, context, purpose |
| **2. Goals** | ½ | SMART metrics with baselines and targets |
| **3. Tenets** | ½ | Guiding principles, non-negotiables |
| **4. State of the Business** | 1 | Current situation snapshot |
| **5. Lessons Learned** | ½–1 | What worked, what didn't - brutal honesty |
| **6. Strategic Priorities** | 2–3 | Core section - execution plan |
| **Appendix** | Unlimited | Supporting data, charts, tables |

**Key Principles:**
- Lead with the "why" - make the problem or opportunity obvious
- Anchor in data, not opinions - every claim backed by evidence
- Structure for flow - problem → context → solution → impact
- Close with clear next steps - ownership and deliverables
- Brutal honesty in lessons learned - no sugar-coating

---

## TEMPLATE CONFIGURATION

This workflow supports two methods for template selection:

### Method 1: Explicit Data Parameters (Preferred)

When invoked with explicit `data` block from menu item:

```yaml
- trigger: generate-summary-compliance
  workflow: '{module_root}/workflows/generate-outputs/workflow.md'
  data:
    primary_document: 'as-is-process-documentation.md'
    template: 'management-summary-compliance'
  description: 'Create Compliance Management Summary'
  section: 'Outputs'
```

| Data Parameter | Description |
|----------------|-------------|
| `data.template` | Template name (e.g., 'management-summary-compliance') |
| `data.primary_document` | Source document filename (overrides template default) |

### Method 2: Agent Detection (Fallback)

When no `data` block is provided, the workflow detects the calling agent and uses the appropriate template:

| Agent ID | Domain | Source Document | Output Template |
|----------|--------|-----------------|-----------------|
| `process-documentation-analyst` | Process AS-IS | as-is-process-documentation.md | management-summary-process.md |
| `client-journey-analyst` | Client Experience | cx-journey-documentation.md | management-summary-cx.md |
| `control-analyst` | Compliance & Controls | compliance-control-assessment.md | management-summary-compliance.md |
| `innovation-analyst` | Innovation Analysis | innovation-analysis-template.md | management-summary-innovation.md |

### Available Templates

| Template Name | Output File | Default Source |
|---------------|-------------|----------------|
| `management-summary-process` | management-summary-process.md | as-is-process-documentation.md |
| `management-summary-cx` | management-summary-cx.md | cx-journey-documentation.md |
| `management-summary-compliance` | management-summary-compliance.md | compliance-control-assessment.md |
| `management-summary-innovation` | management-summary-innovation.md | innovation-analysis-template.md |

---

## INITIALIZATION SEQUENCE

### 1. Module Configuration Loading

Load and read full config from {module_root}/config.yaml and resolve:

- `project_name`, `output_folder`, `user_name`, `communication_language`, `document_output_language`

### 2. First Step EXECUTION

Load, read the full file and then execute `{workflow_path}/steps/step-01-init.md` to begin the workflow.
