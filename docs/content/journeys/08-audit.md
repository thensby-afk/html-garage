# Journey: Audit

## Purpose
Tech Services needs to verify, on demand, whether a tool found in the wild is legitimately certified — and whether it has been modified since certification. This journey provides a rapid compliance check using the tool's CMMYY code.

## Actors

| Actor | Role |
|---|---|
| Auditor (Tech Services) | Locates a tool in use, performs the audit check |
| HTML Garage (Audit view) | Queries the registry and returns verification result |
| SQLite registry | Source of certification record |

## Steps

**Visual pre-check (before opening the app)**
1. Auditor locates an HTML tool in use (e.g. received by email, found on a shared drive, or observed in a business process).
2. Auditor checks the filename: does it end with `_CMMYY.html` (e.g. `forecast_C1026.html`)? If not, the tool is likely unlicensed — proceed to formal check.
3. Auditor opens the tool and checks for a certification footer at the bottom of the page. A certified tool will display a footer with the CMMYY code and certification date.

**Formal check in the app**
4. Auditor navigates to **Tech Services > Audit**.
5. **Option A:** Auditor enters the CMMYY code from the tool's footer into the text field and clicks **Look up**.
6. **Option B:** Auditor uploads the HTML file — the app extracts the CMMYY code from the `acn-cmmyy` meta tag or filename suffix and performs the lookup automatically.
7. The app queries the registry for a matching `cmmyy_code`.

**Result interpretation**
8. **Not found:** "No registered solution found for that code — this tool is unlicensed." The tool has not been certified and should not be in use.
9. **Found, active, valid:** Full certificate details are displayed. The tool is in good standing.
10. **Found, active, expired:** Details are displayed with an EXPIRED badge. The tool's certification has lapsed — the owner should be directed to recertify.
11. **Found, retired:** Details are displayed with a RETIRED badge and a note that the solution is no longer in service. If the tool is still in use, this is a compliance issue.

## Key decision points

- **CMMYY code not visible in footer.** The tool may have been modified post-certification (the footer may have been stripped), or it was never certified. Upload the file for extraction — if extraction fails, the tool is unlicensed.
- **Code found but details don't match the tool.** The CMMYY code may have been copied from a different certified tool and fraudulently embedded. The solution name and owner in the registry should match the tool's stated purpose.
- **Tool has been modified post-certification.** Certification is invalidated by modification, analogous to insurance being voided by unapproved vehicle modifications. Tech Services should direct the owner to recertify.

## Inputs and outputs

| | Description |
|---|---|
| **Input** | CMMYY code (typed or extracted from uploaded file) |
| **Output** | Registry record (solution name, owner, programme, expiry, status) or unlicensed flag |

## Notes

The current audit check is registry-based only: it confirms that a solution with the given CMMYY code was certified, and returns its status. It does not perform a file hash comparison to detect post-certification modification. File integrity checking (comparing a hash of the current file against a hash stored at certification time) is planned for a future version.

As an interim control, auditors can use the Rescan All function to re-run C1–C9 against the stored certified version and compare results against the tool in hand.
