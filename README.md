# AI Interview System

Autonomous mock interview between an AI Interviewer (Alex) and an AI Candidate (built from a resume).

## 🎯 What It Does

Two AI agents have a realistic interview:
- **Alex (Interviewer)** — skeptical senior engineer who grills the candidate
- **Candidate** — an AI persona generated from your resume

Both speak with natural voices, real pauses, thinking sounds, filler words, and **content-based interruptions**.

## ✨ Features

- 📄 **Resume parsing** via Groq LLM (extracts name, skills, projects, experience)
- 🎙️ **Chunked TTS** with per-sentence emotion tags (each sentence gets its own tone)
- ⚡ **Natural interruptions** — interviewer cuts off candidate when specific trigger phrases appear
- ⏸️ **Realistic pauses** — thinking sounds, hesitation, self-corrections
- 🎭 **Emotion mapping** — 10 emotions (warm, skeptical, impressed, thoughtful, nervous, etc.)
- 📊 **JSON transcript** — full conversation logged with per-chunk emotions
- 🔄 **Dual voice engines** — Edge TTS for interviewer, Fish Audio for candidate

## 🛠️ Tech Stack

| Component | Tool |
|---|---|
| LLM | Groq (`openai/gpt-oss-120b`) |
| Interviewer Voice | Microsoft Edge TTS |
| Candidate Voice | Fish Audio (voice cloning) |
| Audio Playback | pygame |
| PDF Parsing | pypdf |

## 📋 Requirements

- Python 3.10+
- Linux (tested on Ubuntu/XFCE)
- Working microphone/speakers
- API keys: Groq + Fish Audio

## 🚀 Setup

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/ai-interview-system.git
cd ai-interview-system
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Create `.env` file

```bash
nano .env
```

Add your API keys:

```
GROQ_API_KEY=your_groq_key_here
FISH_API_KEY=your_fish_key_here
FISH_VOICE_ID=your_voice_id_here
FISH_MODEL=s2.1-pro-free
```

### 4. Place your resume

```bash
cp /path/to/your/resume.pdf ./resume.pdf
```

### 5. Run

```bash
python3 phase_10.py
```

## ⚙️ Configuration

Key settings in `phase_10.py`:

| Setting | Default | Description |
|---|---|---|
| `MAX_TURNS` | 12 | Total interview turns |
| `INTERRUPTION_MAX` | 2 | Max interruptions per interview |
| `INTERRUPTION_COOLDOWN` | 3 | Min turns between interruptions |
| `FORCED_DSA_TURNS` | [7, 8] | Turns where DSA question is forced |
| `CHUNK_MAX_WORDS` | 45 | Max words per audio chunk |

## 📂 Project Structure

```
.
├── phase_10.py              # Main interview engine
├── resume.pdf               # Your resume (NOT in git)
├── .env                     # API keys (NOT in git)
├── .gitignore               # Git ignore rules
├── requirements.txt         # Python dependencies
├── opener_cache/            # Pre-generated interruption openers (auto-created)
└── interview_transcript.json # Auto-generated transcript (NOT in git)
```

## 🎬 How It Works

1. **Resume parsed** → extracted into name, skills, projects, experience
2. **Two system prompts** built → one for interviewer, one for candidate
3. **Loop begins** → interviewer asks question → candidate answers → repeat
4. **Each answer** split into chunks, each chunk gets its own emotion + TTS
5. **Interruptions** triggered by content (e.g., candidate says "from scratch" → Alex interrupts)
6. **Wrap-up** at turns 11-12 (summary + closing)
7. **Transcript** saved as JSON at the end

## 🐛 Known Issues

- Groq free tier has 200K tokens/day limit
- Fish Audio free tier has rate limits
- Requires Linux (ALSA for audio)
- `en-IN-NeerjaExpressiveNeural` voice needed for interviewer

## 🤝 Contributing

Pull requests welcome. For major changes, open an issue first.

## 👤 Author

**Tushar Singh**

