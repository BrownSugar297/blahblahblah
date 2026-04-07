# 🧠 Corrective RAG (CRAG)
### Advanced Retrieval-Augmented Generation with Self-Correction

A production-inspired implementation of **Corrective Retrieval-Augmented Generation (CRAG)** using modern LLM tooling. This project demonstrates how to build **self-evaluating, adaptive RAG systems** that mitigate hallucinations and handle retrieval failures gracefully.

---

## 📌 What is CRAG?

Traditional RAG systems blindly trust retrieved documents, which often leads to hallucinations if the source material is irrelevant or outdated. 

**CRAG (Corrective RAG)** introduces an intelligent validation step:
> *"Are these retrieved documents actually useful for the user's query?"*

If the retrieved context is deemed irrelevant, the system dynamically switches to **web search** (via Tavily), ensuring the LLM always has high-quality data before generating an answer.

---

## 🔄 System Workflow

```mermaid
graph TD
    A[User Query] --> B[Retrieve Documents]
    B --> C{Grade Relevance}
    C -- Relevant --> D[Generate Answer]
    C -- Irrelevant --> E[Tavily Web Search]
    E --> D
    D --> F[Self-Critique]
    F --> G[Final Refined Answer]
🚀 Key Features✅ LLM-based Document Grading: Uses a specialized grader prompt to evaluate document relevance.🌐 Automatic Fallback: Seamless integration with Tavily Web Search when local vector data is insufficient.🔍 Self-Critique Mechanism: A secondary LLM pass to review the draft for accuracy and tone.🔄 Dual Implementation: * LangChain: For a clean, sequential pipeline.LangGraph: For stateful, modular, and scalable architecture.📁 Project StructurePlaintext.
├── crag_langchain.py    # Sequential pipeline version
├── crag_langgraph.py    # Stateful graph-based version
├── vectorstore.py       # Shared Chroma DB & Gemini Embedding logic
├── .env                 # API keys (Groq, Google, Tavily)
└── README.md            # Project documentation
⚙️ Installation & Setup1. Clone & InstallBashgit clone [https://github.com/your-username/corrective-rag.git](https://github.com/your-username/corrective-rag.git)
cd corrective-rag
pip install langchain langgraph langchain-groq langchain-google-genai chromadb tavily-python python-dotenv
2. Environment SetupCreate a .env file in the root directory:Code snippetGROQ_API_KEY=your_groq_api_key
GOOGLE_API_KEY=your_google_api_key
TAVILY_API_KEY=your_tavily_api_key
3. Initialize Vector StoreThe first run of vectorstore.py will ingest Wikipedia data, generate Gemini Embeddings, and store them in a local Chroma DB.Bashpython vectorstore.py
🛠️ Tech StackComponentTechnologyLLMGroq (LLaMA 3.3)EmbeddingsGoogle GeminiVector StoreChroma DBSearch EngineTavily APIOrchestrationLangChain & LangGraph⚖️ LangChain vs. LangGraphFeatureLangChain (Pipeline)LangGraph (Graph)StructureLinear/SequentialCyclic & State-AwareLogicFixed FlowConditional RoutingScalabilityGood for PrototypesBuilt for Production AgentsState ManagementFunctional PassingCentralized State Schema👨‍💻 AuthorAshikur Rahman AI Engineer & Researcher Specializing in Agentic RAG, Explainable AI (XAI), and Time-Series Forecasting.📜 LicenseThis project is open-source and available under the MIT License.
