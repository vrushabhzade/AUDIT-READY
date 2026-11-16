# Audit Ready

> **“Walk in tomorrow. Be ready today.”**  
> Autonomous compliance audit and document verification AI Skill for **UGREEN AI NAS**, built for small clinics, schools, and light manufacturing plants.

---

## Overview

Small facilities live in fear of unannounced inspections. Licenses, fire certificates, pollution consents, and mandatory registers are often scattered across folders, binders, or blurry phone photos. Expired documents or missing mandatory records lead to severe penalties, suspension of operations, or legal liabilities.

**Audit Ready** transforms a local **UGREEN AI NAS** into an automated, on-premise compliance auditor:
1. **Discovers** statutory compliance documents and photos across NAS shares.
2. **Extracts** validity dates, certificate numbers, and issuing bodies using local multimodal AI (`ug-document` & `ug-photo`).
3. **Cross-checks** findings against sector-specific statutory compliance matrices.
4. **Tags** documents on the filesystem (`audit:valid`, `audit:expiring-soon`, `audit:expired`, `audit:missing`).
5. **Stages** valid documents into an organized, **Inspector-Ready Folder**.
6. **Generates** a comprehensive **Audit Gap Report** and action checklist.

All data remains **100% on-premise** on the UGREEN AI NAS—zero confidential health records, student data, or factory files are ever transmitted to the cloud.

---

## Submission Deliverables

| Deliverable | File | Description |
| :--- | :--- | :--- |
| **Project Proposal** | [`Audit_Ready_Project_Proposal.pdf`](Audit_Ready_Project_Proposal.pdf) | Official 10-point proposal (404 words, &le; 500 word limit, &lt; 1 MB). |
| **Pre-test Skill Package** | [`audit-ready.zip`](audit-ready.zip) | Validated Uliya Skill package containing `SKILL.md` and linked references. |
| **Skill Definition** | [`audit-ready/SKILL.md`](audit-ready/SKILL.md) | Uliya orchestration specification with subagent delegations. |
| **Compliance Checklists** | [`audit-ready/references/compliance-checklists.md`](audit-ready/references/compliance-checklists.md) | Statutory checklists for clinics, schools, and factories. |
| **Facility Taxonomy** | [`audit-ready/references/facility-profiles.md`](audit-ready/references/facility-profiles.md) | Folder staging structure and metadata tagging rules. |
| **Disclosures & Licenses** | [`audit-ready/references/disclosures-and-licenses.md`](audit-ready/references/disclosures-and-licenses.md) | Open source licenses, new hackathon capabilities, AI tool disclosures. |

---

## Technical Architecture & Uliya NAS Capabilities

Audit Ready coordinates specialized Uliya NAS subagents using the official capability catalog (`v2.2.0`):

```text
[User / Admin] 
       │
       ▼
[audit-ready (Main Skill)]
       │
       ├─► file-agent (ug-filesystem) ──► Locate documents & photo scans
       │
       ├─► document-agent (ug-document) ─► Extract validity & dates from digital PDFs
       │
       ├─► photo-agent (ug-photo) ──────► Vision OCR on framed licenses & register photos
       │
       ├─► document-agent (ug-document) ─► Synthesize Compliance Gap Report
       │
       ├─► file-agent (ug-filesystem & ug-filemgr) ─► Stage Inspector Folder & apply metadata tags
       │
       └─► knowledge-agent (ug-knowledge) ─► Persist Markdown report to NAS storage
```

---

## Inspector-Ready Staging Hierarchy

When executed, Audit Ready organizes verified compliance records into a clean, audit-compliant structure:

```text
Inspector_Ready_Audit_Pack/
├── 01_Statutory_Licenses/              # Operating licenses, municipal permits
├── 02_Safety_and_Fire_NOC/             # Fire NOCs, structural fitness certificates
├── 03_Environmental_and_Health/        # Pollution consents, BMWM, water purity reports
├── 04_Mandatory_Registers_and_Logs/    # Daily registers, maintenance logs, calibration tags
├── 05_Personnel_and_Clearances/        # Medical licenses, police background checks
└── 06_Audit_Reports/                   # Audit_Gap_Report.md & Action Checklist
```

---

## Static Validation

The Skill package has been validated with the official Uliya static checker:

```bash
node check-skill.mjs audit-ready
# Status: "static-pass" | 0 errors | 0 warnings
```

---

## License

This project is licensed under the MIT License. See [disclosures-and-licenses.md](audit-ready/references/disclosures-and-licenses.md) for full details.
