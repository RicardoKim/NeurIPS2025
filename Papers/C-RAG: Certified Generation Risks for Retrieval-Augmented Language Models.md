---
tags:
  - paper
  - RAG
  - conformal-prediction
  - certified-guarantees
status: 🟩 Done
authors:
  - Mintong Kang
  - Ning Yu
  - Dawn Song
  - Bo Li
conference: ICML
year: "2024"
link: https://openreview.net/forum?id=FMa4c5NhOe
priority: ⭐⭐⭐⭐
created: 2026-01-12
---
# C-RAG: Certified Generation Risks for Retrieval-Augmented Language Models
> [!abstract] Abstract
> Despite the impressive capabilities of large language models (LLMs) across diverse applications, they still suffer from trustworthiness issues, such as hallucinations and misalignments. Retrieval-augmented language models (RAG) have been proposed to enhance the credibility of generations by grounding external knowledge, but the theoretical understandings of their generation risks remains unexplored. In this paper, we answer: 1) whether RAG can indeed lead to low generation risks, 2) how to provide provable guarantees on the generation risks of RAG and vanilla LLMs, and 3) what sufficient conditions enable RAG models to reduce generation risks. We propose C-RAG, the first framework to certify generation risks for RAG models. Specifically, we provide conformal risk analysis for RAG models and certify an upper confidence bound of generation risks, which we refer to as conformal generation risk. We also provide theoretical guarantees on conformal generation risks for general bounded risk functions under test distribution shifts. We prove that RAG achieves a lower conformal generation risk than that of a single LLM when the quality of the retrieval model and transformer is non-trivial. Our intensive empirical results demonstrate the soundness and tightness of our conformal generation risk guarantees across four widely-used NLP datasets on four state-of-the-art retrieval models.
---
## 🔑 Key Contributions
- First framework to provide certified generation risk guarantees for RAG models
- Theoretical proof that RAG achieves lower conformal generation risk than non-RAG baselines
- Extension of certification guarantees to handle test distribution shifts
- Introduction of corrective strategies to improve RAG robustness
## 📝 Summary
> [!summary] TL;DR
> C-RAG applies conformal risk analysis to RAG models, providing a provable upper bound on generation risk. The framework certifies that retrieval augmentation reduces risk compared to baselines, even under distribution shift.
### Background & Motivation
- RAG is designed to reduce hallucination and improve factual accuracy by grounding LLM outputs in retrieved documents
- Existing RAG evaluations are empirical. No prior work provides theoretical guarantees on generation risk.
- Two questions drive the work:
    1. Can RAG provably lead to low generation risks?
    2. How can we certify these risks with formal guarantees?
### Methodology
- Uses conformal risk analysis to derive high-probability upper bounds on generation risk
- Applies to general bounded risk functions (not limited to specific loss types)
- Framework certifies risk under distribution shifts between training and test data
- Retrieval parameters ($N_{rag}$, diversity thresholds $\lambda_g$, $\lambda_s$) are varied to study their effect on certified risk bounds
### Experiments & Results
- Datasets: AESLC, CommonGen, DART, E2E
- Retrieval methods: BM25, Biencoder-SFT
- Key finding: Certified conformal generation risk ($\hat{\alpha}_{rag}$) is consistently lower for RAG than baselines
- Risk bounds remain valid under distribution shift conditions
- Empirical risk closely tracks the theoretical upper bound, indicating tightness
---
## 💭 Critical Analysis / Thoughts
> [!quote] My Take
> C-RAG addresses a genuine gap: most RAG research is empirical, and this provides a formal lens. The conformal approach is principled but its practical utility depends on how tight the bounds are and whether they inform deployment decisions.
- **Pros**:
    - Fills a theoretical void in RAG literature
    - Distribution shift robustness is practically relevant
    - General bounded risk function formulation increases applicability
- **Cons**:
    - Certification relies on assumptions about calibration data representativeness
    - Bounds may be loose in adversarial or heavily out-of-distribution settings
    - Practical impact on model selection or deployment thresholds is unclear
---
## 🔗 References & Links
- [Link to Paper](https://openreview.net/forum?id=FMa4c5NhOe)
- [Code Repository]()