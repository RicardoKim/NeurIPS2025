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
link: https://openreview.net/forum?id=S1fc92uemC&referrer=%5Bthe%20profile%20of%20Jiaxuan%20You%5D(%2Fprofile%3Fid%3D~Jiaxuan_You2)
priority: ⭐⭐⭐
created: 2026-01-02
---


# RankRAG - Unifying Context Ranking withRetrieval-Augmented Generation in LLMs

> [!abstract] Abstract
> Large language models (LLMs) typically utilize the top-k contexts from a retriever in retrieval-augmented generation (RAG). In this work, we propose a novel method called RankRAG, which instruction-tunes a single LLM for both context ranking and answer generation in RAG. In particular, the instruction-tuned LLMs work surprisingly well by adding a small fraction of ranking data into the training blend, and outperform existing expert ranking models, including the same LLM exclusively fine-tuned on a large amount of ranking data. For generation, we compare our model with many strong baselines, including ChatQA-1.5, an open-sourced model with the state-of-the-art performance on RAG benchmarks. Specifically, our Llama3-RankRAG-8B and Llama3-RankRAG-70B significantly outperform Llama3-ChatQA-1.5-8B and Llama3-ChatQA-1.5-70B, respectively, on nine general knowledge-intensive benchmarks for RAG. In addition, it also performs comparably to GPT-4 on five RAG benchmarks in the biomedical domain without instruction fine-tuning on biomedical data, demonstrating its superb capability for generalization to new domains.

---

## 🔑 Key Contributions
- 
- 
- 

## 📝 Summary
> [!summary] TL;DR
> One sentence summary of the main idea.

### Background & Motivation
- What problem are they solving?

### Methodology
- How did they solve it?

### Experiments & Results
- What did they find?

---

## 💭 Critical Analysis / Thoughts
> [!quote] My Take
> Strengths, weaknesses, and potential future work.

- **Pros**:
- **Cons**:

---

## 🔗 References & Links
- [Link to Paper](URL)
- [Code Repository](URL)
