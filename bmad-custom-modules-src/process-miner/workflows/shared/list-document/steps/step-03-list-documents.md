---
name: 'step-03-list-documents'
description: 'Scan source-documentation folder and display documents with descriptions and links'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/shared/list-document'

# File References
thisStepFile: '{workflow_path}/steps/step-03-list-documents.md'
workflowFile: '{workflow_path}/workflow.md'

# Document location (resolved from session)
source_docs_folder: '{current_process_folder}/source-documentation'
---

# Step 3: List Documents

## STEP GOAL:

Scan the selected process's source-documentation folder and display all documents with AI-generated descriptions and links. This is the final step of the workflow.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- CRITICAL: Read the complete step file before taking any action
- Display results clearly in card format (not table)

### Role Reinforcement:

- You are a session utility specialist
- Be brief and helpful - present results clearly
- This is the final step - end gracefully

### Step-Specific Rules:

- Focus ONLY on scanning, reading, and displaying documents
- Handle empty folders gracefully
- Generate concise AI summaries for each document
- Provide useful links to documents

## EXECUTION PROTOCOLS:

- Scan `{source_docs_folder}` for all files
- Get filesystem metadata (uploaded/modified date) for each file
- Read each document's content (text files, images, PDFs)
- Generate 2-paragraph AI description for each document
- Display in card format
- End the workflow

## CONTEXT BOUNDARIES:

- You have the process folder path from step 2
- Documents are stored in `source-documentation/` subfolder
- This step reads document content to generate descriptions
- Workflow ends after displaying results

## Sequence of Instructions

### 1. Scan Source Documentation Folder

Scan the folder at `{current_process_folder}/source-documentation/` for all files.

**If folder does not exist:**
```
No source-documentation folder found for {current_process_name}.

Documents are stored when you use the *import-docs workflow.
```
**End workflow.**

**If folder exists but is empty:**
```
No documents found in source-documentation folder for {current_process_name}.

Use *import-docs to add documents to this process.
```
**End workflow.**

### 2. Build Document Cards

For each file found:

1. **Get metadata**: Extract filename, extension, and filesystem modified date (display as "uploaded" date)
2. **Read content**: Load the document content (use appropriate method for file type - text, image, PDF)
3. **Generate title**: Create a concise, descriptive title for the document based on its content (do NOT use the filename)
4. **Generate description**: Create a 1-paragraph AI summary capturing the document's purpose and key information

### 3. Display Document Cards

Display the results in card format:

```
## Documents for {current_process_name} ({current_process_id})

---

**{ai_generated_title_1}** (uploaded: {date_1})
[{filename_1}]({relative_path_1})

{ai_description_paragraph}

---

**{ai_generated_title_2}** (uploaded: {date_2})
[{filename_2}]({relative_path_2})

{ai_description_paragraph}

---

**Total: {count} document(s)**

**Folder:** `{current_process_folder}/source-documentation/`
```

### 4. End Workflow

Display completion message:
```
---
Document listing complete.
```

**Workflow ends here.** No further steps to load.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- Source-documentation folder correctly located
- All documents in folder listed
- Document content read successfully
- AI-generated title created for each document
- AI description (1 paragraph) generated for each document
- Card format displayed correctly
- Links point to correct file paths
- Workflow ends gracefully

### SYSTEM FAILURE:

- Not finding documents that exist
- Failing to read document content
- Using filename instead of generated title
- Missing or incomplete AI descriptions
- Incorrect file paths in links
- Crashing on empty folder
- Attempting to load another step after completion

**Master Rule:** This is the FINAL step. Read document content, generate descriptions, display cards, and end the workflow gracefully. Do NOT attempt to load any further steps.
