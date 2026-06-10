# Cognify — RAG-Powered Knowledge Assistant 🤖

A locally-running Retrieval-Augmented Generation (RAG) chatbot that lets you upload PDF documents and chat with them intelligently — entirely on your own machine, with no data sent to external APIs.


Built on an open-source stack: **LLaMA 3.2** (via Ollama) · **BGE Embeddings** (HuggingFace) · **Qdrant** (Docker) · **Streamlit**

---

## How It Works

1. **Upload** a PDF document through the Streamlit UI
2. **Embed** — the document is chunked and stored as vectors in a local Qdrant database
3. **Chat** — ask questions; the app retrieves relevant chunks and passes them to LLaMA 3.2 for a grounded, context-aware answer

---

## Features

- 📂 **PDF Upload & Preview** — drag-and-drop upload with inline PDF rendering
- 🧠 **Local Embeddings** — uses `BAAI/bge-small-en` via HuggingFace (no API key needed)
- 🗄️ **Vector Storage** — Qdrant running in Docker for fast semantic retrieval
- 🦙 **Local LLM** — LLaMA 3.2 3B served via Ollama (fully offline)
- 💬 **Chat Interface** — multi-turn conversation with session history
- 🛡️ **Privacy-First** — all processing happens locally; no data leaves your machine

---

## Tech Stack

| Component | Technology |
|---|---|
| UI Framework | [Streamlit](https://streamlit.io/) |
| LLM | [LLaMA 3.2 via Ollama](https://ollama.com/) |
| Embeddings | [BAAI/bge-small-en (HuggingFace)](https://huggingface.co/BAAI/bge-small-en) |
| Vector Store | [Qdrant](https://qdrant.tech/) (Docker) |
| Orchestration | [LangChain](https://python.langchain.com/) |
| PDF Parsing | [Unstructured](https://github.com/Unstructured-IO/unstructured) |

---

## Project Structure

```
RAG-Based-LLM-Chatbot/
├── new.py              # Main Streamlit app (entry point)
├── chatbot.py          # ChatbotManager — LLM + retrieval chain
├── vectors.py          # EmbeddingsManager — PDF processing + Qdrant storage
├── requirements.txt    # Python dependencies
└── sct.png             # App screenshot
```

---

## Prerequisites

Make sure the following are installed before running the app:

- **Python 3.10+**
- **Docker** — to run Qdrant
- **Ollama** — to run LLaMA 3.2 locally

---

## Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/GURPREETKAURJETHRA/RAG-Based-LLM-Chatbot.git
cd RAG-Based-LLM-Chatbot
```

### 2. Start Qdrant (Docker)

```bash
docker pull qdrant/qdrant
docker run -p 6333:6333 qdrant/qdrant
```

Qdrant will be available at `http://localhost:6333`.

### 3. Pull the LLM (Ollama)

```bash
ollama pull llama3.2:3b
```

### 4. Set Up a Python Environment

**Option A — venv:**
```bash
# macOS / Linux
python3 -m venv venv
source venv/bin/activate

# Windows
python -m venv venv
venv\Scripts\activate
```

**Option B — Conda:**
```bash
conda create --name rag-chatbot python=3.10
conda activate rag-chatbot
```

### 5. Install Dependencies

```bash
pip install -r requirements.txt
```

### 6. Run the App

```bash
streamlit run new.py
```

The app opens automatically at `http://localhost:8501`.

---

## Usage

1. Navigate to **🤖 Chatbot** in the sidebar
2. Upload a PDF in the left column
3. Check **✅ Create Embeddings** in the middle column and wait for confirmation
4. Start asking questions in the **💬 Chat with Document** column on the right

---

## Configuration

Default settings (editable in `new.py`, `chatbot.py`, and `vectors.py`):

| Parameter | Default | Description |
|---|---|---|
| Embedding model | `BAAI/bge-small-en` | HuggingFace BGE model |
| LLM model | `llama3.2:3b` | Ollama model name |
| LLM temperature | `0.7` | Response creativity (0 = deterministic) |
| Qdrant URL | `http://localhost:6333` | Local Qdrant instance |
| Collection name | `vector_db` | Qdrant collection |
| Chunk size | `1000` | Characters per document chunk |
| Chunk overlap | `250` | Overlap between chunks |
| Top-k retrieval | `1` | Number of chunks retrieved per query |

---

## Dependencies

```
streamlit
langchain
langchain_community
langchain_core
langchain-huggingface
langchain-qdrant
langchain-ollama
unstructured[pdf]
onnx==1.16.1
qdrant-client
python-dotenv
```

---

## Contributing

Contributions are welcome! To get started:

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/your-feature`
3. Commit your changes: `git commit -m "Add your feature"`
4. Push to your fork: `git push origin feature/your-feature`
5. Open a Pull Request

Please open an issue first for major changes.

---

## Useful Links

- [Streamlit Docs](https://docs.streamlit.io/)
- [LangChain Docs](https://python.langchain.com/)
- [Qdrant Docs](https://qdrant.tech/documentation/)
- [Ollama Models](https://ollama.com/library)

---
---

*If you found this project helpful, drop a ⭐ on the repo!*
