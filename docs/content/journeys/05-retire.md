# Journey: Retire

## Purpose
When a solution is decommissioned — the business process it supported has ended, or the tool has been replaced — it should be formally retired in the registry. This closes the record and removes the tool from active reporting while preserving the audit trail.

## Actors

| Actor | Role |
|---|---|
| Solution owner | Initiates the retirement |
| HTML Garage | Updates the registry entry |
| SQLite registry | Stores the retired status and reason |

## Steps

1. Owner navigates to **The Filing Cabinet**.
2. Owner clicks **Retire** (from the board or directly from home screen).
3. The app displays a dropdown of all active registered solutions.
4. Owner selects the solution to retire.
5. Owner provides a brief retirement reason (e.g. "Process discontinued", "Replaced by Power BI dashboard").
6. Owner checks a declaration confirming the solution is no longer in use.
7. Owner clicks **Retire solution**.
8. App sets `status = 'retired'`, records `retired_at`, `retirement_reason`, and `retirement_declared_by` in the registry.
9. App displays a confirmation screen.

## Key decision points

- **Solution still in use.** If the solution is still being used by others, the owner should not retire it unilaterally. Coordination with users is out of scope for this journey.
- **Retired in error.** The registry does not currently support un-retiring a solution. If retired in error, a new certification must be raised.

## Inputs and outputs

| | Description |
|---|---|
| **Input** | Selected solution; retirement reason; declaration |
| **Output** | Registry entry updated: status=retired, retired_at, retirement_reason |

## Notes

Retired solutions remain visible in the registry with a RETIRED status badge. They are excluded from the default active-solutions view but accessible via filter. This preserves the audit trail for solutions that may be referenced in historical records.
