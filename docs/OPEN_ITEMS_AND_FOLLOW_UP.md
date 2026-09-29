# Open Items And Follow-Up

This document tracks the remaining workstreams that are related to KPM API access but not yet confirmed as completed.

## Current Open Items

### 1. Connector-contract setup

Still required:

- Contact Tim Pilzecker or Manuel Wollmerstedt.
- Clarify and establish the connector-contract for the EVG7 system context.

Why it matters:

- This is separate from the certificate and SIR steps.
- API connectivity cannot be assumed complete merely because the certificate exists.

### 2. KPM roles and rights

Still required:

- Confirm the correct cluster for the use case.
- Confirm the required role set for the technical user or associated operational context.
- Submit the corresponding authorization request.

Known hints shared during the process:

- Possible clusters: `KPMEE` or `KPMTE(VDS)`
- Mentioned roles: `DV-B-SICHT`, `DV-ERF-30`, `DV-ERF-42`

Why it matters:

- Integration readiness is broader than transport-layer or certificate readiness.
- The user can be technically registered yet still lack the required functional permissions.

### 3. GSBR Party confirmation

Still required:

- Confirm with Defect Management and the system-responsible contacts which Party should be joined or reused in GSB.

Context:

- Fabian indicated that KPM Defect Manager already has a direct KPM connection through GSB.
- That may reduce ambiguity about the correct Party or existing integration path.

### 4. SIR creation confirmation

Still required:

- Await Joern Hoyer's confirmation that the SIR was created using the submitted fully qualified CN.

Why it matters:

- The SIR is the operational change artifact in GSB.
- Without confirmation, the process should not be treated as complete.

## Recommended Follow-Up Checklist

Use this checklist to close the setup professionally:

1. Confirm the target Party for EVG7 in GSBR.
2. Confirm the connector-contract owner and request path.
3. Confirm the correct KPM cluster.
4. Confirm the exact KPM roles needed for the integration use case.
5. Confirm SIR creation and capture the reference identifier if one exists.
6. Store the final operational artifacts in a durable team location.

## Lessons Learned

### LeanIX access is helpful but not mandatory

A missing LeanIX permission does not end the process if the system-responsible owner can identify the correct application and Party context.

### Technical user creation comes before certificate issuance

The technical user is a prerequisite for the Soft-PSE request. Attempting to shortcut this only creates rework.

### Certificate prerequisites are easy to underestimate

Two prerequisites caused friction and should be checked early:

1. Certificate-management authorization for the cost center
2. A valid VW Group reminder mailbox

### Fully qualified CN is the real handoff artifact

The practical identity used for downstream GSB handling is the fully qualified CN, not just the user display name or TAM ID.

### Parallelize related tracks

Connector-contract work, role assignment, and GSBR registration should be pursued in parallel when possible. They are related but not identical processes.

## Recommended Future Improvements

1. Capture the final SIR identifier here once available.
2. Add the confirmed Party name once officially validated.
3. Add the confirmed connector-contract details once assigned.
4. Add the final KPM role model once approved.
