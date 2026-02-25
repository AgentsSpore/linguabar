# AGENTS.md — LinguaBar

## Overview

LinguaBar is a global network of bars and restaurants where people connect face-to-face across borders with real-time AI translation. Each venue has smart tables equipped with tablets (camera, mic, screen). Patrons sit down and start a live video conversation with someone at another LinguaBar anywhere in the world — the software handles speech recognition, translation, and synthesis in real-time.

The current codebase is a web-based chat prototype — the first step toward the full vision.

## Full Vision Architecture

```
┌─────────────────────────────────────────────────────┐
│                   TABLE TERMINAL                     │
│  Camera + Mic + Screen (tablet)                      │
└─────────────────────┬───────────────────────────────┘
                      │
        ┌─────────────▼──────────────┐
        │    Edge Server (in-bar)     │
        │  • AI noise cancellation    │
        │  • Local caching            │
        │  • Low-latency relay        │
        └─────────────┬──────────────┘
                      │
        ┌─────────────▼──────────────┐
        │       Cloud Platform        │
        │                             │
        │  ASR ──▶ Translation ──▶ TTS│
        │  (Whisper)  (LLM)   (voice) │
        │                             │
        │  WebRTC Signaling           │
        │  Matchmaking Engine         │
        │  Session Management         │
        │  Bar Admin Dashboard        │
        │  Analytics & Billing        │
        └─────────────────────────────┘
```

## Current Prototype Architecture

```
┌─────────────────┐     ┌─────────────────────────┐
│   Flutter Web   │────▶│   FastAPI Backend       │
│   (port 3050)   │     │   (port 8050)           │
└─────────────────┘     │                         │
                        │  WebSocket rooms        │
                        │  Matchmaking queue      │
                        │  Translation endpoint   │
                        └─────────────────────────┘
```

## Tech Stack

| Layer | Stack |
|-------|-------|
| Backend | FastAPI (Python 3.11+), uv, WebSocket |
| Frontend | Flutter Web/Tablet, Riverpod, go_router |
| Video/Audio (planned) | WebRTC |
| ASR (planned) | Whisper / Deepgram (streaming) |
| Translation | LLM-based contextual translation |
| TTS (planned) | Voice synthesis with speaker adaptation |

## Key Files

### Backend
| File | Description |
|------|-------------|
| [`backend/app.py`](backend/app.py) | FastAPI app — rooms, matchmaking, translation |

### Frontend
| File | Description |
|------|-------------|
| [`flutter/lib/app.dart`](flutter/lib/app.dart) | MaterialApp, routing |
| [`flutter/lib/core/routing/app_router.dart`](flutter/lib/core/routing/app_router.dart) | go_router configuration |
| [`flutter/lib/features/onboarding/onboarding_screen.dart`](flutter/lib/features/onboarding/onboarding_screen.dart) | Language selection |
| [`flutter/lib/features/matchmaking/matchmaking_screen.dart`](flutter/lib/features/matchmaking/matchmaking_screen.dart) | Partner matching |
| [`flutter/lib/features/rooms/rooms_screen.dart`](flutter/lib/features/rooms/rooms_screen.dart) | Room browser |
| [`flutter/lib/features/chat/chat_room_screen.dart`](flutter/lib/features/chat/chat_room_screen.dart) | Real-time chat |

## API Endpoints

```
GET  /rooms              — list available language rooms
POST /rooms              — create a room
GET  /rooms/{id}         — room details
WS   /rooms/{id}/ws      — WebSocket connection for chat
POST /matchmaking/join   — join matchmaking queue
POST /translate          — translate text snippet
GET  /health             — health check
```

## Screen Flows

```
Onboarding (language selection)
  ├── → Matchmaking → Chat Room (roulette)
  └── → Room Browser → Chat Room
```

## Key Scenarios

| Scenario | Description |
|---|---|
| Casual Chat | Random match with someone from another country |
| Themed Tables | Connect around shared interests (cuisine, travel, music) |
| Group Tables | 4-6 people from different countries at one virtual table |
| Culture Exchange | Structured cultural discovery conversations |
| Global Events | Themed nights across all bars in the network |
| Business Networking | Premium professional connections |

## Development

```bash
# Backend
cd backend && uv sync
uv run uvicorn app:app --reload --port 8050

# Flutter
cd flutter && flutter pub get
flutter run -d chrome --web-port 3050
```

## Roadmap

- [x] Text chat with basic translation
- [x] Room system and matchmaking
- [ ] WebRTC video/audio integration
- [ ] Streaming ASR (speech-to-text)
- [ ] Streaming LLM translation with conversation context
- [ ] TTS with voice adaptation
- [ ] Live subtitles overlay on video
- [ ] AI noise cancellation for bar environments
- [ ] Smart matchmaking (interests, timezone, rating)
- [ ] Tablet-optimized UI
- [ ] Bar admin dashboard
- [ ] Mobile companion app

## Notes

- Current implementation is a prototype (text chat + basic translation)
- No persistent database — state is in-memory
- Real-time pipeline (ASR → LLM → TTS) is stubbed, not yet integrated
- Target deployment: tablets mounted on bar tables
