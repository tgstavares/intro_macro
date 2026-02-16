---
name: macro-module-spec
description: Transform a high-level idea for a macroeconomics teaching module into a concrete implementation brief with file naming, data plan, section structure, and acceptance criteria. Use when a user proposes a new module topic, asks for module planning, or needs a scoped handoff before notebook or Quarto writing.
---

# Macro Module Spec

Create a module brief that is concrete enough for notebook and Quarto execution without re-deciding scope.

## Inputs
Collect these fields before writing outputs:

- Topic statement (one sentence).
- Teaching goal (what students should understand after reading).
- Data sources (Eurostat/OECD/other).
- Candidate statistics or empirical relationships.
- Expected deliverables (figures, tables, narrative depth).

If one or two fields are missing, infer reasonable defaults and label them as assumptions.

## Output Artifacts
Write two artifacts:

1. `automation_drafts/manifests/NN_topic_slug.yaml`
2. `automation_drafts/manifests/NN_topic_slug.md`

The YAML file should include:

- `module_id`
- `title_pt`
- `subtitle_pt`
- `language_policy`
- `style_anchor_modules`
- `notebook_file`
- `qmd_file`
- `render_order`
- `sources` (with URL and access method)
- `figures_required`
- `tables_required`
- `sections`
- `validation_checks`
- `open_questions`

The Markdown file should include:

- Plain-language summary of the module objective.
- Why this module matters for the course sequence.
- A short "done definition".
- Language and style constraints for downstream agents.

## Scoping Rules
Keep first version small:

- Target 3 to 6 figures.
- Target 1 to 5 tables.
- Limit sections to 2 to 8.
- Prioritize one primary narrative thread.

If the requested scope is larger, split into Phase 1 and Phase 2 inside the manifest.

## Handoff Rules
End with a handoff block for the notebook agent:

- Required datasets and query parameters.
- Required derived variables.
- Figure/table checklist with exact labels.
- Known data caveats.
- Language requirement (`pt-PT` with limited technical English terms).
- Figure/table style requirement anchored to modules `01_` and `02_`.

Do not start implementing notebook code in this skill.

## Quality Bar
Reject vague module specs. Require explicit:

- naming (`NN_topic_slug`)
- dataset identifiers
- figure/table counts
- acceptance checks
- language policy (`pt-PT`)
- style baseline references (`01_portugal_eurostat.qmd`, `02_portugal_contas_nacionais_plus.qmd`)

If these are absent, ask for clarifications or create assumptions with clear flags.
