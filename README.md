# ExamForge — AI Question Paper Generator

Generates MCQs, Short, Long, and Quiz questions from any subject + topic using Gemini AI.

## Project Structure

```
question-paper-gen/
├── app.py            ← Flask backend (API + server)
├── index.html        ← Frontend (HTML + CSS + JS)
├── requirements.txt  ← Python packages
└── README.md
```

## Setup

### Step 1 — Get Gemini API Key (FREE)
Visit: https://aistudio.google.com/app/apikey
Click "Create API Key" → Copy it

### Step 2 — Install dependencies
```bash
pip install -r requirements.txt
```

### Step 3 — Set your API key
Option A — Edit app.py directly (line 17):
```python
GEMINI_API_KEY = "paste_your_key_here"
```

Option B — Environment variable:
```bash
# Windows
set GEMINI_API_KEY=your_key_here

# Mac/Linux
export GEMINI_API_KEY=your_key_here
```

### Step 4 — Run
```bash
python app.py
```

### Step 5 — Open browser
http://localhost:5000

---

## Architecture (for Viva)

```
User fills form (Subject, Topic, Difficulty, Types, Count)
           ↓
     Frontend (HTML/CSS/JS)
     fetch POST /generate
           ↓
     Backend (Flask/Python)
     build_prompt() → structured JSON prompt
           ↓
     Gemini 1.5 Flash API
     Returns JSON with questions
           ↓
     Frontend renders sections
     (MCQ / Short / Long / Quiz)
```

## API Endpoint

**POST** `/generate`

Request body:
```json
{
  "subject": "DBMS",
  "topic": "Normalization",
  "difficulty": "medium",
  "types": ["mcq", "short", "long"],
  "num": 5
}
```

Response:
```json
{
  "mcq": [
    {
      "question": "What is 1NF?",
      "options": ["A) ...", "B) ...", "C) ...", "D) ..."],
      "answer": "A) ..."
    }
  ],
  "short": ["Define normalization.", "..."],
  "long":  ["Explain all normal forms with examples.", "..."]
}
```

## Features
- MCQs with 4 options + correct answer shown
- Short answer questions (2-4 marks)
- Long answer questions (8-10 marks)  
- Quiz mode (rapid fire Q&A)
- Difficulty: Easy / Medium / Hard
- 1-15 questions per section
- Copy, Print, Download (.txt)
