# Solution Overview

## What it is

HTML Garage is a web-based governance and certification platform for citizen-developer HTML tools. It provides a structured process — modelled on the MOT testing regime for motor vehicles — that lets Tech Services set and enforce security standards while giving citizen developers a clear, low-friction path to compliance.

The analogy is deliberate. The MOT is a periodic check against a defined standard. It does not prevent cars from being driven — it ensures that cars on the road meet a minimum roadworthiness threshold. The HTML Garage does the same for HTML tools.

## The model

| Vehicle analogy | HTML Garage equivalent |
|---|---|
| MOT test | C1–C9 automated security scan |
| Tax disc | CMMYY certification code embedded in the tool |
| Vehicle registration | Entry in the SQLite registry |
| Garage | HTML Garage web app |
| MOT certificate | C001 certificate PDF |
| Recall notice | Tech Services recall for solutions that fail updated checks |
| Insurance invalidated by modification | Certification invalidated if tool is modified post-certification |

## Key capabilities

**Certification.** Citizen developers bring their tools through a structured intake, pre-scan, remediation, and post-scan process. Tools that pass receive a certificate and a CMMYY code embedded in the HTML. The CMMYY encodes the certification expiry month and year (C + MM + YY).

**Registry.** Every certified solution is recorded in a SQLite database: solution name, description, owner, programme, risk rating, certification date, and expiry. The registry is searchable and filterable.

**Recertification.** Solutions must be recertified on expiry. The recertification journey pre-fills registration details from the existing registry entry.

**Change of ownership.** When a solution changes hands, the registry is updated to reflect the new owner. The certification remains valid.

**Retirement.** When a solution is decommissioned, it is marked as retired in the registry. Retired solutions remain visible for audit purposes.

**Audit.** Tech Services can verify any tool in the wild by entering its CMMYY code. The audit view returns the full registry entry and flags whether the certification has expired.

**Rescan.** Tech Services can re-run the C1–C9 checks against all stored certified files at any time. This catches tools that pass initial certification but fail updated criteria.

**Recall.** When a rescan identifies at-risk solutions, Tech Services can generate a filtered list of affected owners and produce a recall notice.

## Architecture

```
Accenture Tile platform
  └── HTML Garage (single self-contained HTML file)
        ├── SQLite database (Tile-managed)
        │     └── registrations table
        ├── File storage (Tile-managed)
        │     └── tools/{id}/{filename}.html  (certified files)
        │     └── tools/{id}/report.md        (scan reports)
        └── User identity (tile.role())
              └── canWriteSqlite flag gates registry writes
```

The app runs entirely client-side. No server-side code. The Tile platform provides SQLite access, file storage, and user identity. All security logic — scanning, risk rating, certificate generation — runs in the browser.

## Enforcement boundary

A tool that has been through the HTML Garage carries:
- A `_CMMYY` suffix in its filename (e.g. `dashboard_C1026.html`)
- An embedded `acn-cmmyy` meta tag and certification footer
- An entry in the registry

A tool without these markers is unlicensed. Tech Services can use the CMMYY suffix as a visual check, and the audit function to confirm registry status.
