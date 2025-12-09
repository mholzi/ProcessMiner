---
name: 'capture-item'
description: 'Atomic workflow for capturing structured items with IDs and cross-references'
version: '1.0.0'
type: 'atomic-primitive'
status: 'active'

# Interface Contract
requires:
  - item_type: 'enum[exception, pain_point, control_point, system, enhancement_idea, innovation_idea, market_trend, regulation]'
  - mode: 'enum[create, edit, enhance]'

provides:
  - captured_item: 'object with id, structured fields, links'
  - updated_files: 'array of modified file paths'

# Session Variables (set by upstream)
# - contributor_name, contributor_role: Set by agent activation
# - current_process_id, current_process_name, current_process_folder: Set by select-existing-process workflow

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/shared/capture-item'

# Process selection - use shared workflow
select_process_workflow: '{module_root}/workflows/shared/select-existing-process/workflow.md'

# Shared Protocols
protocolsFile: '{module_root}/workflows/shared/protocols/protocols.md'

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
partyModeWorkflow: '{project-root}/.bmad/core/workflows/party-mode/workflow.md'
brainstormingWorkflow: '{project-root}/.bmad/core/workflows/brainstorming-session/workflow.md'

# Item Type Configuration
item_configs:
  exception:
    id_prefix: 'EX'
    detail_file: 'exceptions-detail.md'
    main_doc_section: 'Process Exceptions'
    fields:
      - name: 'frequency'
        type: 'enum[RARE, OCCASIONAL, FREQUENT]'
        required: true
      - name: 'handling_procedure'
        type: 'string'
        required: true
      - name: 'trigger_condition'
        type: 'string'
        required: false

  pain_point:
    id_prefix: 'PP'
    detail_file: 'pain-points-detail.md'
    main_doc_section: 'Pain Points & Challenges'
    fields:
      - name: 'severity'
        type: 'enum[HIGH, MEDIUM, LOW]'
        required: true
      - name: 'impact'
        type: 'string'
        required: true
      - name: 'root_cause'
        type: 'string'
        required: false

  control_point:
    id_prefix: 'CP'
    detail_file: 'control-points-detail.md'
    main_doc_section: 'Controls & Compliance'
    fields:
      - name: 'control_type'
        type: 'enum[PREVENTIVE, DETECTIVE, CORRECTIVE]'
        required: true
      - name: 'requirement_source'
        type: 'string'
        required: true
      - name: 'control_owner'
        type: 'string'
        required: true
      - name: 'testing_frequency'
        type: 'string'
        required: false

  system:
    id_prefix: 'SYS'
    detail_file: null
    main_doc_section: 'System Dependencies'
    fields:
      - name: 'system_type'
        type: 'enum[CORE, SUPPORTING, EXTERNAL]'
        required: true
      - name: 'vendor'
        type: 'string'
        required: false
      - name: 'integration_status'
        type: 'enum[INTEGRATED, MANUAL, HYBRID]'
        required: true

  innovation_idea:
    id_prefix: 'II'
    detail_file: 'innovation-ideas-detail.md'
    main_doc_section: 'Innovation Backlog'
    fields:
      - name: 'category'
        type: 'enum[PROCESS, TECHNOLOGY, BUSINESS_MODEL, CUSTOMER_EXPERIENCE]'
        required: true
      - name: 'source'
        type: 'enum[MARKET_TREND, COMPETITOR, INTERNAL, CUSTOMER_FEEDBACK]'
        required: true
      - name: 'strategic_fit'
        type: 'enum[HIGH, MEDIUM, LOW]'
        required: true
      - name: 'feasibility_score'
        type: 'number'
        required: false

  market_trend:
    id_prefix: 'TR'
    detail_file: 'market-trends-detail.md'
    main_doc_section: 'Market Trends'
    fields:
      - name: 'trend_category'
        type: 'enum[TECHNOLOGY, REGULATORY, MARKET, CUSTOMER_BEHAVIOR]'
        required: true
      - name: 'maturity'
        type: 'enum[EMERGING, GROWING, MATURE, DECLINING]'
        required: true
      - name: 'relevance'
        type: 'enum[HIGH, MEDIUM, LOW]'
        required: true
      - name: 'impact_potential'
        type: 'enum[TRANSFORMATIVE, SIGNIFICANT, MODERATE, MINIMAL]'
        required: false

  enhancement_idea:
    id_prefix: 'EI'
    detail_file: 'enhancement-ideas-detail.md'
    main_doc_section: 'Enhancement Ideas'
    fields:
      - name: 'enhancement_type'
        type: 'enum[AUTOMATION, OPTIMIZATION, INTEGRATION, UX_IMPROVEMENT]'
        required: true
      - name: 'complexity'
        type: 'enum[LOW, MEDIUM, HIGH]'
        required: true
      - name: 'expected_benefit'
        type: 'string'
        required: true

  regulation:
    id_prefix: 'REG'
    detail_file: 'regulations-detail.md'
    main_doc_section: 'Regulatory Requirements'
    fields:
      - name: 'regulation_type'
        type: 'enum[COMPLIANCE, REPORTING, OPERATIONAL, DATA_PROTECTION]'
        required: true
      - name: 'authority'
        type: 'string'
        required: true
      - name: 'compliance_status'
        type: 'enum[COMPLIANT, PARTIAL, NON_COMPLIANT, NOT_ASSESSED]'
        required: true
      - name: 'deadline'
        type: 'string'
        required: false
---

# Capture Item Workflow

## PURPOSE

This atomic workflow captures a single structured item (exception, pain point, control, or system) with:
- Unique ID assignment
- Type-specific field capture
- Process step cross-references
- Confidence assessment
- Y/E/R approval with Rewrite sub-menu

## MANDATORY EXECUTION RULES

### Universal Rules:
- **NEVER** generate content without user input
- YOU ARE A FACILITATOR, not a content generator
- Narrative-first approach — let user describe in their words
- Extract structured data from narrative
- IMPORTANT: `contributor_name` and `contributor_role` are already set by agent activation - DO NOT ask again

### Role Reinforcement:
- Continue using established persona from parent workflow
- Maintain professional, supportive tone
- Collaborative dialogue — you bring documentation expertise

---

## INITIALIZATION SEQUENCE

### 1. Process Selection (Shared Workflow)

If `current_process_folder` is not already set by a calling workflow:
- Load, read and execute `{select_process_workflow}` to select process
- Set session variables: `current_process_id`, `current_process_name`, `current_process_folder`

Note: `contributor_name` and `contributor_role` are already set by agent activation.

### 2. Execute Capture

After process is selected, proceed to execution sequence.

---

## EXECUTION SEQUENCE

### 1. Initialize Based on Item Type

```
<action>Load item configuration from item_configs.{{item_type}}</action>
<action>Set id_prefix = {{item_config.id_prefix}}</action>
<action>Set detail_file = {{item_config.detail_file}}</action>
<action>Load existing items to determine next sequence number</action>
```

### 2. Gather Narrative (Facilitator Mode)

```
<format>
Tell me about this {{item_type_display}} in your own words.
What happens? When does it occur? What's the impact?
</format>

<capture response="narrative_description">
  Allow free-form description from SME
</capture>
```

### 3. Extract Structured Data

```
<action>From narrative, extract:
  - name: Short descriptive name (3-5 words)
  - description: Full description preserving SME's words
</action>

<action>Generate ID: {{id_prefix}}-{{process_abbrev}}-{{next_sequence}}</action>
```

### 4. Capture Type-Specific Fields

```
<check if="item_type == 'exception'">
  <ask response="frequency">
  How often does this exception occur?
  - **[R] Rare** — Less than once a month
  - **[O] Occasional** — A few times a month
  - **[F] Frequent** — Weekly or more often
  </ask>

  <ask response="handling_procedure">
  What's the procedure when this exception occurs?
  </ask>
</check>

<check if="item_type == 'pain_point'">
  <ask response="severity">
  How severe is this pain point?
  - **[H] High** — Major impact on efficiency/quality
  - **[M] Medium** — Noticeable but manageable
  - **[L] Low** — Minor inconvenience
  </ask>

  <ask response="impact">
  What's the business impact of this pain point?
  </ask>
</check>

<check if="item_type == 'control_point'">
  <ask response="control_type">
  What type of control is this?
  - **[P] Preventive** — Stops issues before they happen
  - **[D] Detective** — Identifies issues when they occur
  - **[C] Corrective** — Fixes issues after they're found
  </ask>

  <ask response="requirement_source">
  What regulatory requirement or policy does this control address?
  (e.g., SOX, BSA/AML, internal policy #)
  </ask>

  <ask response="control_owner">
  Who owns this control? (Role or department)
  </ask>
</check>

<check if="item_type == 'system'">
  <ask response="system_type">
  What type of system is this?
  - **[C] Core** — Primary system for this process
  - **[S] Supporting** — Helps but not essential
  - **[E] External** — Third-party or outside system
  </ask>

  <ask response="integration_status">
  How does this system integrate with the process?
  - **[I] Integrated** — Fully automated data flow
  - **[M] Manual** — Manual data entry/export
  - **[H] Hybrid** — Mix of automated and manual
  </ask>
</check>

<check if="item_type == 'innovation_idea'">
  <ask response="category">
  What category of innovation is this?
  - **[P] Process** — Improves how work gets done
  - **[T] Technology** — New tech enablement or modernization
  - **[B] Business Model** — Changes revenue, pricing, or market approach
  - **[C] Customer Experience** — Enhances client interaction or satisfaction
  </ask>

  <ask response="source">
  Where did this innovation idea come from?
  - **[M] Market Trend** — Identified from industry trends
  - **[C] Competitor** — Observed from competitor analysis
  - **[I] Internal** — Suggested by staff or leadership
  - **[F] Customer Feedback** — Requested or implied by customers
  </ask>

  <ask response="strategic_fit">
  How well does this align with strategic priorities?
  - **[H] High** — Directly supports key strategic objectives
  - **[M] Medium** — Supports strategy indirectly
  - **[L] Low** — Nice to have, not strategically critical
  </ask>
</check>

<check if="item_type == 'market_trend'">
  <ask response="trend_category">
  What category is this trend?
  - **[T] Technology** — Emerging tech or digital transformation
  - **[R] Regulatory** — New regulations or compliance requirements
  - **[M] Market** — Industry or competitive dynamics
  - **[C] Customer Behavior** — Changing customer expectations
  </ask>

  <ask response="maturity">
  What's the maturity level of this trend?
  - **[E] Emerging** — Early stage, few adopters
  - **[G] Growing** — Gaining traction, increasing adoption
  - **[M] Mature** — Widely adopted, proven
  - **[D] Declining** — Past peak, being replaced
  </ask>

  <ask response="relevance">
  How relevant is this trend to our organization?
  - **[H] High** — Directly impacts our business
  - **[M] Medium** — Indirect or future impact
  - **[L] Low** — Minimal relevance currently
  </ask>
</check>

<check if="item_type == 'enhancement_idea'">
  <ask response="enhancement_type">
  What type of enhancement is this?
  - **[A] Automation** — Automate manual tasks
  - **[O] Optimization** — Improve efficiency of existing process
  - **[I] Integration** — Connect systems or data flows
  - **[U] UX Improvement** — Better user/staff experience
  </ask>

  <ask response="complexity">
  What's the implementation complexity?
  - **[L] Low** — Simple change, minimal effort
  - **[M] Medium** — Moderate effort and coordination
  - **[H] High** — Significant effort, multiple dependencies
  </ask>

  <ask response="expected_benefit">
  What's the expected benefit of this enhancement?
  </ask>
</check>

<check if="item_type == 'regulation'">
  <ask response="regulation_type">
  What type of regulatory requirement is this?
  - **[C] Compliance** — Mandatory regulatory compliance
  - **[R] Reporting** — Reporting and disclosure requirements
  - **[O] Operational** — Operational requirements
  - **[D] Data Protection** — Privacy and data handling
  </ask>

  <ask response="authority">
  Which regulatory authority or standard requires this?
  (e.g., OCC, FDIC, SEC, GDPR, SOX, PCI-DSS)
  </ask>

  <ask response="compliance_status">
  What's the current compliance status?
  - **[C] Compliant** — Fully meeting requirements
  - **[P] Partial** — Partially compliant, gaps exist
  - **[N] Non-Compliant** — Not meeting requirements
  - **[A] Not Assessed** — Status unknown
  </ask>
</check>
```

### 5. Link to Process Steps

```
<action>Load process_steps from structured-data.json</action>

<format>
Which process step(s) does this {{item_type_display}} relate to?

{{foreach ps in process_steps}}
- [ ] **{{ps.id}}**: {{ps.name}}
{{/foreach}}

Select all that apply (comma-separated numbers or IDs):
</format>

<capture response="linked_steps">
  Parse selected process step IDs
</capture>
```

### 6. Set Confidence Level

```
<ask response="confidence">
How confident are you in this information?
- **[H] High** — Verified, documented, or certain
- **[M] Medium** — Based on experience, likely accurate
- **[L] Low** — Uncertain, needs verification
</ask>
```

### 7. Present Draft for Approval

```
<action>Compose structured item:
  {
    "id": "{{generated_id}}",
    "name": "{{extracted_name}}",
    "description": "{{narrative_description}}",
    {{type_specific_fields}},
    "links": {
      "process_steps": [{{linked_steps}}]
    },
    "confidence": "{{confidence}}"
  }
</action>

<invoke-protocol name="adaptive_approval">
  <param name="content_type">{{item_type_display}}</param>
  <param name="content">{{formatted_item_display}}</param>
</invoke-protocol>
```

### 8. Handle Approval Response

```
<handle option="Y">
  <action>Mark item as approved</action>
  <action>Proceed to file updates</action>
</handle>

<handle option="E">
  <ask>What would you like to change?</ask>
  <action>Apply edits</action>
  <action>Return to step 7 for re-approval</action>
</handle>

<handle option="R">
  <display>
  **Rewrite Options:**
  - **[A] Advanced Elicitation** — Use structured techniques
  - **[P] Party Mode** — Get multiple AI perspectives
  - **[B] Brainstorming** — Creative exploration
  - **[Q] Quick Questions** — Targeted clarification
  - **[X] Back** — Return to approval menu
  </display>

  <handle option="A">
    <action>Load {advancedElicitationTask}</action>
    <action>Execute with item context</action>
    <action>Return to step 7 with refined content</action>
  </handle>

  <handle option="P">
    <action>Load {partyModeWorkflow}</action>
    <action>Execute with item as topic</action>
    <action>Return to step 7 with consensus</action>
  </handle>

  <handle option="B">
    <action>Load {brainstormingWorkflow}</action>
    <action>Execute with item context</action>
    <action>Return to step 7 with ideas incorporated</action>
  </handle>

  <handle option="Q">
    <action>Generate 3-5 targeted questions based on gaps</action>
    <action>Collect answers</action>
    <action>Return to step 7 with refined content</action>
  </handle>
</handle>
```

### 9. Update Output Files (Silent)

```
<action silent="true">Update {current_process_folder}/structured-data.json:
  - Add item to appropriate array (exceptions, pain_points, controls, systems)
  - Update session.checkpoint.last_item_id = {{generated_id}}
  - Update session.last_updated = {{timestamp}}
</action>

<check if="detail_file != null">
  <action silent="true">Update {current_process_folder}/{{detail_file}}:
    - Add item entry with full details
    - Include cross-references to PS# IDs
  </action>
</check>

<action silent="true">Update {current_process_folder}/as-is-process-documentation.md:
  - Add item to appropriate section
  - Include ID and brief description
</action>
```

### 10. Return to Caller

```
<output>
  captured_item: {{structured_item}}
  updated_files: [
    "structured-data.json",
    {{if detail_file}}"{{detail_file}}",{{/if}}
    "as-is-process-documentation.md"
  ]
</output>
```

---

## ITEM DISPLAY FORMATS

### Exception Display
```
**{{id}}: {{name}}**
- **Frequency:** {{frequency}}
- **Description:** {{description}}
- **Handling:** {{handling_procedure}}
- **Related Steps:** {{linked_steps}}
- **Confidence:** {{confidence}}
```

### Pain Point Display
```
**{{id}}: {{name}}**
- **Severity:** {{severity}}
- **Description:** {{description}}
- **Impact:** {{impact}}
- **Related Steps:** {{linked_steps}}
- **Confidence:** {{confidence}}
```

### Control Point Display
```
**{{id}}: {{name}}**
- **Type:** {{control_type}}
- **Description:** {{description}}
- **Requirement:** {{requirement_source}}
- **Owner:** {{control_owner}}
- **Related Steps:** {{linked_steps}}
- **Confidence:** {{confidence}}
```

### System Display
```
**{{id}}: {{name}}**
- **Type:** {{system_type}}
- **Integration:** {{integration_status}}
- **Description:** {{description}}
- **Related Steps:** {{linked_steps}}
- **Confidence:** {{confidence}}
```

### Innovation Idea Display
```
**{{id}}: {{name}}**
- **Category:** {{category}}
- **Source:** {{source}}
- **Description:** {{description}}
- **Strategic Fit:** {{strategic_fit}}
- **Related Steps:** {{linked_steps}}
- **Confidence:** {{confidence}}
```

### Market Trend Display
```
**{{id}}: {{name}}**
- **Category:** {{trend_category}}
- **Maturity:** {{maturity}}
- **Relevance:** {{relevance}}
- **Description:** {{description}}
- **Impact Potential:** {{impact_potential}}
- **Related Steps:** {{linked_steps}}
- **Confidence:** {{confidence}}
```

### Enhancement Idea Display
```
**{{id}}: {{name}}**
- **Type:** {{enhancement_type}}
- **Complexity:** {{complexity}}
- **Description:** {{description}}
- **Expected Benefit:** {{expected_benefit}}
- **Related Steps:** {{linked_steps}}
- **Confidence:** {{confidence}}
```

### Regulation Display
```
**{{id}}: {{name}}**
- **Type:** {{regulation_type}}
- **Authority:** {{authority}}
- **Status:** {{compliance_status}}
- **Description:** {{description}}
- **Deadline:** {{deadline}}
- **Related Steps:** {{linked_steps}}
- **Confidence:** {{confidence}}
```

---

## SUCCESS/FAILURE METRICS

### SUCCESS:
- Item captured with unique ID
- All required fields populated
- Linked to at least one PS# ID
- Approved via Y/E/R pattern
- All output files updated consistently

### FAILURE:
- Generated content without user input
- Missing required fields
- No process step links
- Files updated inconsistently
- Skipped approval step
