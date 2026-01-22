# Personalized Study Planner: Adaptive RAG System

[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/)
[![LangChain](https://img.shields.io/badge/Framework-LangChain-green.svg)](https://python.langchain.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A high-fidelity **Retrieval-Augmented Generation (RAG)** system designed to transform dense university materials (PDFs and PPTXs) into structured, time-aware study schedules. This system features an **Adaptive Inference** mechanism that optimizes performance based on available hardware.


---

## 🚀 Key Features

* **Multimodal Data Ingestion:** Automated text extraction and cleaning from university lecture slides (PPTX) and textbooks (PDF).
* **Dual-Retriever Strategy:** * **Primary:** `BAAI/bge-base-en-v1.5` for high-precision semantic retrieval.
    * **Baseline:** `all-MiniLM-L6-v2` for efficient benchmarking.
* **Adaptive Inference Mechanism:** Hardware-aware switching logic:
    * **GPU Mode:** Deploys **Zephyr-7B** (4-bit quantized) for complex planning and reasoning.
    * **CPU Mode:** Deploys **Qwen-1.5B** for rapid, low-resource summarization.
* **Zero-Hallucination Guarantee:** Uses strict **ChatML** prompt engineering to ensure the model only references the provided context, achieving a 0.0% hallucination rate.

---

## 📂 Repository Structure

```text
├── notebooks
  ├── 01_Preprocessing.ipynb         # Data extraction from PDFs/PPTXs and cleaning
  ├── 02_Vector_Store_Creation.ipynb # Chunking strategy and ChromaDB indexing
  ├── 03_RAG_Generation.ipynb        # Core RAG pipeline and adaptive LLM logic
  ├── 04_Evaluation_Study.ipynb       # Quantitative metrics and LaTeX report generation
├── Prompts.txt                    # Log of optimized ChatML and system prompts
├── Report.pdf                     # Final technical research paper
├── Proposal_GenAI.pdf             # Initial project scope and methodology

## ⚙️ Installation & Setup
### 1. Prerequisites
Google Colab is recommended (T4 GPU for optimal performance).
A folder named GenAiProject_Dataset in your Google Drive containing your .pdf and .pptx files.

### 2. Install Dependencies

pip install -q langchain langchain-community chromadb \
  sentence-transformers pypdf python-pptx \
  accelerate bitsandbytes transformers

### 🛠️ Technical WorkflowIngestion:
      Parses textbooks and lecture slides, preserving semantic structure while removing noise.Indexing: Utilizes RecursiveCharacterTextSplitter to chunk text and stores embeddings in a Chroma vector database.Generation: Retrieves the top-$k$ relevant chunks and uses a structured prompt to generate a plan including daily breakdowns, specific page/slide citations, and estimated time blocks.

### 📊 Performance Metrics

Metric	System Result
Source Grounding	100%
Hallucination Rate	0.00%
Avg. Citations per Plan	25
Time References per Plan	43
Inference Mode	Adaptive (GPU/CPU)

## 🎯 Conclusion
By anchoring the generation in specific course documents, this system provides students with a reliable, structured, and cited roadmap for their studies, eliminating the "ungrounded information" problem common in generic LLMs.

