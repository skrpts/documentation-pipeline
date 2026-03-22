---
type: skill
id: code-analysis
title: Code Analysis
description: "Analyses source code structure, extracting functions, classes, modules, and their relationships for documentation purposes"
tags: [Production, Tested]
connections:
  - target: llm-service
    type: runs_on
---

## Capability

Analyses source code to extract its structural elements — functions, classes, modules, constants, type definitions, and their relationships. Produces a structured inventory that downstream documentation steps can work from. Supports JavaScript, TypeScript, Python, Go, Rust, Java, C#, and Ruby.

## When to Use

- Before generating documentation for unfamiliar code
- Auditing a codebase for documentation coverage
- Understanding module dependencies and public API surface
- Preparing for a documentation sprint on legacy code

## Inputs

Source code (files, modules, or snippets), programming language

## Outputs

Structured analysis: module overview, function/method signatures with parameters and return types, class hierarchies, exported vs internal symbols, dependency graph, complexity notes

## Limitations

- Heuristic analysis — does not compile or execute the code
- May miss dynamic patterns (metaprogramming, runtime-generated APIs, monkey-patching)
- Type inference is best-effort for dynamically typed languages
- Cannot follow imports across files when given a single snippet
