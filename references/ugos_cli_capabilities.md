
# UGOS System Capabilities & Architectural Mapping

This document specifies the public UGOS CLI capabilities and child expert mappings utilized by `beacon-vault` as defined in the official capability catalog.

---

## 1. Domain to Sub-Agent Mapping

The parent Skill coordinates workflow delegation across specialized sub-agents registered in the catalog:

| Domain              | Catalog CLI         | Registered Agent           | Primary Actions                                              |
| :------------------ | :------------------ | :------------------------- | :----------------------------------------------------------- |
| **file**      | `ug-filesystem`   | `file-agent`             | `find`, `ls`, `mkdir`, `cpmv`                        |
| **document**  | `ug-document`     | `document-agent`         | `extract`, `qa`, `metadata`                            |
| **album**     | `ug-photo`        | `photo-agent`            | `vision-ocr`, `vision-vlm`, `search-picture`           |
| **knowledge** | `ug-knowledge`    | `knowledge-agent`        | `audio-transcription`, `save-text`, `collect-evidence` |
| **monitor**   | `ug-surveillance` | `security-monitor-agent` | `event-timeline`, `identity-resolve`, `event-evidence` |

---

## 2. Ingestion Topology

All sensory data and inspection captures are organized within categorized application workspaces on the NAS:

```text
BeaconVault/
├── documents/
│   ├── prescriptions/
│   └── financial_bills/
├── perimeter_security/
│   ├── snapshots/
│   └── event_logs/
├── voice_memos/
│   ├── audio_recordings/
│   └── transcripts/
└── emergency_audit/
    └── telemetry_trail/
```

---

## 3. Sub-Agent Capability Scope

Child experts invoke the following catalog capabilities during delegated task execution:

### A. File Discovery & Organization (`file-agent`)

- **Capability:** `ug-filesystem`
- **Actions:**
  - `find`: Searches input drop zones for newly received assistive captures and audio recordings.
  - `ls`: Inspects directory contents to verify target files and permissions before processing.
  - `mkdir`: Creates categorized archive directories for processed assets.
  - `cpmv`: Moves verified inspection files into permanent archive folders after user approval.

### B. Document Intelligence (`document-agent`)

- **Capability:** `ug-document`
- **Actions:**
  - `extract`: Extracts structured fields including expiration dates, dosages, warnings, and invoice amounts using schemas such as `medical-report` or `invoice`.
  - `qa`: Resolves user inquiries regarding printed correspondence, utility bills, and formal notices.
  - `metadata`: Determines page counts and structural properties of scanned PDF materials.

### C. Vision Inspection (`photo-agent`)

- **Capability:** `ug-photo`
- **Actions:**
  - `vision-vlm`: Analyzes handheld object captures using visual language understanding to identify physical items.
  - `vision-ocr`: Extracts raw textual content from packaged containers and product labels.
  - `search-picture`: Locates historical inspection frames by date, detected label, or location criteria.

### D. Speech Transcription & Knowledge Store (`knowledge-agent`)

- **Capability:** `ug-knowledge`
- **Actions:**
  - `audio-transcription`: Converts speech recordings into structured multi-speaker text transcripts.
  - `save-text`: Writes finalized transcription records and synthesized notes into verified files.
  - `collect-evidence`: Retrieves indexed context to formulate answers for user accessibility queries.

### E. Perimeter Safety Monitoring (`security-monitor-agent`)

- **Capability:** `ug-surveillance`
- **Actions:**
  - `event-timeline`: Queries surveillance logs filtered by detection topics such as `Human` or `Package`.
  - `identity-resolve`: Analyzes camera events to identify recognized family members versus strangers.
  - `event-evidence`: Retrieves visual snapshot references and motion telemetry for audit trail verification.

---

## 4. Execution Principles

1. **Strict Delegation:** The parent Skill issues delegation tasks using verified identifiers without invoking low-level primitives directly.
2. **Sequential Flow:** Output artifacts from discovery steps are verified before passing references to downstream analysis agents.
3. **Approval Boundary:** Destructive operations, relocation tasks, or external emergency triggers require explicit user confirmation (`waiting_approval`).
