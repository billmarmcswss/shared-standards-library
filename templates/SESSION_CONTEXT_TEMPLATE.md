# SESSION_CONTEXT_TEMPLATE.md
# [Project Name]
# Purpose: Session continuity logbook for project work — tracks status,
# decisions, and progress across all sessions.
#
# Version: 1.0
# Last Updated: [2026-03-26 1619 EST]
# Status: Active
# Applies To: [Project Name]
# Source References: None — original standard established [YYYY-MM-DD]
# Change Summary: Initial version — session log opened [YYYY-MM-DD]

---

## Log Metadata

| Field             | Value                                      |
|-------------------|--------------------------------------------|
| Log Number        | Log [N] — [Project Name]                  |
| Status            | ACTIVE — opened [YYYY-MM-DD HH:MM TZ]     |
| Continued From    | [N/A or filename of previous log]          |
| Continued In      | [N/A until this log is closed out]         |
| Closed Out        | [N/A until closed — enter date/time/title] |

---
## Current Status Dashboard
# This section is always current. Update it at the start and end of every session.
# It reflects the state of the project RIGHT NOW — not history.

| Field                        | Value                                      |
|------------------------------|--------------------------------------------|
| Current Document / Task      | [Name of document or task in progress]     |
| Section / Phase In Progress  | [Specific section or phase being worked]   |
| Last Completed Milestone     | [What was finished — date/time]            |
| Next Queued Item             | [What comes after current task]            |
| Open Decisions / Blockers    | [Anything unresolved that affects work]    |
| Session Status               | [OPEN — HH:MM TZ | CLOSED — HH:MM TZ]     |

---
## Carryover Block
# Populated when this log is opened from a previous log.
# If this is Log 1 / a fresh project, enter N/A in all fields.
# Do not delete this block even if empty — it confirms no carryover intentionally.

| Field                        | Value                                      |
|------------------------------|--------------------------------------------|
| Carried In From              | [N/A or filename of previous log]          |
| Carryover Date / Time        | [N/A or YYYY-MM-DD HH:MM TZ]              |
| Items Carried Forward        | [N/A or list of open items brought in]     |
| Decisions Carried Forward    | [N/A or unresolved decisions brought in]   |
| Notes from Previous Log      | [N/A or anything that didn't fit above]    |

---
## Session Log
# Permanent running record of all sessions. Never delete entries.
# Add a new entry block at the TOP of the log after the header line
# so the most recent session is always visible without scrolling.
# Use [DONE], [WIP], [NEXT], or [HOLD] tags on all task lines.

---

### Entry Format Reference
## [YYYY-MM-DD HH:MM TZ] — [Short Session Title]
**Session Opened:**  [YYYY-MM-DD HH:MM TZ]
**Session Closed:**  [YYYY-MM-DD HH:MM TZ | OPEN if not yet closed]
**Milestone:**       [One-line description of what this session accomplished]

**Tasks This Session:**
- [DONE] [Task description]
- [WIP]  [Task description — carry to next session if incomplete]
- [NEXT] [Task queued but not started]
- [HOLD] [Task deferred — reason noted inline]

**Decisions Made:**
- [Decision description — enough detail to reconstruct reasoning later]

**Notes:**
- [Anything that doesn't fit above — observations, blockers, references]

---

### Log Entries — Most Recent First

[First entry goes here]

---
## Closeout Entry Format — Use When Paginating to a New Log
## [YYYY-MM-DD HH:MM TZ] — LOG CLOSED — Continued in [new filename]
**Reason for Pagination:** [Milestone reached | Log length | Other]
**Open Items Carried Forward:** [List or N/A]
**New Log Started:** [YYYY-MM-DD HH:MM TZ]

---