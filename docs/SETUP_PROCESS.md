# Setup Process

This runbook describes the end-to-end process used to prepare KPM API access via GSBR for the EVG7 technical user, alongside the separate KPM authorization work needed for functional use.

## Process Overview

The consumer registration path is not limited to GSBR. It requires coordination across application ownership, TAM user creation, VW PKI certificate provisioning, GSB-side SIR creation, and separate KPM-side authorization for postbox access.

## 1. Understand The GSBR Structure

GSBR access is organized around Parties.

- One Party corresponds to one application.
- The Party is mapped to a LeanIX application object.
- The consumer side typically requires:
  - Party
  - Consumer Contract based on a Provider Contract
  - Consumer SIR
- Only the SIR actually changes the GSB configuration.

Practical implication: finding the right Party is a prerequisite, but the technical enablement is not complete until the SIR exists.

## 2. Identify The Application And Party Context

Initial blocker:

- The application name was not known at the start.
- LeanIX access was not available due to a workspace permission error.

Resolution path:

1. Ask a domain contact in Defect Management.
2. The technical side was not known there either.
3. The question was redirected to Hartmut Petry as the system-responsible contact for `EVG7`.

Outcome:

- `EVG7` was confirmed as the relevant application context.
- Hartmut also clarified that a TAM technical user was required before GSBR registration could proceed.

## 3. Request The Technical User In My.serve

The technical user was requested through My.serve rather than GSBR.

Path used:

1. Open My.serve.
2. Search for `technical user`.
3. Select `Technical account (NONE-PERSON-ACCOUNT)`.
4. Choose the create action.

Values used:

- Display name: `EVG7-KPMAPI`

Outcome:

- Technical user ID received: `GF9HW3R`
- Confirmation mail delivered with login, password, and application details.

## 4. Initial SIR Request Attempt

After the technical user was available, the TAM details were sent to Joern Hoyer to request SIR creation.

Data shared for the attempt included:

- TAM user ID
- CN-related data
- OU / O / C / VWPKI identity details

Outcome:

- The request could not proceed.
- Strong authentication using a certificate was still missing.

Additional guidance received:

- Tim Pilzecker or Manuel Wollmerstedt should be contacted separately for the connector-contract.

## 5. Request Certificate-Management Authorization

The Soft-PSE request could not be completed initially because certificate-management rights for the cost center were missing.

Blocking issue:

- No authorization for cost center `H0060320`

Resolution path:

1. Submit `Application for authorization to manage certificates`.
2. Wait for approval.

Outcome:

- Authorization approved under `RITM18419370`.

## 6. Prepare The Reminder Mailbox

The Soft-PSE request also required an eligible reminder resource mailbox.

Constraints:

- Personal mailboxes were not accepted.
- The mailbox had to be an active VW Group shared or group mailbox.

Resolution path:

1. Hartmut Petry pointed to Martin Spresser.
2. Martin coordinated with Viktor Shults.
3. The mailbox attributes were adjusted for use with the technical user.

Outcome:

- Mailbox established: `evg7-kpmapi@porsche-engineering.de`

## 7. Order The Soft-PSE Certificate

Once authorization and mailbox prerequisites were satisfied, the Soft-PSE request was submitted in My.serve.

Values used in the request:

| Field | Value |
|---|---|
| Debited cost center | `H0060320` |
| Company | `Volkswagen AG and further companies` |
| Certification Authority | `New Root` |
| Validity | `2 years` |
| Technical User ID | `GF9HW3R` |
| Reminder mailbox | `evg7-kpmapi@porsche-engineering.de` |

Outcome:

- Request completed under `RITM18478843`
- GID assigned: `B328BF108D223E40`

## 8. Receive The Certificate

The Soft-PSE certificate was received via encrypted email.

Certificate identity:

- Fully qualified CN: `Systemuser EVG7-KPMAPI VWPKI B328BF108D223E40`
- Validity: `04.09.2026 - 03.09.2028`

This fully qualified CN is the decisive identity artifact for the next integration step.

## 9. Submit The CN For SIR Creation

After certificate issuance, the fully qualified CN was sent to Joern Hoyer so the SIR can be created.

Notes:

- The CN can potentially be auto-detected via KIRA.
- If not, it can be entered manually based on the submitted certificate identity.

Current status:

- Waiting for confirmation that the SIR has been created.

## 10. Request KPM Read And Write Access To Relevant Postboxes

This is a separate requirement from GSBR registration and must not be assumed complete just because the technical user and certificate exist.

Requested target outcome:

- Read and write access for the technical user to the relevant project-specific postboxes in KPM

Responsible path:

- Request through Defect Management
- Primary contacts mentioned in the original task: Maximilian Burkhard and Bianca Luga

Important note:

- The KPM role and cluster discussion is related, but the postbox access itself should be explicitly requested and explicitly confirmed.

## Why The Sequence Matters

The key dependency chain is:

1. Application context
2. Technical user
3. Certificate-management authorization
4. Shared reminder mailbox
5. Soft-PSE certificate
6. Fully qualified CN
7. SIR creation
8. KPM postbox read/write authorization

Skipping or reordering these steps leads to avoidable delays, especially at the certificate and strong-authentication boundary.
