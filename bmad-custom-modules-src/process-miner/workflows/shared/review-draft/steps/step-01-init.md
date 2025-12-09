---
name: 'step-01-init'
description: 'Initialize document review by selecting process, loading document, resolving schema, and detecting existing sessions'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/shared/review-draft'

# File References
thisStepFile: '{workflow_path}/steps/step-01-init.md'
nextStepFile: '{workflow_path}/steps/step-02-sync.md'
continueFile: '{workflow_path}/steps/step-01b-continue.md'
workflowFile: '{workflow_path}/workflow.md'
registryFile: '{output_folder}/processes/process-registry.md'

# No template - this workflow operates on existing documents
---

# Step 1: Review Initialization

## STEP GOAL:

To initialize the document review workflow by: (1) loading the target document, (2) resolving the schema, (3) analyzing ALL section completeness, and (4) offering a guided review approach.

**Note:** Process selection is handled by the shared `select-existing-process` workflow BEFORE this step. `current_process_id`, `current_process_name`, and `current_process_folder` are already set.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- NEVER generate content without user input
- CRITICAL: Read the complete step file before taking any action
- CRITICAL: When loading next step, ensure entire file is read
- YOU ARE A FACILITATOR, not a content generator
- IMPORTANT: Process is already selected - DO NOT ask for process selection again
- IMPORTANT: `contributor_name` and `contributor_role` are already set by agent activation - DO NOT ask again

### Role Reinforcement:

- You are a document review facilitator
- If you already have been given a name, communication_style and identity, continue to use those while playing this new role
- We engage in collaborative dialogue, not command-response
- You bring document analysis expertise, user brings domain knowledge
- Maintain professional, supportive tone throughout

### Step-Specific Rules:

- Focus ONLY on document loading and setup
- FORBIDDEN to look ahead to future steps
- Handle initialization professionally
- DETECT existing review sessions and handle continuation properly
- ALWAYS show ALL section statuses, not just sync-enabled ones
- DO NOT ask for process selection or contributor info - use session variables

## EXECUTION PROTOCOLS:

- Show analysis before taking any action
- Initialize review-state.json with session data
- FORBIDDEN to load next step until setup is complete

## CONTEXT BOUNDARIES:

- Variables from workflow.md are available in memory
- `current_process_id`, `current_process_name`, `current_process_folder` are set by select-existing-process workflow
- `contributor_name` and `contributor_role` are set by agent activation
- Previous context = existing review-state.json if present
- Don't assume knowledge from other steps

## WORKFLOW DATA (from calling agent):

This workflow expects the following data from the calling agent's menu configuration:
- `primary_document`: The filename of the agent's main document (e.g., "as-is-process-documentation.md")
- `template`: The template name for schema resolution (e.g., "as-is-process-documentation")

## INITIALIZATION SEQUENCE:

### 1. Document Selection

With process now selected, determine the document to review:

**Priority 1: Agent-provided primary_document**
- If `primary_document` is provided by the calling agent:
  - Look for `{current_process_folder}/{primary_document}`
  - If found, use this document automatically
  - If not found, inform user and fall back to manual selection

**Priority 2: Explicit document path**
- If a full document path is provided by user:
  - Use the provided path directly
  - Validate file exists and is readable

**Priority 3: Manual selection**
- If no document identified via above methods:
  - Scan `{current_process_folder}` for all .md files
  - Present as numbered options:
    ```
    Documents found in {current_process_name}:

    | # | Document | Last Modified |
    |---|----------|---------------|
    | 1 | as-is-process-documentation.md | [date] |
    | 2 | exceptions-detail.md | [date] |
    ...

    Enter document number:
    ```
  - **WAIT for user input.**

### 2. Load and Parse Document

Once document is identified:

1. **Read the complete document** including frontmatter
2. **Parse frontmatter** to extract:
   - `template:` field (for schema resolution)
   - Any existing metadata (title, process_id, etc.)
3. **Discover all sections** by scanning for `##` headers
4. **Store section inventory** with titles and line numbers

### 3. Schema Resolution Chain

Execute the schema resolution chain:

**Step 3a: Use Agent-Provided Template (if available)**
- If `template` is provided by the calling agent's data block:
  - Use this value directly (no need to parse frontmatter)
  - Construct schema path: `{module_root}/templates/{template}.schema.yaml`
  - Attempt to load schema from module's templates folder
  - If found, proceed with schema-driven mode

**Step 3b: Check Document Frontmatter**
- If no agent-provided template, check document frontmatter for `template:` field:
  - Construct schema path: `{module_root}/templates/{template-name}.schema.yaml`
  - Example: `template: as-is-process-documentation` → looks for `as-is-process-documentation.schema.yaml`
  - Attempt to load schema from module's templates folder
  - If found, proceed with schema-driven mode

**Step 3c: Check Local Override**
- Check for `schema.yaml` in same folder as document
- If found, use as override (replaces template schema entirely)

**Step 3d: Fallback to Auto-Discovery**
- If no schema found via any method:
  - Set `schema_mode: "auto-discovery"`
  - All sections will be reviewed without sync capabilities
  - Inform user: "No schema found - operating in auto-discovery mode (section review only, no sync)"

**Store schema resolution result:**
```
schema_resolved: true/false
schema_path: "path or null"
schema_mode: "template" | "local" | "auto-discovery"
sync_enabled_sections: [list of section patterns with sync]
```

### 4. Check for Existing Session

Check if `review-state.json` exists in the document's folder:

**If review-state.json exists:**
- Read the file completely
- Check if it references the same document
- If same document with incomplete review:
  - **STOP here** and load `./step-01b-continue.md` immediately
  - Do not proceed with initialization
  - Let step-01b handle the continuation logic

**If review-state.json references different document:**
- Ask user: "Found a review session for a different document. Start fresh for this document?"
- If yes, proceed with new session
- If no, let user choose which document to review

### 5. Confirm Contributor Information

Contributor details are already captured during agent activation. Use session variables:

```
contributor_name: {contributor_name}  (from agent activation)
contributor_role: {contributor_role}  (from agent activation)
```

Display brief confirmation:
```
Reviewer: {contributor_name} ({contributor_role})
```

**DO NOT ask for name or role again.**

### 6. Create Review State

Initialize `review-state.json` in the document's folder:

```json
{
  "process_id": "[selected process ID]",
  "process_name": "[selected process name]",
  "process_folder": "[full path to process folder]",
  "document_path": "[full path to document]",
  "document_name": "[filename]",
  "schema_path": "[path or null]",
  "schema_mode": "[template|local|auto-discovery]",
  "contributor": {
    "name": "[user input]",
    "role": "[user input]"
  },
  "started": "[ISO8601 timestamp]",
  "last_updated": "[ISO8601 timestamp]",
  "sections": [
    {
      "id": 1,
      "title": "[section title from document]",
      "line_number": 0,
      "completeness": "[complete|partial|empty]",
      "confidence": 0,
      "gaps": ["list of identified gaps"],
      "has_sync": true/false,
      "sync_status": {
        "main_count": 0,
        "detail_count": 0,
        "pending_sync": 0
      },
      "review_status": "pending"
    }
  ],
  "summary": {
    "complete_sections": 0,
    "partial_sections": 0,
    "empty_sections": 0,
    "total_pending_sync": 0
  },
  "review_mode": null,
  "recommended_section": null,
  "recommendation_reason": null,
  "current_section": null,
  "sync_completed": false
}
```

**Note:** The `confidence` field stores the initial calculated confidence (0-100) based on section analysis. This value is displayed in the Section Status Overview table and updated as the user reviews each section.

### 7. Analyze Section Completeness (ALL SECTIONS)

For EVERY section in the document, analyze completeness by checking:

**Completeness Indicators:**
- **Complete**: Section has substantive content (>100 chars), no TBD/TODO markers, has required references
- **Partial**: Section has some content but contains TBD/TODO markers or missing required elements
- **Empty**: Section header exists but no meaningful content
- **Gap**: Section is missing required cross-references or structured IDs

**For sync-enabled sections, also check:**
- Does detail document exist?
- Are items in detail doc reflected in main doc summary table?
- Count items in each (main vs detail)

### 8. Display Session Summary with Full Status

Present initialization summary showing ALL sections with confidence scores:

```
**Review Session Initialized**

| Field | Value |
|-------|-------|
| Process | {current_process_id} - {current_process_name} |
| Document | [filename] |
| Schema Mode | [template/local/auto-discovery] |
| Reviewer | [name] ([role]) |

---

**Section Status Overview:**

| # | Section | Status | Confidence |
|---|---------|--------|------------|
| 1 | Process Overview | partial | 65% |
| 2 | Process Steps | complete | 85% |
| 3 | Exception Paths | empty | 5% |
| 4 | Control Points | partial | 70% |
| 5 | System Dependencies | complete | 90% |
| 6 | Organizational Mapping | empty | 5% |
| 7 | Existing Documentation | empty | 5% |
| 8 | Process Gaps | empty | 5% |
| 9 | Pain Points | complete | 95% |

**Summary:**
- Complete: X sections
- Partial: Y sections
- Empty: Z sections
- Pending Sync: N items across M sections
```

**Confidence Scoring at Initialization:**

Calculate initial confidence for each section based on:
- **90-100%**: Complete content, no TBD/TODO markers, all required fields populated
- **70-89%**: Mostly complete but has minor gaps (some TBD markers, missing optional fields)
- **50-69%**: Partial content with significant gaps (multiple TBD markers, missing required fields)
- **20-49%**: Minimal content, mostly placeholder text
- **5-19%**: Empty or only header/description present

Store initial confidence in review-state.json for each section.

### 9. Offer Review Approach

Based on the analysis, present review options:

```
---

**How would you like to proceed?**

[G] **Gap-Based Review** - Start with sections needing attention
    Recommended: Section [#] ([name]) - [reason]

[S] **Sequential Review** - Work through all sections in order (1-9)

[Y] **Sync First** - Sync pending items before review (if applicable)

[P] **Pick Section** - Jump to a specific section

Enter your choice:
```

**WAIT for user input.**

**Handle user selection:**

- **G (Gap-Based):** Set `review_mode: "gap-based"`, identify highest-priority gap section, proceed to step-03
- **S (Sequential):** Set `review_mode: "sequential"`, set `current_section: 1`, proceed to step-03
- **Y (Sync First):** If sync-enabled sections have pending items, proceed to step-02-sync
- **P (Pick Section):** Ask "Which section? (1-9):", store selection, proceed to step-03

**Store review approach in review-state.json:**
```json
{
  "review_mode": "[gap-based|sequential|sync-first|pick]",
  "recommended_section": [number or null],
  "recommendation_reason": "[text or null]"
}
```

### 10. Proceed to Next Step

**Based on user selection:**

- If user selected **Y (Sync First)** and sync items pending: load, read entire file, then execute `{workflow_path}/steps/step-02-sync.md`
- Otherwise: load, read entire file, then execute `{workflow_path}/steps/step-03-review-loop.md`

Display: **Proceeding to [sync check / section review]...**

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- Used process selection from session variables (not asked again)
- Used contributor info from session variables (not asked again)
- Document loaded and parsed correctly
- Schema resolution chain executed completely
- ALL section completeness analyzed (not just sync-enabled)
- Full status table displayed showing every section
- Review approach options presented to user
- User selection captured and stored in review-state.json
- review-state.json created with all sections and review_mode
- Existing sessions properly detected and routed to step-01b
- Next step correctly determined based on user selection

### SYSTEM FAILURE:

- Asked for process selection (already done by select-existing-process workflow)
- Asked for contributor name or role (already captured by agent activation)
- Not showing ALL sections in status table
- Showing only sync-enabled sections
- Not offering review approach options (G/S/Y/P)
- Proceeding without user selecting review approach
- Proceeding without loading document
- Not executing schema resolution chain
- Not creating review-state.json
- Not routing to step-01b when session exists
- Hardcoding schema or section information

**Master Rule:** Process selection and contributor info are ALREADY SET. DO NOT ask again. ALL sections MUST be shown. User MUST choose review approach. Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
