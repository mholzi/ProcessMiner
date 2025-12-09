---
name: 'step-03-consolidate'
description: 'Merge, deduplicate, and assign structured IDs to extracted data'

# Path Definitions
workflow_path: '{module_root}/workflows/shared/import-existing-docs'
module_path: '{module_root}'
config_source: '{module_root}/config.yaml'

# File References
thisStepFile: '{workflow_path}/steps/step-03-consolidate.md'
nextStepFile: '{workflow_path}/steps/step-04-gap-analysis.md'
previousStepFile: '{workflow_path}/steps/step-02-analyze.md'
workflowFile: '{workflow_path}/workflow.md'

# Configuration
structured_id_system: '{config_source}:structured_id_system'
existing_data_file: '{current_process_folder}/structured-data.json'

# Import Mode (session variable from step-01)
import_mode: session-variable

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
partyModeWorkflow: '{project-root}/.bmad/core/workflows/party-mode/workflow.md'
---

# Step 3: Data Consolidation & Deduplication

## STEP GOAL:

To merge extracted data from all documents, identify and consolidate duplicates, assign structured IDs, and build cross-reference mappings.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 **NEVER** generate content without user input
- 📖 **CRITICAL**: Read the complete step file before taking any action
- 🔄 **CRITICAL**: When loading next step with 'C', ensure entire file is read
- 📋 **YOU ARE A FACILITATOR**, not a content generator

### Role Reinforcement:

- ✅ You are a documentation analyst performing data consolidation
- ✅ Merge similar items while preserving all source references
- ✅ Flag conflicts for SME resolution - never auto-resolve
- ✅ Assign preliminary structured IDs following the ID system

### Step-Specific Rules:

- 🎯 Focus ONLY on consolidation, deduplication, and ID assignment
- 🚫 **FORBIDDEN** to perform gap analysis in this step (that's step 4)
- 💬 Preserve all source references when merging items
- 📋 Flag any conflicting information explicitly

## EXECUTION PROTOCOLS:

- 🎯 Merge extracted data from all documents
- 💾 Identify and consolidate duplicates
- 📖 Assign preliminary structured IDs
- 💬 Build cross-reference mappings
- 🚫 **FORBIDDEN** to load next step until consolidation is complete

## CONTEXT BOUNDARIES:

- Extracted data from step 2 is available
- Use structured_id_system from config for ID format
- Don't analyze gaps yet - just consolidate
- Conflicts are flagged, not resolved

---

## CONSOLIDATION SEQUENCE:

### 0. Check Import Mode and Load Existing Data (if augment)

**IF import_mode == 'augment':**

1. Load existing data from `{existing_data_file}`
2. Extract highest existing IDs for each type:
   - `max_ps_id` = highest PS-XX-### number
   - `max_pp_id` = highest PP-XX-### number
   - `max_cp_id` = highest CP-XX-### number
   - `max_sys_id` = highest SYS-XX-### number
3. Store existing items for deduplication check
4. Display: "Augment mode: Found {n} existing process steps, {n} pain points, {n} controls, {n} systems. New items will be assigned IDs starting from the next available number."

**IF import_mode == 'replace' or 'fresh':**
- Start ID numbering from 001
- No existing data to merge

### 1. Merge Extracted Data

Combine all extracted elements from all processed documents into unified lists:
- Process Steps list
- Pain Points list
- Controls list
- Systems list
- Roles list

### 2. Identify and Consolidate Duplicates (with Augment Awareness)

Apply consolidation rules:

| Scenario | Action |
|----------|--------|
| Same process step described in multiple docs | Consolidate, note all sources |
| Similar pain points with different wording | Merge if >80% semantic similarity |
| Same system mentioned across docs | Single entry with all references |
| Conflicting information | Flag for SME clarification |

**Additional rules for augment mode:**

| Scenario | Action |
|----------|--------|
| New item matches existing item (>80% similarity) | Flag as potential duplicate, ask user |
| New item adds detail to existing item | Offer to enhance existing item's description |
| New item contradicts existing SME-validated item | Flag conflict, preserve existing, note discrepancy |

When potential duplicate with existing data is found, present:
```
⚠️ **Potential Duplicate Detected**

New extracted item: "{new_item_description}"
Existing item: {existing_id} - "{existing_description}"

Options:
[S] Skip - Don't import (existing is sufficient)
[E] Enhance - Add new details to existing item
[A] Add Anyway - Import as separate item (new ID)
```

### 3. Assign Preliminary Structured IDs

Using the structured ID system configuration, assign IDs:

**For fresh/replace mode (starting from 001):**
- **Process Steps**: PS-{XX}-{###} (e.g., PS-01-001)
- **Pain Points**: PP-{XX}-{###} (e.g., PP-01-001)
- **Controls/Compliance**: CP-{XX}-{###} (e.g., CP-01-001)
- **Systems**: SYS-{XX}-{###} (e.g., SYS-01-001)

**For augment mode (continuing from existing):**
- **Process Steps**: PS-{XX}-{max_ps_id + 1} (e.g., if max is PS-01-005, next is PS-01-006)
- **Pain Points**: PP-{XX}-{max_pp_id + 1}
- **Controls/Compliance**: CP-{XX}-{max_cp_id + 1}
- **Systems**: SYS-{XX}-{max_sys_id + 1}

Note: {XX} represents a category or phase code, {###} is sequential.

### 4. Build Cross-Reference Mappings

Where evident from source documents, establish relationships:

- "Step X uses System Y" -> Link PS# to SYS#
- "Control Z applies to Step X" -> Link CP# to PS#
- "Issue A occurs in Step X" -> Link PP# to PS#

### 5. Document Conflicts

For any conflicting information found:
- Document both/all versions
- Note the source documents
- Flag as "requires SME clarification"
- Do NOT auto-resolve

### 6. Check for Conflicts

After consolidation, evaluate conflict status:

**IF conflicts were found:**
- Display conflicts requiring SME clarification
- Show each conflict with:
  - Element type and name
  - Conflicting values from different sources
  - Source document references
- Ask user to resolve before continuing:
  "**Conflicts Found ({conflict_count}):**
  {conflict_details}

  Please clarify which version is correct, or provide the accurate information."
- After user resolves conflicts, proceed to next step

**IF no conflicts found:**
- Proceed silently to next step (no output, no menu)

---

## CRITICAL STEP COMPLETION NOTE

Once all extracted data has been consolidated with IDs assigned:
- **If conflicts exist**: Wait for user resolution, then load and execute `{nextStepFile}`
- **If no conflicts**: Immediately load and execute `{nextStepFile}` (silent auto-continue)

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- All extracted data merged into unified lists
- Duplicates identified and consolidated properly
- All source references preserved in consolidated items
- Structured IDs assigned to all elements
- Cross-references built where evident
- Conflicts flagged and presented to user for resolution (if any)
- Silent auto-continue when no conflicts exist

### ❌ FAILURE:

- Losing source references during consolidation
- Auto-resolving conflicts without SME input
- Not assigning structured IDs
- Incorrectly merging distinct items
- Performing gap analysis in this step (premature)
- Displaying verbose output when no conflicts exist
- Prompting user unnecessarily when no conflicts found

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
