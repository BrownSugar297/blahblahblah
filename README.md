
# Corrective RAG (CRAG) Project

## Project Structure

```
CRAG/
│
├── .env                  ← your API keys (fill this in)
├── requirements.txt      ← install dependencies
├── vectorstore.py        ← builds/loads the shared Chroma DB
├── crag_langchain.py     ← CRAG using plain LangChain
└── crag_langgraph.py     ← CRAG using LangGraph (with graph nodes)
```

---

## Setup

### 1. Fill in your API keys in `.env`
```
GROQ_API_KEY=your_groq_key_here
GOOGLE_API_KEY=your_google_key_here
TAVILY_API_KEY=your_tavily_key_here
USER_AGENT=crag-app/1.0
```

Get free keys from:
- Groq   → https://console.groq.com
- Google → https://aistudio.google.com
- Tavily → https://tavily.com

### 2. Create virtual environment
```bash
python -m venv .venv
.venv\Scripts\activate        # Windows
source .venv/bin/activate     # Mac/Linux
```

### 3. Install dependencies
```bash
pip install -r requirements.txt
```

### 4. Run
```bash
python crag_langchain.py    # plain LangChain version
python crag_langgraph.py    # LangGraph version
```

---

## How CRAG works

```
Basic RAG:   retrieve → generate
CRAG:        retrieve → GRADE → generate (if good docs)
                              → web search (if bad docs)
                      → critique → final answer
```

The **grade** step is what makes CRAG different.
Instead of blindly using whatever docs are retrieved,
it checks if they are actually useful first.

---

## Notes

- The `chroma_db/` folder is created automatically on first run
- First run takes a few minutes (embedding Wikipedia article)
- Every run after that loads the DB instantly
- Both scripts share the same DB (no double embedding)

