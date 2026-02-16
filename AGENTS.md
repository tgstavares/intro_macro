# AGENTS.md

## Purpose
Use this repository to create and publish teaching modules for Introductory Macroeconomics (Portugal focus) as Quarto webpages.

## Scope
Apply these instructions to all files under this repository root.

## Workflow Contract
Follow this sequence for each new module:

1. Define the module concept and expected outputs.
2. Build or update a notebook to fetch data and test figures/tables.
3. Convert notebook results into a standalone `.qmd` module.
4. Validate text, figures, tables, and basic reproducibility.
5. Register the module in `index.qmd` and `_quarto.yml`.
6. Render website and prepare commit/push for GitHub Pages.

Do not skip step 5, because this site depends on explicit entries in both files.

## Naming Convention
Use two-digit numeric prefixes to keep ordering stable:

- Notebook: `NN_topic_slug.ipynb`
- Quarto module: `NN_topic_slug.qmd`
- Optional local output folder: `NN_topic_slug_files/`

When inserting a module between existing numbers, prefer a new unused number (for example `03_`, `04_`) rather than renaming old modules.

## Required Module Structure
Each new `.qmd` module should contain:

- YAML frontmatter with `title`, `subtitle`, `lang`, `format`, and `execute`.
- One setup cell for imports/helpers (`#| label: setup`, `#| include: false`).
- A short introduction stating learning goals and data sources.
- Sections with explicit figure/table captions.
- A closing section with interpretation limits and caveats.

Use these baseline frontmatter values unless there is a documented reason to diverge:

- `lang: pt-PT`
- `format.html.theme: cosmo`
- `format.html.toc: true`
- `format.html.toc-location: left`
- `format.html.number-sections: true`
- `format.html.from: markdown+tex_math_single_backslash`
- `execute.echo: false`
- `execute.warning: false`
- `execute.message: false`
- `execute.cache: true`

## Language Policy (Mandatory)
Write narrative text and captions in European Portuguese (`pt-PT`).

- Allow technical terms in English only when they are the standard term in the literature (for example `input-output`, `labor share`, `nowcasting`).
- Prefer Portuguese first and keep the English term in parentheses when clarity is improved.

## Figure/Table Style Baseline (Mandatory)
Match the visual style used in:

- `01_portugal_eurostat.qmd`
- `02_portugal_contas_nacionais_plus.qmd`

For new modules, keep this baseline:

- Plotly figures should use `template="plotly_white"`.
- Keep chart titles centered (`title_x=0.5`) and axis titles minimal when context is clear.
- Keep legends clean (`legend_title_text=""`) and non-obtrusive.
- Use explicit `fig-cap` / `tbl-cap` for publication outputs.
- Keep table formatting compact and readable, consistent with existing styled tables.

## Integration Points
After creating a new module, update:

- `index.qmd`:
  - Add numbered entry with module link.
  - Add source links to the `.qmd` file and supporting notebook on GitHub.
- `_quarto.yml`:
  - Add the new `.qmd` filename under `project.render`.

Keep ordering consistent across `index.qmd` and `_quarto.yml`.

## Quality Gates (Default Strictness)
Run these checks before publish:

1. `./quarto.sh render <new-module>.qmd`
2. `./quarto.sh render index.qmd`
3. `./quarto.sh render` (full site pass)
4. Confirm generated HTML exists in `docs/`.
5. Manually review major figures/tables for label correctness and obvious outliers.
6. Verify no placeholder text remains (for example `TODO`, `TBD`, `[BREVEMENTE]` for published entries).
7. Verify narrative language is pt-PT (allowing only limited technical English terms).
8. Verify figure/table visual style is consistent with modules `01_` and `02_`.

## Publish Contract
For release completion:

1. `git status` is clean except intended changes.
2. Commit includes source files and rendered `docs/` outputs.
3. Push to `main` (or merge to `main`) for GitHub Pages publication.

## Multi-Agent Split (Optional)
Use this split when tasks are large:

- Agent A (Spec): module framing, learning goals, data inventory.
- Agent B (Notebook): data extraction, transformations, chart/table experiments.
- Agent C (Publish): `.qmd` synthesis, index/quarto registration, render and git checks.

Use a shared handoff artifact (`module manifest`) so each agent works from the same assumptions.

## Tuning Knobs
Adjust these controls as needed:

- `strict_render_scope`: `full` (default) or `module-only`
- `require_notebook_link_in_index`: `true` (default) or `false`
- `enforce_numbered_prefix`: `true` (default) or `false`
- `minimum_quality_gate_level`: `manual+render` (default), `render-only`, or `manual-heavy`
- `publish_mode`: `direct-main` (default) or `feature-branch-pr`

If you relax a knob for speed, record the exception in the commit message.
