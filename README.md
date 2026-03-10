<div align="center">
  <img src="https://raw.githubusercontent.com/moltis-org/moltis/main/website/favicon.svg" width="100" height="100" alt="PocketTTS Coqui Bridge">
  <h1>PocketTTS Coqui Bridge</h1>
  <p><strong>The Sovereign Voice Layer for Moltis</strong></p>
  <p><em>Real-time TTS. Zero Latency. 100% Local.</em></p>

  <p>
    <a href="#key-advantages">Advantages</a> •
    <a href="#installation">Installation</a> •
    <a href="#comparison">The Killer Edge</a> •
    <a href="#moltis-integration">Moltis Integration</a> •
    <a href="#features">Features</a>
  </p>
</div>

---

## 🚀 Stop Paying for Your Own Voice

**PocketTTS Coqui Bridge** is a game-changing, production-grade bridge that brings elite-level Text-to-Speech directly to your hardware. No expensive GPUs, no predatory API fees, and absolutely no data harvesting.

We built this because sovereign infrastructure isn't just a luxury—it's a requirement. Whether you're powering a [Moltis](https://github.com/moltis-org/moltis) agent or building a private assistant, this bridge is your ticket to high-performance, cost-free voice synthesis.

### 💎 Key Advantages

*   **⚡ Real-Time CPU Performance** — Optimized to run lightning-fast on standard CPUs. Get instant response times without the need for high-end GPUs.
*   **💰 100% Free & Self-Hosted** — Zero costs. Zero subscriptions. Zero character limits. You own the compute, you own the voice.
*   **👥 Custom Voice Cloning** — Seamlessly clone any voice with just seconds of audio. Your clones stay private, local, and under your control.
*   **🤖 Moltis-Native** — Designed from the ground up to integrate perfectly into the Moltis ecosystem.
*   **🐳 One-Click Deployment** — Fully Dockerized for a "it just works" experience on any server.
*   **🎨 Admin UI** — A professional, dark-themed dashboard to manage, test, and export your custom voices.

## Why PocketTTS Coqui Bridge?

**PocketTTS Coqui Bridge** is a production-oriented FastAPI service that exposes Coqui-compatible TTS endpoints. Designed primarily for the [Moltis](https://github.com/moltis-org/moltis) ecosystem, it allows you to swap expensive, privacy-invasive paid APIs (like OpenAI or ElevenLabs) for a self-hosted powerhouse.

*   **Secure by Design** — Your voice data never leaves your network. No telemetry, no "AI safety" filters, no surveillance.
*   **Production-Ready** — This isn't a hobby script. It’s a FastAPI-wrapped service with session-based authentication, SQLite persistence, and a protected Admin UI.
*   **Moltis-Native** — Drop-in compatibility for Moltis. Configure it once and your bot has a voice forever, for free.
*   **One-Click Docker** — Deployment so easy it feels like cheating.

## Installation

### Deploy in 60 Seconds (Docker)
The fastest path to sovereign voice:

```bash
docker run -d \
  --name tts-bridge \
  -p 8000:8000 \
  -e APP_USERNAME=admin \
  -e APP_PASSWORD=your_secure_password \
  -e SESSION_SECRET=$(openssl rand -hex 32) \
  -v $(pwd)/data:/app/data \
  --restart always \
  ghcr.io/moltis-org/pockettts-coqui-bridge:latest
```

## Comparison: The End of Paid APIs

| Feature | OpenAI TTS | ElevenLabs | **PocketTTS Bridge** |
| :--- | :--- | :--- | :--- |
| **Cost** | Per-character | Tiered / Expensive | **$0.00 (Forever)** |
| **Privacy** | Logged/Analyzed | Data Harvesting | **Zero-Knowledge** |
| **Offline** | No | No | **Yes** |
| **Latency** | Network Dependent | Variable | **Local-speed** |
| **Custom Voices** | Limited | Paid | **Unlimited Cloning** |

## Architecture

```text
┌─────────────────┐      ┌──────────────────────────┐      ┌─────────────────┐
│     Moltis      │      │  PocketTTS Coqui Bridge  │      │   Local Data    │
│  (Or any App)   │      │       (FastAPI)          │      │    (SQLite)     │
└────────┬────────┘      └────────────┬─────────────┘      └────────┬────────┘
         │                            │                             │
         │   POST /api/tts            │      Register Voice         │
         ├───────────────────────────►├────────────────────────────►│
         │                            │      Store Embeddings       │
         │   Receive .wav             │                             │
         │◄───────────────────────────┤                             │
         │                            │      Synthesize             │
         │                            │◄────────────────────────────┘
         │                            │      (Pocket-TTS + Coqui)
```

## Features

*   **Coqui-Compatible API** — Standardized `POST /api/tts` endpoint supporting JSON and Multipart.
*   **Voice Registry** — Managed via SQLite. Built-in voices + your own high-fidelity clones.
*   **Protected Admin UI** — Manage voices, test synthesis, and update settings through a clean, Pico.css-powered dashboard.
*   **Instant Voice Cloning** — Upload a sample, generate an embedding, and use it immediately.
*   **Multi-Format Support** — Returns high-quality `.wav` or compressed `.mp3` on the fly.

## 🔌 Moltis Integration

Integrating with your Moltis bot is effortless. Update your `config.toml` to point to your new bridge:

```toml
[voice.tts]
enabled = true
provider = "coqui"

[voice.tts.coqui]
endpoint = "http://your-server-ip:8000"
```

## Getting Started

### 1. Configure Moltis
To use this bridge with your Moltis instance, update your `config.toml`:

```toml
[voice.tts]
enabled = true
provider = "coqui"

[voice.tts.coqui]
endpoint = "http://localhost:8000"
```

### 2. Access the Admin UI
Navigate to `http://localhost:8000` to access the management dashboard.
*   **Clone voices** by uploading 10-30 seconds of clear audio.
*   **Preview** voices before deploying them to your bot.
*   **Monitor** the SQLite registry.

## Local Development (Non-Docker)

```bash
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
pip install pocket-tts torch --index-url https://download.pytorch.org/whl/cpu
cp .env.example .env
# Edit .env with your credentials
uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload
```

---

## 🛡 License
MIT. Built for the community that values sovereignty. Stop the API tax today.
