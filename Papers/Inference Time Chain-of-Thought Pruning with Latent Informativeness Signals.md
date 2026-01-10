---
tags:
  - paper
  - research
status: 🟩 Done
authors:
conference: NeurIPS
year: 2025
link:
priority: ⭐⭐⭐
created: 2026-01-10
---

# Inference-Time Chain-of-Thought Pruning with Latent Informativeness Signals

---

## 🔑 Key Contributions

- Propose **KAPPA**, inference time pruning algorithm based on information theory
- Demonstrates large reduction in memory and token cost compared to BoN and ST-BoN with minimal accuracy drop

## 📝 Summary

> [!summary] TL;DR
> Instead of fully generating all reasoning branches, KAPPA uses model internal uncertainty signals to progressively prune bad branches early, keeping only the most promising one.

### Background & Motivation

- Best-of-N / Self-Consistency improves reasoning by sampling multiple CoT traces
  - But all branches must be generated to completion which makes inference extremely expensive
- Prior Work
  - ST-BoN : truncates branches when they start to produce different token
    - Simple but pruning is based on simple consistency
  - DeepConf: uses confidence, uncertainty, reliability to filter
    - But still requires many traces to run to complete
- There is no fine-grained, quality-aware, progressive pruning of reasoning paths during generation

### Methodology

- (1) Draft Phases
  - Sample N reasoning branches up to a cutoff point where all branches are pairwise inconsistent
- (2) Scoring & Progressive Pruning phase
  - Compute
    - smoothing information gain (EMA over Meadian-of-Means of KL Divergence)
      - robustified information gain signal to stabilize pruning decisions by suppressing token-level noise and capturing trajectory-level trends
    - Compute Uncertainty signals
      - Max logit from output
    - Entropy
    - Aggregate them into a trajectory level score
  - Gradually prune the lowest-scoring branches on a linear schedule until only one remains
- (3) Continuation Phase
  - Continue decoding only the surviving branch to completion

### Experiments & Results

- Model
  - DeepSeek-R1-Distill Qwen 1.5B
  - Qwen2.5-7B-Instruct
- Benchmarks
  - GSM8K
  - MATH500
- Findings

  - Lower Memory
  - ![img](../Assets/Inference-Time%20Chain-of-Thought%20Pruning%20with%20Latent%20Informativeness%20Signals%20Figure2.png)

  - Lower tokens
  - ![img](../Assets/Inference-Time%20Chain-of-Thought%20Pruning%20with%20Latent%20Informativeness%20Signals%20Figure3.png)

---

## 💭 Critical Analysis / Thoughts

> [!quote] My Take
> Runtime reasoning control using information-theoretic signals, but the pruning schedule and scoring stability are still fragile

- **Pros**:
  - Training-Free and uses token-level distribution signals
  - Significant compute and memory savings
- **Cons**:
  - Over pruning problem
  - Scoring function requires hyper-parameter tuning
  - Can the quality of a reasoning trajectory be reliably inferred early enough to justify greedy pruning?

---

## 🔗 References & Links

- https://openreview.net/pdf/056c8a1a9a5724fb64de40cc4374d2740f3871c5.pdf
