# Process Registry

Central registry of all documented processes with sequential numbering.

---

## Active Processes

| # | Process ID | Process Name | Status | Created | Last Updated |
|---|------------|--------------|--------|---------|--------------|
| 001 | ONB-001 | Onboarding | TRANSFORMATION COMPLETE | 2025-12-09 | 2025-12-09 |
| 002 | COB-002 | Client Onboarding process | COMPLETE | 2025-12-09 | 2025-12-09 |
| 003 | COB-003 | Client Onboarding | COMPLETE | 2025-12-09 | 2025-12-09 |

---

## Registry Notes

- **Folder Pattern**: `{###}-{PROCESS_NAME}` (e.g., `001-onboarding`, `002-loan-origination`)
- **Next Number**: 4
- **Status Values**: `DRAFT`, `IN_PROGRESS`, `REVIEW`, `COMPLETE`, `TRANSFORMATION COMPLETE`, `APPROVED`, `ARCHIVED`

---

## How to Use

1. When starting a new process, check the **Next Number** above
2. Create folder using pattern: `docs/processes/{###}-{process-name-kebab-case}`
3. Add entry to the table above
4. Increment **Next Number** for next process
