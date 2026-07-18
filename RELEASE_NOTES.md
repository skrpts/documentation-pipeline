# Release Notes

## v1.2.0
GH#863 (K-045 intent/output-mismatch) — wire the `generate-examples` feeder into the execution DAG. It was defined but never invoked, so the code examples never reached the deliverable. Added a backing `example-generation` skill (from_step resolves by skill title), inserted the step between code analysis and documentation writing, and bound `write-documentation` to consume its output via explicit `from_step` bindings. Converted positional/title step refs in both prompts to `context_params` + `{{step.context.*}}`. Bound `language-polish` `source` to the Documentation Writing deliverable and re-pinned `polish-language` to 1.0.6.

## v1.1.32
GH#845 — republish with American English (en-US) content, completing the source-only GH#805 flip that never reached the Hub. Copy only — no functional or behaviour change.

## v1.1.31
GH#745 — declare per-step `output: {name, type}` on every execution step (code_analysis/text, documentation/text, formatted_docs/text, sanitised_docs/text, polished_docs/text, compliance_verdict/decision, consistency_verdict/decision). Lights up the #744 rich flow-map. Content-only; no bindings or logic changes.

## v1.1.30
GH#645 Row 3b — migrate to K-037 dep-referenced schema. Strip 10 inline shared-content files and declare 10 hub-shared deps (UUID id + slug name + version + checksum from `gen-dep-checksums.mjs`). Closes pre-Step-3 inline-vendoring for this bundle.

## v1.1.29
Wave 2: re-signed with canonical engine signing pipeline.

## v1.1.28
Tags migrated inline into manifest (GH#586). tags.yaml retired.

## v1.1.27
Bundle re-signed with canonical engine signing pipeline (Wave 2 migration).

## v1.1.26
Signature fix — RELEASE_NOTES.md now included in integrity checksum.

## v1.1.25
Initial catalog release with full structural and content-quality validation. All scanner checks pass.
