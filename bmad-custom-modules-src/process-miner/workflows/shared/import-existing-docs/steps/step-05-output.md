---
name: 'step-05-output'
description: 'Generate structured JSON output file with all extracted data'

# Path Definitions
workflow_path: '{module_root}/workflows/shared/import-existing-docs'
module_path: '{module_root}'
config_source: '{module_root}/config.yaml'

# File References
thisStepFile: '{workflow_path}/steps/step-05-output.md'
nextStepFile: '{workflow_path}/steps/step-06-validate.md'
previousStepFile: '{workflow_path}/steps/step-04-gap-analysis.md'
workflowFile: '{workflow_path}/workflow.md'

# Output Configuration
source_documents_folder: '{current_process_folder}/source-documentation'
output_file: '{current_process_folder}/imported-data.json'
structured_data_file: '{current_process_folder}/structured-data.json'
gap_analysis_file: '{current_process_folder}/gap-analysis.md'

# Import Mode (session variable from step-01)
import_mode: session-variable

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
partyModeWorkflow: '{project-root}/.bmad/core/workflows/party-mode/workflow.md'
---

# Step 5: Generate Structured Output

## STEP GOAL:

To format all extracted, consolidated, and gap-analyzed data into a structured JSON output file compatible with downstream workflows.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 **NEVER** generate content without user input
- 📖 **CRITICAL**: Read the complete step file before taking any action
- 🔄 **CRITICAL**: When loading next step with 'C', ensure entire file is read
- 📋 **YOU ARE A FACILITATOR**, not a content generator

### Role Reinforcement:

- ✅ You are a documentation analyst generating structured output
- ✅ Format must match schema for downstream workflow compatibility
- ✅ Include all metadata, confidence scores, and source references
- ✅ Preserve gap analysis information in output

### Step-Specific Rules:

- 🎯 Focus ONLY on JSON output generation
- 🚫 **FORBIDDEN** to perform SME validation in this step (that's step 6)
- 💬 Follow the exact JSON schema specified
- 📋 Include all elements even those with low confidence

## EXECUTION PROTOCOLS:

- 🎯 Format data according to JSON schema
- 💾 Include import metadata and source references
- 📖 Include gap and conflict information
- 💾 Save to output_file
- 🚫 **FORBIDDEN** to load next step until output is generated

## CONTEXT BOUNDARIES:

- Consolidated data from step 3 is available
- Gap analysis from step 4 is available
- Use exact JSON schema below
- Output must be compatible with start-new-process workflow

---

## OUTPUT GENERATION SEQUENCE:

### 1. JSON Schema Definition

Format extracted data into this standard schema:

```json
{
  "import_metadata": {
    "source_documents_folder": "{source_documents_folder}",
    "source_documents": [
      {
        "filename": "{doc_name}",
        "stored_path": "{source_documents_folder}/{doc_name}",
        "original_path": "{original_path}",
        "format": "{doc_format}",
        "processed_date": "{date}",
        "page_count": 0,
        "extraction_confidence": "high|medium|low"
      }
    ],
    "processed_by": "{user_name}",
    "import_date": "{date}",
    "extraction_method": "AI-assisted pattern recognition",
    "completeness_score": 0
  },
  "process_metadata": {
    "process_name": "{extracted_process_name}",
    "business_unit": "{extracted_business_unit}",
    "purpose": "{extracted_purpose}",
    "trigger": "{extracted_trigger}",
    "frequency": "{extracted_frequency}",
    "confidence": "high|medium|low"
  },
  "process_steps": [
    {
      "id": "PS-XX-001",
      "name": "{extracted_step_name}",
      "description": "{extracted_description}",
      "owner": "{extracted_owner}",
      "rationale": "{extracted_rationale}",
      "source_reference": "{document_name}, page {page_number}",
      "confidence": "high|medium|low",
      "systems_used": ["SYS-XX-001"],
      "controls_applied": ["CP-XX-001"],
      "needs_clarification": false
    }
  ],
  "pain_points": [
    {
      "id": "PP-XX-001",
      "description": "{extracted_pain}",
      "impact": "{extracted_impact}",
      "frequency": "{extracted_frequency}",
      "linked_steps": ["PS-XX-001"],
      "source_reference": "{document_name}, page {page_number}",
      "confidence": "high|medium|low"
    }
  ],
  "controls": [
    {
      "id": "CP-XX-001",
      "description": "{extracted_control}",
      "type": "{extracted_type}",
      "requirement": "{extracted_requirement}",
      "owner": "{extracted_owner}",
      "linked_steps": ["PS-XX-001"],
      "source_reference": "{document_name}, page {page_number}",
      "confidence": "high|medium|low"
    }
  ],
  "systems": [
    {
      "id": "SYS-XX-001",
      "name": "{extracted_system_name}",
      "purpose": "{extracted_purpose}",
      "integration": "{extracted_integration}",
      "linked_steps": ["PS-XX-001"],
      "source_reference": "{document_name}, page {page_number}",
      "confidence": "high|medium|low"
    }
  ],
  "gaps": {
    "missing_metadata": ["{gap_list}"],
    "incomplete_steps": ["{incomplete_step_ids}"],
    "missing_pain_points": "{gap_description}",
    "missing_controls": "{gap_description}",
    "missing_systems": "{gap_description}",
    "needs_sme_clarification": ["{clarification_items}"]
  },
  "conflicts": [
    {
      "type": "{conflict_type}",
      "description": "{conflict_description}",
      "sources": ["{doc1}, page X", "{doc2}, page Y"],
      "requires_resolution": true
    }
  ]
}
```

### 2. Populate JSON Structure

Fill in all fields from consolidated and gap-analyzed data:
- Replace placeholders with actual extracted values
- Use empty arrays [] for missing collections
- Use null for missing single values
- Include all items regardless of confidence level

### 3. Save Output File(s) Based on Import Mode

**For all modes:**
- Always save raw extracted data to `{output_file}` (imported-data.json)
- This preserves a record of what was extracted from source documents

**Mode-specific behavior:**

| import_mode | Primary Output | Action |
|-------------|----------------|--------|
| `fresh` | `{structured_data_file}` | Create new structured-data.json |
| `replace` | `{structured_data_file}` | Overwrite existing (backup already created in step-01) |
| `augment` | `{structured_data_file}` | Merge new items into existing structured-data.json |

**For augment mode merge:**
1. Load existing `{structured_data_file}`
2. Append new process_steps to existing array
3. Append new pain_points to existing array
4. Append new controls to existing array
5. Append new systems to existing array
6. Update metadata (add import_date, source_documents)
7. Preserve all existing SME-validated content
8. Write merged result to `{structured_data_file}`

### 4. Save and Continue

After generating the JSON output:
- Save raw extracted data to `{output_file}` (always)
- Save/merge to `{structured_data_file}` (based on mode)
- Display summary:
  ```
  **Import Complete**
  - Raw extracted data: {output_file}
  - Structured data: {structured_data_file} ({mode_description})
  - New items added: {counts_by_type}
  ```
- Proceed silently to next step

---

## CRITICAL STEP COMPLETION NOTE

Once JSON output file has been created and saved to `{output_file}`, immediately load and execute `{nextStepFile}` (silent auto-continue).

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Raw extracted data saved to imported-data.json
- Structured data saved/merged to structured-data.json (based on mode)
- All extracted elements included in output
- Schema matches specification exactly
- Confidence scores and source references included
- Gap information preserved in output
- **For augment mode:** Existing SME-validated data preserved
- **For augment mode:** New IDs continue from existing sequence
- Silent auto-continue to next step

### ❌ FAILURE:

- Not creating JSON file
- Missing required fields in schema
- Not including source references
- Not including gap/conflict information
- Starting SME validation in this step (premature)
- **For augment mode:** Overwriting existing data without merge
- **For augment mode:** Reassigning existing IDs
- Displaying verbose output or prompting user unnecessarily

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
