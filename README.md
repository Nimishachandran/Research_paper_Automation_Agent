# Malayalam HTR Research Automation Agent

An agentic AI pipeline that automatically searches, downloads, ranks, and analyses Malayalam/Indic Handwritten Text Recognition (HTR) research papers from arXiv and Semantic Scholar — then generates a structured comparison report using LLaMA-3.3-70B via Groq.

---

## What It Does

| Agent | Role |
|---|---|
| Search Agent | Queries arXiv + Semantic Scholar across multiple HTR-related queries |
| Download Agent | Downloads PDFs and extracts text using PyPDF2 |
| Ranking Agent | Scores and ranks papers by relevance to Malayalam HTR |
| Summarisation Agent | Sends each paper to LLaMA-3.3-70B for architecture-level analysis |
| Comparison Agent | Generates cross-paper comparisons: CER/WER trends, architecture evolution |
| Export Agent | Saves full structured report as `.txt` |

---

## Sample Output

From a single run the pipeline:
- Searched and found **141 unique papers** across arXiv and Semantic Scholar
- Successfully downloaded **94 PDFs**
- Analysed the **top 25 ranked papers** in detail
- Generated a full report covering architecture evolution, performance benchmarks, and model recommendations

---

## Pipeline Architecture

```
arXiv + Semantic Scholar
        ↓
   Search Agent  (141 papers found)
        ↓
  Download Agent  (94 PDFs downloaded)
        ↓
   Ranking Agent  (top 25 selected)
        ↓
Summarisation Agent  (LLaMA-3.3-70B via Groq)
        ↓
  Comparison Agent  (CER/WER trends, architecture insights)
        ↓
   Export Agent  → COMPLETE_malayalam_htr_analysis.txt
```

---

## Tech Stack

- **LLM:** LLaMA-3.3-70B via [Groq](https://groq.com) (free tier)
- **Agentic Framework:** LangGraph (StateGraph with typed state)
- **Paper Sources:** arXiv API, Semantic Scholar API
- **PDF Processing:** PyPDF2
- **Rate Limit Handling:** Dual Groq API key rotation
- **Platform:** Kaggle Notebooks (GPU not required)

---

## Key Features

- Multi-query search across 6 different query strings for maximum coverage
- Automatic deduplication of papers across sources
- Rate limit handling via dual API key rotation — no manual intervention needed
- Progress checkpointing every 5 papers so analysis can resume after interruption
- Full architecture-level LLM analysis per paper, not just abstracts

---

## How to Run

### 1. Set up Groq API keys

Get free API keys from [console.groq.com](https://console.groq.com). Add them as Kaggle secrets:
- `GROQ_API_KEY`
- `GROQ_API_KEY1` (second key for rate limit rotation)

### 2. Install dependencies

```bash
pip install langgraph groq arxiv PyPDF2 requests
```

### 3. Run the notebook

Open `papers.ipynb` and run all cells. The pipeline will:
1. Search arXiv and Semantic Scholar automatically
2. Download and rank papers
3. Analyse the top 25 with LLaMA-3.3-70B
4. Save the full report to `/kaggle/working/analysis_results/`

Estimated runtime: **15–30 minutes** depending on Groq rate limits.

---

## Report Structure

The generated report covers:
- Architecture evolution across years (HMM → CNN → CRNN → Transformer)
- CER/WER performance trends per paper
- Malayalam script-specific techniques identified
- Recommended architecture with reasoning
- Implementation roadmap for building a production HTR system

---

## Notes

- This pipeline is designed for Malayalam/Indic HTR research but can be adapted to any research domain by changing the search queries in the Search Agent
- The free Groq tier supports 30 requests/min and 14,400/day — sufficient for 25-paper analysis with dual key rotation
- PDFs that fail to download are skipped gracefully; the pipeline continues with available papers

---

## Author

Nimisha Chandran S R  
[LinkedIn](https://linkedin.com/in/YOUR-PROFILE) | [GitHub](https://github.com/Nimishachandran)
