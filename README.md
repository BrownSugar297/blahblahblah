# 🧠 Corrective RAG (CRAG)  
### Advanced Retrieval-Augmented Generation with Self-Correction

A production-inspired implementation of **Corrective Retrieval-Augmented Generation (CRAG)** using modern LLM tooling.

This project demonstrates how to build **self-evaluating, adaptive RAG systems** using:

- ⚡ Groq LLM (LLaMA 3.3)
- 🔍 Tavily Web Search (fallback retrieval)
- 🧠 Gemini Embeddings
- 🗂️ Chroma Vector Database
- 🔗 LangChain (pipeline orchestration)
- 🧩 LangGraph (stateful graph execution)

---

## 📌 What is CRAG?

Traditional RAG systems blindly trust retrieved documents.

**CRAG (Corrective RAG)** introduces an intelligent validation step:

> _“Are these retrieved documents actually useful?”_

If not, the system dynamically switches to **web search**, improving answer quality.

---

## 🔄 System Workflow


Retrieve → Grade → (DB or Web)
↓
Generate
↓
Critique
↓
Final Answer


---

## 🚀 Key Features

- ✅ LLM-based **document relevance grading**
- 🌐 **Automatic fallback** to web search (Tavily)
- 🔍 Built-in **self-critique mechanism**
- ✨ Multi-step **answer refinement**
- 🔄 Dual implementation:
  - LangChain (simple pipeline)
  - LangGraph (scalable architecture)

---

## 📁 Project Structure


.
├── crag_langchain.py # LangChain pipeline version
├── crag_langgraph.py # LangGraph graph-based version
├── vectorstore.py # Shared Chroma vector DB builder
├── .env # API keys
└── README.md


---

## 🔑 Environment Setup

Create a `.env` file in the root directory:


GROQ_API_KEY=your_groq_api_key
GOOGLE_API_KEY=your_google_api_key
TAVILY_API_KEY=your_tavily_api_key


---

## ⚙️ Installation

```bash
pip install -r requirements.txt
📦 Required Libraries
langchain
langgraph
langchain-groq
langchain-google-genai
chromadb
tavily-python
python-dotenv
🧠 Vector Store (vectorstore.py)
Loads data from Wikipedia (Artificial Intelligence article)
Splits into semantic chunks
Generates embeddings using Gemini
Stores vectors in Chroma DB
⏱ First Run
Takes ~3 minutes (embedding batches)
⚡ Subsequent Runs
Loads instantly from disk
🔹 Version 1 — LangChain (Pipeline)

📄 crag_langchain.py

Flow:
Retrieve documents
Grade relevance (LLM)
Choose:
Use DB (if relevant)
Use Web Search (if not)
Generate answer
Critique answer
Rewrite final answer
▶️ Run
python crag_langchain.py
🔹 Version 2 — LangGraph (Graph-Based)

📄 crag_langgraph.py

🧩 Graph Architecture
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
Node-based modular design
Shared state across steps
Conditional routing
Production scalability
▶️ Run
python crag_langgraph.py
⚖️ LangChain vs LangGraph
Feature	LangChain	LangGraph
Structure	Sequential	Graph-based
Logic	Linear	Conditional routing
Complexity	Simple	Scalable
Use Case	Learning	Production systems
🧪 Example Query
query = "What are the main applications of artificial intelligence?"
💡 Output Includes:
Initial Answer
Self-Critique
Improved Final Answer
🧠 Core Insight
if grade == "relevant":
    use_vector_db()
else:
    use_web_search()

👉 This decision-making step is what transforms basic RAG into Corrective RAG (CRAG).

🔍 Tech Stack
Component	Technology
LLM	Groq (LLaMA 3.3)
Embeddings	Gemini
Vector Store	Chroma DB
Retrieval	Tavily API
Orchestration	LangChain
Execution Flow	LangGraph
📈 Future Improvements
🧠 Add conversational memory
🔁 Multi-query retrieval
📊 Re-ranking models
🌐 Streamlit UI
📚 Multi-document ingestion
👨‍💻 Author

Ashikur Rahman Ashik
AI / ML Enthusiast

Focus Areas:
Retrieval-Augmented Generation (RAG)
LLM Systems
Explainable AI
⭐ Final Thoughts

This project demonstrates:

✔ Retrieval + Reasoning
✔ Self-evaluation
✔ Dynamic decision-making

A strong step toward building production-grade AI systems 🚀

📜 License

This project is open-source and available under the MIT License.


---

## 🔥 Extra (Important Advice)

This README is now **portfolio-level**. To make it even stronger:

- Add a **demo GIF / screen recording**
- Add **architecture diagram (draw.io)**
- Deploy with **Streamlit or FastAPI**
- Add **GitHub badges (stars, license, python version)**

---

If you want next step, I can:
✅ Create **architecture diagram (very important for recruiters)**  
✅ Add **Streamlit UI code**  
✅ Optimize your repo to look like **top AI engineer GitHub profile**
