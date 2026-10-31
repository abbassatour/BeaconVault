
# Disclosures, Third-Party Components & Licenses

This document discloses all third-party components, open-source libraries, original developments, and AI assistance utilized in the creation of the `beacon-sovereign-vault` Skill for the UGREEN Hackathon 2026.

---

## 1. Principal Functionality Developed for this Hackathon

The core innovation developed for this hackathon is the autonomous assistive orchestration pipeline between a mobile accessibility cockpit (BeaconOS) and UGREEN AI NAS (UGOS), specifically:

1. **Local Sensory Ingestion Engine:** Automated zero-latency background ingest of assistive visual inspection snapshots, OCR streams, and emergency sensor logs over local LAN.
2. **Local Assistive Knowledge Base (RAG):** On-device vector indexing and semantic retrieval tailored specifically for visually impaired users needing instant answers about physical objects, bills, medication, and smart-home safety events.
3. **Emergency Blackbox Service:** Tamper-proof, local physical archival of distress coordinates and sensory recordings, ensuring complete self-custody of legal and safety audit logs.

---

## 2. Open-Source Libraries & Components

| Component / Library           | Source Repository             | License      | Purpose in Project                                                               |
| :---------------------------- | :---------------------------- | :----------- | :------------------------------------------------------------------------------- |
| **Drift SQLite Engine** | `simolus3/drift`            | MIT License  | Local-first relational database and differential sync tracking on client nodes.  |
| **Web3dart**            | `xclud/web3dart`            | Apache 2.0   | Cryptographic signature verification and Sovereign DID address derivation.       |
| **FastAPI**             | `tiangolo/fastapi`          | MIT License  | Lightweight asynchronous local P2P gateway protocol handling.                    |
| **Uvicorn**             | `encode/uvicorn`            | BSD 3-Clause | ASGI web server implementation for local streamable communication.               |
| **Flutter SDK**         | `flutter/flutter`           | BSD 3-Clause | UI and sensory feedback layer for mobile, desktop, and Fire TV display surfaces. |
| **Pydantic**            | `pydantic/pydantic`         | MIT License  | Schema validation and data modeling for skill configuration payloads.            |
| **Supabase Client**     | `supabase/supabase-flutter` | MIT License  | Optional encrypted cloud relay fallback when devices are away from home.         |

---

## 3. AI Tools & Methodologies Used

- **AI Coding Assistants (Anthropic Claude / OpenAI / GitHub Copilot):** Used strictly as developer productivity tools for code formatting, drafting documentation, and generating boilerplate Markdown templates conforming to the Uliya Skill Development Standard.
- **Author Attribution:** All architectural choices, protocol designs, integration workflows, and submission texts were directed, reviewed, and finalized by the project author, Abbas Satour.
