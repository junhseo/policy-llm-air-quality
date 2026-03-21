# Policy-Aware LLM for Air Quality & Decision Support

## Overview

This project aims to develop a **policy-specialized large language model (LLM)** that supports **air quality analysis and decision-making** by integrating:

* Public policy documents (government, international organizations)
* Scientific literature (e.g., arXiv)
* Air quality data sources (e.g., OpenAQ, GEOS-based outputs)

The system is designed to bridge **data → analysis → policy recommendation**, enabling:

* Context-aware interpretation of PM2.5 and AQI
* Policy-oriented responses with structured reasoning
* Integration with interactive dashboards and chatbot interfaces

---

## Objectives

* Build a **domain-adapted LLM** for environmental policy applications
* Evaluate **RAG vs Fine-tuning approaches**
* Develop an **end-to-end pipeline** from document ingestion to chatbot deployment
* Provide a reproducible framework for **policy-aware AI systems**

---

## Key Features

* Document ingestion from:

  * Government websites
  * International organization reports
  * Open-access research papers
* Automated preprocessing:

  * HTML/PDF parsing
  * Text cleaning
  * Chunking
* Dataset construction:

  * Instruction / QA generation from documents
* Model training:

  * LoRA / QLoRA-based fine-tuning on Llama models
* Deployment:

  * Local inference engine
  * Chatbot API integration (FastAPI)
* (Optional) Retrieval-Augmented Generation (RAG)

---

## System Architecture

```text
                ┌────────────────────────┐
                │  Public Documents      │
                │ (Gov / Reports / arXiv)│
                └────────────┬───────────┘
                             │
                             ▼
                ┌────────────────────────┐
                │  Data Collection       │
                │  (Crawler / API)       │
                └────────────┬───────────┘
                             │
                             ▼
                ┌────────────────────────┐
                │  Preprocessing         │
                │  - Text extraction     │
                │  - Cleaning            │
                │  - Chunking            │
                └────────────┬───────────┘
                             │
                             ▼
                ┌────────────────────────┐
                │ Dataset Construction   │
                │  (QA / Instruction)    │
                └────────────┬───────────┘
                             │
                             ▼
                ┌────────────────────────┐
                │ Fine-tuning (LoRA)     │
                │  Llama-based model     │
                └────────────┬───────────┘
                             │
                             ▼
                ┌────────────────────────┐
                │  Local Inference API   │
                │  (FastAPI / vLLM)      │
                └────────────┬───────────┘
                             │
                             ▼
                ┌────────────────────────┐
                │ Chatbot / Dashboard    │
                └────────────────────────┘
```

---

## Repository Structure

```text
policy_llm_project/
├─ data/
│  ├─ raw/
│  ├─ processed/
│  └─ eval/
├─ configs/
│  ├─ sources.yaml
│  ├─ cleaning.yaml
│  └─ finetune.yaml
├─ src/
│  ├─ collectors/
│  ├─ preprocess/
│  ├─ dataset/
│  ├─ finetune/
│  ├─ serve/
│  └─ utils/
├─ scripts/
│  ├─ run_collect.py
│  ├─ run_preprocess.py
│  ├─ run_build_dataset.py
│  ├─ run_train.py
│  └─ run_serve.py
├─ requirements.txt
└─ README.md
```

---

## Pipeline

### Step 1: Data Collection

Collect documents from:

* Government websites
* Policy reports (PDF)
* arXiv API

```bash
python scripts/run_collect.py
```

---

### Step 2: Preprocessing

* Extract text (HTML / PDF)
* Clean and normalize
* Remove noise

```bash
python scripts/run_preprocess.py
```

---

### Step 3: Chunking

Split documents into manageable chunks for training and retrieval.

---

### Step 4: Dataset Construction

Generate instruction-style or QA-style training data.

```bash
python scripts/run_build_dataset.py
```

---

### Step 5: Fine-tuning

Train a Llama-based model using LoRA.

```bash
python scripts/run_train.py
```

---

### Step 6: Inference / Chatbot

Run local inference and connect to chatbot API.

```bash
python scripts/run_serve.py
```

---

## Tech Stack

* **Language**: Python
* **LLM**: Llama (fine-tuned with LoRA / QLoRA)
* **Training**: Hugging Face Transformers, PEFT, TRL
* **Data Processing**: BeautifulSoup, PyMuPDF
* **API**: FastAPI
* **Optional**: vLLM / llama.cpp
* **Data Sources**: OpenAQ, government datasets, scientific literature

---

## Experiment Design

This project compares three approaches:

### 1. Baseline LLM

* No fine-tuning
* No retrieval

### 2. Fine-tuned LLM

* Domain-adapted using policy documents

### 3. RAG + Fine-tuned LLM (Recommended)

* Retrieval for up-to-date knowledge
* Fine-tuning for response structure and reasoning

---

## Example Use Cases

* "What is the current air quality near me?"
* "Compare PM2.5 trends between two cities over 10 years"
* "What policy recommendations apply under high AQI conditions?"
* "Summarize key findings from a policy report"

---

## Demo (Coming Soon)

* Chatbot interaction (AQI + recommendation)
* Dashboard visualization (time-series, comparison)
* Policy-aware response generation

---

## Important Notes

* Only collect data from:

  * Publicly available sources
  * Documents with permitted usage
* Always verify:

  * Terms of Service
  * Licensing conditions
* This project is intended for **research and prototyping purposes**

---

## Future Work

* Improved QA dataset generation (semantic parsing, LLM-assisted labeling)
* Integration with real-time AQI APIs
* Multi-modal support (maps, satellite data)
* Policy evaluation metrics (explainability, uncertainty)
* Deployment optimization (low-latency inference)

---

## Author

Junhyun Seo
Assistant Research Scientist
NASA Goddard Space Flight Center (GESTAR II)

---

## License

TBD
