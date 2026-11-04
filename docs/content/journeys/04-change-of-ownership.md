# Journey: Change of Ownership

## Purpose
When a solution changes hands — the original owner leaves the team, moves to a different role, or hands off — the registry must reflect the new owner. This journey updates the record without requiring recertification.

## Actors

| Actor | Role |
|---|---|
| Current or departing owner (or their manager) | Initiates the transfer |
| New owner | Receives ownership; named in the updated record |
| HTML Garage | Updates the registry entry |
| SQLite registry | Stores the updated record and transfer history |

## Steps

1. User navigates to **The Filing Cabinet**.
2. User clicks **Change of Ownership** (from the board or directly from home screen).
3. The app displays a dropdown of all active registered solutions.
4. User selects the solution to transfer.
5. User enters the new owner's email address and confirms the transfer.
6. App updates the `owner_email` field in the registrations table and writes a transfer history record.
7. App displays a confirmation screen with the updated details.

## Key decision points

- **Multiple solutions.** The transfer covers one solution at a time. If multiple solutions need to be transferred, the journey is repeated.
- **Retired solutions.** Retired solutions cannot have their ownership transferred. They must be reactivated first (or a new certification raised).

## Inputs and outputs

| | Description |
|---|---|
| **Input** | Selected solution; new owner email |
| **Output** | Updated registry entry; transfer history record |

## Notes

The existing certification remains valid after a transfer. The new owner inherits the existing CMMYY code and expiry date. At the next recertification, the new owner's email will be recorded as certifier.
