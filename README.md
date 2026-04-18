# 🚀 The AI Strategist

> A Multi-Agent AI System for Personalized Hackathon Strategy Planning

Built by **Himanshu Kamishetti** — Python Developer | ML & Data Science Enthusiast

[![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.100+-green.svg)](https://fastapi.tiangolo.com/)
[![Streamlit](https://img.shields.io/badge/Streamlit-1.28+-red.svg)](https://streamlit.io/)
[![CrewAI](https://img.shields.io/badge/CrewAI-Latest-purple.svg)](https://www.crewai.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## 📖 Overview

**The AI Strategist** transforms raw hackathon ideas into tailored, executable strategies using a pipeline of specialized AI agents. Given your team's strengths and the hackathon duration, it performs real-time market research, identifies risks, designs an MVP architecture, and crafts a winning 3-minute pitch — all automatically.

```
Your Idea + Team Type + Time → Personalized Hackathon Strategy
```

---

## ✨ Features

- **🔍 Market Research Agent** — Competitor analysis, market gaps, and tech stack recommendations tailored to your team
- **⚠️ Critical Risk Agent** — Scope creep detection, demo failure prediction, and mitigation strategies
- **🏗️ Solution Architect Agent** — 6-dimensional MVP design (Problem → Innovation → Audience → Feasibility → Wow Factor → Differentiation)
- **🎯 Pitch Strategy Agent** — Full 3-minute pitch script with demo choreography and Q&A prep
- **👥 Team-Aware Personalization** — Strategies adapt for Frontend, Backend, AI/ML, and Full-Stack teams
- **⏱️ Duration-Aware Planning** — Time budgets and feature scoping based on hackathon length (1–168 hours)
- **⚡ Dual LLM Architecture** — Ollama (local) for research/analysis + Groq (cloud) for architecture/pitch generation

---

## 🏗️ Project Structure

```
AI-Strategist/
├── backend/
│   ├── agents/
│   │   ├── __init__.py
│   │   ├── architect_agent.py      # MVP architecture design agent
│   │   ├── critical_agent.py       # Risk assessment agent
│   │   ├── pitch_agent.py          # Pitch strategy agent
│   │   └── research_agent.py       # Market research agent
│   ├── __init__.py
│   ├── api.py                      # FastAPI backend server
│   ├── orchestrator.py             # Workflow orchestration logic
│   └── tasks.py                    # CrewAI task definitions
├── frontend/
│   └── app.py                      # Streamlit UI
├── test.py                         # General tests
├── test_groq.py                    # Groq API connection test
├── test_serper.py                  # Serper API connection test
├── .gitignore
├── LICENSE
├── README.md
└── requirements.txt
```

---

## ⚙️ Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Streamlit |
| Backend API | FastAPI + Uvicorn |
| Agent Framework | CrewAI |
| Local LLM | Ollama (Gemma 2B) |
| Cloud LLM | Groq (Gemma2 9B IT) |
| Web Search | Serper API |
| Language | Python 3.10+ |

---

## 🚀 Getting Started

### Prerequisites

- Python 3.10 or higher
- [Ollama](https://ollama.com/) installed and running locally
- Groq API key (optional, but recommended for speed)
- Serper API key (for web search in research/critical agents)

### 1. Clone the Repository

```bash
git clone https://github.com/Himanshukamishetti/AI-Straitegist.git
cd AI-Straitegist
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

### 3. Pull the Local LLM

```bash
ollama pull gemma:2b
ollama serve   # Start the Ollama server on port 8080
```

> **Note:** The orchestrator connects to Ollama at `http://localhost:8080`. Make sure it's running before starting the backend.

### 4. Set Up Environment Variables

Create a `.env` file in the project root:

```env
GROQ_API_KEY=your_groq_api_key_here
SERPER_API_KEY=your_serper_api_key_here
```

- Get a free Groq API key at [console.groq.com](https://console.groq.com)
- Get a Serper API key at [serper.dev](https://serper.dev)

> If `GROQ_API_KEY` is not set, all agents will fall back to the local Ollama model.

### 5. Start the Backend

```bash
python backend/api.py
```

The FastAPI server starts at `http://127.0.0.1:8000`. You can explore the API docs at `http://127.0.0.1:8000/docs`.

### 6. Start the Frontend

Open a new terminal:

```bash
streamlit run frontend/app.py
```

The Streamlit UI opens at `http://localhost:8501`.

---

## 🧪 Testing

```bash
# Test the full workflow
python test.py

# Test Groq API connection
python test_groq.py

# Test Serper API connection
python test_serper.py
```

---

## 🔌 API Reference

### `POST /generate-strategy`

Generate a personalized hackathon strategy.

**Request Body:**
```json
{
  "theme": "AI in Education",
  "idea": "An AI-powered app to help students learn new languages.",
  "team_strength": "AI/ML",
  "hackathon_duration": 24
}
```

| Field | Type | Description |
|---|---|---|
| `theme` | string | Hackathon theme or focus area |
| `idea` | string | Your raw project idea |
| `team_strength` | string | One of: `Frontend`, `Backend`, `AI/ML`, `Full-Stack` |
| `hackathon_duration` | integer | Duration in hours (1–168) |

**Response:**
```json
{
  "success": true,
  "research": "...",
  "critical_analysis": "...",
  "mvp_plan": "...",
  "pitch": "...",
  "team_strength": "AI/ML",
  "hackathon_duration": 24
}
```

### `GET /health`

Health check endpoint. Returns `{"status": "healthy"}`.

---

## 🤖 Agent Workflow

```
User Input
    │
    ▼
┌─────────────────────┐
│  Research Agent      │  ← Ollama (local)
│  Market + Competitors│
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│  Critical Agent      │  ← Ollama (local)
│  Risks + Mitigation  │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│  Architect Agent     │  ← Groq (cloud) ⚡
│  MVP Blueprint       │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│  Pitch Agent         │  ← Groq (cloud) ⚡
│  3-Min Pitch Script  │
└──────────┬──────────┘
           │
           ▼
    Strategy Output
```

---

## 🎛️ Team Strength Guide

| Team Type | Focus | Best For |
|---|---|---|
| **Frontend** | UI/UX, responsive design, visual appeal | Consumer apps, design-heavy projects |
| **Backend** | APIs, databases, server architecture | Data platforms, infrastructure tools |
| **AI/ML** | Models, data pipelines, intelligent features | Prediction, automation, NLP projects |
| **Full-Stack** | End-to-end integration, balanced features | Complete web applications |

---

## 📋 Requirements

Key dependencies (see `requirements.txt` for full list):

```
fastapi
uvicorn
streamlit
crewai
crewai-tools
langchain-community
python-dotenv
reportlab
requests
```

---

## 🐛 Troubleshooting

**Ollama connection error:**
Make sure Ollama is running: `ollama serve`

**Groq API errors:**
Verify your `GROQ_API_KEY` in `.env` is valid and has available quota.

**Serper search not working:**
Check your `SERPER_API_KEY`. Research and Critical agents require this for web search.

**Pitch agent returns empty output:**
This is a known extraction issue with some CrewAI versions. The orchestrator includes an automatic fallback pitch generator that activates when extraction fails.

**Port already in use:**
Change the port in `api.py`: `uvicorn.run(app, host="0.0.0.0", port=8001)`

---

## 🤝 Contributing

Contributions are welcome! Feel free to open issues or submit pull requests.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## 👨‍💻 Author

**Himanshu Kamishetti**  
Python Developer | Machine Learning & Data Science Enthusiast  
📍 Nagpur, Maharashtra  
📧 [himanshukamishetti@gmail.com](mailto:himanshukamishetti@gmail.com)  
🐙 [github.com/Himanshukamishetti](https://github.com/Himanshukamishetti)  
💼 [linkedin.com/in/himanshukamishetti](https://www.linkedin.com/in/himanshukamishetti/)

---

## 📄 License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

<div align="center">
  <p>🤖 Powered by Multi-Agent AI • Built for Hackathon Success</p>
  <p>⭐ Star this repo if you found it useful!</p>
</div>
