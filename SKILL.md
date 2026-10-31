
---
name: beacon-sovereign-vault
description: "Local-first assistive AI intelligence and private sensory archive for UGOS NAS, providing hands-free document indexing, perimeter security event archival, and spatial knowledge retrieval for visually impaired users."
---
# BeaconVault: Sovereign Assistive Intelligence Skill

## 1. User Goal

The goal of the `beacon-sovereign-vault` Skill is to transform UGREEN AI NAS into an always-on, 100% private, assistive home intelligence hub for visually impaired individuals and digital minimalists. It continuously ingests, organizes, indexes, and semantically retrieves multi-modal data generated from assistive phones (BeaconOS) and perimeter security cameras (Ring Doorbell/CCTV) over zero-latency local Wi-Fi without relying on commercial public clouds.

For detailed architecture and storage topology, see [UGOS CLI Capabilities](references/ugos_cli_capabilities.md).

---

## 2. Required Inputs

The skill accepts the following structured data streams via authorized local network endpoints (`/beacon_sync` WebSocket/REST):

- **Document & Visual Scans:** Handheld assistive camera inspection frames (medication labels, utility bills, mail, printed paperwork) with bounding metadata and preliminary OCR text.
- **Voice Memos & Audio Thoughts:** Recorded audio snippets (`.wav`, `.m4a`) and localized speech transcripts.
- **Perimeter Security Events:** High-resolution video snapshots, motion sensor timestamps, and doorbell ding metadata from residential Ring/CCTV nodes.
- **Emergency Telemetry Dispatches:** Encrypted SOS snapshots containing exact GPS coordinates, battery health telemetry, and local timestamp signatures.

---

## 3. Supported UGOS CLI & System Capabilities

The skill interfaces with UGOS underlying Linux/Docker services through authorized system primitives:

- **Storage Management:** Manages private share volumes under `/volume1/BeaconVault/` with categorized directories (`documents/`, `perimeter/`, `memos/`, `emergency/`).
- **Local AI Embedding Engine:** Generates on-device semantic vector embeddings for all ingested text and descriptions.
- **Local Vision & LLM Inference:** Leverages UGOS built-in NPU/GPU inference runtime to analyze scene images, extract tables, and summarize documents locally.
- **Knowledge Base (Local RAG):** Maintains vector indexes for sub-second semantic retrieval across historical user data.
- **P2P Event Daemon:** Runs a zero-trust local background daemon on port `8492` for high-speed P2P LAN replication with BeaconOS client devices.

For exact CLI commands and filesystem parameters, refer to [UGOS CLI Capabilities Reference](references/ugos_cli_capabilities.md).

---

## 4. Expert Agent Orchestration Workflow

Data Flow Diagram:

[Handheld Beacon Phone / Ring Camera]
         │
         │ 1. Local LAN Transfer (P2P WebSocket / < 2ms)
         ▼
┌─────────────────────────────────────────────────────────────────┐
│              UGOS Agent: beacon-sovereign-vault                │
│                                                                 │
│  Phase A: Ingestion & Privacy Vault Guard                       │
│  • Validates EIP-55 Sovereign DID cryptographic signature       │
│  • Routes raw media to `/volume1/BeaconVault/{category}/{date}/`│
│                                                                 │
│  Phase B: Local AI Processing & Vectorization                   │
│  • Generates vector embeddings for OCR text & voice memos       │
│  • Tags metadata (date, category, priority, room coordinate)    │
│  • Updates UGOS Knowledge Base index                            │
│                                                                 │
│  Phase C: Ambient Voice Retrieval (Living Room RAG)             │
│  • Receives voice query from Fire TV / Mobile / Living Room Spk │
│  • Executes semantic similarity lookup (< 50ms)                 │
│  • Synthesizes concise natural-language audio response          │
└─────────────────────────────────────────────────────────────────┘

### Detailed Execution Pipeline:

1. **Secure Ingestion:** When the user captures a document or registers a voice note, BeaconOS streams the payload directly to the NAS via LAN Direct.
2. **Metadata Tagging:** The UGOS agent classifies the item into one of four vaults: `Documents`, `Perimeter_Security`, `Memos`, or `Emergency_Attestations`.
3. **Local Knowledge Indexing:** Text from documents and audio transcripts is vectorized locally using UGOS on-device embedding models. No external cloud API calls are made.
4. **Natural Query Resolution:** When the user asks: *"When does my prescription medicine expire?"* or *"Who came to the door this morning?"*, the agent executes local hybrid search (Keyword + Vector) and returns a concise, accessible spoken summary.

---

## 5. Completion and Failure Handling

- **LAN Disconnection / Network Partition:** If local Wi-Fi drops, client devices buffer changes in their encrypted Drift SQLite database. Upon reconnection, the skill executes differential Delta Sync (`vaultDeltaRequest`) with Last-Write-Wins (LWW) conflict resolution.
- **Storage Quota & Archival:** When volume usage exceeds 85%, the skill automatically compresses historical raw video snapshots while preserving all vector embeddings and text descriptions intact.
- **Corrupted Ingestion Stream:** If a payload arrives incomplete or fails DID cryptographic verification, the skill rejects the entry, logs a warning in UGOS system audit logs, and prompts the client to resend.

---

## 6. Disclosures & Attributions

All third-party components, open-source libraries, licenses, and AI tools used in developing this skill are fully documented in [Disclosures and Licenses](references/disclosures_and_licenses.md).
