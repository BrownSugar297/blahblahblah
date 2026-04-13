
# RAGAS Learning Project — Google Gemini + ChromaDB

A simple RAG pipeline that **evaluates itself** using RAGAS metrics.
Uses **Google Gemini (free)** as the LLM and **ChromaDB (persistent)** as the vector store.

---

## What This Project Does

1. Loads a text document from `data/sample.txt`
2. Splits it into chunks and stores them in ChromaDB (saved to disk)
3. For each evaluation question, retrieves relevant chunks + generates an answer
4. Runs RAGAS to score the pipeline on 4 metrics
5. Prints a clean report

---

## Setup (3 steps)

### Step 1 — Get a free Google API key
Go to: https://aistudio.google.com/app/apikey
Click "Create API key" — it's free, no credit card needed.

### Step 2 — Add your key to `.env`
Open the `.env` file and replace the placeholder:
```
GOOGLE_API_KEY=your_actual_key_here
```

### Step 3 — Install and run
```bash
# Create virtual environment
python -m venv venv

# Activate it
source venv/bin/activate        # Mac/Linux
venv\Scripts\activate           # Windows

# Install dependencies
pip install -r requirements.txt

# Run the project
python main.py
```

---

## Usage

```bash
# Full run: build ChromaDB + evaluate
python main.py

# Force rebuild ChromaDB from scratch
python main.py --rebuild

# Interactive mode: ask your own questions
python main.py --query
```

---

## RAGAS Metrics Explained

| Metric | What it measures | Range |
|---|---|---|
| **Faithfulness** | Is the answer grounded in retrieved context? (no hallucination) | 0–1 |
| **Answer Relevancy** | Does the answer actually address the question? | 0–1 |
| **Context Precision** | Is the retrieved context relevant to the question? | 0–1 |
| **Context Recall** | Was all the needed information retrieved? | 0–1 |

Higher is better. Aim for 0.8+ on all metrics.

---

## Project Structure

```
ragas-gemini-project/
├── .env                  # Your API key (never commit this!)
├── requirements.txt      # Dependencies
├── main.py               # Entry point
├── README.md             # This file
├── data/
│   └── sample.txt        # Document to query (replace with your own!)
├── src/
│   ├── config.py         # Gemini LLM + embeddings setup
│   ├── rag.py            # RAG pipeline logic
│   └── evaluate.py       # RAGAS evaluation logic
└── chroma_db/            # Auto-created: persistent vector store
```

---

## Use Your Own Document

Replace `data/sample.txt` with any `.txt` file, then rebuild:
```bash
python main.py --rebuild
```

Also update the questions in `src/evaluate.py` → `EVAL_QUESTIONS` to match your document.

---

## Troubleshooting

**`GOOGLE_API_KEY not found`** — Make sure `.env` file has your key and no spaces around `=`

**`quota exceeded`** — Gemini free tier has rate limits. Wait a minute and retry.

**`chromadb error`** — Delete the `chroma_db/` folder and run again with `--rebuild`
