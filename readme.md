⚙️ S-VISION

The Ultimate Cross-Platform Personal AI Assistant
A real-time voice AI that can hear, see, speak, and control your computer — on any OS. Supports Windows, macOS, and Linux. Built on the Gemini Live API for native audio streaming, delivering zero subscriptions and total digital autonomy.

✨ Overview
S-VISION provides a completely flexible architecture. If you have no cloud quota left, no internet connection, or strict privacy requirements, you can seamlessly transition from the Gemini Live API to a completely local stack.

You can select your Speech Recognition, Language Model, and Voice Generator from the ⚙ → ENGINE & PROVIDERS panel. The local model can be on your machine or utilizing a third-party API. Both share the same protocol, allowing ultimate flexibility. None of the local processing libraries are loaded into memory unless explicitly activated (the engine decision takes 0.16 ms).

A local engine inherits the holographic avatar, lip-sync, self-echo guard, push-to-talk, wake word, memory, undo features, and all local system plugins. Every tool that interacts with the OS now validates its outcome: returning done if verified, unverified if the command was sent but could not be confirmed, or failed.

🚀 Capabilities
Core Features
Holographic Avatar & Facial Acting: An animated human head in the HUD using real facial geometry. Brows track phrases, gaze saccades, natural blinking, and nods on stressed syllables. It looks away while thinking and meets your eyes while listening.

Real Lip-Sync: Generates ~50 mouth shapes a second from audio formants and transcripts. The language-free mouth articulation uses Unicode reduction, working flawlessly across Latin, Cyrillic, and Greek scripts.

Push-to-Talk & Wake Word: Use Ctrl+Space for push-to-talk (global on Windows). Alternatively, use the local wake word detection which auto-sleeps after 2 minutes of silence.

Self-Echo Guard: S-VISION's microphone recognizes the tail of its own voice and drops it, preventing the assistant from answering its own output without muting the user.

Faster Live Engine & Instant Acknowledgment: Built on Gemini 3.1 Flash Live. S-VISION speaks a short, context-aware reply in your language the instant a longer background task starts.

Recallable Persistent Memory: Infinite memory size. The prompt carries a core identity, and S-VISION looks up the rest on demand via a local search. The UI includes a Memory Panel to view and delete facts.

Undo & Real Confirmation: Take back file movements, renames, creations, or system setting changes. Critical actions (Shutdown, Restart, WiFi) require physical button confirmation on the UI.

Audio Device Picker: Choose microphones and speakers by exact hardware name. S-VISION probes the host APIs (DirectSound, MME, WASAPI) with silence at startup to ensure the selected device actually routes audio properly.

Session Continuity: Network drops, voice changes, or microphone swaps no longer wipe the conversational context.

Video on the HUD: Plays YouTube, local files, or direct video URLs right where the avatar sits. Starts muted by default to prevent audio interference. Audio streams are automatically decoupled and synced to bypass YouTube combined-stream format errors.

Reactive HUD & Live Theming: Recolor the HUD and avatar via a hex wheel. A waveform pulses to real audio from your mic or S-VISION's voice.

System & Browser Control: Launch apps, adjust volume/brightness, control WiFi, manage windows, navigate tabs, and interact with web pages by voice.

Visual Awareness & Hardware Monitoring: Screen capture and webcam vision piped into the session. Continuous CPU, RAM, GPU, and temperature telemetry with voice alerts.

Proactive Morning Briefing: On first boot, S-VISION greets you, recaps yesterday's session, reads the time, and fetches live news.

Smart Application Launching/Closing: Closing an app politely asks the specific running executable to terminate, protecting S-VISION's own processes. Opening an already running app brings its window to the front rather than spawning a duplicate.

Untrusted Content Boundary: Web pages and fetched documents are wrapped in strict data markers. S-VISION will report instructions found inside files rather than executing them.

🔌 The Engine Panel
⚙ → ENGINE & PROVIDERS configures the conversational stack without file editing:

Hearing: CPU Whisper or transcription APIs.

Thinking: Local hardware (Ollama, LM Studio) or hosted APIs.

Speaking: Local Piper neural voices, system OS voices, or ElevenLabs.

Each component features a TEST button that connects and measures latency to prevent silent failures. Side-calls (like reading a document or parsing the screen) can also be routed to a secondary model to preserve Gemini's text quota without altering the primary conversational voice.

🌍 Multilingual Voice Following
When using Piper TTS, S-VISION reads the language tag returned by Whisper's transcription and instantly swaps the TTS voice to match the language you spoke. No extra language-detection dependencies are used.

🐧 Platform Honesty (Wayland & macOS)
Wayland (default on modern Ubuntu/Fedora) and secure macOS environments actively block programs from typing, clicking, or screen recording. S-VISION detects these session constraints at startup. Instead of pretending a click worked, the LLM is explicitly informed of its limits, allowing S-VISION to honestly state: "this session does not permit me to drive the screen."

📦 Quick Start & Installation
S-VISION automatically isolates OS-specific dependencies.

Bash
git clone [Repository URL]
cd S-VISION
python setup.py        # Installs OS-aware dependencies
python main.py
Requirements
OS: Windows 10/11, macOS, or Linux (X11 recommended; Wayland disables UI control).

Python: 3.11, 3.12, or 3.13.

Hardware: Microphone and Speakers. No GPU required (Avatar, HUD, Whisper, and Piper all run optimally on CPU).

Dependencies: yt-dlp installed via setup for HUD video playback.

Optional: Wake word engine (openwakeword), local STT (faster-whisper), local TTS (piper-tts) — all downloaded via one-click inside the UI.

🔑 Models & API Keys Specification
Supported Models & Engines
Primary Live Engine: Runs natively on Gemini 3.1 Flash Live, delivering ultra-low latency and roughly 2× faster time-to-first-word. The Live model uses a two-rung ladder (current and previous) and only steps down on quota exhaustion or loss of access, never on network blips.

Local & Third-Party LLMs: Supports local execution (Ollama, LM Studio, llama.cpp, vLLM) and hosted APIs (OpenAI, Groq, DeepSeek, Mistral, xAI, OpenRouter, Together) via the /v1/chat/completions protocol.

Reasoning Models: For models like qwen3, deepseek-r1, and their distills, S-VISION filters out <think>...</think> blocks directly on the stream so the assistant does not read its internal reasoning aloud.

Gemini Model Ladder: For background tasks and one-shot text calls, a 9-rung measured fallback ladder is used to prevent hangs if a model fails:

gemini-3.5-flash-lite (0.56s)

gemini-3.1-flash-lite (0.60s)

gemini-flash-lite-latest (0.60s)

gemini-2.5-flash (0.67s)

gemini-2.5-flash-lite (0.74s)

gemini-3.5-flash (1.13s)

gemini-3-flash-preview

gemini-3.6-flash

gemini-flash-latestCooldowns apply: Quota exhausted (429) rests for 5 minutes; No answer (503/504) rests for 30 minutes; Not found/No access (404) rests for 6 hours.

Speech-to-Text (STT): Local hearing is powered by Whisper (faster-whisper) running on the CPU. The first-turn warm-up delay (8.9s) was eliminated by running a throwaway recognition on startup, reducing first-turn latency to 1.16s. It also detects the spoken language to route the TTS voice correctly.

Text-to-Speech (TTS):

Piper: The default local neural voice. Operates fully offline, synthesizing 5.15s of speech in 0.34s (15× faster than real-time) on a CPU. Supports 176 voices across 52 languages. Downloads only once per voice (~63 MB).

System Voices: Windows SAPI, macOS say, Linux espeak-ng.

ElevenLabs: Premium streamed voices requiring an active API key and account.

Dynamic Tool Budgeting: A full LLM like Gemini receives all 56,148 characters of tool declarations. A local, smaller model receives a strict budget (e.g., 12 tools, 11,615 characters) utilizing a brief description to prevent JSON parsing failures and context overflow.

API Keys, Credentials & Security
Gemini API Key: A free Gemini API key is required to use the default Gemini Live engine. If a purely local STT/LLM/TTS stack is chosen, no API keys or accounts are required.

Storage Location: All keys, provider credentials, and plugin tokens are stored in config/api_keys.json in plaintext.

Security Protocol: config/api_keys.json and config/certs/ (which holds self-signed TLS certificates for the dashboard) are strictly excluded from version control via .gitignore.

Data Leak Mitigation: If the api_keys.json file is ever accidentally committed to a public repository, the user must immediately revoke the Gemini key at Google AI Studio and generate a new one, as deleting the file in a subsequent commit does not remove it from git history.

Dashboard Security: The remote phone dashboard operates via local HTTP by default (HTTPS is opt-in) utilizing a pairing key secured by PBKDF2 at 200,000 rounds of hashing (80 ms cost). It includes rate-limiting (five-minute lockout after six wrong attempts), token expiration, and a verified "Revoke all devices" kill switch.

🗂️ Project Structure
main.py: Core loop — Live session, audio I/O, viseme extraction, tool dispatch.

ui.py: PyQt6 HUD — avatar canvas, waveform, log panel, camera feed.

setup.py: OS-aware installer.

providers/: Architecture for local LLMs, STT, and TTS endpoints. Includes tts_piper.py, stt_whisper.py, and llm_openai.py.

plugins/: Community/optional skills (WhatsApp, Telegram, Screen Agent, Gmail, Code Helper, 3D Printers, Calorie Counter). Loads lazily on first use.

actions/: 12 Bundled OS skills (Web search, System Monitor, Computer Settings, File Controller).

memory/: long_term.json (persistent store) and config_manager.py.

dashboard/: FastAPI server and static pages for remote phone control.

core/: Core internal logics (gemini.py for one-shot calls, undo.py, avatar_mesh.py, platform_support.py).

config/: api_keys.json and certs/ (created on first launch, strictly git-ignored).