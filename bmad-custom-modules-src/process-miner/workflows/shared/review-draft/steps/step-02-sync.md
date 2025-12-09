---
name: 'step-02-sync'
description: 'Document synchronization check - compare main document with detail documents based on schema'

# Path Definitions
workflow_path: '{project-root}/.bmad/custom/modules/process-miner/workflows/review-draft'

# File References
thisStepFile: '{workflow_path}/steps/step-02-sync.md'
nextStepFile: '{workflow_path}/steps/step-03-review-loop.md'
workflowFile: '{workflow_path}/workflow.md'
---

# Step 2: Document Synchronization

## STEP GOAL:

To synchronize the main document with any detail documents defined in the schema, identifying new items, orphans, and conflicts before proceeding with the review.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- NEVER generate content without user input
- CRITICAL: Read the complete step file before taking any action
- CRITICAL: When loading next step, ensure entire file is read
- YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:

- You are a document synchronization specialist
- If you already have been given a name, communication_style and identity, continue to use those while playing this new role
- We engage in collaborative dialogue, not command-response
- You bring data reconciliation expertise, user brings domain knowledge
- Maintain professional, methodical tone throughout

### Step-Specific Rules:

- Focus ONLY on synchronization between documents
- FORBIDDEN to modify content without user approval
- Present full item content for sync decisions (never just IDs)
- Track all sync changes with contributor attribution

## EXECUTION PROTOCOLS:

- Show analysis before taking any action
- Present sync decisions one at a time
- Apply changes only after user confirmation
- Update review-state.json when sync is complete

## CONTEXT BOUNDARIES:

- Schema is loaded (from step-01-init)
- Document is loaded (from step-01-init)
- review-state.json exists with section inventory
- Only sync-enabled sections require processing

## CONDITIONAL EXECUTION:

**IMPORTANT:** This step only runs if schema has sync-enabled sections.

Check review-state.json or schema:
- If no sync-enabled sections exist: Skip directly to step-03-review-loop
- If sync-enabled sections exist: Execute this step

## SYNCHRONIZATION SEQUENCE:

### 1. Identify Sync-Enabled Sections

From the loaded schema, identify sections with `sync_enabled: true`:

For each sync-enabled section, extract:
- `title_pattern`: How to find the section in main document
- `detail_document`: Path to the detail document
- `structured_id_prefix`: ID pattern (e.g., "EX", "PP", "CP")

### 2. Load Detail Documents

For each sync-enabled section:

1. **Construct detail document path** (relative to main document folder)
2. **Check if detail document exists**
   - If exists: Load completely
   - If not exists: Note as "detail document not found"
3. **Parse detail document** for structured items:
   - Find all items matching the ID prefix pattern (e.g., EX001, EX002)
   - Extract item metadata: ID, name, description, added_by, created_date

### 3. Extract Main Document Items

For each sync-enabled section in the main document:

1. **Find the section** using title_pattern
2. **Parse summary tables** within the section
3. **Extract item IDs** from the tables
4. **Build inventory** of items in main document

### 4. Compare and Categorize

For each sync-enabled section, compare main vs detail:

**NEW_ITEMS:** Items in detail doc but NOT in main doc
- These were added via *add- commands and need to be synced

**ORPHANED_ITEMS:** Items in main doc but NOT in detail doc
- These may have been manually added or detail doc was modified

**CONFLICTS:** Items in BOTH but with different content
- Requires resolution: which version is correct?

### 5. Present Sync Analysis

If no discrepancies found:
```
**Document Sync Check:** All documents are in sync.

No new items, orphans, or conflicts detected.

Proceeding to section review...
```
- Update review-state.json: `sync_completed: true`
- Proceed to step-03-review-loop

If discrepancies found:
```
**Document Sync Analysis**

| Category | Count | Action Needed |
|----------|-------|---------------|
| New items to add | [n] | Sync to main doc |
| Orphaned items | [n] | Investigate/Remove |
| Data conflicts | [n] | Manual resolution |
```

### 6. Process New Items

For each new item (not yet in main document):

**Display full item content:**
```
---
### [ID]: [Name]

**Added by:** [contributor] ([role]) on [date]

| Field | Content |
|-------|---------|
| **[Field1]** | [value] |
| **[Field2]** | [value] |

**Description:**
[full description text]

---

| # | Decision for [ID] |
|---|-------------------|
| y | Include in sync |
| n | Exclude from sync |
| e | Edit before syncing |

Your decision for [ID]:
```

**Handle decision:**
- If 'y': Mark for inclusion
- If 'n': Mark as excluded
- If 'e': Collect edits, show updated content, confirm

### 7. Process Conflicts (if any)

For each conflict:

**Display both versions:**
```
---
### Conflict: [ID] - [Name]

**MAIN DOCUMENT VERSION:**
[full content from main doc]

---

**DETAIL DOCUMENT VERSION:**
[full content from detail doc]

---

**Key Differences:**
- [field]: "[main value]" vs "[detail value]"

| # | Resolution |
|---|------------|
| m | Keep MAIN document version |
| d | Use DETAIL document version |
| c | Custom - I'll provide correct content |

Your decision:
```

### 8. Process Orphans (if any)

For orphaned items:
```
**Orphaned Items ([count])**

These items exist in the main document but NOT in detail documents.

| ID | Name | Section | Likely Cause |
|----|------|---------|--------------|
| [id] | [name] | [section] | [cause] |

| # | Action |
|---|--------|
| 1 | Keep orphans - Leave in main document |
| 2 | Remove orphans - Delete from main document |
| 3 | Recreate - Add to detail documents |
| 4 | Review each - Decide per item |

Select (1-4):
```

### 9. Preview Changes

Before applying, show complete preview:
```
**Preview: Changes to Main Document**

**Summary Table Updates:**
[Show rows being added/modified]

**Narrative Text Updates:**
[Show text changes if any]

| # | Action |
|---|--------|
| 1 | Apply all changes |
| 2 | Modify selections - go back |
| 3 | Cancel sync - proceed without changes |

Select (1-3):
```

### 10. Apply Sync Changes

If user confirms:
1. **Create backup** of current document state (optional)
2. **Apply each approved change** to main document
3. **Update summary tables** with new items
4. **Update narrative text** if needed
5. **Add change log entry:**
   ```
   | [date] | [contributor] | [role] | Synced documents: [n] added, [n] conflicts resolved, [n] orphans handled |
   ```
6. **Update review-state.json:**
   - `sync_completed: true`
   - `last_updated: [timestamp]`

### 11. Present MENU OPTIONS

Display: **Sync Complete - Select an Option:** [C] Continue to Section Review

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed when user selects 'C'
- User can chat or ask questions - always respond then redisplay menu

#### Menu Handling Logic:

- IF C: Update review-state.json, then load, read entire file, then execute `{nextStepFile}`
- IF Any other comments or queries: help user respond then redisplay menu

---

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN sync is complete (or skipped for no sync sections) and user selects C, will you:

1. Update review-state.json with `sync_completed: true`
2. Load, read entire file, then execute `{nextStepFile}` to begin section review

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- All sync-enabled sections processed
- User made informed decisions for each discrepancy
- Full item content shown for decisions (not just IDs)
- Changes applied correctly to main document
- Change log updated with sync summary
- review-state.json updated with sync completion

### SYSTEM FAILURE:

- Showing only IDs without full content for decisions
- Applying changes without user confirmation
- Not creating change log entry
- Skipping sync-enabled sections
- Modifying detail documents (this step only modifies main doc)

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
