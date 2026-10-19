# AI-Powered Study Assistant - # ai-study-assistant
### Prototype RAG + multi-agent study assistant with source-cited answers using LangChain, CrewAI, ChromaDB and Groq

![Python](https://img.shields.io/badge/Python-3.12-blue)
![LangChain](https://img.shields.io/badge/LangChain-0.3.25-green)
![CrewAI](https://img.shields.io/badge/CrewAI-0.114.0-orange)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

## About This Project

This project is a prototype RAG and multi-agent system that answers questions about university
lecture materials and returns page-level source citations.

Real university lecture slides (344 pages, 7 PDFs) serve as the knowledge base. 
Questions can be asked in German or English – the system automatically translates 
queries for semantic search since the source documents are in German and English.

## Architecture

```mermaid
flowchart TD
    A[User Query DE/EN] --> B[Agent 1: Classifier\nclassifies topic, complexity & keywords]
    B --> C[classification result]
    C --> D[Agent 2: Solver]
    D <--> E[ChromaDB Vector Store\n412 chunks, k=5]
    D --> F[Answer in German]
```


## Tech Stack

| Component | Technology |
|---|---|
| LLM | Llama 4 (meta-llama/llama-4-scout-17b-16e-instruct) via Groq API |
| RAG Framework | LangChain 0.3.25 |
| Agent Framework | CrewAI 0.114.0 |
| Vector Database | ChromaDB 0.6.3 |
| Embeddings | HuggingFace – sentence-transformers/all-MiniLM-L6-v2 |
| Environment | Kaggle Notebook |

## Features

- **RAG Pipeline** – semantic search across 344 pages of lecture materials
- **Agent-to-Agent Communication** – Classifier passes results to Solver
- **Automatic Translation** – German queries are translated internally for 
  vector search (source PDFs are in English)
- **Interactive Widget UI** – chat interface directly inside the Kaggle Notebook
- **Source Citations** – every answer references the exact PDF page numbers

## Setup

### 1. Prerequisites
- Kaggle Account
- Groq API Key (free at [console.groq.com](https://console.groq.com))

### 2. Configure Kaggle Secrets
In Kaggle under **Add-ons → Secrets**:
GROQ_API_KEY = gsk_...


### 3. Upload your own PDFs
Upload PDF documents via **Add Data → Upload** and adjust the 
`base_path` variable in Cell 3.

### 4. Run the Notebook
Execute all cells in order. After Cell 6, the interactive chat 
interface appears.

## Notebook Structure

| Cell | Description |
|---|---|
| Cell 0 | Project documentation (Markdown) |
| Cell 1 | Install all dependencies |
| Cell 2 | API setup, LLM & embedding configuration |
| Cell 3 | Auto-detect PDF files |
| Cell 4 | Build RAG pipeline & vector database |
| Cell 5 | RAG test (single query) |
| Cell 6 | Multi-Agent UI (CrewAI + ipywidgets) |

## Enterprise ITSM Relevance

This project demonstrates the core architecture behind an AI-supported
IT service management assistant:

- RAG can replace manual searches through ITIL documentation and internal knowledge bases.
- The classifier agent can be adapted to categorize support tickets by topic and priority.
- The solver agent can generate first-level solution suggestions based on retrieved documentation.
- The same workflow could later be integrated into enterprise systems such as BMC Helix or container-based deployments.

This repository contains a standalone prototype. It is not connected to an
enterprise ITSM platform.
## License

MIT License – feel free to use and adapt.


