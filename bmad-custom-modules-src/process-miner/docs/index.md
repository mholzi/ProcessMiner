# ProcessMiner Documentation

## Overview

ProcessMiner is a banking process documentation module that extracts tacit knowledge from SMEs through progressive elicitation techniques.

## Documentation Index

### Agents

- [Process Documentation Analyst](./process-documentation-analyst.md) - Foundation agent for process capture

### Workflows

- [Workflow Architecture](./workflow-architecture.md) - How ProcessMiner workflows operate
- [Structured Referencing](./structured-referencing.md) - ID system (PS#, EX#, PP#, CP#, SYS#)

### Integration

- [7-Agent Workflow](./seven-agent-workflow.md) - Sequential agent coordination
- [Data Schema](./data-schema.md) - Process data structure

## Quick Reference

### Agent Communication Style

> Forensic and methodical. Examines piece by piece like evidence at a crime scene - every word precise, every question surgical. Straight-to-the-point delivery with zero fluff. Speaks in data points and structured references.

### Core Principles

1. **Progressive Elicitation First** - Start broad, drill down only where needed
2. **AI Drafts, SME Validates** - Never ask SMEs to write from scratch
3. **Structured Referencing** - Every element gets a unique ID
4. **Banking Compliance Non-Negotiable** - Rationale and traceability required
5. **Multi-Altitude Output** - Executive summaries + detailed specs
6. **Import Before Interview** - Check existing docs first

### Structured IDs

| Prefix | Element | Usage |
|--------|---------|-------|
| PS# | Process Step | PS001, PS002, PS003... |
| EX# | Exception | EX001, EX002... |
| PP# | Pain Point | PP001, PP002... |
| CP# | Control Point | CP001, CP002... |
| SYS# | System | SYS001, SYS002... |
