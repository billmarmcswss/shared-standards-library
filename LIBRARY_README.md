# LIBRARY_README.md
# Shared Standards Library
# Purpose: Governing document for the Shared Standards Library.
# Defines what the library is, what it contains, how it is maintained,
# and how documents travel into new projects.
#
# Version: 1.0
# Last Updated: 2026-03-24 0919 EST
# Status: Active
# Applies To: All Projects
# Source References: None — original governing document established 2026-03-24
# Change Summary: Initial version — library established 2026-03-24

---

## Purpose

The Shared Standards Library is a collection of living documents that serve as the
foundation for all analytical and data projects. It exists to ensure that every
project begins with a consistent, principled, and well-documented starting point
regardless of subject matter, data source, or analytical method.

These documents are not static. They are expected to evolve as industry practices
change, as new tools are adopted, and as lessons are learned across projects. Every
change is tracked in CHANGELOG.md with a version number, date, and plain-language
description of what changed and why.

This library is not a project. It does not contain data, notebooks, or project-specific
outputs. It contains only the standards, templates, and guides that inform how projects
are built and conducted.

### Core Principles

- **Consistency** — every project starts from the same foundation
- **Integrity** — findings are reported without bias, assertions are supported by evidence
- **Attribution** — sources of data, standards, and methods are cited where they exist
- **Versioning** — every document change is recorded; nothing is silently updated
- **Portability** — documents travel into new projects cleanly without modification

---

## Document Inventory

The library contains ten documents organized across three locations within the
repository. Every document carries a standard header block showing version, status,
and source references.

### Root
| Document | Purpose |
|---|---|
| `LIBRARY_README.md` | Governs the library — this document |
| `PROJECT_STANDARDS.md` | Master coding and analytical standards for all projects |
| `CHANGELOG.md` | Tracks all version changes across every document in the library |

### guides\
| Document | Purpose |
|---|---|
| `DATA_ETHICS_GUIDE.md` | Unbiased analysis principles, no-assertion language, source attribution |
| `OBIA_TAGGING_GUIDE.md` | O/D/I/A evidence tagging reference with examples |
| `VISUALIZATION_STANDARDS.md` | CVD compliance, palette standards, chart selection guidance |

### templates\
| Document | Purpose |
|---|---|
| `SESSION_CONTEXT_TEMPLATE.md` | Blank scaffold for any new project session continuity file |
| `NOTEBOOK_TEMPLATES.md` | Ready-to-paste cell blocks — HEADER, CONFIG, EVIDENCE |
| `DECISION_LOG_TEMPLATE.md` | Blank decision log scaffold with entry format pre-built |
| `EVIDENCE_LOG_TEMPLATE.md` | Blank evidence log scaffold with O/D/I/A structure pre-built |

### Document Status Definitions
| Status | Meaning |
|---|---|
| `Active` | Current version — use this document |
| `Draft` | Under construction — not yet ready for use in projects |
| `Deprecated` | Superseded by a newer document — do not use in new projects |

---

## How to Use This Library

### Starting a New Project

Every new project begins with the same three steps regarding this library:

**Step 1 — Copy the core documents into the new project**

These three documents go into every new project's Claude knowledge base without
exception:

| Document | Why |
|---|---|
| `PROJECT_STANDARDS.md` | Coding and analytical rules that govern all work |
| `DATA_ETHICS_GUIDE.md` | Unbiased findings and source attribution principles |
| `SESSION_CONTEXT_TEMPLATE.md` | Fill in project-specific fields and save as SESSION_CONTEXT.md |

**Step 2 — Copy additional documents as the project type warrants**

| Project Type | Additional Documents |
|---|---|
| Notebook-based analytics | `NOTEBOOK_TEMPLATES.md`, `OBIA_TAGGING_GUIDE.md`, `VISUALIZATION_STANDARDS.md` |
| Decision support framework | `DECISION_LOG_TEMPLATE.md`, `EVIDENCE_LOG_TEMPLATE.md` |
| Both | All of the above |

**Step 3 — Do not modify library documents inside a project**

Documents copied into a project are working copies. If a standard needs to change,
the change is made here in the library first, then the updated document is copied
into any active projects that need it. The library is always the source of truth.

### Maintaining This Library

When any document in this library is updated:

1. Edit the local file in:
   `C:\Users\billm\OneDrive\Projects\SharedStandards\shared-standards-library\`
2. Update the document's version number, last updated date, and change summary
   in its header block
3. Record the change in `CHANGELOG.md`
4. Commit and push to GitHub:
```
   git add .
   git commit -m "descriptive message explaining what changed and why"
   git push origin main
```
5. Re-upload the updated document to the `Shared Standards Library` Claude Project
   knowledge base

### One Unit of Work at a Time

Documents in this library are built and reviewed one section at a time. No document
is committed to GitHub or uploaded to the Claude Project knowledge base until it is
complete and confirmed. This applies equally to notebook cells, document sections,
and template blocks — the same production discipline governs all units of work.

---

## Backup and Storage

The library maintains a three-layer storage and backup structure. All three layers
are expected to be current at all times.

### Storage Layers

| Layer | Location | How It Updates | Protects Against |
|---|---|---|---|
| OneDrive | `C:\Users\billm\OneDrive\Projects\SharedStandards\shared-standards-library\` | Automatic continuous sync | PC drive failure, file corruption |
| GitHub | `https://github.com/billmarmcswss/shared-standards-library` | Manual commit and push | Everything — also provides full version history |
| Claude Project | `Shared Standards Library` project knowledge base | Manual upload | Session continuity — what Claude reads during work sessions |

### What Each Layer Holds

**OneDrive** is the primary working copy. All edits happen here first. OneDrive
syncs automatically to Microsoft's cloud without any action required, providing
continuous protection against local hardware failure.

**GitHub** is the version-controlled remote repository. Every commit captures a
named, dated snapshot of the library at that point in time. GitHub is the authoritative
record of what changed, when, and why.

**Claude Project knowledge base** is the working context layer. It is what Claude
reads during sessions. It must be manually updated when documents change — it does
not sync automatically with OneDrive or GitHub.

### Important Notes

- Large binary files such as raw data CSVs and parquet files do not belong in this
  repository. This is a documents-only library. OneDrive handles markdown files
  without issue.
- The external hard drive remains available as an optional fourth backup layer for
  periodic manual copies if desired.
- If the three layers fall out of sync, GitHub is the authoritative source. Restore
  from GitHub first, then re-upload to the Claude Project knowledge base.

---

## Versioning and Changelog Protocol

### Document Version Numbering

Every document in this library carries a version number in its header block.
Version numbers follow a simple two-part format:
```
Major.Minor
```

| Part | When It Increments | Example |
|---|---|---|
| Major | Substantive change to content, structure, or governing rules | 1.0 → 2.0 |
| Minor | Small correction, clarification, or addition that does not change intent | 1.0 → 1.1 |

Version 1.0 is the initial published version of any document. Draft versions
prior to first publication carry no version number — they are marked `Status: Draft`
in the header block until confirmed and committed.

### Header Block Standard

Every document in this library opens with this header block:
```
# [Document Title]
# [Library or Project Name]
# Purpose: [one sentence]
#
# Version: [Major.Minor]
# Last Updated: [YYYY-MM-DD HH:MM TZ]
# Status: [Active | Draft | Deprecated]
# Applies To: [All Projects | specific context]
# Source References: [external standards cited, if any]
# Change Summary: [one-line description of what changed in this version]
```

### Changelog Protocol

Every change to any document in this library is recorded in `CHANGELOG.md`
regardless of how small the change appears. Silent updates are not permitted.

Each entry in `CHANGELOG.md` follows this format:
```
## [YYYY-MM-DD HH:MM TZ] — [Document Name] v[Major.Minor]
**Change Type:** [Major | Minor]
**Changed By:** [author or session reference]
**Summary:** [plain-language description of what changed]
**Reason:** [why the change was made — industry standard update, error correction,
             lesson learned, new project requirement, etc.]
```

### Source Attribution Standard

When a rule, standard, or principle in any library document derives from an
external source, that source is cited inline at the point of use. Citation
format is plain text — no formal academic style required — but must include
enough information for the source to be located independently.

Examples of acceptable inline citations:
```
# Source: PEP 8 — Style Guide for Python Code (python.org/dev/peps/pep-0008)
# Source: CMS Medicare Claims Processing Manual, Chapter 12
# Source: IBM Carbon Design System CVD palette (carbondesignsystem.com)
# Source: Tufte, Edward R. The Visual Display of Quantitative Information, 2001
```

If no external source exists — the standard is original to this library —
the source reference in the header block reads:
```
# Source References: None — original standard established [YYYY-MM-DD]
```
```

---

That is the complete document. Save it as `LIBRARY_README.md` in the root of:
```
C:\Users\billm\OneDrive\Projects\SharedStandards\shared-standards-library\