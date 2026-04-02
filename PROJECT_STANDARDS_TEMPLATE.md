# PROJECT_STANDARDS_TEMPLATE.md
# Shared Standards Library
# Purpose: Single source of truth for all project-wide standards including
# coding rules, naming conventions, visualization requirements,
# output integrity rules, and data ethics standards.
#
# Version: 1.0
# Last Updated: [2026-04-02 0948 EST]
# Status: Active
# Applies To: All Projects
# Source References: None — original standard established [2026-04-02]
# Change Summary: Initial version — PROJECT_STANDARDS_TEMPLATE.md established
---

## Purpose and Scope

This document is the single source of truth for all project-wide standards.
It governs every notebook, every module, and every session regardless of
subject matter, data source, or analytical method. When in doubt, refer
here first.

### Required for All Projects
- Coding standards and rules
- Notebook structure and cell naming conventions
- File naming conventions
- Version control standards
- Visualization standards
- Data ethics standards
- Data library and tool stack

### Optional — Include When Applicable
- O/D/I/A output tagging — for projects producing evidence logs or
  decision support outputs. O/D/I/A stands for Observed, Derived,
  Inferred, and Assumed — a classification system that tags every
  analytical output by how it was produced, ensuring transparency
  and auditability. See Section 9 for full reference.
- Knowledge base upload naming — for projects using a Claude Project
  knowledge base.

Every project that uses this library copies this template and fills in the
project-specific sections marked [FILL IN PER PROJECT]. All other sections
apply as written without modification.

Do not modify this template inside a project. If a standard needs to change,
the change is made in the Shared Standards Library first, then the updated
template is copied into any active projects that need it. The library is
always the source of truth.

---

## Core Principles

These principles underpin every standard in this document. When a specific
rule does not cover a situation, default to these principles.

- **Consistency** — every project starts from the same foundation; standards
  are applied uniformly across all notebooks, modules, and sessions
- **Integrity** — findings are reported without bias; assertions are
  supported by evidence and tagged accordingly
- **Attribution** — sources of data, standards, and methods are cited
  where they exist; original standards are noted as such
- **Reproducibility** — all work can be re-run and verified by anyone
  with access to the data and this document
- **Portability** — standards travel into new projects cleanly without
  modification; project-specific values are isolated in designated
  fill-in sections
- **Transparency** — every change to every document is recorded;
  nothing is silently updated
- **Troubleshootability** — all code and markdown cells carry stable
  IDs so errors can be reported, located, and resolved precisely
  regardless of environment.
---

## Coding Standards

These rules apply to every notebook, every module, every session.
No exceptions. When in doubt, refer here first.

### Rule 1 — No Hardcoded Variables

No literal values embedded directly in code logic. Every threshold, weight,
ratio, minimum count, palette color, file path, or tuning parameter must be
defined in the CONFIG cell with an accompanying rationale block.

Correct:
# [PROJECT]-00-CONFIG-01
# Minimum record threshold
# Rationale: [explain the source and reason for this value]
MIN_THRESHOLD = [value]

# Scoring thresholds — PROVISIONAL
# Rationale: Placeholder values pending score distribution analysis
# Action required: Recalibrate after running distribution analysis
THRESHOLD_HIGH   = [value]   # >= this → [outcome]
THRESHOLD_MEDIUM = [value]   # >= this and < HIGH → [outcome]
                             # <  this → [outcome]

Incorrect:
# Hardcoded — never do this
df['category'] = df['score'].apply(
    lambda x: 'High' if x >= 0.75 else ('Medium' if x >= 0.50 else 'Low')
)

Exceptions — values that may appear inline without CONFIG definition:
- Commonly accepted industry/statistical constants
  (e.g., random_state=42, confidence=0.95, p_value=0.05)
- Library method defaults used as layout conveniences, not project
  decisions (e.g., figsize=(12, 6))

Even for exceptions, add a brief inline comment explaining the value.

### Rule 2 — Provisional Values Must Be Labeled

Any threshold or parameter set before data distribution analysis must be
marked clearly:

THRESHOLD_HIGH = [value]   # PROVISIONAL — recalibrate after distribution
                           # analysis in [PROJECT]-07-VIZ-01

Provisional values must be resolved before the module is marked COMPLETE.
The evidence_log must record when and how final values were set, tagged A
until calibrated, then updated to D once derived from distribution analysis.

### Rule 3 — Reproducibility

RANDOM_STATE = 42   # Industry-standard reproducibility seed
# Source: Common convention in data science and machine learning practice

Use RANDOM_STATE everywhere a random seed is required. Never use a literal
42 in code logic — always reference the CONFIG variable.

### Rule 4 — Minimum Subgroup Size

MIN_SUBGROUP_SIZE = [value]   # Minimum records for peer group validity
                              # Rationale: [explain why this value was chosen;
                              # below this threshold peer comparison is
                              # statistically unreliable]

Any peer group calculation falling below MIN_SUBGROUP_SIZE receives a neutral
score rather than a computed score. Document all neutral assignments in the
evidence log tagged A.

The neutral score value must be defined in the CONFIG cell:
NEUTRAL_SCORE = [value]   # Score assigned when subgroup is too small
                          # to produce a statistically reliable result

### Rule 5 — Threshold Design Process

Thresholds that route records to outcome pathways must follow this
process before the notebook is marked COMPLETE:

1. Set provisional values in CONFIG with # PROVISIONAL label
2. Build scoring logic and run against the full population
3. Analyze score distribution (histogram and percentile table in VIZ section)
4. Identify natural breaks or set deliberate percentile-based cutoffs
5. Update CONFIG with final values and remove # PROVISIONAL label
6. Document rationale in the project decision log and evidence log (tag: D)

A notebook cannot be marked COMPLETE until all provisional values are resolved.
### Rule 6 — No Emojis or Special Characters in Code or Print Statements

Use plain text only in all code cells and print statements.

Approved status indicators:
- PASS
- FAIL
- WARNING
- NOTE
- COMPLETE

Prohibited:
- Checkmarks, cross marks, warning symbols (e.g. ✓ ✗ ⚠)
- Arrows or decorative Unicode characters (e.g. → ← ★)
- Emoji of any kind

Rationale: Special characters cause encoding issues across environments
and are unprofessional in most project contexts.

### Rule 7 — Null Value Handling

Null values in signal or scoring columns are treated as 0 — signal did
not fire.

df['signal_col'] = df['signal_col'].fillna(0)
# Rationale: null value means signal could not be calculated, typically
# due to zero denominator or missing data. Does not mean signal fired
# negatively. Treatment: no contribution to score. Tag: A

Rules:
- Null fills must occur in the VALIDATE section, not SCORE
- Document null counts and fill action in the evidence log tagged A
- If null count changes from a previously confirmed baseline, flag as
  WARNING in validate output
- The fill value and rationale must be defined in the CONFIG cell:

NULL_FILL_VALUE = 0   # [FILL IN PER PROJECT — adjust if project logic
                      # requires a different null treatment, and document
                      # rationale here]

### Rule 8 — Diagnostic Cells Are Temporary

Cells prefixed with DIAG are temporary troubleshooting tools only.

- Use format: # [PROJECT]-DIAG-[nn] (e.g. # PROJ-DIAG-01)
- Delete all DIAG cells before committing notebook to version control
- Never include DIAG cells in a final notebook
- DIAG cells do not appear in notebook_map.md

Rationale: Diagnostic cells are investigative tools, not analytical
outputs. Leaving them in a committed notebook creates confusion about
what is part of the official analysis and what is not.

### Rule 9 — Confirm Data Counts From Source

Never assume population counts, distributions, or file contents from
documentation alone. Always confirm from the actual data before writing
assertions, comments, or session notes.

# Always run this pattern when loading a new file
print(f"Row count: {len(df):,}")
print(df['[column_name]'].value_counts().sort_index())

Rules:
- Session documentation may lag behind actual file contents
- If actual counts differ from documented counts, correct the
  documentation before proceeding — do not adjust the assertion
  to match wrong documentation
- Confirm and correct in this order: data first, then assertions,
  then comments, then SESSION_CONTEXT.md.

### Rule 10 — Column Format Verification

Never assume column value formats from documentation or prior project
design. Always confirm actual values via diagnostic before using them
in assertions, mapping dictionaries, or logic.

When a format discovery occurs:
  1. Fix the assertion to match confirmed values
  2. Add a markdown cell immediately before the affected PREP cell
     documenting the discovery
  3. Record in the project decision log
  4. Add to this rule's known format discoveries table below

### Known Format Discoveries
# [FILL IN PER PROJECT — document confirmed column format discoveries
# here as they are found during development]

| Column | File | Confirmed Format | Discovered In | Notes |
|--------|------|-----------------|---------------|-------|
| [name] | [file] | [format] | [cell ID] | [notes] |


### Rule 11 — Cell Execution Protocol

Notebooks are built and executed one cell at a time. No exceptions.
The sequence for every cell is:

1. Claude produces one cell — markdown or code — and nothing else
2. User copies cell into the notebook environment and runs it
3. User confirms output or reports any errors
4. Claude addresses errors if present before proceeding
5. Only after confirmation does Claude produce the next cell

Rationale: Building multiple cells at once prevents error isolation,
makes troubleshooting impossible, and removes the ability to verify
analytical outputs as they are produced.

This protocol applies to every notebook in every project.

### Rule 12 — All Imports in CONFIG Cell Only

All library imports are declared once in the CONFIG cell at the top of
the notebook. No imports appear in any other cell.

Correct:
# [PROJECT]-00-CONFIG-01
import duckdb
import polars as pl
import matplotlib.pyplot as plt

Incorrect:
# Importing mid-notebook — never do this
# [PROJECT]-05-SCORE-01
import polars as pl

Rules:
- The CONFIG cell is the single location for all imports
- If a library is needed, it is imported in CONFIG regardless of where
  in the notebook it is first used
- Re-importing a library further down in a notebook is prohibited
- This applies to all notebooks in every project

Rationale: Centralizing imports in CONFIG ensures dependencies are
visible in one place, makes environment troubleshooting faster, and
prevents confusion about what a notebook requires to run.

---

## Notebook Structure Standards

### Opening Markdown Cell Required

Every notebook must begin with a markdown cell before any code cell.
This cell carries the ID [PROJECT]-00-HEADER-00 and must include:

- Module or notebook name and full title
- Decision type and Decision Owner role (if applicable)
- Current status and last updated date
- Purpose statement
- Inputs table (file, source, description)
- Outputs table (file, description)
- Scoring dimensions or key logic summary (if applicable)
- Decision outcomes or escalation pathways (if applicable)
- Provisional value notice (if applicable)
- O/D/I/A tag reference table (if applicable)
- Data source citation

No code may precede this markdown cell. No exceptions.

### Cell ID Format

Every code cell and every markdown cell in every notebook carries a unique,
stable ID as the first comment line (code cells) or first line (markdown cells).
Cell IDs are the project's error-reporting and navigation standard — always
reference a cell ID when reporting an issue, never a line number.

Format:
[PROJECT]-[SECTION_NUM]-[SECTION_NAME]-[CELL_NUM]

| Component    | Description                                    | Example  |
|--------------|------------------------------------------------|----------|
| PROJECT      | Project prefix — defined per project           | PROJ     |
| SECTION_NUM  | Two-digit section number                       | 03       |
| SECTION_NAME | Section vocabulary word (see table below)      | SCORING  |
| CELL_NUM     | Two-digit cell number within the section       | 02       |

Full example:
PROJ-03-SCORING-02
Meaning: this project, Section 3, Scoring logic, second cell in that section.

In a code cell:
# PROJ-03-SCORING-02
# Composite score calculation — weighted sum of all dimensions

In a markdown cell:
<!-- PROJ-03-SCORING-02 -->
## Composite Score Calculation

PROJECT PREFIX:
[FILL IN PER PROJECT — define the prefix used in all cell IDs for this project]
Example: PROJECT_PREFIX = "PROJ"

SECTION NAME VOCABULARY:
Standardized across all projects. Use only these names.

| Code     | Meaning                          | Typical Content                                          |
|----------|----------------------------------|----------------------------------------------------------|
| CONFIG   | Configuration and parameters     | Thresholds, weights, paths — all with rationale blocks   |
| LOAD     | Data loading                     | Read files, confirm row counts                           |
| VALIDATE | Data validation                  | Schema checks, null counts, range assertions             |
| PREP     | Feature engineering / preparation| Derived columns, joins, normalization                    |
| PEER     | Peer group calculations          | Subgroup medians, min-size enforcement                   |
| SCORE    | Scoring logic                    | Dimension scores, composite score                        |
| PATHWAY  | Pathway or tier assignment       | Threshold-based routing logic                            |
| VIZ      | Visualizations                   | All plots and charts                                     |
| OUTPUT   | Output generation                | Write parquet, CSV, markdown tables                      |
| EVIDENCE | Evidence logging                 | Tagged summary of cell outputs                           |

SECTION NUMBERING CONVENTION:
Section numbers are fixed per project type to maintain consistency across notebooks.

| Section Num | Section Name | Notes                                          |
|-------------|--------------|------------------------------------------------|
| 00          | CONFIG       | Always first cell in every notebook            |
| 01          | LOAD         | Load inputs                                    |
| 02          | VALIDATE     | Validate loaded data before processing         |
| 03          | PREP         | Feature engineering                            |
| 04          | PEER         | Peer group work (if applicable)                |
| 05          | SCORE        | Core scoring logic                             |
| 06          | PATHWAY      | Pathway or tier assignment                     |
| 07          | VIZ          | Visualizations                                 |
| 08          | OUTPUT       | Write outputs                                  |
| 09          | EVIDENCE     | Evidence log summary cell                      |

Not every notebook uses every section. Skip numbers that do not apply —
do not renumber to fill gaps.

TROUBLESHOOTING BY CELL ID:
When reporting an error, always reference the cell ID, never a line number.

Correct:
"Cell PROJ-05-SCORE-01 is throwing a KeyError on column 'composite_score'"

Incorrect:
"Line 47 is throwing a KeyError"

Rationale: Line numbers differ between environments and change as notebooks
are edited. Cell IDs are stable regardless of environment or edit history.

## File Naming Conventions

### Notebooks
[project-slug].ipynb

Examples:
  my-project_analysis.ipynb
  my-project_scoring.ipynb

### Output Data Files
[descriptor]_v[version].parquet

Examples:
  records_scored_v1.parquet
  population_filtered_v1.parquet

### Output Figures
[descriptor]_v[version].png

Examples:
  score_distribution_v1.png
  pathway_breakdown_v1.png

### Decision Brief Memos
[project-slug]_recommendation_memo_v[version].md

Examples:
  my-project_recommendation_memo_v1.md

---

## Optional — Include When Applicable

### Decision Folder Documents
# [FILL IN PER PROJECT — include if the project uses a formal
# decision folder structure]

Every decision folder contains exactly these four files, named exactly:

  README.md
  decision_log.md
  evidence_log.md
  notebook_map.md

### Knowledge Base Upload Naming
# [FILL IN PER PROJECT — if using a Claude Project knowledge base,
# files with generic names (README.md, decision_log.md, etc.) must
# be renamed before uploading to avoid naming conflicts across modules.
# Define the renaming convention here.]

Rule: Files on disk and in version control keep their original names
always. Only copies uploaded to the knowledge base receive prefixed
names. This keeps the repository structure clean and the knowledge
base unambiguous.

## Version Control Standards

### Commit Message Standards

Every commit message must be descriptive and action-oriented.
The message must tell someone reading the repository history exactly
what changed and why — without having to open the commit.

Correct:
  Add scoring logic for dimension 3 — peer group billing frequency
  Fix null fill in VALIDATE section — was running in SCORE, moved per Rule 7
  Update CONFIG thresholds — provisional values replaced after VIZ analysis

Incorrect:
  update files
  fix stuff
  wip

### Commit Sequence

Every change follows this sequence before being considered complete:

1. Edit the local file
2. Update the document version number, last updated date, and change
   summary in its header block
3. Record the change in the project changelog
4. Commit and push to version control:

   git add .
   git commit -m "descriptive message explaining what changed and why"
   git push origin main

5. Re-upload any changed documents to the project knowledge base
   (if applicable)

### What Belongs in Version Control

This library and all projects derived from it are documents-only
repositories. Do not commit the following:

- Raw data files (CSV, parquet, Excel)
- Notebook checkpoint files (.ipynb_checkpoints)
- Environment or dependency files unless intentionally added
- Temporary or diagnostic outputs

## Visualization Standards

### CVD Compliance Required

All visualizations must be readable by individuals with color vision
deficiency. This is not optional — it applies to every plot in every
notebook, including quick exploratory charts.

Rules:
- Use only the project CVD palette defined in CONFIG (see below)
- Do not use red/green combinations
- Do not use color as the sole differentiator — always pair color with
  shape, pattern, or label where possible
- All axis labels, titles, and legends must be present and legible

### Project CVD Palette

The following palette is the project standard for all visualizations.
Paste this block into every notebook CONFIG cell so the palette is
always locally defined and never imported from another notebook.

CVD_PALETTE = {
    'category_a' : '#DC267F',   # Magenta  — [FILL IN PER PROJECT]
    'category_b' : '#FFB000',   # Amber    — [FILL IN PER PROJECT]
    'category_c' : '#648FFF',   # Blue     — [FILL IN PER PROJECT]
    'neutral'    : '#BBBBBB',   # Gray     — no flag / neutral
}
# Source: IBM Carbon Design System CVD palette (carbondesignsystem.com)

### Chart Requirements

Every chart must include:
- A descriptive title
- Labeled axes with units where applicable
- A legend if more than one category is plotted
- A data source note if the underlying data has an external origin

### Visualization Library

matplotlib is the project standard for all figures.
# [FILL IN PER PROJECT — note any additional libraries in use,
# e.g. seaborn for statistical plots]

If using Polars DataFrames, convert to numpy arrays for matplotlib:
  df['column'].to_numpy()

## O/D/I/A Output Tagging
# Optional — include for projects producing evidence logs or decision
# support outputs.

### Purpose

Every analytical output is tagged with one of four classifications that
describe how the output was produced. This ensures transparency and
auditability across all findings.

### Tag Definitions

| Tag | Meaning  | Example                                              |
|-----|----------|------------------------------------------------------|
| O   | Observed | Direct count or value read from the data             |
| D   | Derived  | Calculated from observed values                      |
| I   | Inferred | Reasoned from patterns, not directly measured        |
| A   | Assumed  | Design decision made without data confirmation       |

### Rules

- Every output in the evidence log carries exactly one O/D/I/A tag
- No output may assert intent, wrongdoing, or causation under any tag
- Assumed (A) tags must be resolved to D before a notebook is marked
  COMPLETE wherever data confirmation is possible
- Inferred (I) tags must include the reasoning chain that supports
  the inference

### Usage Examples

O — "Provider count in population: 22,400 (O)"
D — "Composite score: weighted sum of dimensions D1-D4 (D)"
I — "Billing pattern consistent with upcoding based on peer comparison (I)"
A — "Minimum subgroup size set to 10 pending statistical review (A)"

### Where Tags Appear

- Evidence log entries
- Markdown cells summarizing analytical outputs
- Decision brief memos
- Any session note that records an analytical finding

## Data Ethics Standards

### Core Requirement

All analytical outputs must be reported without bias. Findings describe
what the data shows — nothing more. No output, visualization title,
axis label, markdown cell, memo, or log entry may assert intent,
causation, or wrongdoing on the part of any individual, organization,
or entity in the data.

This applies under every O/D/I/A tag and in every section of every
notebook.

### Required Language

Use language that describes observations and patterns only.

Correct:
- "anomalous billing pattern"
- "elevated composite risk score"
- "flagged for program integrity review"
- "billing volume exceeds peer median by X%"
- "record meets threshold for escalation pathway"

Incorrect:
- "fraudulent provider"
- "intentional overbilling"
- "confirmed abuse"
- "provider committed fraud"

### Source Attribution

When a rule, standard, or finding derives from an external source,
that source is cited inline at the point of use. Citation format is
plain text — no formal academic style required — but must include
enough information for the source to be located independently.

Examples of acceptable inline citations:
# Source: PEP 8 — Style Guide for Python Code (python.org/dev/peps/pep-0008)
# Source: IBM Carbon Design System CVD palette (carbondesignsystem.com)
# Source: [Agency or publication name, document title, URL if available]

If no external source exists — the standard is original to this
project — the source reference reads:
# Source: None — original standard established [YYYY-MM-DD]

### Sensitive Data Handling
# [FILL IN PER PROJECT — document any data sensitivity requirements,
# access restrictions, or compliance obligations specific to this
# project's data sources]

## Tool Stack Standards

### Data Library Standard

New projects use the following three-tool stack. Each tool has a defined
lane. Do not substitute or collapse lanes without documented rationale
in the project decision log.

### Tool Assignments

DuckDB — intake and filtering layer
  - Read and query parquet and CSV files directly without full memory load
  - Filter large populations to analytical subsets before DataFrame creation
  - Multi-file and multi-year queries handled at this layer
  - Returns Polars DataFrame via .pl() method

Polars — analytical layer
  - All feature engineering, scoring, peer group calculations, and
    pathway assignment performed in Polars
  - Immutable DataFrames — always assign results, no in-place operations
  - Write outputs as parquet via df.write_parquet()

Pandas — dependency fallback only
  - Use only when a required library outputs pandas and cannot be
    redirected
  - Convert immediately: pl.from_pandas(df)
  - Do not build analytical logic in pandas in new projects

### Standard Flow

DuckDB (filter/query) → Polars (analyze) → matplotlib (visualize)
                              ↕
                      pandas (fallback only)

### Import Standard

Every new notebook CONFIG cell must include:

import duckdb
import polars as pl
DUCKDB_VERSION = duckdb.__version__   # Logged for reproducibility
POLARS_VERSION = pl.__version__       # Logged for reproducibility

### Environment Verification

Confirm both DuckDB and Polars versions before building new notebooks.

import duckdb; print(duckdb.__version__)
import polars as pl; print(pl.__version__)

Note versions in the notebook HEADER cell. If either version is
significantly behind the current release, note it and adjust syntax
accordingly.

### Visualization Library

matplotlib is the project standard for all figures. This does not
change regardless of which data library is in use.

### Backwards Compatibility

This tool stack applies to all new projects. Existing projects that
were built on pandas are not retrofitted. If an existing project is
being extended, retain the original library for consistency and note
the exception in the project decision log.

