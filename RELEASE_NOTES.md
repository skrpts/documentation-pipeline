# Release Notes

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
Initial catalogue release with full structural and content-quality validation. All scanner checks pass.
