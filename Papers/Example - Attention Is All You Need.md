---
tags: [paper, nlp, transformer]
status: 🟩 Done
authors: [Ashish Vaswani, Noam Shazeer, Niki Parmar, et al.]
conference: NeurIPS
year: 2017
link: https://arxiv.org/abs/1706.03762
priority: ⭐⭐⭐⭐⭐
created: 2025-12-29
---

# Attention Is All You Need

> [!abstract] Abstract
> The dominant sequence transduction models are based on complex recurrent or convolutional neural networks that include an encoder and a decoder. The best performing models also connect the encoder and decoder through an attention mechanism. We propose a new simple network architecture, the Transformer, based solely on attention mechanisms, dispensing with recurrence and convolutions entirely.

---

## 🔑 Key Contributions
- Proposed the **Transformer** architecture, which relies entirely on self-attention.
- Introduced **Multi-Head Attention** to capture different types of relationships.
- Achieved SOTA on translation tasks (WMT 2014) with significantly less training time.
- Replaced RNNs/LSTMs, allowing for massive parallelization.

## 📝 Summary
> [!summary] TL;DR
> Introduces the Transformer architecture, replacing RNNs with self-attention for sequence modeling, enabling parallel training and setting a new SOTA in machine translation.

### Background & Motivation
- **Problem**: RNNs (LSTMs/GRUs) process data sequentially $t, t-1, \dots$, which precludes parallelization within training examples. Long-range dependencies are hard to learn due to path length.
- **Goal**: Reduce sequential computation and capture global dependencies directly.

### Methodology
- **Self-Attention**: Relates different positions of a single sequence to compute a representation of the sequence.
- **Scaled Dot-Product Attention**: $Attention(Q, K, V) = softmax(\frac{QK^T}{\sqrt{d_k}})V$
- **Positional Encoding**: Since there's no recurrence, sine/cosine functions are added to embeddings to inject order information.
- **Architecture**: Encoder-Decoder stack with residual connections and LayerNorm.

### Experiments & Results
- **WMT 2014 English-to-German**: 28.4 BLEU (new SOTA).
- **Training Cost**: A small fraction of the training cost of the best models from the literature.

---

## 💭 Critical Analysis / Thoughts
> [!quote] My Take
> The foundational paper for modern NLP. The shift from recurrence to attention was a paradigm shift that enabled the LLM era (BERT, GPT).

- **Pros**: Highly parallelizable, handles long-term dependencies well.
- **Cons**: Quadratic complexity $O(n^2)$ with respect to sequence length limits very long contexts (though modern variants address this).

---

## 🔗 References & Links
- [Link to Paper](https://arxiv.org/abs/1706.03762)
- [Official Code (Tensor2Tensor)](https://github.com/tensorflow/tensor2tensor)
