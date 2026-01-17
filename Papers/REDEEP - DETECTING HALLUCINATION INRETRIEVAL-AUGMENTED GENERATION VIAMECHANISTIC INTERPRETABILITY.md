---
tags:
  - paper
  - research
status: 🟩 Done
authors:
conference: ICLR
year: 2025
link: https://arxiv.org/pdf/2410.11414
priority: ⭐⭐⭐
created: 2026-01-17
---

# REDEEP - DETECTING HALLUCINATION INRETRIEVAL-AUGMENTED GENERATION VIAMECHANISTIC INTERPRETABILITY

> [!abstract] Abstract
> Retrieval-Augmented Generation (RAG) models are designed to incorporate external knowledge, reducing hallucinations caused by insufficient parametric (internal) knowledge. However, even with accurate and relevant retrieved content, RAG models can still produce hallucinations by generating outputs that conflict with the retrieved information. Detecting such hallucinations requires disentangling how Large Language Models (LLMs) utilize external and parametric knowledge. Current detection methods often focus on one of these mechanisms or without decoupling their intertwined effects, making accurate detection difficult. In this paper, we investigate the internal mechanisms behind hallucinations in RAG scenarios. We discover hallucinations occur when the Knowledge FFNs in LLMs overemphasize parametric knowledge in the residual stream, while Copying Heads fail to effectively retain or integrate external knowledge from retrieved content. Based on these findings, we propose ReDeEP, a novel method that detects hallucinations by decoupling LLM’s utilization of external context and parametric knowledge. Our experiments show that ReDeEP significantly improves RAG hallucination detection accuracy. Additionally, we introduce AARF, which mitigates hallucinations by modulating the contributions of Knowledge FFNs and Copying Heads.

---

## 🔑 Key Contributions
- Investigate internal mechanisms behind RAG hallucination
- Propose a hallucination detection method in RAG situation that decouples and regresses external context and parametric knowledge signals
- Introduce method to mitigate hallucination by modulating attention and feed-forward contribution

## 📝 Summary
> [!summary] TL;DR
> Explain RAG Hallucination mechanism using mechanistic interpretability and propose a way to detect and mitigate it
### Background & Motivation
- LLM can hallucinate with accurate retrieval context
- This paper posits that hallucinations arise due to the internal mechanics of transformers: over-reliance on parametric knowledge and under-utilization of external context
### Methodology
- Mechanistic interpretability analysis
	- Define following two metrics 
		- External Context Score(ECS) : How much tokens are grounded in retrieved context
			- Identify copying-sensitive attention heads
			- For each generation step
				- Select top k% tokens with the highest attention scores
				- Compute cosine similarity between:
					- The current token’s hidden state (last layer)
					- The mean-pooled hidden states of the attended context tokens
		- Parametric Knowledge Score(EKS)
			- Projection hidden state into vocabulary space using Logit Lends
			- Calculate distribution difference between before and after FFN layers
	- Key findings
		- In hallucinated outputs: ECS is low and PKS is high
		- Even when retrieved document contains the correct answer, the model fails to route information through attention
- ReDeEP : Hallucination Detection
	- Using ECS and PKS as two decoupled explanatory variables
	- Train a regression model to predict hallucination probability
- AARF : Hallucination Mitigation
	- Amplifying head attention for copying and suppressing FFN contribution when hallucination score is over threshold
### Experiments & Results
- Evaluated on benchmarks such as **RAGTruth** and **Dolly** using LLaMA-based models
- ReDeEP significantly outperforms existing hallucination detection baselines
- ECS/PKS features alone already provide strong separability between hallucinated and faithful outputs
- AARF consistently reduces hallucination rate without retraining the model

---

## 💭 Critical Analysis / Thoughts
> [!quote] My Take
> This paper shows that RAG hallucination comes from a reasoning control failure inside model 

- **Pros**:
	- Provide a mechanistic explanation for RAG hallucination
	- Connect this interpretability analysis to both detection and mitigation
- **Cons**:
	- ECS and PKS are still proxy metrics
	- Cannot distinguish between safety refusal and RAG hallucination

---

## 🔗 References & Links
- [Link to Paper](https://arxiv.org/pdf/2410.11414)
