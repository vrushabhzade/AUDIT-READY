# Disclosures, AI Usage, and Third-Party Licenses

This document discloses third-party components, open source libraries, newly developed functionality, and AI tool usage for the `audit-ready` Skill submitted to the UGREEN AI NAS Hackathon.

## 1. Hackathon Development Disclosures

### Principal Functionality Newly Developed for This Hackathon
The `audit-ready` Skill and all supporting orchestration artifacts were conceived and developed exclusively during this Hackathon period. Newly developed capabilities include:
- Multi-sector statutory compliance auditing taxonomy for small clinics, schools, and light manufacturing plants.
- Multi-expert coordination protocol leveraging Uliya subagents (`file-agent`, `document-agent`, `photo-agent`, `knowledge-agent`).
- Automated inspector-ready directory synthesis, copying valid documents into clean regulatory hierarchies while isolating expired items.
- Dynamic metadata status tagging (`audit:valid`, `audit:expiring-soon`, `audit:expired`, `audit:missing`, `audit:review-needed`).
- Comprehensive Executive Readiness Scoring and Gap Analysis reporting with automated remediation recommendations.

### AI Tools and Their Principal Uses
During the creation and refinement of this Skill package, the following AI tools and models were utilized:
- **Google DeepMind Gemini Models**: Used for regulatory domain knowledge structuring, prompt formulation, multi-agent orchestration architecture design, and static validation verification.
- **UGREEN AI NAS On-Device Models**: Utilized by the target NAS runtime environment for local document parsing, structured field extraction, visual OCR on scanned certificates, and report composition.

---

## 2. Third-Party Components and Open Source Licenses

The `audit-ready` Skill relies on the following open source specifications, runtimes, and schemas:

| Component | Source / Project | License | Principal Role |
| :--- | :--- | :--- | :--- |
| **Uliya Skill Development Kit** | UGREEN Technology Co., Ltd. | MIT License | Standardized orchestration schema, capability catalog contract (v2.2.0), and static checker engine. |
| **Node.js Runtime Engine** | OpenJS Foundation (https://nodejs.org) | MIT License | Execution environment for static verification scripts and JSON validation utilities. |
| **Python Standard Library** | Python Software Foundation (https://python.org) | PSF License | Data processing utilities and report generation formatting tools. |
| **Markdown Standard (CommonMark / GFM)** | CommonMark Project (https://commonmark.org) | Creative Commons / BSD | Standard document formatting specification for Skill instructions and report generation. |

All third-party assets are utilized in strict adherence to their respective open source licensing terms. No proprietary third-party commercial software or external cloud API subscriptions are required to run this Skill.
