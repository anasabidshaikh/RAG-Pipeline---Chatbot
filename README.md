# 🤖 Production-Grade RAG Pipeline & AI Support Agent (n8n Workflow)

An enterprise-ready n8n automation pipeline featuring document ingestion from Google Drive, automatic chunking, local embeddings, vector storage in Pinecone, and an interactive RAG Chatbot Agent.

---

## 🚀 Architectural Overview

This system is built using two distinct sub-processes:

1. **Document Ingestion & Indexing Pipeline**: Automatically monitors a target Google Drive folder, parses incoming documents, generates vector embeddings locally using Ollama (`nomic-embed-text:latest`), and upserts vectors into a Pinecone Index (`rag-pipeline-and-chatbot` / Namespace: `FAQ`).
2. **Interactive RAG Chatbot Agent**: Receives user questions via chat triggers, dynamically executes semantic retrieval against Pinecone using function calling, and synthesizes accurate responses using an LLM (`qwen3-vl:235b-instruct`).

---

## 🛠️ Tech Stack & Node Configuration

### Ingestion Pipeline
- **Google Drive Trigger**: Polls target folder (`$vars.GDRIVE_TARGET_FOLDER_ID`) for new document uploads.
- **Download File Node**: Downloads binary content and converts Google Workspace formats automatically.
- **Data Loader & Text Splitter**: Custom binary loader paired with `Recursive Character Text Splitter`.
- **Embeddings**: Local Ollama execution using `nomic-embed-text:latest`.
- **Vector Database**: Pinecone Vector Store (`mode: "insert"`).

### Interactive Chatbot Pipeline
- **Chat Trigger**: Captures incoming chat session payloads.
- **AI Agent**: LangChain Agent executing retrieval-augmented generation.
- **Chat LLM**: Local Ollama execution using `qwen3-vl:235b-instruct`.
- **Retrieval Tool**: Pinecone Vector Store configured in `retrieve-as-tool` mode (`Tool Name: Policy_and_FAQ`).

---

## 📦 Project Structure

```text
├── .gitignore
├── LICENSE
├── README.md
├── docker-compose.yml
└── workflows/
    └── RAG-Pipeline-v1.json
