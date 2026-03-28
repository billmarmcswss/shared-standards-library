# CHANGELOG.md
# Shared Standards Library
# Purpose: Tracks all version changes across every document in the library.
# No document in this library is silently updated — every change is recorded here.
#
# Version: 1.0
# Last Updated: 2026-03-28 HH:MM TZ
# Status: Active
# Applies To: All Projects
# Source References: None — original standard established 2026-03-28
# Change Summary: Initial version — CHANGELOG established 2026-03-28

---

## Entry Format Reference

Every change to any document in this library gets one entry below using this
exact format. Do not skip entries for small changes — every change is recorded.
```
## [YYYY-MM-DD HH:MM TZ] — [Document Name] v[Major.Minor]
**Change Type:** [Major | Minor]
**Changed By:** [author or session reference]
**Summary:** [plain-language description of what changed]
**Reason:** [why the change was made — industry standard update, error correction,
             lesson learned, new project requirement, etc.]
```

### Change Type Definitions

| Type | When to Use |
|---|---|
| `Major` | Substantive change to content, structure, or governing rules |
| `Minor` | Small correction, clarification, or addition that does not change intent |

---

## Change Log

## 2026-03-28 1333 EST — .gitignore v1.0
**Change Type:** Major
**Changed By:** Bill Matthews — session 2026-03-28
**Summary:** Initial commit — added .gitignore to documents-only repository
**Reason:** Repository established — .gitignore created to exclude temporary files

---

## 2026-03-28 1333 EST — LIBRARY_README.md v1.0
**Change Type:** Major
**Changed By:** Bill Matthews — session 2026-03-28
**Summary:** Initial commit — governing document for Shared Standards Library
**Reason:** Library established — LIBRARY_README.md created to define purpose,
            inventory, usage, storage, and versioning protocol for all future
            projects
```

---

Save it as `CHANGELOG.md` in the root of:
```
C:\Users\billm\OneDrive\Projects\SharedStandards\shared-standards-library\