# KPM API Access Via GSBR

This repository is the working reference for registering and operating access to the KPM API through GSBR for the EVG7 application context. It converts the original request history into a reusable setup guide so future technical-user onboarding does not depend on email threads or individual memory.

## Purpose

This repository documents how to register a technical user as a consumer of the KPM API:

- API: `volkswagenag.com/PP/QM/GroupProblemManagementService/V3`
- Integration path: GSBR and related VW provisioning steps
- Application context: `EVG7`

## Scope

This repository covers:

1. The required reference data for the technical user.
2. The end-to-end setup sequence.
3. The GSBR, certificate, and SIR dependencies.
4. The key contacts involved in the process.
5. The open parallel workstreams that are still required.
6. Lessons learned for future repetitions.

## Document Index

| Document | Purpose |
|---|---|
| [docs/REFERENCE_DATA.md](docs/REFERENCE_DATA.md) | Canonical technical user data, certificate information, contacts, and portal links |
| [docs/SETUP_PROCESS.md](docs/SETUP_PROCESS.md) | Step-by-step setup runbook from application identification to SIR creation |
| [docs/OPEN_ITEMS_AND_FOLLOW_UP.md](docs/OPEN_ITEMS_AND_FOLLOW_UP.md) | Parallel tracks, pending actions, and operational follow-up checklist |

## High-Level Flow

The process is not a single GSBR-only action. It crosses several systems and approval paths.

1. Identify the correct application and responsible party.
2. Request a technical TAM user.
3. Establish certificate-management authorization for the cost center.
4. Set up a valid shared reminder mailbox.
5. Request and receive the Soft-PSE certificate.
6. Send the fully qualified CN for SIR creation.
7. Complete parallel items such as connector-contract setup and KPM role assignment.

## Core Dependency Rule

The setup order matters:

1. A technical user must exist before the certificate request can be completed.
2. A certificate must exist before the SIR can be created.
3. GSBR consumer setup also depends on clarifying the correct Party and provider-based contract path.

## Current Technical User Context

| Item | Value |
|---|---|
| Application / Party context | `EVG7` |
| Technical user display name | `EVG7-KPMAPI` |
| Technical user ID | `GF9HW3R` |
| GID | `B328BF108D223E40` |
| Fully qualified CN | `Systemuser EVG7-KPMAPI VWPKI B328BF108D223E40` |
| Cost center | `H0060320` |
| Reminder mailbox | `evg7-kpmapi@porsche-engineering.de` |
| Certificate validity | `04.09.2026 - 03.09.2028` |

## Operational Note

GSBR registration, certificate provisioning, connector-contract setup, and KPM authorization are related but separate workstreams. They should be coordinated in parallel when possible rather than treated as one serial request.

## Recommended Use

Use this repository as the source of truth when:

1. Repeating the setup for another technical user.
2. Explaining the EVG7 KPM API onboarding path to another team member.
3. Following up with GSBR, GSB, PKI, or KPM stakeholders.
4. Auditing which prerequisites were already completed and which are still pending.
