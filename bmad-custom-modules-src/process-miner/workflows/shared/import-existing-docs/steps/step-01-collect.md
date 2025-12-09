---
name: 'step-01-collect'
description: 'Collect and store source documents for analysis'

# Path Definitions
workflow_path: '{module_root}/workflows/shared/import-existing-docs'
module_path: '{module_root}'
config_source: '{module_root}/config.yaml'

# File References
thisStepFile: '{workflow_path}/steps/step-01-collect.md'
nextStepFile: '{workflow_path}/steps/step-02-analyze.md'
workflowFile: '{workflow_path}/workflow.md'

# Output Configuration
source_documents_folder: '{current_process_folder}/source-documentation'
output_file: '{current_process_folder}/imported-data.json'
gap_analysis_file: '{current_process_folder}/gap-analysis.md'
existing_data_file: '{current_process_folder}/structured-data.json'
backup_folder: '{current_process_folder}/backups'

# Import Mode (session variable - set by pre-flight check or parameter)
# Values: auto | fresh | augment | replace
import_mode: session-variable

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
partyModeWorkflow: '{project-root}/.bmad/core/workflows/party-mode/workflow.md'
---

# Step 1: Document Collection & Format Detection

## STEP GOAL:

To collect source documentation from the user, detect formats, and preserve originals for audit trail before analysis begins.

## PRE-FLIGHT CHECK: EXISTING DATA DETECTION

Before collecting documents, check if this process already has documented data.

### Detection Sequence:

1. **Check for existing structured data:**
   - Look for `{current_process_folder}/structured-data.json`
   - If exists and contains data (process_steps array not empty), existing data is present

2. **If existing data detected AND import_mode is `auto` (or not set):**

   Display warning and options:
   ```
   ⚠️ **Existing Process Data Detected**

   This process folder already contains documented data:
   - Process Steps: {count} items
   - Pain Points: {count} items
   - Controls: {count} items
   - Systems: {count} items

   Importing new documentation requires choosing how to handle existing data:

   **[A] Augment** - Merge new imports with existing data
     • Preserves all SME-validated content
     • New items get sequential IDs (continues from highest existing)
     • Best for: Adding supplementary documentation

   **[R] Replace** - Overwrite existing with new imports
     • Existing structured-data.json will be backed up
     • All documentation files regenerated from imports
     • Best for: Starting fresh from different source docs

   **[C] Cancel** - Exit without changes
     • No modifications made
     • Return to menu
   ```

   Wait for user selection before proceeding.

3. **If import_mode is `fresh` and existing data found:**
   - Display error: "Cannot proceed - existing data found but import_mode is 'fresh'"
   - Exit workflow

4. **Set import_mode session variable** based on user choice or parameter:
   - `augment` → merge with existing
   - `replace` → backup existing, then overwrite
   - For `replace`: Create backup at `{current_process_folder}/backups/structured-data-{timestamp}.json`

5. **If no existing data OR import_mode is `fresh`:**
   - Proceed directly to document collection (no prompt needed)

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 **NEVER** generate content without user input
- 📖 **CRITICAL**: Read the complete step file before taking any action
- 🔄 **CRITICAL**: When loading next step with 'C', ensure entire file is read
- 📋 **YOU ARE A FACILITATOR**, not a content generator

### Role Reinforcement:

- ✅ You are a documentation analyst and data extraction specialist
- ✅ If you already have been given communication or persona patterns, continue to use those
- ✅ We engage in collaborative dialogue, not command-response
- ✅ You bring extraction expertise, user brings their domain knowledge and documents

### Step-Specific Rules:

- 🎯 Focus ONLY on document collection and format detection
- 🚫 **FORBIDDEN** to start extracting or analyzing content in this step
- 💬 Ask questions conversationally to understand what documents are available
- 📋 Preserve all original documents in source folder

## EXECUTION PROTOCOLS:

- 🎯 Show analysis before taking any action
- 💾 Create source documentation folder
- 📖 Store all provided documents with metadata
- 🚫 **FORBIDDEN** to load next step until document collection is complete

## CONTEXT BOUNDARIES:

- Variables from workflow.md and config are available in memory
- `current_process_folder` must be set by the agent before workflow starts
- Don't assume knowledge from other steps
- Document collection happens in this step only

---

## COLLECTION SEQUENCE:

### 1. Create Source Documentation Folder

**🛑 STOP - EXECUTE NOW (DO NOT SKIP):**

You MUST execute this Bash command RIGHT NOW before reading any further:

```bash
mkdir -p "{source_documents_folder}"
```

**⏸️ CHECKPOINT - DO NOT PROCEED UNTIL VERIFIED:**

After executing mkdir, you MUST immediately run this verification command:

```bash
ls -la "{source_documents_folder}" && echo "✅ FOLDER CREATED SUCCESSFULLY" || echo "❌ FOLDER CREATION FAILED"
```

**🚨 HARD STOP - VERIFY OUTPUT:**
- You MUST see "✅ FOLDER CREATED SUCCESSFULLY" in the output
- If you see "❌ FOLDER CREATION FAILED" - STOP and report error to user
- If you did not execute both commands above, GO BACK AND EXECUTE THEM NOW

**❌ FAILURE HANDLING:**
- If folder creation fails, display error to user:
  "**Error:** Could not create source documentation folder at `{source_documents_folder}`"
- Ask user: "Would you like me to try again, or use a different location?"
- **DO NOT PROCEED** until folder exists and verification shows success

### 2. Welcome and Explain Import Process

Greet the user and explain the import process:

"I'll analyze your existing documentation and extract structured process data.

**What I can process:**
- PDF documents
- Word documents (.doc, .docx)
- Markdown files (.md)
- PowerPoint presentations (.ppt, .pptx)
- Excel spreadsheets (.xls, .xlsx)
- Plain text files (.txt)
- Web pages/URLs

**What I'll extract:**
- Process steps and sequences
- Pain points and challenges
- Controls and compliance requirements
- Systems and tools used
- Roles and responsibilities

**Note:** All submitted documents will be preserved in:
`{source_documents_folder}/`"

### 3. Gather Document Sources

Ask the user how they will provide documentation:

**Options:**
- File path(s) on this system
- Paste content directly
- URL(s) to web documentation
- Combination of above

### 4. Process Each Source Type

#### For File Paths:
- Ask for the file path(s) (one per line, or comma-separated)
- For each file path provided, execute the following sequence:

**🛑 STOP - EXECUTE FOR EACH FILE (DO NOT SKIP):**

**Step A - Validate file exists:**
You MUST execute this Bash command RIGHT NOW:

```bash
ls -la "{user_provided_path}" && echo "✅ FILE EXISTS" || echo "❌ FILE NOT FOUND"
```

**⏸️ CHECKPOINT:** You MUST see "✅ FILE EXISTS" before proceeding. If not, report error and ask for correct path.

**Step B - Copy file to source folder:**
You MUST execute this Bash command RIGHT NOW:

```bash
cp "{user_provided_path}" "{source_documents_folder}/" && echo "✅ FILE COPIED" || echo "❌ COPY FAILED"
```

**Step C - Verify copy succeeded:**
You MUST execute this verification command RIGHT NOW:

```bash
ls -la "{source_documents_folder}/{filename}" && echo "✅ FILE STORED SUCCESSFULLY" || echo "❌ FILE STORAGE FAILED"
```

**🚨 HARD STOP - VERIFY ALL THREE COMMANDS EXECUTED:**
- Did you run `ls -la` on the source file? If not, GO BACK AND RUN IT
- Did you run `cp` to copy the file? If not, GO BACK AND RUN IT
- Did you run `ls -la` to verify the copy? If not, GO BACK AND RUN IT
- You MUST see "✅ FILE STORED SUCCESSFULLY" before adding to processing queue

**❌ FAILURE HANDLING:**
- If file not found: Display "**Error:** File not found at `{user_provided_path}`. Please check the path and try again."
- If copy fails: Display "**Error:** Could not copy file. Check permissions or disk space."
- Track failed files separately and report at end of collection
- **DO NOT** add failed files to processing queue

- Add successfully stored files to processing queue with metadata (original path + stored path) ONLY after verification passes

#### For Pasted Content:
- Ask user to paste the documentation content
- Ask what format the content is (Plain text, Markdown, HTML, Other)

**🛑 STOP - EXECUTE NOW (DO NOT SKIP):**

**Step A - Save pasted content:**
You MUST use the Write tool RIGHT NOW to save the pasted content to:
`{source_documents_folder}/pasted-content-{timestamp}.{format}`

(Use appropriate extension: .txt for plain text, .md for markdown, .html for HTML)

**Step B - Verify save succeeded:**
You MUST execute this verification command RIGHT NOW:

```bash
ls -la "{source_documents_folder}/pasted-content-{timestamp}.{format}" && echo "✅ PASTED CONTENT SAVED" || echo "❌ SAVE FAILED"
```

**🚨 HARD STOP - VERIFY:**
- Did you use the Write tool to save the file? If not, GO BACK AND DO IT NOW
- Did you run `ls -la` to verify? If not, GO BACK AND RUN IT
- You MUST see "✅ PASTED CONTENT SAVED" before proceeding

**❌ FAILURE HANDLING:**
- If save fails: Display "**Error:** Could not save pasted content. Check disk space or permissions."
- Offer to retry or use alternative filename

- Add to processing queue ONLY after verification passes

#### For URLs:
- Ask for the URL(s) (one per line)
- For each URL, execute the following sequence:

**🛑 STOP - EXECUTE FOR EACH URL (DO NOT SKIP):**

**Step A - Fetch URL content:**
You MUST use the WebFetch tool RIGHT NOW to retrieve content from `{url}`

**Step B - Save fetched content:**
You MUST use the Write tool RIGHT NOW to save the markdown content to:
`{source_documents_folder}/web-{sanitized_domain}-{timestamp}.md`

(Sanitize domain: replace dots and slashes with dashes, e.g., `example-com`)

**Step C - Verify URL content saved:**
You MUST execute this verification command RIGHT NOW:

```bash
ls -la "{source_documents_folder}/web-{sanitized_domain}-{timestamp}.md" && echo "✅ WEB CONTENT SAVED" || echo "❌ SAVE FAILED"
```

**🚨 HARD STOP - VERIFY ALL THREE STEPS EXECUTED:**
- Did you use WebFetch to get the content? If not, GO BACK AND DO IT NOW
- Did you use Write tool to save the file? If not, GO BACK AND DO IT NOW
- Did you run `ls -la` to verify? If not, GO BACK AND RUN IT
- You MUST see "✅ WEB CONTENT SAVED" before adding to processing queue

**❌ FAILURE HANDLING:**
- If WebFetch fails: Display "**Error:** Could not fetch content from `{url}`. URL may be inaccessible or require authentication."
- If save fails: Display "**Error:** Could not save fetched content."
- Track failed URLs separately and report at end of collection
- **DO NOT** add failed URLs to processing queue

- Add to processing queue ONLY after verification passes

### 5. Display Processing Queue Summary

**🔍 MANDATORY VALIDATION - Verify all stored documents:**

```validation
USE Bash tool to execute:
echo "=== SOURCE DOCUMENTATION FOLDER CONTENTS ===" && ls -la "{source_documents_folder}/" && echo "=== FILE COUNT ===" && ls -1 "{source_documents_folder}/" | wc -l
```

Show the user what will be processed:

**Documents to process:**
- {queue_count} files ready for analysis (must match file count from validation above)
- Stored in: `{source_documents_folder}/`

**Files stored:**
{list each file from ls output with format: "- {filename} ({size})"}

**⚠️ If any files failed to store:**
{list failed files with reasons}

### 6. Confirm Ready to Proceed

Ask: "Ready to proceed with analysis? [yes/no]"

If no: Allow user to add more documents or make corrections.

---

## PRESENT MENU OPTIONS

Display: "**Select an Option:** [A] Add More Documents [C] Continue to Analysis"

### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'
- After other menu items execution, return to this menu
- User can chat or ask questions - always respond and then redisplay menu

### Menu Handling Logic:

- **IF A**: Loop back to step 3 to collect additional documents
- **IF C**: Execute PRE-CONTINUATION VALIDATION below, then proceed

---

## PRE-CONTINUATION VALIDATION (Before loading next step)

**🛑 MANDATORY - Execute these checks before loading {nextStepFile}:**

```validation
CHECK 1 - Source folder exists and contains files:
USE Bash tool to execute:
test -d "{source_documents_folder}" && ls -1 "{source_documents_folder}/" | head -1 | grep -q . && echo "✅ VALIDATION PASSED: Source folder exists with files" || echo "❌ VALIDATION FAILED: No source documents stored"
```

```validation
CHECK 2 - Count stored documents:
USE Bash tool to execute:
FILE_COUNT=$(ls -1 "{source_documents_folder}/" 2>/dev/null | wc -l | tr -d ' ')
echo "Stored document count: $FILE_COUNT"
if [ "$FILE_COUNT" -gt 0 ]; then echo "✅ VALIDATION PASSED"; else echo "❌ VALIDATION FAILED: No documents stored"; fi
```

**❌ FAILURE HANDLING - If validation fails:**
- Display: "**Cannot proceed:** No source documents were successfully stored in `{source_documents_folder}/`"
- Display: "Please add at least one document before continuing."
- Return to menu options - do NOT load next step

**✅ SUCCESS - Only if both validations pass:**
- Display: "✅ {FILE_COUNT} document(s) stored and verified. Proceeding to analysis..."
- Load, read entire file, then execute `{nextStepFile}`

---

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN:
1. [C continue option] is selected AND
2. [PRE-CONTINUATION VALIDATION passes] AND
3. [At least one document verified in source folder]

Will you then load and read fully `{nextStepFile}` to execute and begin document analysis.

**🚫 NEVER proceed to next step if validation fails.**

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Source documentation folder created using `mkdir -p` command
- Folder creation verified using `ls -la` command
- All provided documents copied/saved to source folder
- Each file storage verified individually with `ls -la` command
- Document metadata captured (format, path, size)
- Processing queue populated only with verified files
- Pre-continuation validation executed and passed
- User confirmed ready to proceed

### ❌ FAILURE:

- Not executing `mkdir -p` command to create folder
- Not verifying folder creation with `ls -la`
- Not executing `cp` command to copy files
- Not verifying each file storage with validation commands
- Proceeding without any documents collected
- Not preserving original documents
- Not detecting file formats
- Skipping pre-continuation validation
- Proceeding to next step when validation fails
- Skipping to analysis without user confirmation

### 🔧 TOOL USAGE REQUIREMENTS:

This step MUST use these tools:
- **Bash tool**: For `mkdir`, `cp`, `ls`, and validation commands
- **Write tool**: For saving pasted content and fetched URL content
- **WebFetch tool**: For retrieving URL content

**Descriptive instructions are NOT sufficient. Actual tool execution is MANDATORY.**

**Master Rule:** Skipping steps, optimizing sequences, not executing required tool commands, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
