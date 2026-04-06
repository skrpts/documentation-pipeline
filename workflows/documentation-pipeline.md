---
type: workflow
id: documentation-pipeline
title: Documentation Pipeline
description: "Analyses source code and generates detailed technical documentation with examples, formatted as clean markdown"
tags: [Production, Documentation, Learning]
connections:
  - target: code-analysis
    type: uses
  - target: documentation-writing
    type: uses
  - target: documentation-standards
    type: references
  - target: llm-service
    type: runs_on
  - target: documentation-checklist
    type: uses
  - target: brief-compliance-check
    type: uses
  - target: consistency-check
    type: uses
  - target: format-conversion
    type: uses
  - target: defang-content
    type: uses
metadata:
  estimated_duration: "10-20 minutes"
  trigger: manual
---

## Overview

This workflow takes source code and produces complete, publication-ready technical documentation. It runs in four stages: structural analysis, documentation writing, example generation, and final formatting. Each stage builds on the output of the previous one, producing progressively richer documentation.

The pipeline works with any programming language and adapts its output depth based on the target audience.

## Pipeline Stages

### Stage 1: Code Analysis

**Input:** Source code and programming language

Invoke the **code-analysis** skill via the **analyse-code** prompt. Analyses the code's structure — functions, classes, modules, types, dependencies, and patterns. Produces a structured inventory that the later stages work from.

**Output:** Structural analysis with every documentable element catalogued.

### Stage 2: Documentation Writing

**Input:** Code analysis from Stage 1, audience and documentation type

Invoke the **documentation-writing** skill via the **write-documentation** prompt. Generates detailed technical documentation: overview, API reference with parameter tables, error conditions, and per-function usage notes. Adapts depth and terminology to the target audience.

**Output:** Complete technical documentation in draft form.

### Stage 3: Example Generation

**Input:** Code analysis and documentation from previous stages

Invoke the **generate-examples** prompt to create practical, runnable usage examples in three tiers: quick start (copy-paste ready), common patterns (2-4 real-world scenarios), and advanced usage (complex integration). Examples use realistic data and include error handling where appropriate.

**Output:** Tiered usage examples ready to merge into the final document.

### Stage 4: Format and Assemble

**Input:** Documentation and examples from previous stages

Invoke the **markdown-formatting** skill via the **format-documentation** prompt. Merges all content into a single polished document. Adds table of contents, cross-references, consistent heading hierarchy, and properly formatted code blocks. Performs a completeness check against the documentation standards.

**Gate:** Every public function must have at least one example. No placeholder text or empty sections in the final output.

**Output:** Publication-ready markdown document.

## Error Handling

- If the source code is a snippet rather than a full file, the pipeline documents what it can see and flags missing context
- If the language is not specified, the analysis stage infers it from syntax and notes the assumption
- If the code has no public API surface (all private/internal), the pipeline documents the module's purpose and internal structure with a note that no public API was found

## Inputs

| Name | Required | Description | Example |
|------|----------|-------------|---------|
| `{{input.source_code}}` | Yes | The source code to document. Paste the full file or relevant module. | A function, class, or module you want documented |
| `{{input.language}}` | Yes | Programming language of the source code | `typescript`, `python`, `go`, `rust` |
| `{{input.audience}}` | No | Who will read this documentation. Default: developers (library consumers) | `library consumers`, `contributors`, `end users` |
| `{{input.doc_type}}` | No | Type of documentation to generate. Default: API reference | `API reference`, `README`, `developer guide`, `module overview` |

## Outputs

| Name | Description |
|------|-------------|
| Technical documentation | Publication-ready markdown document with overview, API reference, usage examples, and edge cases |
| Table of contents | Auto-generated TOC with links to all sections |
| Quality report | Completeness status — any functions without examples or unclear items flagged |

## Setup

Before running this workflow:

1. **No external services required** — paste your source code directly as input. No GitHub access, no file system access, no API keys needed.
2. **Review the documentation standards** — the `documentation-standards` source document defines formatting conventions. Customize it to match your project's style if needed.
3. **Choose your audience** — the documentation depth changes significantly based on who will read it. Specify the audience for best results.

## Provider Notes

- The code analysis stage benefits from models with strong code comprehension — larger models produce more accurate type inference and pattern recognition
- Documentation writing works well with any capable model — the quality difference between providers is smaller here
- Example generation benefits from models that can produce syntactically valid code — test the output
- The formatting stage is lightweight and runs well on any model
- Total token usage scales with code size — a 200-line module uses roughly 8,000-12,000 tokens across all stages

## Example Input

To test this workflow immediately after import:

```
Source code:
  function debounce(fn, delay = 300) {
    let timer = null;
    return function (...args) {
      clearTimeout(timer);
      timer = setTimeout(() => fn.apply(this, args), delay);
    };
  }

  function throttle(fn, limit = 100) {
    let inThrottle = false;
    return function (...args) {
      if (!inThrottle) {
        fn.apply(this, args);
        inThrottle = true;
        setTimeout(() => (inThrottle = false), limit);
      }
    };
  }

  export { debounce, throttle };

Language: javascript
Audience: library consumers
Doc type: API reference
```
