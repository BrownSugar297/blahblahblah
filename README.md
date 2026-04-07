🧠 Corrective RAG (CRAG) — LangChain & LangGraph Implementation

A complete implementation of Corrective Retrieval-Augmented Generation (CRAG) using:

⚡ Groq LLM (LLaMA 3.3)
🔍 Tavily Web Search (fallback)
🧠 Gemini Embeddings
🗂️ Chroma Vector Database
🔗 LangChain (pipeline)
🧩 LangGraph (graph-based execution)
📌 What is CRAG?

CRAG (Corrective RAG) improves traditional RAG by adding a self-evaluation step:

Instead of blindly trusting retrieved documents, CRAG asks:
"Are these documents actually useful?"

🔄 Workflow
Retrieve → Grade → (DB or Web)
           ↓
        Generate → Critique → Final Answer
🚀 Key Features
✅ Intelligent document validation (LLM-based grading)
🌐 Automatic fallback to web search
🔍 Self-critique mechanism
✨ Improved final answers (multi-step refinement)
🔄 Two implementations:
LangChain (simple pipeline)
LangGraph (production-ready graph)
📁 Project Structure
.
├── crag_langchain.py    # Simple pipeline version
├── crag_langgraph.py    # Graph-based version
├── vectorstore.py       # Shared Chroma DB builder
├── .env                 # API keys
└── README.md
🔑 Environment Setup

Create a .env file:

GROQ_API_KEY=your_key_here
GOOGLE_API_KEY=your_key_here
TAVILY_API_KEY=your_key_here
⚙️ Installation
pip install -r requirements.txt
Required Libraries
langchain
langgraph
langchain-groq
langchain-google-genai
chromadb
tavily-python
python-dotenv
🧠 Vector Store (vectorstore.py)
Loads data from Wikipedia (AI article)
Splits into chunks
Converts into embeddings using Gemini
Stores in Chroma DB
🔁 First Run:
Takes ~3 minutes (batch embedding)
⚡ Later Runs:
Loads instantly from disk
🔹 Version 1 — LangChain

📄 crag_langchain.py

Flow:
Retrieve documents
Grade relevance (LLM)
Choose:
DB (if relevant)
Web search (if not)
Generate answer
Critique answer
Rewrite final answer
▶️ Run
python crag_langchain.py
🔹 Version 2 — LangGraph

📄 crag_langgraph.py

🧩 Graph Structure
START
  ↓
retrieve
  ↓
grade
  ├── relevant → use_db
  └── irrelevant → web_search
         ↓
      generate
         ↓
      critique
         ↓
   final_answer
         ↓
        END
🧠 Why LangGraph?
Each step = Node
Shared State
Conditional routing
Scalable for production
▶️ Run
python crag_langgraph.py
⚖️ LangChain vs LangGraph
Feature	LangChain	LangGraph
Structure	Single function	Node-based graph
Logic	Sequential	Conditional routing
Complexity	Simple	Scalable
Use Case	Learning	Production systems
🧪 Example Query
query = "What are the main applications of artificial intelligence?"
💡 Output
Initial answer
Self critique
Improved final answer
🧠 Core Idea (Most Important)
if grade == "relevant":
    use_vector_db()
else:
    use_web_search()

👉 This decision-making step is what makes CRAG powerful.

🔍 Technologies Used
Groq LLM — ultra-fast inference
Gemini Embeddings — semantic search
Chroma DB — vector storage
Tavily API — real-time search
LangChain — pipeline abstraction
LangGraph — stateful graph execution
📈 Future Improvements
Add memory (chat history)
Multi-query retrieval
Re-ranking models
UI with Streamlit
Support multiple documents
👨‍💻 Author

Ashikur Rahman Ashik

AI / ML Enthusiast
Focus: RAG, LLM Systems, Explainable AI
⭐ Final Note

This project demonstrates:

✔ Retrieval + Reasoning
✔ Self-evaluation
✔ Dynamic decision making

A strong step toward production-grade AI systems 🚀
