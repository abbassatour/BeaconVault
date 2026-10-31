

# UGOS System CLI & Capability Primitives

This reference specifies the planned UGOS command-line interface (CLI) commands, container mounts, and system permissions utilized by the `beacon-sovereign-vault` Skill.

---

## 1. Storage Volume Architecture

The skill operates within a sandboxed, dedicated user share volume:

```text
/volume1/BeaconVault/
├── documents/
│   ├── prescriptions/
│   ├── financial_bills/
│   └── correspondence/
├── perimeter_security/
│   ├── snapshots/
│   └── ring_event_logs/
├── voice_memos/
│   ├── raw_audio/
│   └── transcriptions/
└── emergency_blackbox/
    ├── sos_audit_trail.jsonl
    └── gps_telemetry/
```

---

## 2. UGOS CLI Commands Executed by Agent

### A. Storage & File System Primitives

- `ugos-storage create-dir --path "/volume1/BeaconVault/documents"`: Creates categorized storage directories with access permissions restricted to authorized household users.
- `ugos-storage write-file --path "<target_path>" --atomic`: Atomically writes incoming images and audio streams with SHA-256 integrity verification.
- `ugos-storage get-quota --volume "/volume1"`: Queries current disk headroom to trigger automated archival compression when utilization exceeds 85%.

### B. AI Engine & Vector Processing Primitives

- `ugos-ai embedding create --model "bge-small-en-v1.5" --input "<extracted_text>"`: Generates on-device dense vector embeddings for indexed documents and audio transcripts.
- `ugos-ai vision inference --model "internvl-chat-2b" --image "<snapshot_path>"`: Analyzes camera captures locally on the NAS NPU/GPU to describe visual layouts without transmitting home footage to third-party APIs.

### C. Knowledge Base (RAG) Management Primitives

- `ugos-knowledge index add --kb "BeaconAssistiveKB" --doc-id "<uuid>" --vector "<embedding>" --metadata "<json>"`: Adds extracted knowledge chunks to the local vector index.
- `ugos-knowledge search --kb "BeaconAssistiveKB" --query "<user_voice_query>" --top-k 3`: Retrieves contextually relevant snippets to formulate real-time answers for the user's audio screen reader.

---

## 3. Network Daemon Configuration

The skill registers a lightweight local listener service:

- **Protocol:** Authenticated WebSockets over HTTP/1.1 (`/beacon_sync`)
- **Port:** `8492` (Auto-incrementing fallback: `8492–8499`)
- **Transport Security:** Cryptographic challenge-response handshake based on EIP-55 Ethereum Public Key / W3C DID addresses.
- **Latency Budget:** Sub-10ms local response time for real-time mobile and TV synchronization.
