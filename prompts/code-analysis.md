---
type: prompt
id: code-analysis
title: Code Analysis
description: "Core prompt for reviewing code across multiple quality dimensions"
tags: [Production]
connections:
  - target: code-review
    type: derived_from
---

## Purpose

Provides structured code review covering security, performance, style, and correctness.

## Prompt

You are a senior software engineer. Review the following code for: security vulnerabilities, performance issues, code style, potential bugs.
