# Reference Data

This document contains the canonical reference data used during the KPM API consumer-registration process.

## API And Application Context

| Item | Value |
|---|---|
| Target API | `volkswagenag.com/PP/QM/GroupProblemManagementService/V3` |
| Application / Party context | `EVG7` |
| Technical user display name | `EVG7-KPMAPI` |
| Technical user ID (TAM) | `GF9HW3R` |
| GID | `B328BF108D223E40` |
| Fully qualified CN | `Systemuser EVG7-KPMAPI VWPKI B328BF108D223E40` |
| Cost center | `H0060320` |
| Reminder resource mailbox | `evg7-kpmapi@porsche-engineering.de` |
| Certificate valid from | `04.09.2026` |
| Certificate valid to | `03.09.2028` |
| Company for Soft-PSE request | `Volkswagen AG and further companies` |
| Certification authority | `New Root` |
| Department | `PEG-IT (Porsche Engineering Services GmbH)` |

## Key Contacts

| Name | Role / Contribution |
|---|---|
| Maximilian Burkhard | Defect Management contact; redirected the technical question to Hartmut Petry |
| Bianca Luga | Defect Management contact |
| Hartmut Petry | System-responsible contact and party administrator for `EVG7` |
| Joern Hoyer (`K-DAED/1`) | GSB team contact responsible for creating the SIR |
| Tim Pilzecker (`E2DC/3`) | Contact for connector-contract setup |
| Manuel Wollmerstedt (`A-IBDN-R/A`) | Contact for connector-contract setup |
| Martin Spresser (`PEG-FI`) | Helped on mailbox, KPM roles, and cluster guidance |
| Viktor Shults (`A-IBDN-A/1`, VDS) | Adjusted mailbox attributes for the technical user |
| Fabian | Shared that KPM Defect Manager has a direct KPM connection through GSB |
| Sedrik | Supervisor kept informed throughout the process |

## Portal Links

| System | URL |
|---|---|
| GSBR | `https://gsbr.wob.vw.vwg/gsbr/` |
| My.serve | `https://myserveprod.service-now.com/myserve?id=vwag_index` |
| My.serve Technical Account request | `https://myserveprod.service-now.com/myserve?id=sc_cat_item&table=sc_cat_item&sys_id=6dfb6857ff520810ac0aecaf435b5eb4` |
| My.serve Soft-PSE request | `https://myserveprod.service-now.com/myserve?id=sc_cat_item&sys_id=d6f97576fff11010ac0aecaf435b5e1f` |
| My.serve certificate-management authorization | `https://myserveprod.service-now.com/myserve?id=sc_cat_item&sys_id=2f1c0ed7eb8f6e90908cf24e0bd0cde5` |
| LeanIX Volkswagen workspace | `https://vwgroup.leanix.net/` |
| PKI Wiki Soft-PSE for Technical User | `https://group-wiki.wob.vw.vwg/wikis/spaces/VWPKIWIKI/pages/198454243/Application+for+Soft-PSEs+for+Technical+User` |
| GSBR Wiki | `https://group-wiki.wob.vw.vwg/wikis/display/TECHSOAESB/Group+Service+Bus+Registry` |

## Request And Ticket References

| Item | Value |
|---|---|
| Certificate-management authorization request | `RITM18419370` |
| Soft-PSE request | `RITM18478843` |

## Important Interpretation Notes

1. The fully qualified CN is VW-generated around the chosen display name and the generated GID.
2. The technical user display name alone is not sufficient for strong-authentication-based integration steps.
3. The reminder mailbox must be a valid shared or group mailbox within the VW Group context.
4. LeanIX access problems do not block the process permanently if the system-responsible contact can confirm the correct Party context.
