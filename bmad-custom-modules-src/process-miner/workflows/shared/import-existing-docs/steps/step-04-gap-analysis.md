---
name: 'step-04-gap-analysis'
description: 'Identify gaps between extracted data and complete documentation requirements'

# Path Definitions
workflow_path: '{module_root}/workflows/shared/import-existing-docs'
module_path: '{module_root}'
config_source: '{module_root}/config.yaml'

# File References
thisStepFile: '{workflow_path}/steps/step-04-gap-analysis.md'
nextStepFile: '{workflow_path}/steps/step-05-output.md'
previousStepFile: '{workflow_path}/steps/step-03-consolidate.md'
workflowFile: '{workflow_path}/workflow.md'

# Output Configuration
gap_analysis_file: '{current_process_folder}/gap-analysis.md'

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
partyModeWorkflow: '{project-root}/.bmad/core/workflows/party-mode/workflow.md'
---

# Step 4: Gap Analysis

## STEP GOAL:

To compare extracted data against complete documentation requirements and identify what's present, partial, or missing.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 **NEVER** generate content without user input
- 📖 **CRITICAL**: Read the complete step file before taking any action
- 🔄 **CRITICAL**: When loading next step with 'C', ensure entire file is read
- 📋 **YOU ARE A FACILITATOR**, not a content generator

### Role Reinforcement:

- ✅ You are a documentation analyst performing gap analysis
- ✅ Compare what was extracted vs what's needed for complete documentation
- ✅ Be thorough but fair - don't create false gaps
- ✅ Identify what needs SME clarification

### Step-Specific Rules:

- 🎯 Focus ONLY on gap identification
- 🚫 **FORBIDDEN** to generate structured output in this step (that's step 5)
- 💬 Be specific about what's missing
- 📋 Categorize gaps by severity/importance

## EXECUTION PROTOCOLS:

- 🎯 Compare against documentation requirements
- 💾 Identify present, partial, and missing elements
- 📖 Generate gap analysis report
- 💾 Save to gap_analysis_file
- 🚫 **FORBIDDEN** to load next step until gap analysis is complete

## CONTEXT BOUNDARIES:

- Consolidated data from step 3 is available
- Use documentation requirements checklist below
- Don't generate JSON output yet
- Gap analysis is for planning SME follow-up questions

---

## GAP ANALYSIS SEQUENCE:

### 1. Documentation Requirements Checklist

Compare extracted data against these requirements for complete process documentation:

#### Process Metadata
- [ ] Process name
- [ ] Business unit/owner
- [ ] Process purpose
- [ ] Trigger/initiator
- [ ] Frequency/volume

#### Process Steps (minimum 5 steps recommended)
- [ ] Sequential step descriptions
- [ ] Step owners/performers
- [ ] Step rationale (why needed)
- [ ] Step inputs/outputs

#### Pain Points
- [ ] Identified challenges
- [ ] Impact assessment
- [ ] Frequency of occurrence
- [ ] Link to affected steps

#### Controls & Compliance
- [ ] Control descriptions
- [ ] Regulatory requirements traced
- [ ] Control owners
- [ ] Link to process steps

#### Systems & Tools
- [ ] System names
- [ ] System purposes
- [ ] Integration details
- [ ] Link to process steps

#### Cross-References
- [ ] Process steps to controls mapping
- [ ] Process steps to systems mapping
- [ ] Pain points to process steps mapping

### 2. Categorize Findings

Group extracted data into:

**Well Documented (Complete):**
- Elements with high confidence scores
- Complete information available
- Source references clear

**Partially Documented:**
- Elements with medium confidence scores
- Some information missing
- May need SME clarification

**Missing or Unclear:**
- Elements not found in documentation
- Very low confidence extractions
- Critical gaps for complete documentation

**Needs SME Clarification:**
- Conflicting information between sources
- Ambiguous statements
- Implicit assumptions that need verification

### 3. Calculate Completeness Score

**Formula:** (elements_found / elements_required) x 100

**Guidelines:**
- >70% completeness: Good foundation, targeted SME follow-up
- 50-70% completeness: Moderate foundation, significant SME input needed
- <50% completeness: May be better to start fresh with start-new-process

### 4. Generate Gap Analysis Report

Create and save to `{gap_analysis_file}`:

```markdown
# Gap Analysis Report

**Process:** {process_name}
**Date:** {date}
**Analyst:** {user_name}
**Completeness Score:** {score}%

## Well Documented
{list_well_documented_areas}

## Partially Documented
{list_partial_areas}

## Missing or Unclear
{list_missing_areas}

## Needs SME Clarification
{list_clarification_items}

## Conflicts to Resolve
{list_conflicts}

## Recommended Next Steps
{recommendations_based_on_score}
```

### 5. Save and Continue

After generating the gap analysis report:
- Save report to `{gap_analysis_file}`
- Proceed silently to next step (no output, no menu)

---

## CRITICAL STEP COMPLETION NOTE

Once gap analysis report has been generated and saved to `{gap_analysis_file}`, immediately load and execute `{nextStepFile}` (silent auto-continue).

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- All consolidated data compared against requirements
- Gaps categorized correctly (complete/partial/missing/unclear)
- Completeness score calculated
- Gap analysis report saved to file
- Silent auto-continue to next step

### ❌ FAILURE:

- Not comparing against full requirements list
- Creating false gaps or missing real gaps
- Not calculating completeness score
- Not saving gap analysis report
- Generating structured JSON output in this step (premature)
- Displaying verbose output or prompting user unnecessarily

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
