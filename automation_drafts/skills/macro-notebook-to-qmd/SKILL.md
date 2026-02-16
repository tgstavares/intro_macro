---
name: macro-notebook-to-qmd
description: Convert a macroeconomics analysis notebook into a publication-ready Quarto module with structured sections, consistent captions, and concise teaching narrative. Use when notebook experiments are ready and need to become a stable `.qmd` page for the course website.
---

# Notebook To QMD

Transform notebook outputs into a reproducible Quarto teaching module.

## Preconditions
Require these inputs:

- Notebook exists (`NN_topic_slug.ipynb`).
- Module manifest exists (`automation_drafts/manifests/NN_topic_slug.yaml`).
- Core figures/tables already validated for plausibility.

If manifest is missing, stop and request the module spec step first.

## Conversion Workflow
Follow this order:

1. Read manifest objectives and section plan.
2. Extract only relevant notebook cells and logic.
3. Build `NN_topic_slug.qmd` with:
   - frontmatter matching project style
   - setup chunk with imports/helpers
   - narrative sections aligned to manifest
   - figure/table code with stable labels and captions
   - language and style rules from the manifest
4. Add short interpretation text after each major figure/table.
5. Add caveats/limits section near the end.

## Writing Constraints
Keep teaching prose:

- concise and direct
- interpretation-first after each output
- explicit about definitions and units
- written in European Portuguese (`pt-PT`)

Avoid:

- dumping exploratory dead-ends
- leaving notebook scratch comments
- introducing new datasets not listed in manifest

## Caption and Label Standards
For every major output:

- include a `fig-cap` or table caption
- include location and period in caption when relevant
- use consistent label prefixes (`fig-`, `tbl-`)
- match baseline figure/table styling from `01_portugal_eurostat.qmd` and `02_portugal_contas_nacionais_plus.qmd`
- for Plotly charts, keep `template="plotly_white"` and centered chart titles (`title_x=0.5`) unless a justified exception exists

If a figure is exploratory and not publication-worthy, exclude it.

## Reproducibility Rules
Ensure:

- deterministic imports and transformations
- no hidden manual edits required between runs
- execute options match repository defaults unless manifest states otherwise

If the notebook depends on local files, document file origin and expected path in module text or comments.

## Language Allowance
Allow technical terms in English only when they are standard in economics usage. Prefer Portuguese wording first and include English terms in parentheses when useful.

## Output
Produce:

- `NN_topic_slug.qmd` ready for integration.
- Short checklist noting:
  - what from notebook was included
  - what was intentionally excluded
  - any unresolved caveats
  - language compliance (`pt-PT`)
  - style compliance against modules `01_` and `02_`
