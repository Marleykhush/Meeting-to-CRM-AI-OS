# AI Meeting-to-CRM Operations System

AI system that converts real-estate viewing calls into validated CRM records. Transcribes audio, extracts structured data via AI, deterministically validates it, then auto-syncs to HubSpot, routes gaps to a human via Telegram form, or flags unusable input — cutting manual entry from ~7 min to under 2.

## How it works

Telegram audio intake → transcription → AI extraction (structured JSON) → deterministic validation → routing:
- **PASSED** → auto-synced to HubSpot (Contact + Deal)
- **REVIEW** → Telegram alert with a form scoped to only the missing/flagged fields; auto-resumes and merges on submission
- **FAILED** → Telegram alert only, no automated recovery (by design for v1)

Every execution is logged to Google Sheets regardless of outcome.

## Setup

Import `Meeting-to-CRM System.json` into n8n. You'll need your own credentials for:
- Telegram Bot (audio intake + notifications)
- A transcription service (Whisper-based)
- Google Gemini (extraction)
- HubSpot Private App token (Contact/Deal scopes)
- Google Sheets (execution logging)

No secrets are included in the export — only credential references.

## Sample data

See `/samples` for example audio/transcripts covering a clean pass, a missing-field case, and a rejected case.

## Docs

Full case study, evaluation results, and failure analysis are in the accompanying submission documents (Case Study, Evaluation Package, AI Collaboration Note).
