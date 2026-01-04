---
tags:
  - RAG
  - Ranking
status: 🟧 To Read
authors:
  - Yue Yu
  - Wei Ping
  - Zihan Liu
  - Boxin Wang
  - Jianxuan You
  - Chao Zhang
  - Mohammad Shoeybi
  - Bryan Catanzaro
conference: NeurIPS
year: 2024
link: https://openreview.net/forum?id=S1fc92uemC
priority: ⭐⭐⭐
created: 2026-01-02
---


# RankRAG - Unifying Context Ranking withRetrieval-Augmented Generation in LLMs

> [!abstract] Abstract
> Large language models (LLMs) typically utilize the top-k contexts from a retriever in retrieval-augmented generation (RAG). In this work, we propose a novel method called RankRAG, which instruction-tunes a single LLM for both context ranking and answer generation in RAG. In particular, the instruction-tuned LLMs work surprisingly well by adding a small fraction of ranking data into the training blend, and outperform existing expert ranking models, including the same LLM exclusively fine-tuned on a large amount of ranking data. For generation, we compare our model with many strong baselines, including ChatQA-1.5, an open-sourced model with the state-of-the-art performance on RAG benchmarks. Specifically, our Llama3-RankRAG-8B and Llama3-RankRAG-70B significantly outperform Llama3-ChatQA-1.5-8B and Llama3-ChatQA-1.5-70B, respectively, on nine general knowledge-intensive benchmarks for RAG. In addition, it also performs comparably to GPT-4 on five RAG benchmarks in the biomedical domain without instruction fine-tuning on biomedical data, demonstrating its superb capability for generalization to new domains.

---

## 🔑 Key Contributions
- One decoder-only LLM handles _retrieve → rerank → generate_ without a separate cross-encoder reranker.
- Ranking is cast into a QA-like instruction format (True/False relevance, or “which passages are relevant”) to encourage transfer to generation.
- strong reranking recall with 5k-50k ranking pairs, reporting competitiveness vs rerankers trained on much more ranking data.

## 📝 Summary
> [!summary] TL;DR
> Treat ranking as an instruction-following subtask inside RAG fine-tuning (QA-shaped prompts), then use the same model to rerank retrieved passages before generating, which yields consistent gains, especially when initial retrieval is noisy.

### Background & Motivation
- Standard RAG often retrieves many chunks (high recall) but LLMs degrade when forced to read too much
	- using a small top-_k_ helps generation but can miss relevant evidence.
- A common fix is an extra reranker model (cross-encoder), but this adds complexity and may generalize worse than the LLM itself.
- Core hypothesis: an instruction-tuned LLM’s ability to use evidence and its ability to judge relevance can be trained to mutually reinforce when framed in an instruction format

### Methodology
Two stage post-training (maybe we can replicate this with unsloth?)

**Stage 1**: SFT for instruction following
- self-explanatory (most models usually do this anyways)

**Stage 2**: instruction-tuning for ranking + generation
	(1) Stage-I SFT data (to preserve instruction-following).
	(2) Context-rich QA datasets (gold context + answer).
	(3) Retrieval-augmented QA: mix gold context with BM25 top-retrieved contexts (total 5 passages) to train robustness to irrelevant context
	(4) Context ranking
	(5) Retrieval-augmented ranking (given 5 passages, explicitly identify which are relevant)


**Inference Pipeline**
Retrieve -> Rerank -> Generate
1. Retriever first pulls top-N passages
2. RankRAG computes a relevance score using the probability of generating "True" (for relevance)
	1. Reranking generates ~1 token per passage
3. Keep top-k then generate using the retrieved passages

### Experiments & Results
- Benchmarks: Open-domain QA (NQ, TriviaQA, PopQA, HotpotQA, 2WikimQA), fact verification (FEVER), conversational QA (Doc2Dial, TopiOCQA, INSCIT).
- Backbone: Llama 3 8B, 70B

**Results**
- RankRAG improves over ChatQA-1.5 across all benchmarks
- Authors highlight larger gains on harder datasets like PopQA and 2WikimQA (>10%)


---

## 💭 Critical Analysis / Thoughts
> [!quote] My Take
> RankRAG is not bad (it simplifies RAG and yields consistent gains) but it is fundamentally bounded by retriever recall and heuristic ranking labels. Lot's of future work remain, especially in uncertainty-aware relevance modeling (when no relevant passages are returned).

- **Pros**:
	- Using a simple, unified reranker model simplifies LLM deployment 
	- Maybe we can use "judge LLMs" to further improve the RAG method?
	- Better token efficiency than classic reranker training
- **Cons**:
	- No public GitHub repository (not very reproducible)
	- Evaluation focuses on common RAG QA suites; less evidence on open-ended generation quality dimensions
	- Reranking helps with noisy retrieval, but the method still assumes the answer is present in the candidate pool

---

## 🔗 References & Links
- [Link to Paper](https://openreview.net/forum?id=S1fc92uemC)
- [Code Repository] 없음
