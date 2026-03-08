---
type: prompt
id: documentation-writer
title: Documentation Writer
description: "Task prompt for generating technical documentation from source code"
tags: [Production]
connections:
  - target: code-review
    type: derived_from
  - target: markdown-formatting
    type: derived_from
  - target: api-documentation-standards
    type: references
---

## Purpose

Generates comprehensive technical documentation from source code, covering purpose, parameters, return values, and usage examples.

## Prompt

Given the following code, generate technical documentation including: purpose, parameters, return values, usage examples.
