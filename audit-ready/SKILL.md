---
name: audit-ready
description: An autonomous compliance audit and document verification workflow for small clinics, schools, and factories on UGREEN AI NAS. Use when administrators need to verify statutory licenses, fire certificates, and mandatory registers, detect expired or missing documents, organize an inspector-ready directory, and generate an audit gap report.
---

# Goal

Audit Ready conducts an automated, privacy-first regulatory compliance review for small clinics, schools, and light manufacturing plants directly on UGREEN AI NAS storage. The Skill identifies required statutory records, extracts validity and expiration dates from digital documents and scanned certificate photos, cross-checks inventory against sector compliance mandates, flags expired or missing items, organizes verified active documents into an inspector-ready folder hierarchy, and generates a detailed Markdown Audit Gap Report.

Detailed statutory requirements, folder structures, and licensing disclosures are documented in the companion references:
- [Compliance Checklists](references/compliance-checklists.md)
- [Facility Profiles and Taxonomy](references/facility-profiles.md)
- [Disclosures, AI Usage, and Third-Party Licenses](references/disclosures-and-licenses.md)

# Required input

The parent Skill collects only the following high-level operational inputs from the user:
- `facility_type`: The target sector category (`clinic`, `school`, or `factory`).
- `source_folder`: The source directory on the storage system containing compliance files and photo scans.
- `target_date`: The inspection target date against which validity is evaluated (defaults to the current date).
- `destination_folder`: The target output directory where the inspector-ready staging structure and gap reports are created.

The parent Skill does not collect private internal parameters owned by subagents, and parent orchestration must not directly execute cli.invoke.

# Generation-time capability evidence

- `ug-filesystem` → `file-agent`
- `ug-filemgr` → `file-agent`
- `ug-document` → `document-agent`
- `ug-photo` → `photo-agent`
- `ug-knowledge` → `knowledge-agent`

# Orchestration

The parent Skill coordinates specialized subagents sequentially, passing verified upstream real results to downstream steps. If an upstream step yields no matching files or an empty result, the workflow reports zero matches and stops dependent tasks without inventing synthetic file paths.

### Step 1: Compliance File Discovery and Inventory Scanning
The parent Skill delegates file discovery to `file-agent`.

`delegate --target file-agent --instruction 'Locate all compliance documents, licenses, certificates, and registers in the specified audit source folder, returning a verified manifest of document paths and image paths.'`

- Downstream handoff: The verified real result containing discovered document file paths and image file paths is handed off to Step 2 and Step 3.
- Empty result handling: If the search discovers no matching files or returns an empty result, report zero matches found and terminate downstream tasks.

### Step 2: Digital Document Extraction and Validity Analysis
The parent Skill delegates text-based document parsing to `document-agent` using the real document file paths confirmed by Step 1.

`delegate --target document-agent --instruction 'Extract structured metadata, license numbers, issuing authorities, and expiry dates from the verified document paths, comparing expiry dates against the audit target date.'`

- Downstream handoff: The extracted validity records, expiration statuses, and identified compliance fields form the digital extraction dataset passed to Step 4.

### Step 3: Multimodal Vision OCR on Framed Licenses and Register Scans
The parent Skill delegates visual analysis to `photo-agent` for image files confirmed by Step 1, such as wall-mounted certificate photos or physical logbook scans.

`delegate --target photo-agent --instruction 'Perform vision OCR and visual inspection on verified certificate and register images to extract issue dates, validity periods, and physical inspection stamps.'`

- Downstream handoff: The visual verification facts from this step are combined with upstream real results from Step 2 to establish the total facility compliance ledger.

### Step 4: Compliance Gap Analysis and Report Drafting
The parent Skill delegates synthesis and report writing to `document-agent`.

`delegate --target document-agent --instruction 'Synthesize extraction findings into a formal Audit Gap Report detailing active documents, expiring items, missing mandatory registers, and required remedial actions.'`

- Downstream handoff: The generated Markdown report text is passed to Step 6, while the list of verified valid documents is passed to Step 5 for staging.

### Step 5: Inspector-Ready Folder Staging and Metadata Tagging
The parent Skill delegates file organization and tagging to `file-agent` using confirmed valid document paths.

`delegate --target file-agent --instruction 'Create an inspector-ready directory structure and copy verified, active compliance files into categorized statutory folders, applying status tags to each document.'`

- Execution boundary: Dependent file copying proceeds only for verified authentic files. Expired or unreadable files are isolated and flagged.

### Step 6: Knowledge Base Archival and Report Persistence
The parent Skill delegates report persistence to `knowledge-agent`.

`delegate --target knowledge-agent --instruction 'Save the generated Audit Gap Report and compliance checklist as a persistent Markdown document in the audit reports destination folder.'`

- Completion: Confirms the exact saved Markdown file path and presents the final Executive Readiness Summary to the user.

# Completion and failure

The parent workflow evaluates the public status returned by each delegation:

- `completed`: Inspect the verified business facts in the result summary. Advance to the next dependent delegation only when upstream required file paths, extraction metadata, or saved report paths are confirmed.
- `failed`: Stop dependent downstream steps immediately. Report the exact failed step, responsible subagent, and all verified results obtained before the failure. Do not fabricate missing values.
- `cancelled`: Halt the workflow without starting subsequent tasks. Report the incomplete status without automatically retrying operations that might duplicate staging folders.
- `waiting_user`: Relay interactive clarification checkpoints to the user (such as ambiguous scanned dates or missing facility categories), and resume the same delegation upon user input.
- `waiting_approval`: When file creation or document tagging operations require platform confirmation, wait for official platform approval and resume the same delegation upon receipt. Conversational agreement does not replace platform authorization.

The Skill is complete. You can upload it to [skillhub](https://skills.ugreen.com/skill-hub/publish).
