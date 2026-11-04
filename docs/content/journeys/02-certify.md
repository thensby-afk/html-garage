# Journey: Certify

## Purpose
Citizen developers certify their HTML tools to obtain a CMMYY code and C001 certificate, creating a registry entry that marks the tool as reviewed and compliant.

## Actors

| Actor | Role |
|---|---|
| Citizen Developer | Owns the tool and drives the journey |
| HTML Garage | Runs checks, generates certificate, writes registry entry |
| AI coding assistant | Remediates tool if pre-scan fails (off-platform step) |
| SQLite registry | Stores the registration record |
| Tile file storage | Stores the certified HTML and scan report |

## Steps

**Notice screen**
1. Developer navigates to **Certify**. The app displays a pre-read notice: what certification involves, what the checks are, and what the certificate means.
2. Developer answers two scope questions: (a) does the tool ingest client data? (b) does it deploy to a client environment? Answers affect the risk rating and check severity.
3. Developer checks a personal declaration confirming compliance with data protection obligations.
4. Developer clicks **I understand — proceed**.

**Intake**
5. Developer selects **New solution** or **Recertification**. If recertification, they choose the existing solution from a dropdown; the form pre-fills.
6. Developer completes the intake form: solution name, programme, description, owner email.
7. Developer uploads the HTML file.
8. Developer clicks **End pre-scan** to submit.

**Pre-scan**
9. The app runs C1–C9 checks against the uploaded file and displays results: PASS, REVIEW, or FAIL per check, with detail.
10. If any critical checks fail (C1, C4, or C3/C5 when clientData=true): **FAIL path** — developer must remediate before proceeding.
11. If checks pass or return only REVIEWs: developer proceeds.

**Remediation (FAIL path only)**
12. Developer downloads a personalised remediation prompt (incorporating their specific failures).
13. Developer uses the prompt with their AI assistant to fix the tool.
14. Developer returns to the **Upload remediated file** screen and uploads the fixed version.
15. Developer clicks **End post-scan**.

**Post-scan and certification**
16. App re-runs C1–C9. Results are shown in a before/after comparison table.
17. If scan passes or conditionally passes: app generates the CMMYY code, C001 certificate, and certification footer.
18. App stores the certified file and scan report in Tile file storage.
19. App writes the registration record to the SQLite registry.
20. App displays the CMMYY code, certificate download link, and instructions to rename the file.
21. Developer downloads the certificate and renames their file to include the `_CMMYY` suffix.

## Key decision points

- **Pre-scan FAIL.** Developer must remediate and re-upload. The app remains on the upload screen.
- **Post-scan FAIL.** Same — developer iterates until the scan passes.
- **Post-scan COND (conditional pass).** Certificate is issued with a note of outstanding review items. The developer is not blocked.
- **Recertification.** Same flow as new, but the intake form pre-fills from the existing registry entry and the new record links back to the previous via `previous_id`.

## Inputs and outputs

| | Description |
|---|---|
| **Input** | HTML tool file; solution metadata (name, programme, owner, description); scope answers |
| **Output** | CMMYY code embedded in HTML; C001 certificate; registry entry; stored file and report |

## Notes

The CMMYY code encodes the expiry date: C + month (2 digits) + year (2 digits) of the next-due date. A solution certified in October 2026 with a 12-month validity period receives code C1027. The developer renames their file accordingly: `mysolution_C1027.html`.

Certification expires 12 months from the date of issue. Solutions must be recertified before expiry to remain in good standing.
