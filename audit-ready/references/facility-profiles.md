# Facility Profiles and Staging Taxonomy

This reference describes the directory structure, file metadata tagging rules, and audit staging protocols executed by the `audit-ready` Skill.

## 1. Supported Facility Profiles

The audit engine supports three primary facility configurations:

1. **Healthcare Clinic (`clinic`)**:
   - Focus: Patient safety, biomedical hazard control, practitioner qualifications, and drug storage regulations.
   - Core Statutory Burden: Health Department, Pollution Control Board, Drug Controller, Fire Department.
2. **Educational Institution (`school`)**:
   - Focus: Student structural safety, potable water quality, sanitation, fire evacuation readiness, and staff child-protection clearances.
   - Core Statutory Burden: Education Board, Fire Department, Public Works Department, District Health Officer.
3. **Light Manufacturing Facility (`factory`)**:
   - Focus: Industrial worker safety, heavy machine and pressure vessel calibration, environmental emission consents, and labor welfare registers.
   - Core Statutory Burden: Directorate of Industrial Safety and Health (DISH), State Pollution Control Board, Fire Directorate, Labor Commissioner.

---

## 2. Inspector-Ready Folder Organization Structure

When organizing verified compliance records, the Skill stages documents into a standardized folder hierarchy inside the user-specified destination folder:

```text
Inspector_Ready_Audit_Pack/
├── 01_Statutory_Licenses/
│   ├── Primary_Operating_License
│   └── Municipal_Trade_Permit
├── 02_Safety_and_Fire_NOC/
│   ├── Fire_Safety_NOC
│   └── Structural_Stability_Certificate
├── 03_Environmental_and_Health/
│   ├── Environmental_Consents_or_Waste_Authorizations
│   └── Potable_Water_Sanitation_Reports
├── 04_Mandatory_Registers_and_Logs/
│   ├── Operational_Daily_Registers
│   └── Equipment_Maintenance_and_Calibration_Logs
├── 05_Personnel_and_Clearances/
│   ├── Staff_Professional_Registrations
│   └── Background_and_Vaccination_Records
└── 06_Audit_Reports/
    ├── Audit_Gap_Report.md
    └── Compliance_Action_Checklist.md
```

---

## 3. Compliance Status Tagging Taxonomy

Documents scanned during the audit receive structured metadata tags on the storage volume to allow instant filtering by administrators and inspectors:

| Status Tag | Description | Action Required |
| :--- | :--- | :--- |
| `audit:valid` | Verified authentic document with validity extending beyond 30 days from the audit target date. | Staged into Inspector Pack; no immediate action. |
| `audit:expiring-soon` | Verified authentic document expiring within 30 calendar days of the audit target date. | Highlighted in Gap Report with renewal instructions; staged with warning notice. |
| `audit:expired` | Document validity has lapsed prior to the audit target date. | Marked as critical deficiency; renewal escalation required immediately. |
| `audit:review-needed` | Scanned image or low-resolution certificate where text or dates are partially obscured. | Flagged for administrator physical verification. |
| `audit:missing` | Mandatory statutory document item expected in the facility checklist but absent from scanned folders. | Registered as critical gap in the final report. |

---

## 4. Remediation Workflow Guidelines

When gaps or expired items are identified, the generated Gap Report provides remediation recommendations:
- **Immediate Escalation**: For lapsed fire safety NOCs or operating licenses, flag operational risks and provide renewal application links or agency contacts.
- **Grace Period Monitoring**: For items expiring within 30 days, generate a reminder ticket for the facility administrator.
- **Physical Document Trace**: For mandatory registers missing from digital folders, prompt the user to photograph physical logbooks using the mobile companion app for visual OCR processing.
