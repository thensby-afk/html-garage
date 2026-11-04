# Journey: Check Register

## Purpose
Solution owners, managers, and Tech Services need visibility of what tools are registered, their status, and their certification details. The Filing Cabinet provides a searchable view of all registry entries.

## Actors

| Actor | Role |
|---|---|
| Any authenticated user | Browses and queries the registry |
| HTML Garage | Queries SQLite and renders results |
| SQLite registry | Source of record |

## Steps

1. User navigates to **The Filing Cabinet** (from home screen or top nav).
2. The app queries the `registrations` table and displays all entries in a sortable table: solution name, programme, owner, risk rating, certification date, expiry date, status.
3. User can filter by status (active / retired) or search by name or programme.
4. User clicks a solution row to expand details: description, CMMYY code, cert serial, scope flags (client data, client deployment), journey type.
5. If the user has write access, action buttons appear: **Change of Ownership**, **Retire**.

## Key decision points

- **Active vs. retired solutions.** Retired solutions remain in the registry but are visually distinguished. The default view shows active solutions; retired are accessible via filter.
- **Expired certification.** Solutions past their `next_due_at` date are flagged with an EXPIRED badge. They remain in the registry but should be prioritised for recertification.

## Inputs and outputs

| | Description |
|---|---|
| **Input** | None — the register is read from SQLite on load |
| **Output** | Read-only view of all registration records |

## Notes

The register is the authoritative source of truth for the HTML tool estate. It is the basis for audit checks, recall operations, and recertification tracking. It does not currently support bulk export — this is planned.
