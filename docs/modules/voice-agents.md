# Voice Agents — Legal Scribe & Litigation Voice Interface

> Source: Notion wiki "VOICE AGENTS-Legal Scribe", "AI VOICE AGENTS", "11Labs Voice Agent", "Introducing Universal-Streaming"

## Overview

Voice Agents provide spoken-language interfaces for litigation workflows — enabling attorneys to dictate evidence notes, conduct voice-driven case research, and produce transcription-to-evidence pipelines directly from deposition recordings and field interviews.

## Agent Inventory

### 1. Legal Scribe Agent

**Purpose**: Real-time transcription of legal dictation with structured output.

| Capability         | Description                                                        |
| ------------------ | ------------------------------------------------------------------ |
| Voice-to-text      | Real-time speech recognition for attorney dictation                |
| Entity extraction  | Auto-extract persons, dates, amounts, legal terms from speech      |
| Claim typing       | Tag dictated assertions as FACT/INFERENCE/OPINION/LEGAL_CONCLUSION |
| Evidence linking   | Associate spoken observations with evidence object IDs             |
| Privilege flagging | Detect and flag potentially privileged content in dictation        |

**Input**: Audio stream (microphone, phone, video conference)
**Output**: Structured transcript with entities, claim types, and evidence links

### 2. Deposition Transcriber Agent

**Purpose**: Process deposition video/audio into searchable, evidence-linked transcripts.

| Capability             | Description                                           |
| ---------------------- | ----------------------------------------------------- |
| Multi-format import    | Support top 10 court reporting firm formats           |
| Speaker diarization    | Identify and label speakers (witness, counsel, judge) |
| Timestamp alignment    | Sync text to video timestamps                         |
| Key excerpt extraction | Flag testimony relevant to RICO elements              |
| Impeachment detection  | Flag contradictions with prior statements or evidence |

**Input**: Deposition video/audio files (MP4, WAV, court reporter formats)
**Output**: Timestamped transcript + evidence linkage + impeachment flags

### 3. Case Research Voice Assistant

**Purpose**: Hands-free case research and question-answering over the evidence base.

| Capability          | Description                                                |
| ------------------- | ---------------------------------------------------------- |
| Voice queries       | "What did Angela Blair say about the Vikta agreement?"     |
| Evidence retrieval  | Search LexVault by voice command                           |
| Timeline navigation | "Walk me through events in Q3 2023"                        |
| Comparison          | "Compare Tesla's response to the original agreement terms" |
| Dictation mode      | Switch to Legal Scribe for note-taking                     |

## Technology Stack

### ElevenLabs Integration

> Reference: Notion "11Labs Voice Agent — UI/UX Control Page"

```html
<elevenlabs-convai
  agent-id="agent_2301kepakz24fmd8e361f6wyaa77"
></elevenlabs-convai>
<script src="https://unpkg.com/@elevenlabs/convai-widget-embed@beta"></script>
```

Configuration:

- Agent ID: `agent_2301kepakz24fmd8e361f6wyaa77`
- Widget: ElevenLabs Conversational AI embed
- Streaming: Universal-Streaming protocol (ultra-fast, ultra-accurate)
- VAD: Voice Activity Detection optimized for agent applications

### Speech-to-Text Pipeline

```
Audio Input → VAD (voice activity detection)
           → STT (speech-to-text, streaming)
           → NER (entity extraction)
           → Claim Typing
           → Evidence Linking (LexVault search)
           → Structured Output (transcript + annotations)
           → LexVault Storage (derivative artifact)
```

### Voice Agent Architecture

```
┌─────────────┐     ┌──────────────┐     ┌─────────────────┐
│ Audio Input  │────▶│ STT Engine   │────▶│ NLP Pipeline    │
│ (mic/file)   │     │ (ElevenLabs) │     │ (entities,      │
└─────────────┘     └──────────────┘     │  claims, links) │
                                          └────────┬────────┘
                                                   │
                    ┌──────────────┐     ┌─────────▼────────┐
                    │ TTS Engine   │◀────│ Agent Logic      │
                    │ (ElevenLabs) │     │ (LexVault search,│
                    └──────┬───────┘     │  case reasoning) │
                           │             └──────────────────┘
                    ┌──────▼───────┐
                    │ Audio Output │
                    │ (speaker)    │
                    └──────────────┘
```

## Integration with Master Repo

| Voice Agent Component | Maps to Repo Artifact                                                      |
| --------------------- | -------------------------------------------------------------------------- |
| Transcription output  | `docs/schemas/evidence-object.schema.json` (derivative type: `transcript`) |
| Entity extraction     | Entity Extractor agent (`config/playbooks.yaml`)                           |
| Claim typing          | Claim Object schema (`docs/schemas/claim-object.schema.json`)              |
| Evidence search       | MCP Router (`config/mcp-servers/`) → LexVault                              |
| Deposition planning   | Deposition Planner agent (`config/playbooks.yaml`)                         |
| Privilege detection   | Privilege Scanner agent (conservative flagging)                            |
| Audit trail           | `docs/schemas/audit-event.schema.json`                                     |

## Deposition Video Processing

> Source: Google Drive "lex-vault-litigation-swarm-prd.md"

### Format Support

Build importers for top 10 court reporting firm formats:

- RealLegal E-Transcript (.ptx)
- Summation (.dii)
- Concordance (.dat)
- MPEG-4 with synced transcript
- WebVTT/SRT subtitle formats

### Processing Pipeline

1. Ingest video + transcript files
2. Speaker diarization (identify counsel, witness, judge)
3. Timestamp alignment (text ↔ video sync)
4. Entity extraction from testimony
5. Key excerpt flagging (RICO relevance scoring)
6. Contradiction detection (compare to prior evidence)
7. Store in LexVault as derivative artifacts

## Notion References

| Wiki                        | URL                                                              | Content                                     |
| --------------------------- | ---------------------------------------------------------------- | ------------------------------------------- |
| Voice Agents - Legal Scribe | [Notion](https://www.notion.so/23eec5c813ef8099813fdb21766b0649) | Voice agent wiki with agent cards           |
| AI Voice Agents             | [Notion](https://www.notion.so/2f6ec5c813ef8014bb87e4f1bcd1ac73) | Voice platform research (Bland, ElevenLabs) |
| 11Labs Voice Agent UI       | [Notion](https://www.notion.so/38b39f36a6d547bb8ed5be0f635f24dd) | ElevenLabs widget embed, agent ID           |
| Video Transcript Template   | [Notion](https://www.notion.so/87f74f7875be4ae0a2b8f1ae5438bfc6) | Litigation evidence transcript format       |
