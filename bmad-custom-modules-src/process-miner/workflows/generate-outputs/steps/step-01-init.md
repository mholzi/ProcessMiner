---
name: 'step-01-init'
description: 'Initialize workflow by selecting process, resolving template configuration, and checking for existing summary'

# Path Definitions
workflow_path: '{module_root}/workflows/generate-outputs'
module_root: '{project-root}/bmad-custom-modules-src/process-miner'

# File References
thisStepFile: '{workflow_path}/steps/step-01-init.md'
nextStepFile: '{workflow_path}/steps/step-02-extract.md'
continueStepFile: '{workflow_path}/steps/step-01b-continue.md'
workflowFile: '{workflow_path}/workflow.md'

# Shared Workflow References
selectProcessWorkflow: '{module_root}/workflows/shared/select-existing-process/workflow.md'

# Template References (by template name - used when data.template is provided)
# Format: template-name → source document, template path, output filename
templatesByName:
  management-summary-process:
    source: 'as-is-process-documentation.md'
    template: '{module_root}/templates/management-summary-process.md'
    output: 'management-summary-process.md'
  management-summary-cx:
    source: 'cx-journey-documentation.md'
    template: '{module_root}/templates/management-summary-cx.md'
    output: 'management-summary-cx.md'
  management-summary-compliance:
    source: 'compliance-control-assessment.md'
    template: '{module_root}/templates/management-summary-compliance.md'
    output: 'management-summary-compliance.md'
  management-summary-innovation:
    source: 'innovation-analysis-template.md'
    template: '{module_root}/templates/management-summary-innovation.md'
    output: 'management-summary-innovation.md'

# Template References (by agent type - fallback when data.template not provided)
templates:
  process-documentation-analyst:
    source: 'as-is-process-documentation.md'
    template: '{module_root}/templates/management-summary-process.md'
    output: 'management-summary-process.md'
  client-journey-analyst:
    source: 'cx-journey-documentation.md'
    template: '{module_root}/templates/management-summary-cx.md'
    output: 'management-summary-cx.md'
  control-analyst:
    source: 'compliance-control-assessment.md'
    template: '{module_root}/templates/management-summary-compliance.md'
    output: 'management-summary-compliance.md'
  innovation-analyst:
    source: 'innovation-analysis-template.md'
    template: '{module_root}/templates/management-summary-innovation.md'
    output: 'management-summary-innovation.md'
---

# Step 1: Workflow Initialization

## STEP GOAL:

To initialize the Management Summary workflow by selecting a process, resolving template configuration (from explicit data parameters OR detecting calling agent), validating source documents exist, and routing to either fresh generation (step-02) or continuation/update (step-01b) based on existing summary state.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step, ensure entire file is read first
- 📋 YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:

- ✅ You are a document synthesizer and executive communication specialist
- ✅ If you already have a name, communication_style, and identity from the calling agent, continue using those
- ✅ We engage in collaborative dialogue, not command-response
- ✅ You bring expertise in Amazon 6-Pager format, user brings domain knowledge

### Step-Specific Rules:

- 🎯 Focus ONLY on initialization, detection, and routing
- 🚫 FORBIDDEN to generate any summary content in this step
- 🚫 FORBIDDEN to load source documents fully (that's step-02)
- 💬 Handle process selection and validation professionally
- 🚪 DETECT existing summary state and route appropriately

## EXECUTION PROTOCOLS:

- 🎯 Execute process selection first
- 🎯 Detect calling agent or ask user
- 🎯 Validate source document exists
- 🎯 Check for existing management summary
- 💾 Set session variables for downstream steps
- 🚫 FORBIDDEN to proceed without valid source document

## CONTEXT BOUNDARIES:

- Variables from workflow.md are available
- Calling agent context may be available from session
- Don't assume source documents exist - validate
- Don't assume summary exists - check

---

## INITIALIZATION SEQUENCE:

### 1. Process Selection

Execute the shared process selection workflow:

Load, read, and execute `{selectProcessWorkflow}` to:
- Present list of existing processes from registry
- User selects target process
- Set session variables:
  - `current_process_id`
  - `current_process_name`
  - `current_process_folder`

If no processes exist in registry:
- Display: "No processes found in registry. Please complete process documentation first using the Process Documentation Analyst."
- **STOP workflow**

### 2. Resolve Template Configuration

Determine template configuration using this priority order:

**Priority 1: Explicit Data Parameters (from menu item)**
If `{data.template}` is provided in the workflow invocation context:
- Look up `{data.template}` in `templatesByName` from frontmatter
- If `{data.primary_document}` is also provided, use it to override the source document
- This is the PREFERRED approach for explicit menu item configuration

Example: Menu item with `data.template: 'management-summary-compliance'` and `data.primary_document: 'as-is-process-documentation.md'` will:
- Use template: `management-summary-compliance.md`
- Use source: `as-is-process-documentation.md` (from data.primary_document)
- Output: `management-summary-compliance.md`

**Priority 2: Calling Agent Detection (fallback)**
If `{data.template}` is NOT provided:

**Option A: Agent Context Available**
If calling agent ID is in session context, use it directly to look up in `templates`.

**Option B: Agent Context Not Available**
Ask user:

"Which type of management summary would you like to generate?

1. **Process Documentation Summary** - AS-IS process analysis (Process Documentation Analyst)
2. **Client Experience Summary** - CX journey analysis (Client Journey Analyst)
3. **Compliance Summary** - Control assessment (Control Analyst)
4. **Innovation Summary** - Innovation analysis (Innovation Analyst)

Select [1-4]:"

Map selection to agent ID:
- 1 → `process-documentation-analyst`
- 2 → `client-journey-analyst`
- 3 → `control-analyst`
- 4 → `innovation-analyst`

Store as: `current_agent_id`, then resolve from `templates` in frontmatter.

### 3. Store Template Variables

Based on resolution from step 2, set session variables:
- `source_document_name` - The source document filename (from data.primary_document OR template config)
- `template_path` - Path to management summary template
- `output_filename` - Output filename for management summary
- `template_source` - 'explicit' (from data params) or 'agent-detected' (from agent lookup)

Display:
"**Template Configuration:**
- Source: {template_source}
- Template: {output_filename}
- Primary Document: {source_document_name}"

### 4. Validate Source Document Exists

Check if source document exists at:
`{current_process_folder}/{source_document_name}`

**If source document NOT found:**

Display:
"⚠️ Source document not found.

**Expected:** {current_process_folder}/{source_document_name}

The {current_agent_id} has not yet created the source documentation for this process.

Please complete the source analysis first:
- For Process Summary → Complete AS-IS Process Documentation
- For CX Summary → Complete Client Journey Analysis
- For Compliance Summary → Complete Compliance Control Assessment
- For Innovation Summary → Complete Innovation Analysis

**Workflow cannot proceed without source documentation.**"

**STOP workflow**

**If source document FOUND:**

Display:
"✅ Source document found: {source_document_name}
   Last modified: {file_modified_date}"

Proceed to next section.

### 5. Check for Existing Management Summary

Check if management summary already exists at:
`{current_process_folder}/{output_filename}`

**If summary EXISTS:**

Store:
- `existing_summary_path` = full path to existing summary
- `existing_summary_modified` = last modified date
- `workflow_mode` = 'update'

Display:
"📄 Existing management summary found.

**File:** {output_filename}
**Last Updated:** {existing_summary_modified}

Routing to change detection..."

→ Route to `{continueStepFile}` (step-01b)

**If summary DOES NOT EXIST:**

Store:
- `workflow_mode` = 'create'

Display:
"📝 No existing management summary found.

Creating new summary for: {current_process_name}
Template: {output_filename}
Source: {source_document_name}

Proceeding to data extraction..."

→ Route to `{nextStepFile}` (step-02)

---

## SESSION VARIABLES SET BY THIS STEP

| Variable | Description |
|----------|-------------|
| `current_process_id` | Process ID from registry |
| `current_process_name` | Human-readable process name |
| `current_process_folder` | Path to process folder |
| `current_agent_id` | Detected or selected agent ID (may be null if explicit template used) |
| `source_document_name` | Filename of source document |
| `source_document_path` | Full path to source document |
| `template_path` | Path to management summary template |
| `output_filename` | Output filename for summary |
| `output_path` | Full path for output file |
| `template_source` | 'explicit' (from data params) or 'agent-detected' (from agent lookup) |
| `workflow_mode` | 'create' or 'update' |
| `existing_summary_path` | (if update mode) Path to existing summary |
| `existing_summary_modified` | (if update mode) Last modified date |

---

## ROUTING LOGIC

```
Process Selected?
    ├── NO → STOP (no processes)
    └── YES → Agent Detected?
                ├── NO → Ask user to select
                └── YES → Source Doc Exists?
                            ├── NO → STOP (missing source)
                            └── YES → Summary Exists?
                                        ├── YES → step-01b-continue.md
                                        └── NO → step-02-extract.md
```

---

## CRITICAL STEP COMPLETION NOTE

This step has TWO possible exits:

1. **If existing summary found:** Load, read entire file, then execute `{continueStepFile}` to detect material changes
2. **If no existing summary:** Load, read entire file, then execute `{nextStepFile}` to begin data extraction

Do NOT present a menu in this step - routing is automatic based on state detection.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Process selected from registry
- Agent ID detected or selected
- Source document existence validated
- Existing summary state checked
- Session variables set correctly
- Correct routing to next step

### ❌ SYSTEM FAILURE:

- Proceeding without valid process selection
- Proceeding without source document validation
- Not checking for existing summary
- Wrong routing decision
- Missing session variables for downstream steps
- Loading step-02 when summary exists (should be step-01b)
- Loading step-01b when no summary exists (should be step-02)

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
