---
name: beacon-vault
description: Sovereign local-first assistive intelligence vault for UGREEN AI NAS. Use when the user requests eyes-free document reading, ambient perimeter safety inspection, audio thought indexing, or sensory accessibility assistance without cloud exposure.
---
# Goal

Transform UGREEN AI NAS into a sovereign, local-first assistive intelligence hub for visually impaired individuals and screen-fatigued household members. BeaconVault orchestrates automated zero-latency ingestion and eyes-free semantic retrieval across physical mail, medication containers, audio memos, and RTSP perimeter security feeds entirely on-device, preserving full data self-custody.

# Required input

Collect only the following user parameters or operational triggers from the accessibility cockpit:

- `query`: The spoken, spatial, or text accessibility query (e.g., inquiring about medication dosage, incoming visitors, or utility bill due dates).
- `source_path`: The sandboxed local NAS directory containing newly ingested camera captures, audio memos, or surveillance snapshots.
- `target_domain`: The target sensory domain (`documents`, `memos`, `perimeter`, or `all`).

Do not collect sub-agent internal states, authentication tokens, or private credentials directly from user input.

# Generation-time capability evidence

- `ug-filesystem` → `file-agent`
- `ug-document` → `document-agent`
- `ug-photo` → `photo-agent`
- `ug-knowledge` → `knowledge-agent`
- `ug-surveillance` → `security-monitor-agent`

# Orchestration

The workflow coordinates specialized UGOS sub-agents in sequential order, passing strictly verified upstream results to downstream tasks:

1. **Sensory Discovery and Ingestion Verification**:
   Delegate path verification to `file-agent` to identify incoming assistive captures or audio clips in the verified drop folder:
   `delegate --target file-agent --instruction 'Find and list newly ingested capture frames and audio files in the user drop folder, validating read permissions and file integrity.'`
2. **Assistive Document and Vision Inspection**:
   When reading medicine boxes, dosage labels, or utility bills, delegate structured extraction to `document-agent`:
   `delegate --target document-agent --instruction 'Extract text, expiration dates, warnings, and structured key-value pairs from verified document images using medical-report or invoice schemas.'`
   For general physical scene inspection or handheld object identification, delegate to `photo-agent`:
   `delegate --target photo-agent --instruction 'Inspect visual scene frames and extract descriptive object labels and text using local VLM and vision OCR capabilities.'`
3. **Voice Thought Transcription and Knowledge Indexing**:
   When raw audio recordings are ingested, pass the verified audio file path to `knowledge-agent`:
   `delegate --target knowledge-agent --instruction 'Transcribe the incoming audio memo into structured text and index it into the local vector knowledge store with semantic timestamps.'`
4. **Perimeter Safety and Visitor Event Verification**:
   When the user inquires about exterior sounds, visitors, or motion alerts, delegate timeline analysis to `security-monitor-agent`:
   `delegate --target security-monitor-agent --instruction 'Query RTSP surveillance event timeline for Human or Package detection events, resolving identity markers and snapshot evidence.'`
5. **Spoken Sensory Synthesis**:
   Synthesize all verified upstream agent findings into a concise, screen-reader-optimized, eyes-free summary answering the user query.

# Completion and failure

- **completed**: When all delegated sub-agents finish with verified real results, synthesize the final speech response, confirm local indexing, and mark execution as completed.
- **failed**: If an input artifact is corrupted, missing, or fails schema validation, report failed, clearly describe the missing resource, and halt downstream execution without hallucinating data.
- **cancelled**: If the user aborts an ongoing audio transcription or search routine, cleanly terminate active agent jobs and report cancelled while preserving existing vault records.
- **waiting_user**: When an input query is ambiguous (e.g., multiple prescription bottles detected in frame), pause execution with status waiting_user and request specific verbal clarification.
- **waiting_approval**: Before executing irreversible state modifications (e.g., permanently archiving files, relocating assets, or triggering external emergency relays), pause in waiting_approval until explicit user confirmation is obtained.
- **Empty or zero matches**: If an inquiry yields no results or zero matches, return an explicit zero matches response and terminate cleanly without substituting unrelated data.

For architectural references and third-party disclosures, see [UGOS Capability Reference](references/ugos_cli_capabilities.md) and [Disclosures &amp; Licenses](references/disclosures_and_licenses.md).
