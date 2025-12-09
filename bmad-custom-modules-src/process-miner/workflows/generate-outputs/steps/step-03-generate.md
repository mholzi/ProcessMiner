---
name: 'step-03-generate'
description: 'Generate the management summary document from extracted data'

# Path Definitions
workflow_path: '{module_root}/workflows/generate-outputs'
module_root: '{project-root}/bmad-custom-modules-src/process-miner'

# File References
thisStepFile: '{workflow_path}/steps/step-03-generate.md'
nextStepFile: '{workflow_path}/steps/step-04-review.md'
workflowFile: '{workflow_path}/workflow.md'

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.md'
partyModeWorkflow: '{project-root}/.bmad/core/workflows/party-mode/workflow.md'
---

# Step 3: Generate Management Summary

## STEP GOAL:

To generate the complete management summary document by populating the template with extracted and validated data, creating a polished Amazon 6-Pager ready for executive review.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input for subjective sections
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step, ensure entire file is read first
- 📋 YOU ARE A FACILITATOR using validated data, not inventing content

### Role Reinforcement:

- ✅ You are a document synthesizer and executive communication specialist
- ✅ Continue using the calling agent's communication style if available
- ✅ Apply Amazon 6-Pager writing principles throughout
- ✅ Focus on clarity, data-driven content, and actionable recommendations

### Step-Specific Rules:

- 🎯 Focus on DOCUMENT GENERATION using extracted data
- 🚫 FORBIDDEN to invent data not validated in step-02
- 🚫 FORBIDDEN to skip template sections
- 💬 Use professional executive language (document_output_language from config)
- 📊 Tables preferred over prose for data presentation

## EXECUTION PROTOCOLS:

- 🎯 Load the appropriate template
- 🎯 Populate all sections with extracted data
- 🎯 Apply Amazon 6-Pager writing principles
- 🎯 Generate complete document
- 💾 Create output file with proper frontmatter
- 🚫 FORBIDDEN to leave {{placeholder}} text in output

## CONTEXT BOUNDARIES:

- All extracted data from step-02 is available
- Template path from step-01 is available
- Document output language from config applies
- Update mode ('full', 'incremental', or new) is known

---

## GENERATION SEQUENCE:

### 1. Load Template

Load the management summary template:
- Path: `{template_path}` (set in step-01)

Display:
"Loading template: {output_filename}
Generating management summary for: {current_process_name}
Mode: {update_mode or 'new'}"

### 2. Initialize Output Document

Create/update the output file at:
`{current_process_folder}/{output_filename}`

**Initialize frontmatter:**

```yaml
---
document_type: Management Summary (Amazon 6-Pager)
process_name: {current_process_name}
process_id: {current_process_id}
agent_type: {current_agent_id}
generated_date: {current_date}
source_document: {source_document_name}
source_modified: {source_document_modified}
version: {increment if update, else 1.0}
status: draft
stepsCompleted: [1, 2, 3]
lastStep: 'generate'
---
```

### 3. Generate Section Content

For each section, populate template with extracted data following Amazon 6-Pager principles.

---

#### Generate Section 1: Introduction

**Write to document:**

Using `{extracted_introduction}`:
- Populate background paragraph (write LAST after other sections are done)
- Fill scope table
- Add key definitions
- Set document purpose statement

**Amazon 6-Pager Principle Applied:**
- Self-sufficient context - reader unfamiliar with domain can understand
- Simplicity and ease of understanding
- No jargon without definition

---

#### Generate Section 2: Goals

**Write to document:**

Using `{extracted_goals}`:
- Create goals table with Baseline | Current | Target | Date columns
- Add success metrics bullets
- Ensure all metrics are SMART

**Amazon 6-Pager Principle Applied:**
- Goals are specific and measurable
- Clear success criteria
- Baseline establishes starting point

---

#### Generate Section 3: Tenets

**Write to document:**

Using `{extracted_tenets}`:
- List each principle with description
- Add constraints table
- Explain rationale for each tenet

**Amazon 6-Pager Principle Applied:**
- Tenets are guiding principles, not tactics
- Non-negotiable constraints are clear
- Values inform decision-making

---

#### Generate Section 4: State of the Business

**Write to document:**

Using `{extracted_state}`:
- Create key metrics summary table
- Write "What's Working" section
- Write "What's Not Working" section
- Create Top 5 critical items table
- Add supporting analysis tables

**Amazon 6-Pager Principle Applied:**
- Data-driven, not opinion-driven
- Current state clearly articulated
- Evidence supports every claim

---

#### Generate Section 5: Lessons Learned

**Write to document:**

Using `{extracted_lessons}`:
- Write "What Worked Well" section
- Write "What Did Not Work" section - with brutal honesty
- Create root cause analysis table
- Add key insights bullets

**Amazon 6-Pager Principle Applied:**
- Brutal honesty - no sugar-coating failures
- Root causes identified, not just symptoms
- Lessons are actionable, not just observations

---

#### Generate Section 6: Strategic Priorities

**Write to document:**

Using `{extracted_priorities}`:
- Create Priority 1, 2, 3 sections with full detail:
  - Objective
  - Rationale
  - Actions table
  - Success criteria
  - Risk if not addressed
- Create Quick Wins table
- Create Strategic Initiatives table
- Create Next Steps table with ownership

**Amazon 6-Pager Principle Applied:**
- Priorities are specific and actionable
- Clear ownership assigned
- Next steps have deadlines
- Recommendations are data-driven

---

#### Generate Appendix

**Write to document:**

Using `{extracted_appendix}`:
- Add complete registers (all items)
- Include Mermaid diagrams
- Add supporting data tables
- List source documents
- List contributors

**Amazon 6-Pager Principle Applied:**
- Appendix has no page limit
- Supporting evidence is comprehensive
- Main document stays focused

---

### 4. Apply Final Polish

After all sections generated:

**Writing Quality Check:**
- Professional language throughout
- Consistent terminology
- Active voice preferred
- No placeholder text remaining
- Tables properly formatted
- Mermaid diagrams valid

**Executive Communication Check:**
- Lead with "why" in each section
- Data anchors every claim
- Flow is logical: problem → context → solution → impact
- Next steps are clear and owned

### 5. Document Complete

Display generation summary:

"**Management Summary Generated**

📄 Document: {output_filename}
📍 Location: {current_process_folder}
📊 Sections: All 6 sections + Appendix
📝 Status: Draft (pending review)

**Content Summary:**
| Section | Content |
|---------|---------|
| Introduction | {element_count} elements |
| Goals | {metric_count} metrics with targets |
| Tenets | {principle_count} principles |
| State of Business | {metric_count} metrics, Top 5 items |
| Lessons Learned | {insight_count} insights |
| Strategic Priorities | 3 priorities, {quick_win_count} quick wins |
| Appendix | {appendix_item_count} supporting items |

**Next:** Review and finalize the document."

---

### 6. Present MENU OPTIONS

Display: "**Select an Option:**
[V] View Generated Document - See the full output
[A] Advanced Elicitation - Explore alternative approaches
[P] Party Mode - Get other agent perspectives
[C] Continue - Proceed to review and finalize"

#### Menu Handling Logic:

- IF V: Display the complete generated document, then redisplay menu
- IF A: Execute `{advancedElicitationTask}`, then redisplay menu
- IF P: Execute `{partyModeWorkflow}`, then redisplay menu
- IF C: Update frontmatter `stepsCompleted: [1, 2, 3]`, load, read entire file, then execute `{nextStepFile}`
- IF Any other comments or queries: help user respond then [Redisplay Menu Options](#6-present-menu-options)

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'
- After other menu items execution, return to this menu
- User can chat or ask questions - always respond and then redisplay menu

---

## SESSION VARIABLES SET BY THIS STEP

| Variable | Description |
|----------|-------------|
| `output_file_path` | Full path to generated document |
| `document_version` | Version number |
| `generation_complete` | Boolean - document fully generated |

---

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN user selects 'C' (Continue) AND document has been fully generated with no placeholder text, will you then update frontmatter to add step 3 to `stepsCompleted`, then load, read entire file, then execute `{nextStepFile}` to begin review and finalization.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Template loaded correctly
- All sections populated with extracted data
- No placeholder text remaining
- Amazon 6-Pager principles applied
- Document saved to correct location
- Frontmatter properly initialized
- Ready for review step

### ❌ SYSTEM FAILURE:

- Leaving {{placeholder}} text in output
- Skipping sections
- Inventing data not from step-02
- Not applying executive writing standards
- Saving to wrong location
- Missing frontmatter
- Not updating stepsCompleted

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
