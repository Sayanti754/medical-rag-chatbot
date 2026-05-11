# Medical Research Q&A — RAG Chatbot

A Retrieval-Augmented Generation (RAG) based chatbot for querying medical and neuroscience research documents. Built with LangChain, hybrid vector search, and Streamlit.

This project extends the [streamlit/example-app-langchain-rag](https://github.com/streamlit/example-app-langchain-rag) base with a medical domain focus — motivated by my research internship on EEG-based Emotion Recognition at NIT Rourkela.

---

## What it does

- Upload medical research PDFs or CSVs (cardiac health, EEG studies, clinical datasets)
- Chunks and embeds documents into a vector store using hybrid search (BM25 + dense retrieval)
- Ask natural language questions and get grounded answers with source citations
- Prevents hallucination by anchoring responses strictly to uploaded documents

---

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Streamlit |
| LLM Framework | LangChain |
| Vector Store | ChromaDB / HNSWLIB |
| Retrieval | Hybrid Search (BM25 + Reciprocal Rank Fusion) |
| Embeddings | HuggingFace / OpenAI |
| Language Model | Mistral 7B / OpenAI GPT |

---

## Domain & Motivation

During my research internship at NIT Rourkela, I worked on EEG-based emotion recognition — extracting alpha, beta, gamma band power features and comparing SVM, Random Forest, and KNN classifiers. Reading and cross-referencing multiple research papers was time-consuming.

This RAG chatbot solves that — it lets researchers query multiple medical PDFs conversationally, making literature review significantly faster.

**Target documents:**
- EEG and neuroscience research papers
- Cardiac health datasets and clinical studies
- General medical literature (nutrition, diagnostics)

---

## Setup

### 1. Clone the repo

```bash
git clone https://github.com/Sayanti754/medical-rag-chatbot
cd medical-rag-chatbot
```

### 2. Set up Python environment

```bash
python -mvenv .venv
source .venv/bin/activate
pip install -U pip
pip install -r requirements.txt
```

> If you run into issues with hnswlib on Ubuntu:
> ```bash
> sudo apt install python3-hnswlib
> ```

### 3. Set up API keys

Create a `.env` file:

```
OPENAI_API_KEY="your_key_here"
HUGGINGFACEHUB_API_TOKEN="your_token_here"
```

Create Streamlit secrets:

```bash
mkdir .streamlit
touch .streamlit/secrets.toml
```

Add to `secrets.toml`:

```toml
OPENAI_API_KEY="your_key_here"
HUGGINGFACEHUB_API_TOKEN="your_token_here"
```

### 4. Run the app

```bash
streamlit run streamlit_app.py
```

---

## Example Queries

### EEG Research
> *"What are the most effective frequency bands for emotion classification in EEG studies?"*

### Cardiac Health
> *"What features distinguish normal from abnormal heart sounds in PCG recordings?"*

### Nutrition / Clinical
> *"What is the recommended calorie intake for a 60kg female to lose 0.5kg per week?"*

---

## How RAG Works Here

This app uses **hybrid search** combining:
- **BM25** — sparse keyword-based retrieval (fast, exact matches)
- **Dense vector search** — semantic similarity using embeddings
- **Reciprocal Rank Fusion (RRF)** — merges both ranked lists for best results

This approach outperforms pure dense or pure sparse retrieval, especially on technical medical terminology.

---

## Project Status

🚧 Active development

- [x] Base RAG pipeline with hybrid search
- [x] PDF and CSV document ingestion
- [x] Streamlit UI with chat history
- [ ] Medical domain fine-tuning with EEG/cardiac datasets
- [ ] LLM explanation layer using Groq API for plain-English summaries
- [ ] Deployment on Streamlit Community Cloud

---

## Background & Related Work

This project is informed by:
- My EEG-based Emotion Recognition internship (NIT Rourkela, 2025) — multi-class classification using SVM, RF, KNN on alpha/beta/gamma band features
- My PMDD Detection Web App — SVM classifier with 91% accuracy deployed on Streamlit
- My Heart Sound Classification research — CNN-LSTM achieving 95.5% accuracy across 5 cardiac classes

---

## References

- Lewis et al. (2020). [Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks](https://arxiv.org/abs/2005.11401)
- Jiang et al. (2023). [Mistral 7B](https://arxiv.org/abs/2310.06825)
- Cormack et al. (2009). [Reciprocal Rank Fusion](https://dl.acm.org/doi/10.1145/1571941.1572114)
- Liu et al. (2024). [Lost in the Middle: How LLMs Use Long Contexts](https://arxiv.org/abs/2307.03172)
- Formal et al. (2021). [SPLADE: Sparse Lexical and Expansion Model](https://dl.acm.org/doi/10.1145/3404835.3463098)

---

## Author

**Sayanti Swarupa**
B.Tech CSE, NIT Rourkela
[GitHub](https://github.com/Sayanti754) • [LinkedIn](https://linkedin.com/in/Sayantiswarupa)
