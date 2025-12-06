---
name: 'workflow-edit-regulatory-framework-mapping'
description: 'Edit session for regulatory-framework-mapping workflow'
target_workflow: '/Users/markusholzhaeuser/ProcessMiner2/.bmad/custom/modules/process-miner/workflows/regulatory-framework-mapping'
target_format: 'New BMAD Standalone Format'
stepsCompleted: [1, 2, 3]
status: 'completed'
date: '2025-12-04'
---

# Workflow Edit: Regulatory Framework Mapping

## User Goal

Convert the legacy XML format workflow to the new BMAD standalone format.

---

## Workflow Analysis

### Target Workflow

- **Path**: /Users/markusholzhaeuser/ProcessMiner2/.bmad/custom/modules/process-miner/workflows/regulatory-framework-mapping
- **Name**: regulatory-framework-mapping
- **Module**: process-miner
- **Format**: Legacy (workflow.yaml + instructions.md)

### Structure Analysis

- **Type**: Document workflow (produces Compliance Control Assessment)
- **Total Steps**: 6 (Step 0-5)
- **Step Flow**: Sequential with conditional step (Step 3 - Regional Requirements)
- **Files**: 2 files (workflow.yaml: 604 lines, instructions.md: 1037 lines)

### Content Characteristics

- **Purpose**: Map regulatory framework to banking processes, producing sections 1.1-1.3 of Compliance Control Assessment
- **Instruction Style**: XML-style prescriptive tags (<step>, <phase>, <check>, <action>, etc.)
- **User Interaction**: One-at-a-time elicitation pattern for regulations, regions, standards
- **Complexity**: High - multi-phase pattern (Analyze → Research → Elicit) per step

### Initial Assessment

#### Strengths

- Well-structured phase pattern (Phase A: Analyze, Phase B: Research, Phase C: Elicit)
- Comprehensive confidence scoring system for regulations
- Rich output format with detailed regulation breakdowns
- Good use of shared tasks (workflow-prerequisites, collect-input-documents, external-research, advanced-elicitation)
- Conditional step handling for regional requirements
- Incremental document saving
- Control gap output on workflow completion

#### Potential Issues

- Large monolithic files (workflow.yaml + instructions.md both 600+ lines)
- XML-style syntax embedded in markdown
- All steps embedded in single instructions.md file
- Complex nested structures difficult to maintain
- Legacy format not compatible with step-file architecture

#### Format-Specific Notes

- Requires conversion from workflow.yaml config to workflow.md frontmatter
- instructions.md must be split into 6 separate step files
- XML tags (<step>, <phase>, <check>, <action>, <wait>, <ask>) need conversion to intent-based markdown
- invoke-task references need restructuring for new format
- Template-output sections need mapping to step output patterns

### Best Practices Compliance

- **Step File Structure**: Non-compliant (no step files, all embedded)
- **Frontmatter Usage**: Partial (workflow.yaml has config, but not in new format)
- **Menu Implementation**: Present but uses XML-style patterns
- **Variable Consistency**: Good (consistent use of session variables and path references)

---

_Analysis completed on 2025-12-04_

---

## Improvement Goals

### Motivation

- **Trigger**: Convert legacy format to new BMAD standalone format
- **User Feedback**: N/A - format migration requested
- **Success Issues**: Current format not compatible with step-file architecture

### User Experience Issues

- Monolithic files are difficult to navigate and maintain
- XML-style syntax mixed with markdown creates cognitive overhead

### Performance Gaps

- N/A - functional parity is the goal

### Growth Opportunities

- Better maintainability with separate step files
- Clearer structure following BMAD best practices
- Improved developer experience when editing workflow

### Instruction Style Considerations

- **Current Style**: XML-style prescriptive tags
- **Desired Changes**: Convert to intent-based markdown sections
- **Style Fit Assessment**: New format better suits collaborative editing

### Prioritized Improvements

#### Critical (Must Fix)

1. Convert workflow.yaml to workflow.md with proper frontmatter
2. Split instructions.md into 6 separate step files (step-00 through step-05)
3. Convert XML tags to intent-based markdown sections

#### Important (Should Fix)

1. Ensure all path references work in new structure
2. Maintain shared task references (invoke-task patterns)
3. Preserve menu handling patterns (A/P/C options)

#### Nice-to-Have (Could Fix)

1. Improve instruction clarity during conversion
2. Add templates/ directory if needed
3. Create data/ directory for any static data

### Focus Areas for Next Step

- Create new directory structure with steps/ folder
- Convert workflow.yaml config to workflow.md frontmatter
- Split instructions.md into individual step files
- Convert XML-style syntax to intent-based markdown

---

_Goals identified on 2025-12-04_

---

## Conversion Log

### Files Created

| File | Size | Description |
|------|------|-------------|
| `workflow.md` | 3,033 bytes | Main workflow entry point with BMAD architecture |
| `steps/step-00-prerequisites.md` | 7,135 bytes | Process selection and AS-IS validation |
| `steps/step-01-input-collection.md` | 8,111 bytes | Supplementary documentation collection |
| `steps/step-02-identify-regulations.md` | 14,030 bytes | Analyze-Research-Elicit for regulations |
| `steps/step-03-regional-requirements.md` | 10,972 bytes | Conditional regional requirements mapping |
| `steps/step-04-document-standards.md` | 12,202 bytes | Industry standards documentation |
| `steps/step-05-completion.md` | 11,777 bytes | Workflow completion and gap saving |

### Files Removed

| File | Description |
|------|-------------|
| `workflow.yaml` | Legacy configuration file (604 lines) |
| `instructions.md` | Legacy instructions file (1,037 lines) |

### Conversion Summary

| Metric | Before | After |
|--------|--------|-------|
| Total files | 2 | 7 |
| Total lines | ~1,641 | ~1,800 (distributed) |
| Format | Legacy XML-style | BMAD Standalone |
| Step isolation | None (monolithic) | Complete (6 step files) |
| Maintainability | Low | High |

### Key Conversions Applied

1. **workflow.yaml → workflow.md**
   - Config moved to frontmatter
   - Added BMAD architecture section
   - Added initialization sequence

2. **XML Tags → Intent-Based Markdown**
   - `<step>` → `# Step N: Title` sections
   - `<phase>` → `### Phase A/B/C:` sections
   - `<check>` → Conditional markdown blocks
   - `<action>` → Instruction paragraphs
   - `<wait>` → "**Wait for user input.**"
   - `<ask>` → Display blocks with options

3. **Menu Handling**
   - Standardized A/P/C pattern across all steps
   - Added menu handling logic section
   - Added execution rules section

4. **Frontmatter Variables**
   - All path definitions in step frontmatter
   - Task references standardized
   - Session variable documentation

---

_Conversion completed on 2025-12-04_
