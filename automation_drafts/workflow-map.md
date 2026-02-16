# Module Automation Workflow Map (Draft)

## Goal
Automate repeated tasks for adding new course modules while preserving manual academic judgment on interpretation quality.

## Repository Anchors
Current fixed anchors in this repository:

- `/Users/tgst/Library/CloudStorage/GoogleDrive-tgstavares@gmail.com/My Drive/Economics/Teaching/2026_a_spring/Macro_I_ug/Classes/Dados/index.qmd`
- `/Users/tgst/Library/CloudStorage/GoogleDrive-tgstavares@gmail.com/My Drive/Economics/Teaching/2026_a_spring/Macro_I_ug/Classes/Dados/_quarto.yml`
- `/Users/tgst/Library/CloudStorage/GoogleDrive-tgstavares@gmail.com/My Drive/Economics/Teaching/2026_a_spring/Macro_I_ug/Classes/Dados/docs/`
- `/Users/tgst/Library/CloudStorage/GoogleDrive-tgstavares@gmail.com/My Drive/Economics/Teaching/2026_a_spring/Macro_I_ug/Classes/Dados/quarto.sh`

## Multi-Agent Split
Use three agents with artifact-based handoffs.

1. Agent A: Spec Agent (`macro-module-spec`)
2. Agent B: Content Agent (`macro-notebook-to-qmd`)
3. Agent C: Integrator Agent (`macro-publish-integrator`)

### Handoff Artifact
Single source of truth:

- `automation_drafts/manifests/NN_topic_slug.yaml`

All later stages should consume this file before any edits.

## End-to-End Sequence
1. Receive module idea.
2. Agent A creates manifest and done definition.
3. Agent B uses manifest + notebook to build `NN_topic_slug.qmd`.
4. Human validation step:
   - review economics interpretation
   - confirm chart/table relevance
   - approve wording and pedagogical fit
5. Agent C updates `index.qmd` and `_quarto.yml`, renders site, and prepares publish steps.

## Suggested CLI Skeleton
These are manual command slots to operationalize the flow:

```bash
# Step A (spec)
# create manifest from idea (skill-driven)

# Step B (content)
./quarto.sh render NN_topic_slug.qmd

# Step C (integration)
./quarto.sh render index.qmd
./quarto.sh render
git status --short
```

## Quality Gates By Phase
Agent A gate:

- Manifest has explicit datasets, section list, figure/table targets.
- Manifest pins language to `pt-PT` and references the style anchors (`01_`, `02_`).

Agent B gate:

- `.qmd` compiles.
- Captions and section logic match manifest.
- Narrative and captions follow pt-PT (with only limited technical English terms).
- Figure/table styling matches the baseline from modules `01_` and `02_`.

Agent C gate:

- Module appears in `index.qmd`.
- Module appears in `_quarto.yml`.
- HTML generated in `docs/`.
- Final visual inspection confirms language/style consistency with modules `01_` and `02_`.

## Fine-Tuning Matrix
Use these knobs to tune automation behavior.

### Knob 1: Scope strictness
- `tight`: max 4 sections, 3 figures, 1 table (fast iteration).
- `balanced` (default): 4 to 8 sections, 3 to 6 figures, 1 to 4 tables.
- `broad`: allow more depth, split into phase deliverables.

### Knob 2: Validation depth
- `render-only`: skip manual checklist (faster, higher risk).
- `manual+render` (default): render plus visual/text review.
- `manual-heavy`: add extra numeric cross-checks and reference verification.

### Knob 3: Publish policy
- `direct-main` (default): push after local checks.
- `branch-pr`: force feature branch and PR review.

### Knob 4: Index metadata
- `minimal`: module link only.
- `standard` (default): module link + `.qmd` + notebook links.
- `extended`: add short description and tags.

### Knob 5: Notebook dependency policy
- `strict`: all published figures/tables must be notebook reproducible.
- `mixed` (default): allow minor in-qmd transforms.
- `qmd-first`: allow substantial in-qmd processing when documented.

### Knob 6: Language strictness
- `pt-only`: no English technical terms unless unavoidable.
- `pt-plus-terms` (default): pt-PT narrative with limited technical English terms.
- `mixed`: more permissive English usage.

### Knob 7: Style strictness
- `locked` (default): follow visual anchors from modules `01_` and `02_`.
- `semi-locked`: preserve major anchors, allow minor palette/layout changes.
- `flexible`: broader style variation allowed if documented.

## Where to Tune
Primary place:

- `/Users/tgst/Library/CloudStorage/GoogleDrive-tgstavares@gmail.com/My Drive/Economics/Teaching/2026_a_spring/Macro_I_ug/Classes/Dados/AGENTS.md`

Skill-specific place:

- `automation_drafts/skills/macro-module-spec/SKILL.md`
- `automation_drafts/skills/macro-notebook-to-qmd/SKILL.md`
- `automation_drafts/skills/macro-publish-integrator/SKILL.md`

For policy changes, update `AGENTS.md` first, then align each skill.

## Migration Path To Real Skills
When these drafts are stable:

1. Copy each draft skill into `$CODEX_HOME/skills/<skill-name>/SKILL.md`.
2. Add `agents/openai.yaml` metadata for UI discoverability.
3. Validate each skill with your skill validation workflow.
4. Run one pilot module through the full pipeline and refine.
