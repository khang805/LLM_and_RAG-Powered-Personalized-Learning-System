# Personalized Study Planner: Adaptive RAG System

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
```

## ⚙️ Installation & Setup
### 1. Prerequisites
Google Colab is recommended (T4 GPU for optimal performance).
A folder named GenAiProject_Dataset in your Google Drive containing your .pdf and .pptx files.

### 2. Install Dependencies

pip install -q langchain langchain-community chromadb \
  sentence-transformers pypdf python-pptx \
  accelerate bitsandbytes transformers

### 🛠️ Technical WorkflowIngestion:
     #### 1. Preprocessing & EmbeddingThe system ingests raw files from Google Drive, performs text cleaning, and utilizes the LangChain framework to split text into semantically meaningful chunks. These are then stored in a Chroma vector database.
     #### 2. Retrieval & Context InjectionUpon a user query (e.g., "Create a 5-day plan for Transformers"), the system retrieves the top-$k$ relevant snippets. The prompt engineering uses ChatML tokens to maintain strict role adherence.
     #### 3. Adaptive GenerationThe system detects the available hardware environment. If a T4 GPU is detected, it deploys Zephyr-7B with 4-bit quantization to produce comprehensive schedules including:
              Daily breakdowns
              Specific page/slide citations
              Time estimates per topic

### 📊 Performance Metrics

| Metric | System Result |
| :--- | :--- |
| **Source Grounding** | 100% |
| **Hallucination Rate** | 0.00% |
| **Avg. Citations per Plan** | 25 |
| **Time References per Plan** | 43 |
| **Inference Mode** | Adaptive (GPU/CPU) |

## 🎯 Conclusion
By anchoring the generation in specific course documents, this system provides students with a reliable, structured, and cited roadmap for their studies. It effectively bridges the gap between static courseware and interactive learning, eliminating the "ungrounded information" problem common in generic LLMs.

## 🎓 Author
M Abdurrahman Khan National University of Computer and Emerging Sciences (FAST), Pakistan
Contact: {i221148}@nu.edu.pk

