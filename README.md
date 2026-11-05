# OnlyFans AI 18+ — AI-Powered Adult Content Platform

Premium AI companion platform with photorealistic characters — chat, photo, video, voice. All AI-generated on local GPU, zero cloud costs.

![Python](https://img.shields.io/badge/Backend-FastAPI-blue)
![Next.js](https://img.shields.io/badge/Frontend-Next.js-black)
![GPU](https://img.shields.io/badge/GPU-RTX_5090-green)
![Status](https://img.shields.io/badge/Status-MVP_Ready-orange)

## Overview

A self-hosted alternative to OnlyFans/Character.AI powered entirely by local AI models. Every interaction — chat, photo, video, voice — is generated in real-time on your own GPU infrastructure. No API costs, no content restrictions, full privacy.

## Features

### AI Chat
- Uncensored local LLM (Dolphin-Mixtral, LumiMaid, custom fine-tunes)
- Character personality system with memory
- Context-aware responses with mood tracking
- VISUAL_PROMPT system — AI describes scenes inline, triggers auto-generation

### AI Photo Generation
- **SDXL + DreamShaper** — photorealistic character images
- **IP-Adapter FaceID** — consistent face across all photos
- **FaceDetailer** — automatic face quality enhancement
- **DWPose ControlNet** — precise body pose control
- **30+ scene presets** — various scenarios and outfits
- Smart routing: standard → cloud (fast), premium → local SDXL (quality)

### AI Video
- **Wan 2.1 I2V** — image-to-video animation (5 sec clips)
- **FaceFusion** — face swap onto any video
- **LivePortrait** — facial animation from reference video
- Vertical 9:16 format (mobile-first)

### AI Voice
- **XTTS v2** — voice cloning from 30-sec sample
- Unique voice per character
- Multi-language support
- Real-time TTS in chat

### Platform
- Token-based economy (photo = 0tokens, video = 0 tokens)
- Subscription tiers (Free / Basic $0 / Pro $0 / VIP $0
- Secure JWT authentication
- Mobile-responsive PWA
- Payment integration (CCBill + crypto USDT)

## Architecture

```
┌─────────────────────────────────────────────────────┐
│                    Frontend                          │
│           Next.js 14 + Tailwind + shadcn/ui          │
│      Character Profiles / Chat / Gallery / Shop      │
└───────────────────────┬─────────────────────────────┘
                        │ WebSocket + REST
┌───────────────────────▼─────────────────────────────┐
│                    Backend                            │
│              FastAPI + SQLAlchemy                     │
│                                                      │
│  ┌──────────┐ ┌───────────┐ ┌─────────────────────┐ │
│  │ Chat     │ │ Auth/JWT  │ │ Token Economy       │ │
│  │ Engine   │ │ + Payments│ │ + Subscriptions     │ │
│  └────┬─────┘ └───────────┘ └─────────────────────┘ │
│       │                                              │
│  ┌────▼──────────────────────────────────────────┐   │
│  │            AI Generation Pipeline             │   │
│  │                                                │   │
│  │  ┌────────┐ ┌────────┐ ┌───────┐ ┌─────────┐ │   │
│  │  │ Ollama │ │ComfyUI │ │Wan2.1 │ │ XTTS v2 │ │   │
│  │  │  LLM   │ │  SDXL  │ │ Video │ │  Voice  │ │   │
│  │  └────────┘ └────────┘ └───────┘ └─────────┘ │   │
│  └────────────────────────────────────────────────┘   │
└───────────────────────┬─────────────────────────────┘
                        │
                 ┌──────▼──────┐
                 │  GPU Farm   │
                 │ RTX 5090 x10│
                 └─────────────┘
```

## Content Pipeline

```
Character Profile (face ref + personality + voice ref)
         │
         ├── Chat request → LLM → text + VISUAL_PROMPT
         │                            │
         │                    ┌───────▼────────┐
         │                    │ SDXL + IP-Adapter│
         │                    │ (consistent face)│
         │                    └───────┬─────────┘
         │                            │
         │                    ┌───────▼────────┐
         │                    │  FaceDetailer   │
         │                    │ (quality fix)   │
         │                    └───────┬─────────┘
         │                            │
         ├── Video request ──▶ Wan 2.1 I2V + FaceFusion
         │
         └── Voice request ──▶ XTTS v2 (cloned voice)
```

## Characters

Each AI character includes:
- **Face reference** — SDXL-generated base portrait
- **Personality prompt** — detailed character backstory and behavior
- **Voice reference** — 30-sec audio sample for XTTS cloning
- **Costume library** — 30+ outfits and scenes
- **Pose library** — DWPose skeletons for body control

## Performance (RTX 5090)

| Task | Speed |
|------|-------|
| Chat response | 143 tok/s |
| Photo generation | 6 sec |
| Photo with face fix | 10 sec |
| Video clip (5 sec) | 3 min |
| Voice (30 sec speech) | 5 sec |

## Monetization

| Tier | Price | Includes |
|------|-------|----------|
| Free | $0 | 50 tokens on signup, text chat only |
| Basic | $9.99/mo | 500 tokens, photos |
| Pro | $19.99/mo | 2000 tokens, photos + video |
| VIP | $49.99/mo | Unlimited, priority generation, custom requests |

**Revenue model:**
- 1000 subscribers avg $20/mo = $20,000/mo
- GPU costs: $0 (local infrastructure)
- Gross margin: 90%+

## Traffic Strategy

- Reddit: r/nsfwai, r/aichat, character-specific subreddits
- Twitter/X: character accounts with preview content
- Telegram: preview channel with watermarked samples
- SEO: "AI girlfriend", "AI companion", "virtual girlfriend"

## Investment

Seeking $100K for GPU farm scaling. See [Luna AI Platform](https://github.com/mjasuhaby/luna-ai-platform) for full investment details.

## Tech Stack

| Component | Technology |
|-----------|-----------|
| Frontend | Next.js 14, TypeScript, Tailwind, shadcn/ui |
| Backend | Python FastAPI, SQLAlchemy, SQLite → PostgreSQL |
| LLM | Ollama (Dolphin-Mixtral, uncensored models) |
| Image | ComfyUI, SDXL DreamShaper, IP-Adapter, FaceDetailer |
| Video | Wan 2.1 I2V, FaceFusion, LivePortrait |
| Voice | XTTS v2 (Coqui) |
| Payments | CCBill (adult-friendly) + USDT/crypto |
| CDN | BunnyCDN |
| Hosting | Self-hosted GPU farm + Hetzner VPS (web) |

## Disclaimer

This platform is for adults only (18+). All content is AI-generated — no real people involved.

## Status

🟡 **MVP Complete** — Chat + Photo + Voice working. Video pipeline ready. Seeking investment for production scaling.

## Author

AI platform developer. Available for custom development and investment discussions.
GitHub: https://github.com/mjasuhaby
