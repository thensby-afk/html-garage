# C1–C9 Security Checks Reference

Checks are run automatically on upload. The scan reads the HTML source and applies each rule deterministically — no manual interpretation required.

## Check definitions

| Check | Label | What it detects | Severity | Result logic |
|---|---|---|---|---|
| C1 | External dependencies | `src=` or `href=` pointing to an external URL | **Critical** | FAIL if any found |
| C2 | Content Security Policy | Presence of a CSP `<meta>` tag | Standard | FAIL if absent |
| C3 | DOM injection / innerHTML | `.innerHTML =` assignments | **Review** | REVIEW if any found |
| C4 | Dynamic code execution | `eval()` or `new Function()` calls | **Critical** | FAIL if any found |
| C5 | Input validation | Presence of validation patterns on form inputs | Standard | PASS if score ≥ 3 of: `required`, `.trim()`, length check, pattern check, empty check; REVIEW if score 1–2; FAIL if score 0 and inputs exist |
| C6 | Formula injection guard | CSV export with no formula injection guard | Standard | REVIEW if CSV export found without guard; N/A if no CSV |
| C7 | Data privacy / local storage | `localStorage`, `sessionStorage`, `document.cookie` | **Review** | REVIEW if any found |
| C8 | Accenture Security Review block | Presence of `ACCENTURE SECURITY REVIEW` or `acn-cert-serial` | Standard | FAIL if absent |
| C9 | Certification footer | Presence of `acn-cmmyy` or `hmw-footer` | Standard | FAIL if absent |

## Severity definitions

| Severity | Meaning |
|---|---|
| **Critical** | Automatic overall FAIL regardless of other results |
| **Review** | Flagged for manual review; does not cause automatic fail unless `clientData=true` |
| **Standard** | FAIL causes overall FAIL or COND result |

## Risk rating calculation

The overall risk rating is computed from the scan results and the solution's scope flags:

| Condition | Rating |
|---|---|
| C1 or C4 fails, clientData=true | CRITICAL |
| C1 or C4 fails, clientData=false | HIGH |
| 2+ checks fail | HIGH |
| 1 check fails, clientData=true | HIGH |
| 1 check fails, clientData=false | MEDIUM |
| 3+ checks in REVIEW, clientData=true | HIGH |
| 3+ checks in REVIEW, clientData=false | MEDIUM |
| 1+ checks in REVIEW, clientData=true | MEDIUM |
| All checks pass | LOW |

## Client data escalation

When a solution declares that it **ingests client data** or **deploys to a client environment**, C3 (DOM injection) and C5 (input validation) are treated as critical. A REVIEW result on either of these checks becomes a FAIL for the purposes of the overall scan pass decision.

## Scan pass / conditional pass / fail

| Outcome | Condition |
|---|---|
| **PASS** | All checks pass |
| **COND** (conditional pass) | No critical failures but warnings present — allowed through with certificate noting review items |
| **FAIL** | C1 or C4 fails, or client-data escalation triggers on C3/C5 |
