---
name: 'step-04-review'
description: 'Review, edit, and finalize the management summary document'

# Path Definitions
workflow_path: '{module_root}/workflows/generate-outputs'
module_root: '{project-root}/bmad-custom-modules-src/process-miner'

# File References
thisStepFile: '{workflow_path}/steps/step-04-review.md'
workflowFile: '{workflow_path}/workflow.md'

# No nextStepFile - this is the final step

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.md'
partyModeWorkflow: '{project-root}/.bmad/core/workflows/party-mode/workflow.md'
---

# Step 4: Review & Finalize

## STEP GOAL:

To collaboratively review the generated management summary with the user, incorporate any edits or refinements, and finalize the document for executive distribution.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER finalize without explicit user approval
- 📖 CRITICAL: Read the complete step file before taking any action
- 📋 YOU ARE A FACILITATOR - user has final say on all content

### Role Reinforcement:

- ✅ You are a document synthesizer and executive communication specialist
- ✅ Continue using the calling agent's communication style if available
- ✅ Support the user in refining their document
- ✅ Offer suggestions but defer to user judgment

### Step-Specific Rules:

- 🎯 Focus on REVIEW and REFINEMENT
- 🚫 FORBIDDEN to finalize without user approval
- 🚫 FORBIDDEN to make substantive changes without user consent
- 💬 Be responsive to edit requests
- ✅ Ensure quality before finalization

## EXECUTION PROTOCOLS:

- 🎯 Present document for review
- 🎯 Support section-by-section editing
- 🎯 Apply requested changes immediately
- 🎯 Confirm finalization with user
- 💾 Update document status to 'final'
- 🎉 Complete workflow gracefully

## CONTEXT BOUNDARIES:

- Generated document from step-03 is available
- User may request edits to any section
- Final approval required before marking complete
- This is the final step - no next step

---

## REVIEW SEQUENCE:

### 1. Present Review Overview

Display:

"**Management Summary Ready for Review**

📄 Document: {output_filename}
📍 Location: {current_process_folder}
📊 Version: {document_version}
📝 Status: Draft

**Amazon 6-Pager Structure:**

| # | Section | Length | Status |
|---|---------|--------|--------|
| 1 | Introduction | ½–1 page | ✅ Generated |
| 2 | Goals | ½ page | ✅ Generated |
| 3 | Tenets | ½ page | ✅ Generated |
| 4 | State of the Business | 1 page | ✅ Generated |
| 5 | Lessons Learned | ½–1 page | ✅ Generated |
| 6 | Strategic Priorities | 2–3 pages | ✅ Generated |
| A | Appendix | Unlimited | ✅ Generated |

**Review Options:**
- Review full document
- Review specific section
- Make edits
- Approve and finalize"

---

### 2. Present REVIEW MENU

Display: "**Select Review Option:**
[F] Full Document - View entire management summary
[1-6] Section Review - View specific section (1=Intro, 2=Goals, etc.)
[X] Appendix - View appendix content
[E] Edit Section - Make changes to a section
[Q] Quality Check - Run final quality validation
[A] Advanced Elicitation - Explore alternatives
[P] Party Mode - Get other agent perspectives
[D] Done - Approve and finalize document"

#### Menu Handling Logic:

- IF F: Display full document, then redisplay menu
- IF 1-6: Display requested section, then redisplay menu
- IF X: Display appendix, then redisplay menu
- IF E: Execute [Edit Flow](#edit-flow), then redisplay menu
- IF Q: Execute [Quality Check](#quality-check), then redisplay menu
- IF A: Execute `{advancedElicitationTask}`, then redisplay menu
- IF P: Execute `{partyModeWorkflow}`, then redisplay menu
- IF D: Execute [Finalization Flow](#finalization-flow)
- IF Any other comments or queries: help user respond then [Redisplay Menu Options](#2-present-review-menu)

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY finalize when user selects 'D' (Done)
- After other menu items execution, return to this menu
- User can chat or ask questions - always respond and then redisplay menu

---

### Edit Flow

When user selects [E] Edit Section:

**Step E1: Identify Section**

Ask: "Which section would you like to edit?
1. Introduction
2. Goals
3. Tenets
4. State of the Business
5. Lessons Learned
6. Strategic Priorities
A. Appendix"

**Step E2: Display Current Content**

Show the current content of the selected section.

**Step E3: Gather Edit Instructions**

Ask: "What changes would you like to make to this section?

You can:
- Provide replacement text
- Describe changes to make
- Ask me to rephrase something
- Add or remove content"

**Step E4: Apply Edits**

Make the requested changes and display the updated section.

**Step E5: Confirm Edit**

Ask: "Here's the updated section. Does this look correct?
[Y] Yes, save changes
[N] No, let me try again
[R] Revert to original"

If Y: Save changes to document, display confirmation
If N: Return to Step E3
If R: Restore original content, display confirmation

Return to main review menu.

---

### Quality Check

When user selects [Q] Quality Check:

Run validation against Amazon 6-Pager standards:

**Checklist:**

```
AMAZON 6-PAGER QUALITY CHECK
═══════════════════════════════════════════════════════════

STRUCTURE
□ All 6 sections present
□ Section lengths within guidelines
□ Appendix properly separated

CONTENT QUALITY
□ Introduction provides sufficient context
□ Goals have baseline, current, and target values
□ Tenets are guiding principles (not tactics)
□ State of Business is data-driven
□ Lessons Learned are brutally honest
□ Strategic Priorities have clear ownership

WRITING STANDARDS
□ Professional language throughout
□ Active voice preferred
□ No jargon without definition
□ Tables used for data (not prose)
□ No placeholder text remaining

EXECUTIVE READINESS
□ Lead with "why" in each section
□ Data anchors every claim
□ Flow: problem → context → solution → impact
□ Next steps are clear and owned
□ Ready for 20-30 minute silent read

═══════════════════════════════════════════════════════════
RESULT: {PASS/ITEMS TO ADDRESS}
═══════════════════════════════════════════════════════════
```

Display results and any items needing attention.

Return to main review menu.

---

### Finalization Flow

When user selects [D] Done:

**Step D1: Final Confirmation**

Display:

"**Ready to Finalize**

You are about to finalize this management summary:

📄 Document: {output_filename}
📍 Location: {current_process_folder}
📊 Version: {document_version} → {new_version}
📝 Status: Draft → **Final**

**This will:**
- Mark the document as finalized
- Update the version number
- Record completion timestamp
- Update document metadata

**Confirm:** Are you ready to finalize this management summary?
[Y] Yes, finalize now
[N] No, continue reviewing"

**Step D2: Process Finalization**

If user confirms [Y]:

1. **Update document frontmatter:**
```yaml
status: final
version: {incremented_version}
finalized_date: {current_date}
finalized_by: {contributor_name}
stepsCompleted: [1, 2, 3, 4]
lastStep: 'complete'
```

2. **Save document**

3. **Display completion message:**

"
═══════════════════════════════════════════════════════════
✅ MANAGEMENT SUMMARY FINALIZED
═══════════════════════════════════════════════════════════

📄 Document: {output_filename}
📍 Location: {current_process_folder}
📊 Version: {new_version}
📅 Finalized: {current_date}

**Your management summary is ready for executive review.**

Remember the Amazon 6-Pager meeting format:
• Distribute document before the meeting
• Executives read in silence for 20-30 minutes
• Discussion follows the reading
• Appendix provides deep-dive material

**Source Document:** {source_document_name}
**Generated By:** ProcessMiner {current_agent_id}

Thank you for using ProcessMiner! 🎉
═══════════════════════════════════════════════════════════
"

**WORKFLOW COMPLETE**

---

## SESSION VARIABLES SET BY THIS STEP

| Variable | Description |
|----------|-------------|
| `review_complete` | Boolean - review process finished |
| `document_finalized` | Boolean - document marked final |
| `final_version` | Final version number |
| `finalized_date` | Completion timestamp |

---

## CRITICAL STEP COMPLETION NOTE

This is the **FINAL STEP** of the workflow.

The workflow completes when:
1. User selects [D] Done
2. User confirms [Y] finalization
3. Document frontmatter updated to 'final' status
4. Completion message displayed

There is no next step - workflow ends here.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Document presented for review
- User able to view any section
- Edits applied correctly when requested
- Quality check available
- Finalization requires explicit approval
- Document properly marked as final
- Workflow completes gracefully with confirmation

### ❌ SYSTEM FAILURE:

- Finalizing without user approval
- Not saving edit changes
- Skipping confirmation step
- Not updating frontmatter on finalization
- Abrupt workflow ending without completion message
- Leaving document in 'draft' status after finalization

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.

---

## WORKFLOW COMPLETE

When this step completes successfully, the entire Generate Management Summary workflow is complete. The user has a finalized Amazon 6-Pager management summary ready for executive distribution.
