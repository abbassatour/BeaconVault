
# Disclosures, Third-Party Components & Licenses

This document discloses all third-party components, open-source libraries, original developments, and AI assistance utilized in the creation of the `beacon-vault` Skill for the UGREEN Hackathon 2026, conforming to official hackathon requirements.

---

## 1. Principal Functionality Developed for this Hackathon

The core innovation developed for this hackathon is the autonomous assistive orchestration pipeline between the client accessibility cockpit (BeaconOS) and UGREEN AI NAS (UGOS), specifically:

1. **Local Sensory Ingestion Engine:** Automated zero-latency background ingest of assistive visual inspection snapshots, OCR streams, and emergency sensor logs over local LAN.
2. **Local Assistive Knowledge Base (RAG):** On-device vector indexing and semantic retrieval tailored specifically for visually impaired users needing instant answers about physical objects, bills, medication, and smart-home safety events.
3. **Emergency Blackbox Service:** Tamper-proof, local physical archival of distress coordinates and sensory recordings, ensuring complete self-custody of legal and safety audit logs.
4. **Declarative Uliya Skill Workflow:** Declarative orchestration uniting `ug-filesystem`, `ug-document`, `ug-photo`, `ug-knowledge`, and `ug-surveillance` into an eyes-free assistive pipeline.

---

## 2. Third-Party Components & Open-Source Libraries

| Component / Library                        | Source Repository                   | License      | Purpose in Project                                                                 |
| :----------------------------------------- | :---------------------------------- | :----------- | :--------------------------------------------------------------------------------- |
| **Model Context Protocol (MCP) SDK** | `modelcontextprotocol/python-sdk` | MIT License  | Standardized interface for declarative agent tool dispatching.                     |
| **Drift SQLite Engine**              | `simolus3/drift`                  | MIT License  | Local-first relational persistence and differential sync tracking on client nodes. |
| **Web3dart**                         | `xclud/web3dart`                  | Apache 2.0   | Cryptographic signature verification and Sovereign DID address derivation.         |
| **FastAPI**                          | `tiangolo/fastapi`                | MIT License  | Lightweight asynchronous local P2P gateway protocol handling.                      |
| **Uvicorn**                          | `encode/uvicorn`                  | BSD 3-Clause | ASGI web server implementation for local streamable communication.                 |
| **Flutter SDK**                      | `flutter/flutter`                 | BSD 3-Clause | UI and sensory feedback layer for mobile, desktop, and Fire TV display surfaces.   |
| **Pydantic**                         | `pydantic/pydantic`               | MIT License  | Schema validation and data modeling for skill configuration payloads.              |
| **Supabase Client**                  | `supabase/supabase-flutter`       | MIT License  | Optional encrypted cloud relay fallback when devices are away from home.           |

---

## 3. AI Tools & Methodologies Used

- **AI Assistance Tools:** Anthropic Claude 3.5 Sonnet and OpenAI GPT-4o.
- **Principal Uses:** Utilized strictly as developer productivity tools for schema syntax validation, agent prompt structuring, regression test harness design, and Markdown formatting conforming to the Uliya Skill Development Standard.
- **Author Attribution:** All architectural choices, protocol designs, integration workflows, and submission texts were directed, authored, and finalized by Abbas Satour.
