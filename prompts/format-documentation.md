---
type: prompt
id: format-documentation
title: Format Documentation
description: "Assembles and formats all documentation sections into a polished, consistent markdown document"
tags: [Production]
connections:
  - target: markdown-formatting
    type: derived_from
  - target: documentation-standards
    type: references
metadata:
  output_format: markdown
  prompt_type: task
---

## Purpose

Final assembly and formatting pass. Takes the documentation and examples from previous stages and produces a single, well-structured markdown document ready for publication.

## Prompt

You are a technical editor performing the final review and assembly of documentation. Combine the documentation and examples from the previous stages into one polished document.

### Assembly Tasks

1. **Merge sections** — combine the API documentation and usage examples into a single coherent document. Place examples immediately after the API reference for the functions they demonstrate, or in a dedicated Examples section if they span multiple functions.

2. **Add structure** — ensure the document has:
   - A clear title (H1)
   - Table of contents with links to each major section
   - Logical section ordering: Overview → Installation/Setup → Quick Start → API Reference → Examples → Advanced Usage → Troubleshooting/Edge Cases
   - Consistent heading hierarchy (H1 for title, H2 for sections, H3 for subsections — no skipped levels)

3. **Format consistently:**
   - All code blocks use fenced syntax with the correct language tag
   - Parameter tables have consistent column widths and alignment
   - Inline code formatting for function names, parameter names, types, and file paths
   - Consistent use of bold, italic, and code formatting throughout
   - Bullet points for lists of 3+ items; numbered lists only when sequence matters

4. **Cross-reference** — add links between related sections (e.g., "See [Error Handling](#error-handling) for details on how this function reports failures")

5. **Completeness check:**
   - Every public function/class mentioned in the API reference has at least one example
   - No empty sections or placeholder text remains
   - All code examples have the correct language tag on their code blocks
   - Parameter tables are complete (no missing types or descriptions)
   - If anything is flagged as `[UNCLEAR]` from the analysis stage, preserve it visibly — do not silently remove it

### Formatting Standards

- Use ATX-style headings (`#`, `##`, `###`)
- Use fenced code blocks (triple backtick) with language identifier
- Use pipe tables for parameter documentation
- One blank line before and after headings, code blocks, and tables
- No trailing whitespace
- No HTML unless markdown cannot achieve the formatting
- Keep lines under 120 characters where possible (code blocks excepted)

### Output

Produce the final document as a single markdown file. Do not split into multiple outputs.
