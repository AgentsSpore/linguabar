# LinguaBar

> A global network of bars and restaurants where people connect face-to-face across borders — with real-time AI translation removing every language barrier.

## The Concept

LinguaBar is a **physical chain of bars/restaurants** equipped with smart tables. Each table has a built-in tablet with camera, microphone, and screen. You sit down, order a drink, and start a live video conversation with someone at another LinguaBar — anywhere in the world. The software handles **real-time speech translation**, so you talk in your language, they talk in theirs, and you understand each other perfectly.

This is not another video chat app. It's a **new category of social venue** — a place where the atmosphere of a real bar meets the magic of borderless human connection.

## Why It Matters

- **People crave real connection** — not another app, but a reason to go out and meet someone genuinely different
- **Language is the last barrier** — real-time AI translation has finally reached the quality needed to make this work
- **Network effect** — every new LinguaBar in the world makes every other one more valuable
- **No tech literacy required** — sit down, tap "Connect", start talking

## Key Experiences

| Experience | Description |
|---|---|
| **Casual Chat** | Random match with someone from another country. Chat roulette over cocktails |
| **Themed Tables** | "World Cuisine", "Travel Stories", "Music" — connect around shared interests |
| **Group Tables** | 4-6 people from different countries at one virtual table |
| **Culture Exchange** | "Tell me about your city" — structured cultural discovery format |
| **Global Events** | Themed nights: "Tokyo Evening", "Latin Night" — all bars in the network join in |
| **Business Networking** | Premium format for professional connections across borders |

## How It Works

```
┌─────────────────────────────────────────────────────┐
│                   TABLE TERMINAL                     │
│  ┌──────────┐  ┌──────────┐  ┌───────────────────┐  │
│  │  Camera  │  │   Mic    │  │  Screen (video +  │  │
│  │          │  │  + noise │  │  subtitles +      │  │
│  │          │  │  cancel  │  │  translation)     │  │
│  └──────────┘  └──────────┘  └───────────────────┘  │
└─────────────────────┬───────────────────────────────┘
                      │
        ┌─────────────▼──────────────┐
        │    Edge Server (in-bar)     │
        │  • Noise cancellation       │
        │  • Local caching            │
        │  • Low-latency relay        │
        └─────────────┬──────────────┘
                      │
        ┌─────────────▼──────────────┐
        │       Cloud Platform        │
        │                             │
        │  ┌───────────────────────┐  │
        │  │  ASR (Speech-to-Text) │  │  Whisper / Deepgram
        │  └───────────┬───────────┘  │
        │  ┌───────────▼───────────┐  │
        │  │  Real-time Translation│  │  LLM (context-aware)
        │  └───────────┬───────────┘  │
        │  ┌───────────▼───────────┐  │
        │  │  TTS (Text-to-Speech) │  │  Voice synthesis
        │  └───────────────────────┘  │
        │                             │
        │  Matchmaking Engine         │
        │  Session Management         │
        │  Bar Admin Dashboard        │
        │  Analytics & Billing        │
        └─────────────────────────────┘
```

## Tech Stack

| Layer | Stack |
|-------|-------|
| Backend | FastAPI (Python 3.11+), uv, WebSocket |
| Frontend | Flutter (tablet UI), Riverpod, go_router |
| Video/Audio | WebRTC for peer-to-peer communication |
| Speech-to-Text | Whisper / Deepgram (streaming ASR) |
| Translation | LLM-based contextual translation (streaming) |
| Text-to-Speech | Voice synthesis with speaker adaptation |
| Noise Cancellation | AI-based noise suppression (bar environment) |

## Revenue Model

| Stream | Description |
|---|---|
| **Food & Drinks** | Core bar revenue — people come, stay longer, order more |
| **Franchise / SaaS** | Bars pay for equipment + software subscription |
| **Premium Tables** | VIP tables with better hardware, private sessions |
| **Themed Events** | Paid events, corporate bookings, language nights |
| **Mobile App** | Continue conversations after leaving the bar |
| **Brand Partnerships** | Sponsors for themed evenings and global events |

## Current Prototype

The current codebase is a **web-based chat prototype** with basic translation — a stepping stone toward the full vision.

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

## Project Structure

```
├── backend/
│   └── app.py              # FastAPI app (WebSocket, matchmaking, translation)
└── flutter/
    └── lib/
        ├── features/
        │   ├── onboarding/  # Language selection
        │   ├── rooms/       # Room browser
        │   ├── matchmaking/ # Partner matching
        │   └── chat/        # Real-time chat
        └── core/
            ├── models/
            ├── state/
            ├── routing/
            └── theme/
```

## License

MIT
