# Review Draft Workflow - Validation Checklist

Use this checklist to validate the review-draft workflow implementation and execution.

## Pre-Review Checks

- [ ] Document path is valid and file exists
- [ ] Document is readable markdown format
- [ ] Schema resolution chain executed (frontmatter → local → auto-discovery)
- [ ] Contributor name and role collected
- [ ] review-state.json initialized with all sections

## Schema Resolution Checks

- [ ] Frontmatter `template:` field checked first
- [ ] Local `schema.yaml` checked second (override)
- [ ] Auto-discovery mode used as fallback
- [ ] Schema mode correctly recorded in review-state.json
- [ ] Sync-enabled sections identified (if schema present)

## Session Continuation Checks

- [ ] Existing review-state.json detected correctly
- [ ] Session status displayed accurately
- [ ] Contributor verification performed
- [ ] Resume point determined correctly
- [ ] User given clear continuation options

## Document Sync Checks (if applicable)

- [ ] Only sync-enabled sections processed
- [ ] Detail documents loaded correctly
- [ ] New items shown with full content (not just IDs)
- [ ] Orphaned items identified
- [ ] Conflicts presented with both versions
- [ ] User decisions collected before applying changes
- [ ] Change log updated with sync summary
- [ ] review-state.json updated with sync_completed: true

## Section Review Checks

- [ ] Subsections reviewed one at a time (never all at once)
- [ ] Confidence score calculated before each subsection
- [ ] Clarification questions generated when confidence < 90%
- [ ] Standard 5-option menu used consistently
- [ ] No emojis used in output
- [ ] Before/after shown for all corrections
- [ ] Progress saved to review-state.json after each subsection
- [ ] Section status updated correctly

## Confidence Scoring Checks

- [ ] Completeness factors assessed (50% weight)
  - [ ] Required fields populated (no TBD, Unknown, TODO)
  - [ ] Sufficient detail depth
  - [ ] Cross-references present where expected
  - [ ] No incomplete sentences
- [ ] Accuracy factors assessed (50% weight)
  - [ ] Consistency with other sections
  - [ ] Terminology matches defined terms
  - [ ] Referenced IDs exist
  - [ ] Logical flow and coherence

## Correction Quality Checks

- [ ] Minor corrections preserve context
- [ ] Before/after diff shown clearly
- [ ] User confirms each correction
- [ ] Corrections tracked with contributor attribution
- [ ] Document updated immediately after confirmation

## Change Log Checks

- [ ] Change log entry includes date
- [ ] Change log entry includes contributor name
- [ ] Change log entry includes contributor role
- [ ] Change log entry summarizes changes made
- [ ] Change log appended (not overwritten)
- [ ] User approves entry before appending

## Summary Checks

- [ ] Statistics calculated correctly from review-state.json
- [ ] Confidence changes compared (before vs after)
- [ ] All sections accounted for in summary
- [ ] Export options offered
- [ ] Export files contain accurate data
- [ ] review-state.json marked as completed

## Data Integrity Checks

- [ ] Document structure preserved
- [ ] Section line numbers accurate
- [ ] Cross-references not broken
- [ ] Structured IDs (PS#, PP#, etc.) intact
- [ ] Document formatting preserved
- [ ] review-state.json consistent with document state

## User Experience Checks

- [ ] Clear instructions at each step
- [ ] Progress visible throughout workflow
- [ ] Commands (back, jump, status, save, help) work correctly
- [ ] Errors handled gracefully with recovery options
- [ ] Session can be paused and resumed successfully

## Template-Agnostic Validation

- [ ] Works with document that has no schema
- [ ] Works with document that has frontmatter template reference
- [ ] Works with document that has local schema.yaml
- [ ] Sections discovered dynamically from ## headers
- [ ] No hardcoded section names in workflow logic
