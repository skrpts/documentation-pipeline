---
type: workflow
id: documentation-pipeline
title: Documentation Pipeline
description: "Analyses code and generates technical documentation as clean markdown"
tags: [Production]
connections:
  - target: code-review
    type: uses
  - target: markdown-formatting
    type: uses
  - target: code-analysis
    type: uses
  - target: documentation-writer
    type: uses
---

## Overview

This workflow analyses source code, reviews its structure and patterns, then generates well-formatted technical documentation in markdown.

## Pipeline Stages

### Stage 1: Code Analysis

Invoke the **code-review** skill to analyse the source code structure, identify patterns, and understand the codebase architecture.

### Stage 2: Generate Documentation

Invoke the **documentation-writer** prompt to produce technical documentation covering purpose, parameters, return values, and usage examples.

### Stage 3: Format Output

Invoke the **markdown-formatting** skill to ensure the generated documentation is clean, well-structured, and follows the API documentation standards.

## Output

Technical documentation in markdown format containing:

- Module/function purpose and description
- Parameter documentation with types
- Return value documentation
- Usage examples with code blocks
- Notes on edge cases and limitations
