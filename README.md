# 🎓 IntelliTeach-AI — Round 2 Prototype (IIT Bombay Upskill India)

IntelliTeach-AI evaluates teaching videos and generates an objective scorecard across:

- Clarity  
- Engagement  
- Confidence  
- Technical Depth  
- Interaction Quality  

This Round-2 prototype demonstrates a complete end-to-end AI workflow using free-tier transcription and scoring models, a structured backend, and a functional frontend UI.

---

# 🚀 Features

- Upload a video (MP4)  
- Automatic transcription via AssemblyAI (Free Tier)  
- Scoring via Groq LLaMA (Free Tier)  
- JSON output with category scores, overall score, and improvement suggestions  
- Transcript preview  
- Streamlit frontend  
- FastAPI backend  
- Complete documentation in `/docs`  
- Hackathon-compliant folder structure  

---

# 🏗️ Architecture Overview

### Frontend — `src/frontend/app.py`
Streamlit interface for:
- Uploading video  
- Communicating with backend  
- Showing transcript + scores  

### Backend — `src/backend/main.py`
FastAPI backend with:
- `POST /analyze` endpoint  
- Temporary file handling  
- AI scoring pipeline connection  
- JSON output formatting  

### AI Pipeline — `src/ai/analyze.py`
Handles:
- AssemblyAI transcription  
- Groq LLaMA scoring  
- Weighted computation  
- Suggestion generation  

### Documentation — `/docs`
Includes:
- `architecture.md`  
- `technical_summary.md`  
- `IntelliTeach.pdf`  

---

# 📁 Folder Structure

```
IntelliTeach-AI/
│
├── src/
│   ├── backend/
│   │   └── main.py
│   ├── frontend/
│   │   └── app.py
│   ├── ai/
│   │   └── analyze.py
│   └── utils/
│
├── docs/
│   ├── architecture.md
│   ├── technical_summary.md
│   ├── IntelliTeach.pdf
│
├── models/
│   └── README.md
│
├── requirements.txt
├── README.md
└── .gitignore
```

---

# ⚙️ Setup Instructions

### 1️⃣ Install dependencies
```
pip install -r requirements.txt
```

### 2️⃣ Add API Keys (PowerShell)
```
setx ASSEMBLYAI_API_KEY "your-assemblyai-key"
setx GROQ_API_KEY "your-groq-key"
```

Restart PowerShell afterward.

### 3️⃣ Run the backend
```
python -m uvicorn src.backend.main:app --reload --port 8000
```

Health check URL:
http://localhost:8000/health

Expected output:
```
{"status": "ok", "message": "Free version running!"}
```

### 4️⃣ Run the frontend
```
streamlit run src/frontend/app.py
```

Upload a short MP4 to view transcript + scorecard.

---

# 🧪 API Documentation

### POST /analyze
Upload a video and receive JSON scoring output.

Example:
```
curl -X POST http://localhost:8000/analyze -F "file=@sample.mp4"
```

Response:
```json
{
  "ok": true,
  "result": {
    "clarity": 82,
    "engagement": 75,
    "confidence": 80,
    "technical": 70,
    "interaction": 65,
    "overall": 75.4,
    "suggestions": ["Improve pacing", "Increase use of examples"],
    "transcript": "Full transcript text here..."
  }
}
```

---

# 📦 Dependencies

- fastapi  
- uvicorn  
- python-multipart  
- requests  
- assemblyai  
- groq  
- streamlit  
- pydantic  

(Version details in `requirements.txt`.)

---
⚠️ Demo Notes & Limitations

Optimized for 30–60 second videos with clear speech
Silent or low-audio videos are handled via contextual fallback logic
Free-tier AI models are used for hackathon compliance
Backend is locally hosted for demo stability but is cloud-deployable

# 👥 Contributors

All contributors worked with equal responsibility across AI, backend, frontend, and documentation.

- **Charu Malik** — AI Pipeline • Backend Integration • Documentation  
- **Khushi Wadhwa** — Frontend Interface • User Workflow • Documentation  
- **Richa Singh** — Architecture Planning • Research • Quality Review  
