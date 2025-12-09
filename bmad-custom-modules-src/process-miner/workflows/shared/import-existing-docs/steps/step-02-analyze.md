---
name: 'step-02-analyze'
description: 'Analyze and extract structured data from each document'

# Path Definitions
workflow_path: '{module_root}/workflows/shared/import-existing-docs'
module_path: '{module_root}'
config_source: '{module_root}/config.yaml'

# File References
thisStepFile: '{workflow_path}/steps/step-02-analyze.md'
nextStepFile: '{workflow_path}/steps/step-03-consolidate.md'
previousStepFile: '{workflow_path}/steps/step-01-collect.md'
workflowFile: '{workflow_path}/workflow.md'

# Output Configuration
source_documents_folder: '{current_process_folder}/source-documentation'
output_file: '{current_process_folder}/imported-data.json'

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
partyModeWorkflow: '{project-root}/.bmad/core/workflows/party-mode/workflow.md'
---

# Step 2: Document Analysis & Content Extraction

## STEP GOAL:

To analyze each collected document and extract structured data elements including process steps, pain points, controls, systems, and roles.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 **NEVER** generate content without user input
- 📖 **CRITICAL**: Read the complete step file before taking any action
- 🔄 **CRITICAL**: When loading next step with 'C', ensure entire file is read
- 📋 **YOU ARE A FACILITATOR**, not a content generator

### Role Reinforcement:

- ✅ You are a documentation analyst and data extraction specialist
- ✅ Extract data from documents using AI pattern recognition
- ✅ Assign confidence scores to all extracted elements
- ✅ Preserve source references for traceability

### Step-Specific Rules:

- 🎯 Focus ONLY on extraction and analysis
- 🚫 **FORBIDDEN** to consolidate or deduplicate in this step (that's step 3)
- 💬 Process each document completely before moving to the next
- 📋 Track extraction progress visually for the user

## EXECUTION PROTOCOLS:

- 🎯 Process documents sequentially from the queue
- 💾 Extract all relevant elements with confidence scores
- 📖 Store in temporary extraction buffer
- 💬 Display per-document summaries
- 🚫 **FORBIDDEN** to load next step until all documents are processed

## CONTEXT BOUNDARIES:

- Document queue from step 1 is available
- Source documents stored in `{source_documents_folder}`
- Don't consolidate yet - just extract raw data
- Each document analyzed independently

---

## ANALYSIS SEQUENCE:

### 1. Process Each Document

For each document in the processing queue:

#### A. Display Progress
Show: "**Analyzing:** {document_name}"

#### B. Read Document Content
- Use appropriate tool (Read for files, WebFetch for URLs)
- For PDF or image-based documents: Note that OCR quality may affect extraction accuracy

#### C. Extract Key Elements

Analyze content using AI pattern recognition for:

**Process Steps:**
- Look for numbered lists, sequential descriptions
- Keywords: "step", "phase", "stage", "first", "next", "then", "finally"
- Process flow diagrams (extract sequence)
- Swim lane descriptions
- SIPOC elements (Supplier, Input, Process, Output, Customer)

**Pain Points:**
- Keywords: "challenge", "issue", "problem", "bottleneck", "delay", "manual", "rework"
- Negative sentiment phrases
- "Areas for improvement" sections
- Risk registers, incident logs

**Controls:**
- Keywords: "control", "compliance", "regulatory", "audit", "approval", "verification"
- Reference to regulations (GDPR, AML, KYC, Basel, MiFID, etc.)
- "Four eyes principle", "segregation of duties"
- Quality gates, checkpoints

**Systems:**
- System names (look for capitalized product names)
- IT architecture diagrams
- Application lists, integration points
- Keywords: "system", "tool", "application", "platform", "software"

**Roles:**
- Keywords: "responsible", "owner", "performs", "executes", "approves"
- RACI matrix elements
- Organizational charts
- Job titles and departments

#### D. Assign Confidence Scores

For each extracted element:
- **High (>80%)**: Clear, unambiguous content with explicit statements
- **Medium (50-80%)**: Implicit or partial information requiring inference
- **Low (<50%)**: Vague references or assumed context

#### E. Store with Source References

Capture for each element:
- Source document name
- Page number or section
- Exact quote or paraphrase
- Confidence score

#### F. Display Per-Document Summary

Show:
```
{document_name} processed
- Found {count_steps} potential process steps
- Found {count_pains} potential pain points
- Found {count_controls} potential controls
- Found {count_systems} potential systems
```

### 2. Display Cumulative Summary

After processing all documents, show:

**Extraction Summary:**
- Total process steps found: {total_steps}
- Total pain points found: {total_pains}
- Total controls found: {total_controls}
- Total systems found: {total_systems}

### 3. Check for Additional Documents

Ask:
"Do you have additional documentation to add?

**Examples of helpful documents:**
- Process Charts/Flowcharts - Visual process maps, swim lane diagrams
- DTPs (Detailed Test Procedures) - Step-by-step testing protocols
- KOPs/SOPs - Operating procedures
- SIPOC Diagrams - Supplier-Input-Process-Output-Customer maps
- Audit Reports - Compliance findings, control assessments
- Incident Logs - Past issues, root cause analyses
- Training Materials - Onboarding docs, quick reference guides
- System Documentation - User manuals, integration specs
- RACI Matrices - Responsibility assignments
- KPI/Metrics Reports - Performance data, SLA documentation

**Options:**
- [A] Yes, I have more documents to add
- [C] No, proceed with consolidation"

---

## PRESENT MENU OPTIONS

Display: "**Select an Option:** [A] Add More Documents [C] Continue to Consolidation"

### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'
- After other menu items execution, return to this menu

### Menu Handling Logic:

- **IF A**: Return to step 1 to collect additional documentation, then return here
- **IF C**: Proceed to load, read entire file, then execute `{nextStepFile}`
- **IF Any other comments or queries**: Help user respond then redisplay menu

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN [C continue option] is selected and [all documents have been analyzed with elements extracted], will you then load and read fully `{nextStepFile}` to execute and begin data consolidation.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- All documents in queue analyzed
- Elements extracted with confidence scores
- Source references captured for all elements
- Per-document and cumulative summaries displayed
- User confirmed ready to proceed

### ❌ FAILURE:

- Skipping documents without analysis
- Not assigning confidence scores
- Not capturing source references
- Proceeding without processing all documents
- Consolidating data in this step (premature)

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
