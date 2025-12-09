# Shared Protocols for Process Miner Workflows

## Overview

This file contains reusable protocol definitions used across Process Miner workflows. These protocols ensure consistent behavior for option generation, item capture, and content approval.

---

## Protocol: smart_options

**Purpose:** Generate contextual options based on process context and banking domain knowledge.

### Parameters
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| question | string | Yes | The question to present to the user |
| context | string | Yes | Current process context for option generation |
| option_type | enum | Yes | Type of options: `exception`, `pain_point`, `control`, `system`, `process_step` |

### Behavior

```
<protocol name="smart_options">
  <input>
    - question: The question to ask
    - context: Process name and context
    - option_type: Type of item being captured
  </input>

  <action>Generate 3-5 contextual options based on:
    - Banking/financial services domain knowledge
    - Common patterns for the option_type
    - The specific process context provided
  </action>

  <format>
  {{question}}

  Based on similar banking processes, common {{option_type}}s include:
  {{foreach option in generated_options}}
  - [ ] {{option.name}} — {{option.brief_description}}
  {{/foreach}}
  - [ ] Other — I'll describe something different

  Select all that apply, or describe your own:
  </format>

  <output>
    - selected_options: Array of selected items
    - custom_input: Any custom text provided
  </output>
</protocol>
```

### Example Usage

```
<invoke-protocol name="smart_options">
  <param name="question">What exceptions can occur during this process?</param>
  <param name="context">Client Account Opening</param>
  <param name="option_type">exception</param>
</invoke-protocol>
```

---

## Protocol: capture_structured_items

**Purpose:** Iteratively capture structured items with unique IDs and cross-references.

### Parameters
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| item_type | enum | Yes | Type: `exception`, `pain_point`, `control`, `system` |
| id_prefix | string | Yes | ID prefix: `EX`, `PP`, `CP`, `SYS` |
| process_steps | array | No | Available PS# IDs for linking |

### Behavior

```
<protocol name="capture_structured_items">
  <input>
    - item_type: Type of item being captured
    - id_prefix: Prefix for generated IDs
    - process_steps: Available process step IDs for cross-referencing
  </input>

  <loop name="item_capture" until="user indicates done">
    <step name="gather_narrative">
      <ask>Tell me about this {{item_type}} in your own words.</ask>
      <capture>narrative_description</capture>
    </step>

    <step name="extract_structured">
      <action>From the narrative, extract:
        - name: Short descriptive name (3-5 words)
        - description: Full description from narrative
        - Type-specific fields based on item_type
      </action>
    </step>

    <step name="assign_id">
      <action>Generate ID: {{id_prefix}}-{{process_abbrev}}-{{sequence_number}}</action>
    </step>

    <step name="link_process_steps">
      <ask>Which process step(s) does this {{item_type}} relate to?
      {{foreach ps in process_steps}}
      - [ ] {{ps.id}}: {{ps.name}}
      {{/foreach}}
      </ask>
      <capture>linked_process_steps</capture>
    </step>

    <step name="set_confidence">
      <ask>How confident are you in this information?
      - [H] High — Verified/documented
      - [M] Medium — Based on experience
      - [L] Low — Uncertain/needs verification
      </ask>
      <capture>confidence_level</capture>
    </step>

    <step name="present_for_approval">
      <invoke-protocol name="adaptive_approval">
        <param name="content_type">{{item_type}}</param>
        <param name="content">{{structured_item}}</param>
      </invoke-protocol>
    </step>
  </loop>

  <output>
    - captured_items: Array of structured items with IDs
    - total_count: Number of items captured
  </output>
</protocol>
```

### Type-Specific Fields

| item_type | Additional Fields |
|-----------|-------------------|
| exception | frequency (RARE/OCCASIONAL/FREQUENT), handling_procedure |
| pain_point | severity (HIGH/MEDIUM/LOW), impact, root_cause |
| control | control_type (PREVENTIVE/DETECTIVE/CORRECTIVE), requirement_source, control_owner |
| system | system_type (CORE/SUPPORTING/EXTERNAL), integration_status, vendor |

---

## Protocol: adaptive_approval

**Purpose:** Present content for approval using the Y/E/R pattern with Rewrite sub-menu.

### Parameters
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| content_type | string | Yes | Type of content being approved |
| content | object | Yes | The content to display for approval |
| allow_rewrite | boolean | No | Enable Rewrite sub-menu (default: true) |

### Behavior

```
<protocol name="adaptive_approval">
  <input>
    - content_type: Description of what's being approved
    - content: Formatted content to display
    - allow_rewrite: Whether to show Rewrite option
  </input>

  <display>
  ---
  **{{content_type}} - Draft:**

  {{content}}

  ---
  How would you like to proceed?
  - **[Y] Yes, Accept** — This accurately captures the {{content_type}}
  - **[E] Edit** — I have minor corrections to make
  {{if allow_rewrite}}
  - **[R] Rewrite** — Let's redraft this together using AI-assisted techniques
  {{/if}}
  </display>

  <handle option="Y">
    <action>Mark content as approved</action>
    <action>Save to structured data with confidence level</action>
    <output>approval_status: "accepted"</output>
  </handle>

  <handle option="E">
    <ask>What would you like to change?</ask>
    <action>Apply user's edits to content</action>
    <action>Re-display for approval (recursive)</action>
  </handle>

  <handle option="R">
    <display>
    **Rewrite Options:**
    - **[A] Advanced Elicitation** — Structured techniques (5 Whys, SIPOC, etc.)
    - **[P] Party Mode** — Multiple AI perspectives discuss
    - **[B] Brainstorming** — Creative exploration session
    - **[Q] Quick Questions** — Targeted clarifying questions
    - **[X] Back** — Return to approval menu
    </display>

    <handle option="A">
      <action>Load and execute {advancedElicitationTask}</action>
      <action>Apply results and re-display for approval</action>
    </handle>

    <handle option="P">
      <action>Load and execute {partyModeWorkflow}</action>
      <action>Apply consensus and re-display for approval</action>
    </handle>

    <handle option="B">
      <action>Load and execute {brainstormingWorkflow}</action>
      <action>Apply ideas and re-display for approval</action>
    </handle>

    <handle option="Q">
      <action>Generate 3-5 targeted questions based on content gaps</action>
      <action>Collect answers and refine content</action>
      <action>Re-display for approval</action>
    </handle>

    <handle option="X">
      <action>Return to main approval menu</action>
    </handle>
  </handle>
</protocol>
```

---

## Protocol: display_progress

**Purpose:** Show consistent progress indicators across workflow steps.

### Parameters
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| current_step | number | Yes | Current step number |
| total_steps | number | Yes | Total number of steps |
| step_name | string | Yes | Name of current step |

### Behavior

```
<protocol name="display_progress">
  <format>
  **Progress: Step {{current_step}} of {{total_steps}} - {{step_name}}**
  </format>
</protocol>
```

---

## Protocol: save_checkpoint

**Purpose:** Save session state for resume capability.

### Parameters
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| step | number | Yes | Current step number |
| last_item_id | string | No | Last captured item ID |
| structured_data_file | path | Yes | Path to structured-data.json |

### Behavior

```
<protocol name="save_checkpoint">
  <action silent="true">
    Update {{structured_data_file}}:
    - session.checkpoint.step = {{step}}
    - session.checkpoint.last_item_id = {{last_item_id}}
    - session.last_updated = {{current_timestamp}}
  </action>
</protocol>
```

---

## Protocol: load_checkpoint

**Purpose:** Load session state for workflow resumption.

### Parameters
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| structured_data_file | path | Yes | Path to structured-data.json |

### Behavior

```
<protocol name="load_checkpoint">
  <action>Read {{structured_data_file}}</action>

  <output>
    - checkpoint_step: Last completed step
    - last_item_id: Last captured item ID
    - session_data: Full session context
  </output>
</protocol>
```

---

## Usage Notes

### Loading Protocols
All workflow steps should reference protocols via:
```yaml
protocolsFile: '{module_root}/workflows/shared/protocols/protocols.md'
```

### Invoking Protocols
```
<invoke-protocol name="protocol_name">
  <param name="param1">value1</param>
  <param name="param2">value2</param>
</invoke-protocol>
```

### Extending Protocols
To add new protocols:
1. Define protocol name and purpose
2. Specify input parameters with types
3. Define behavior using `<action>`, `<ask>`, `<format>` blocks
4. Specify output structure

---

## Protocol: ai_first_analysis

**Purpose:** AI analyzes existing documentation first and proposes structured answers for SME validation. Reduces SME burden by leveraging what's already documented.

### Core Principle

> **AI analyzes first, SME validates.** The AI examines existing documentation, proposes answers based on what it finds, and the SME accepts, edits, or requests deeper elicitation.

### Parameters
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| analysis_target | string | Yes | What the AI should analyze (e.g., "journey stages", "touchpoints") |
| source_documents | array | Yes | Documents to analyze (AS-IS docs, structured-data.json, etc.) |
| output_structure | object | Yes | Expected structure of the proposed answer |
| confidence_threshold | number | No | Minimum confidence to auto-propose (default: 90) |

### Behavior

```
<protocol name="ai_first_analysis">
  <input>
    - analysis_target: What to analyze and propose
    - source_documents: Array of document paths to examine
    - output_structure: Expected structure of the answer
    - confidence_threshold: Minimum confidence for full proposal (default: 90%)
  </input>

  <step name="analyze_sources">
    <action>
    Examine all source_documents and extract information relevant to analysis_target:
    - Identify explicit mentions
    - Infer implicit information from context
    - Note gaps or ambiguities
    - Calculate confidence_score (0-100%)
    </action>
  </step>

  <step name="build_proposal">
    <action>
    Structure findings according to output_structure:
    - Populate fields with extracted/inferred data
    - Mark uncertain fields with [?] indicator
    - Note source references for each field
    </action>
  </step>

  <step name="present_proposal">
    <conditional test="confidence_score >= confidence_threshold">
      <format>
      **AI Analysis Complete** (Confidence: {{confidence_score}}%)

      Based on the existing documentation, here's my understanding:

      {{formatted_proposal}}

      ---
      **Source References:**
      {{source_references}}

      ---
      How would you like to proceed?
      - **[A] Accept** — This accurately captures the information
      - **[E] Edit** — I have corrections or additions
      - **[D] Deep Dive** — Let's explore this further with elicitation techniques
      </format>
    </conditional>

    <conditional test="confidence_score < confidence_threshold">
      <format>
      **AI Analysis** (Confidence: {{confidence_score}}% — below threshold)

      I found partial information in the documentation:

      {{formatted_proposal}}

      **Gaps Identified:**
      {{list_of_gaps}}

      ---
      I need your input to complete this. Let me ask targeted questions:
      </format>
      <action>Generate targeted questions for gaps only</action>
    </conditional>
  </step>

  <step name="handle_response">
    <handle option="A">
      <action>Mark proposal as accepted</action>
      <action>Save to output with confidence level</action>
      <output>status: "accepted", data: {{proposal}}</output>
    </handle>

    <handle option="E">
      <ask>What would you like to change or add?</ask>
      <action>Apply user's edits to proposal</action>
      <action>Re-present for approval (recursive)</action>
    </handle>

    <handle option="D">
      <display>
      **Deep Dive Options:**
      - **[A] Advanced Elicitation** — Structured techniques (5 Whys, SIPOC, etc.)
      - **[P] Party Mode** — Multiple AI perspectives discuss
      - **[B] Brainstorming** — Creative exploration session
      - **[Q] Quick Questions** — Targeted clarifying questions
      - **[X] Back** — Return to proposal
      </display>

      <handle option="A">
        <action>Load and execute {advancedElicitationTask}</action>
        <action>Integrate results into proposal</action>
        <action>Re-present for approval</action>
      </handle>

      <handle option="P">
        <action>Load and execute {partyModeWorkflow}</action>
        <action>Integrate consensus into proposal</action>
        <action>Re-present for approval</action>
      </handle>

      <handle option="B">
        <action>Load and execute {brainstormingWorkflow}</action>
        <action>Integrate ideas into proposal</action>
        <action>Re-present for approval</action>
      </handle>

      <handle option="Q">
        <action>Generate 3-5 targeted questions based on gaps</action>
        <action>Collect answers and refine proposal</action>
        <action>Re-present for approval</action>
      </handle>

      <handle option="X">
        <action>Return to main proposal display</action>
      </handle>
    </handle>
  </step>

  <output>
    - accepted_data: Final validated data
    - confidence: SME-confirmed confidence level
    - edits_made: List of changes from original proposal
  </output>
</protocol>
```

### Example Usage

```
<invoke-protocol name="ai_first_analysis">
  <param name="analysis_target">Journey stages for client touchpoint mapping</param>
  <param name="source_documents">[
    "{current_process_folder}/as-is-process-documentation.md",
    "{current_process_folder}/structured-data.json"
  ]</param>
  <param name="output_structure">{
    "stages": [
      {"name": "string", "description": "string", "process_steps": ["PS#"]}
    ]
  }</param>
  <param name="confidence_threshold">90</param>
</invoke-protocol>
```

### Integration with Existing Protocols

- **Replaces** open-ended `<ask>` sequences for documented content
- **Complements** `smart_options` for generating options when gaps exist
- **Feeds into** `adaptive_approval` for final validation
- **Triggers** `capture_structured_items` when new items need capture

---

## Protocol: batch_ai_analysis

**Purpose:** Analyze and propose multiple related items at once (e.g., all touchpoints for a stage), reducing back-and-forth.

### Parameters
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| batch_target | string | Yes | Category of items to analyze |
| source_documents | array | Yes | Documents to analyze |
| item_schema | object | Yes | Schema for each item |
| grouping | string | No | How to group items (e.g., "by_stage", "by_type") |

### Behavior

```
<protocol name="batch_ai_analysis">
  <input>
    - batch_target: What category of items to find
    - source_documents: Documents to examine
    - item_schema: Expected structure per item
    - grouping: Optional grouping strategy
  </input>

  <step name="batch_analyze">
    <action>
    Scan all source_documents for items matching batch_target:
    - Extract all instances found
    - Structure each according to item_schema
    - Group according to grouping parameter
    - Calculate per-item and overall confidence
    </action>
  </step>

  <step name="present_batch">
    <format>
    **AI Analysis: {{batch_target}}**

    Found {{item_count}} items in existing documentation:

    {{#each group in grouped_items}}
    ### {{group.name}}

    | # | Item | Key Details | Confidence |
    |---|------|-------------|------------|
    {{#each item in group.items}}
    | {{item.index}} | {{item.name}} | {{item.summary}} | {{item.confidence}}% |
    {{/each}}

    {{/each}}

    ---
    **Overall Confidence:** {{overall_confidence}}%

    How would you like to proceed?
    - **[A] Accept All** — All items are correct
    - **[R] Review Each** — Walk through items one by one
    - **[E] Edit List** — Add, remove, or modify items
    - **[D] Deep Dive** — Explore with elicitation techniques
    </format>
  </step>

  <step name="handle_batch_response">
    <handle option="A">
      <action>Mark all items as accepted</action>
      <action>Save batch to output</action>
    </handle>

    <handle option="R">
      <loop for="each item in items">
        <invoke-protocol name="ai_first_analysis">
          <param name="analysis_target">{{item}}</param>
          <param name="source_documents">{{source_documents}}</param>
          <param name="output_structure">{{item_schema}}</param>
        </invoke-protocol>
      </loop>
    </handle>

    <handle option="E">
      <ask>What changes would you like to make?
      - Add items: describe new items to add
      - Remove items: list item numbers to remove
      - Modify items: specify item number and changes
      </ask>
      <action>Apply changes and re-present batch</action>
    </handle>

    <handle option="D">
      <action>Invoke deep dive options from ai_first_analysis protocol</action>
    </handle>
  </step>

  <output>
    - accepted_items: Array of validated items
    - added_items: Items added by user
    - removed_items: Items removed from original
    - modified_items: Items changed from original
  </output>
</protocol>
```

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0.0 | 2024 | Initial protocols: smart_options, capture_structured_items, adaptive_approval |
| 1.1.0 | 2024-12 | Added ai_first_analysis and batch_ai_analysis protocols for AI-first interaction pattern |
