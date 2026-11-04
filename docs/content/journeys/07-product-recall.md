# Journey: Product Recall

## Purpose
When a rescan identifies solutions that now fail updated security checks — or when a known vulnerability is confirmed to affect a class of tools — Tech Services must contact affected owners and direct them to remediate and recertify.

## Actors

| Actor | Role |
|---|---|
| Tech Services | Triggers recall, generates contact list, tracks completion |
| HTML Garage (Recall view) | Filters registry, generates recall notice |
| Solution owners | Receive notice, remediate, recertify |

## Steps

**Identify affected solutions**
1. Tech Services navigates to **Tech Services > Recall**.
2. Tech Services selects filter criteria: Failed C1, Failed C4, risk rating HIGH/CRITICAL, or certification expired. Multiple criteria can be combined.
3. Tech Services clicks **Generate list**.
4. The app queries the registry (using stored `last_scan_result` JSON for check-level filtering) and returns all matching active solutions.

**Contact owners**
5. Tech Services reviews the list: solution name, owner email, programme, risk rating, expiry date.
6. Tech Services clicks **Copy email list** — all owner email addresses are copied to clipboard as a comma-separated list.
7. Tech Services clicks **Generate recall notice** — a formatted recall notice opens in a new window, listing all affected solutions and instructing owners to bring their tools in within 10 working days.
8. Tech Services sends the recall notice to owners via email (this step is performed outside the app).

**Owners respond**
9. Each owner receives the notice and navigates to the HTML Garage.
10. Owner follows the **Certify (Recertification)** journey, selecting their solution from the dropdown.
11. Owner remediates any failing checks and completes certification.
12. The registry entry is updated: new risk rating, new expiry date, previous_id linking to the old record.

**Track completion**
13. Tech Services returns to **Rescan All** to verify that recalled solutions have been recertified and their risk ratings have improved.
14. When all affected solutions are recertified or retired, the recall is considered closed.

## Key decision points

- **Owner is unresponsive.** After 10 working days, Tech Services can escalate via the owner's programme lead. The registry provides programme information for each solution.
- **Solution cannot be remediated.** Owner retires the solution via the **Retire** journey and raises a new certification for a replacement if needed.
- **Recall at scale.** For large-scale recalls (10+ solutions), Tech Services may choose to run the recall in waves by programme, to avoid overwhelming the cert queue.

## Inputs and outputs

| | Description |
|---|---|
| **Input** | Filter criteria (check failures, risk rating, expiry); last_scan_result data from registry |
| **Output** | Filtered solution list; recall notice document; email contact list |

## Notes

The recall notice is generated as a printable HTML document in a new browser window. Tech Services should copy the contents into an email rather than sharing the generated window directly.

Recall tracking is currently manual — Tech Services monitors recertification progress via the Filing Cabinet. Automated recall status tracking is planned.
