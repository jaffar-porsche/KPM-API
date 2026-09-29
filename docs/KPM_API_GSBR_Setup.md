# KPM API Access via GSBR — Setup Process & Reference

**Goal:** Register a technical user as a **consumer** of the KPM API (`volkswagenag.com/PP/QM/GroupProblemManagementService/V3`) via the Group Service Bus Registry (GSBR).

---

## Key Reference Data

| Item | Value |
|---|---|
| Application / Party | EVG7 |
| Technical User Display Name (CN middle part) | EVG7-KPMAPI |
| Technical User ID (TAM) | GF9HW3R |
| GID | B328BF108D223E40 |
| Fully Qualified CN (certificate) | `Systemuser EVG7-KPMAPI VWPKI B328BF108D223E40` |
| Cost Center | H0060320 |
| Reminder Resource Mailbox | evg7-kpmapi@porsche-engineering.de |
| Certificate Valid From / To | 04.09.2026 – 03.09.2028 |
| Company (used in Soft-PSE request) | Volkswagen AG and further companies |
| Certification Authority | New Root |
| Department | PEG-IT (Porsche Engineering Services GmbH) |

---

## Key Contacts

| Name | Role / Helped with |
|---|---|
| Maximilian Burkhard | Defect Management — pointed to Hartmut Petry; asked about GSBR Party |
| Bianca Luga | Defect Management |
| Hartmut Petry | System-responsible / party administrator for EVG7 |
| Joern Hoyer (K-DAED/1) | GSB team — creates the SIR (Service Implementation Request) |
| Tim Pilzecker (E2DC/3) | Contact for connector-contract |
| Manuel Wollmerstedt (A-IBDN-R/A) | Contact for connector-contract |
| Martin Spresser (PEG-FI) | Helped with shared mailbox, KPM roles/cluster guidance |
| Viktor Shults (A-IBDN-A/1, VDS) | Adjusted mailbox attribute for technical user |
| Fabian | Mentioned KPM Defect Manager has direct KPM connection via GSB |
| Sedrik | Supervisor — kept updated throughout |

---

## Key Portal Links

- **GSBR:** https://gsbr.wob.vw.vwg/gsbr/
- **My.serve (VW Service Portal):** https://myserveprod.service-now.com/myserve?id=vwag_index
- **My.serve — Technical Account (NONE-PERSON-ACCOUNT):** https://myserveprod.service-now.com/myserve?id=sc_cat_item&table=sc_cat_item&sys_id=6dfb6857ff520810ac0aecaf435b5eb4
- **My.serve — Application for Soft-PSE for Technical User:** https://myserveprod.service-now.com/myserve?id=sc_cat_item&sys_id=d6f97576fff11010ac0aecaf435b5e1f
- **My.serve — Application for Authorization to Manage Certificates:** https://myserveprod.service-now.com/myserve?id=sc_cat_item&sys_id=2f1c0ed7eb8f6e90908cf24e0bd0cde5
- **LeanIX (Volkswagen workspace):** https://vwgroup.leanix.net/
- **PKI Wiki — Soft-PSE for Technical User:** https://group-wiki.wob.vw.vwg/wikis/spaces/VWPKIWIKI/pages/198454243/Application+for+Soft-PSEs+for+Technical+User
- **GSBR Wiki (original):** https://group-wiki.wob.vw.vwg/wikis/display/TECHSOAESB/Group+Service+Bus+Registry

---

## Step-by-Step Process

### 1. Understand GSBR structure
- GSBR users are organized into **Parties** (1 Party = 1 Application, mapped to a LeanIX Application-Object).
- Consumer side needs: **Party → Consumer Contract (based on a Provider Contract) → Consumer-SIR**.
- Only SIRs (Service Implementation Requests) actually change GSB configuration.

### 2. Identify the application / Party
- Didn't know the application name initially; no LeanIX access (permission error: "Workspace Volkswagen not found").
- Asked **Maximilian Burkhard** → he didn't know the technical side, pointed to **Hartmut Petry** as system-responsible for **EVG7**.

### 3. Request the Technical User (TAM account)
- Hartmut clarified: before any GSBR registration, a **technical user** must be requested first — via **my.serve**, not GSBR itself.
- My.serve → searched "technical user" → selected **"Technical account (NONE-PERSON-ACCOUNT)"** → Action: **Create**.
- Display Name used: `EVG7-KPMAPI`.
- Request completed → received:
  - **TAM User ID:** GF9HW3R
  - Confirmation email with login/password/application details.

### 4. Request TAM user to be added to SIR (initial attempt)
- Emailed **Joern Hoyer** with TAM user details (TAM User ID, CN, OU, O, C, VWPKI) to request SIR creation.
- Joern's response: couldn't proceed — **strong authentication (certificate) required first**.
- He also flagged: contact **Tim Pilzecker** or **Manuel Wollmerstedt** separately to set up a **connector-contract** for the system (still open, see below).

### 5. Order the Soft-PSE Certificate
- Needed to request a certificate via VW PKI (my.serve → "Application for Soft-PSE for Technical User").
- **Blocked:** not authorized to manage certificates for cost center H0060320.
  - Submitted **"Application for authorization to manage certificates"** for H0060320 → approved (RITM18419370).
- Also required: a **"Reminder resource mailbox"** — must be an active VW Group mailbox, personal email not allowed.
  - Initially unclear which mailbox to use; Hartmut pointed to Martin Spresser.
  - Martin coordinated with **Viktor Shults (VDS)** to set up/attach a shared mailbox: **evg7-kpmapi@porsche-engineering.de**.
- Submitted the Soft-PSE request with:
  - Debited cost center: H0060320
  - Company: Volkswagen AG and further companies
  - Certification Authority: New Root
  - Validity: 2 years
  - Technical User ID: GF9HW3R
  - Reminder mailbox: evg7-kpmapi@porsche-engineering.de
- Request completed (RITM18478843) → GID confirmed: **B328BF108D223E40**.

### 6. Certificate issued
- Received Soft-PSE certificate via encrypted email.
- Fully Qualified CN: **`Systemuser EVG7-KPMAPI VWPKI B328BF108D223E40`**
- Valid: 04.09.2026 – 03.09.2028.

### 7. Send CN to Joern Hoyer → SIR creation
- Emailed Joern the fully qualified CN so he can create the SIR (either auto-detected via KIRA, or manually using the CN).
- **Status: pending confirmation from Joern.**

---

## Still Open / In Parallel

- [ ] **Connector-contract**: Contact **Tim Pilzecker** or **Manuel Wollmerstedt** to set this up for the system (EVG7).
- [ ] **KPM roles/rights**: Martin shared role options (cluster: KPMEE vs KPMTE(VDS), plus roles DV-B-SICHT, DV-ERF-30, DV-ERF-42). Need to confirm correct cluster for the use case (EVG7-KPMAPI / BUSCO integration) and submit the request.
- [ ] **GSBR Party confirmation**: Asked Maximilian/Fabian/Defect Management which Party to join in GSB, since KPM Defect Manager reportedly has a direct KPM connection via GSB. Awaiting response.
- [ ] **SIR creation confirmation**: Awaiting Joern's confirmation that the SIR has been created using the submitted CN.

---

## Lessons / Notes for Next Time

- GSBR Party ≠ LeanIX access — you can be blocked from LeanIX but still resolve the Party question by asking your application's system-responsible person directly.
- A technical user (TAM account) must exist *before* a certificate can be requested, and a certificate must exist *before* a SIR can be created.
- Certificate requests require: (1) cost-center certificate-management authorization, and (2) a group/shared reminder mailbox — neither personal email nor missing authorization will work.
- The "fully qualified CN" for a Soft-PSE certificate = VW-generated prefix + your chosen display name + VW-generated suffix (last 16 chars = GID).
- Connector-contracts and KPM role/rights are **separate tracks** from the GSBR/SIR process and should be pursued in parallel, not sequentially.
