# Journey: Update Security Criteria

## Purpose
Security threats evolve. When a new vulnerability class emerges — a new attack vector, a newly disclosed CVE affecting a common pattern — Tech Services must update the C1–C9 checks to detect it, redeploy the app, and assess the impact on existing registered solutions.

## Actors

| Actor | Role |
|---|---|
| Tech Services (security team) | Identifies threat, defines new check, initiates rescan |
| HTML Garage (developer) | Updates `runScan()` logic and redeploys the app |
| HTML Garage (Rescan All view) | Runs updated checks against all stored solutions |
| Citizen developers (affected) | Receive recall notice if their solutions now fail |

## Steps

**Define the new check**
1. Tech Services identifies a new threat or vulnerability pattern (e.g. a newly exploitable JS pattern, a supply chain compromise affecting a specific library pattern).
2. Tech Services translates the threat into a deterministic detection rule: a regex or structural test that can be applied to HTML source text.
3. Tech Services raises a change request with the HTML Garage maintainer.

**Update the app**
4. The maintainer adds or modifies the check in `runScan()` within `harrys-garage.html` (source: `harrys-garage.html` in the repository).
5. The updated check is assigned a check ID (extending C9 as C10, C11, etc., or updating an existing check's logic).
6. The updated security prompt on the Security Prompts screen is revised to describe the new requirement in plain language.
7. The maintainer runs the updated app against a set of test files to validate the check logic.
8. The maintainer deploys to the test site and confirms, then deploys to production.

**Rescan existing solutions**
9. Tech Services navigates to **Tech Services > Rescan All**.
10. The app loads all active solutions that have stored files.
11. Tech Services clicks **Rescan all** (or rescans solutions individually).
12. The app retrieves each stored certified file from Tile file storage, runs the updated `runScan()` logic, and updates `risk_rating`, `last_scan_at`, and `last_scan_result` in the registry.
13. Solutions whose risk rating has changed are highlighted.
14. If multiple solutions now fail: Tech Services navigates to **Recall** to generate a recall list.

## Key decision points

- **Check targets a pattern that existing certified tools are unlikely to have.** Impact assessment may show no existing solutions are affected. No recall required.
- **Check targets a common pattern (e.g. a widely used CDN).** Many existing solutions may fail. Recall and remediation at scale.
- **Check introduces a new REVIEW category vs. a new FAIL category.** REVIEW flags do not force recall but are recorded in the scan result for visibility.

## Inputs and outputs

| | Description |
|---|---|
| **Input** | Threat description; detection rule; updated `runScan()` code |
| **Output** | Redeployed app with updated check; rescan results in registry; recall list (if needed) |

## Notes

The check logic lives entirely in the app source code. There is no external configuration file. Updating checks requires a code change and a redeployment. The deploy workflow is documented in `scripts/deploy-prod.ps1`.

A future version may extract check definitions into a configuration object to allow updates without touching the scan function directly.
