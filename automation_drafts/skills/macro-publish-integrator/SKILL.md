---
name: macro-publish-integrator
description: Integrate a new Quarto module into the website by updating index and render configuration, running render checks, and preparing git publication steps. Use when a module `.qmd` is complete and needs to be surfaced on the site and published to GitHub Pages.
---

# Publish Integrator

Integrate and publish a completed module with minimal manual steps and explicit safety checks.

## Preconditions
Require:

- Completed `NN_topic_slug.qmd`.
- Source notebook path known.
- Module number and title finalized.

If numbering is unresolved, stop and settle numbering before editing index or `_quarto.yml`.

## Integration Workflow
Execute in this order:

1. Update `_quarto.yml`:
   - add `NN_topic_slug.qmd` to `project.render`
   - preserve existing order and indentation
2. Update `index.qmd`:
   - add numbered module entry
   - add source links for `.qmd` and `.ipynb` on GitHub
3. Run renders:
   - module-only render
   - index render
   - full site render
4. Confirm updated HTML under `docs/`.
5. Summarize changed files and publication status.

## Git Workflow
Use non-destructive git checks:

- `git status --short`
- `git diff -- <relevant-files>`

Prepare release steps:

1. Stage intended files.
2. Commit with module-specific message.
3. Push to remote branch (`main` or selected workflow branch).

If branch policy is unclear, ask before pushing.

## Validation Checks
Before marking complete, verify:

- module appears in `index.qmd`
- module included in `_quarto.yml` render list
- rendered `docs/NN_topic_slug.html` exists
- no accidental edits to unrelated files
- module frontmatter keeps `lang: pt-PT`
- narrative/captions are in European Portuguese (limited technical English allowed)
- figure/table styling is consistent with `01_portugal_eurostat.qmd` and `02_portugal_contas_nacionais_plus.qmd`

## Failure Handling
If render fails:

- capture first actionable error
- point to failing file/line when available
- propose minimal fix sequence

Do not continue to push when render is failing.
