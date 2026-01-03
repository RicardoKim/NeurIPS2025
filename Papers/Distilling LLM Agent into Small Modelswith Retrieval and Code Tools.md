---
tags:
  - distillation
status: 🟧 To Read
authors:
  - KAIST
  - Krafton
conference: NeurIPS
year: 2026
link: https://openreview.net/pdf?id=VkicTqszOn
priority:
created: 2026-01-03
---

# Distilling LLM Agent into Small Modelswith Retrieval and Code Tools

> [!abstract] Abstract
> This work shows that distilling agentic, tool-using behavior enables sLM to generalize better to OOD tasks, especially when augmented with first-thought prefixing and self-consistent action generation

---

## 🔑 Key Contributions
- Propose agent distillation based on tool-using behaviors with two methods to overcome limitations of naive distillations

## 📝 Summary
> [!summary] TL;DR
> One sentence summary of the main idea.

### Background & Motivation
- Transfer complex reasoning skill to sLM using CoT methods has proven effective
- Simple distillation agentic behavior into sLM does not guarantee generalization

### Methodology
- Collect agent trajectory of teacher model (thought > action > observation) with 2 major tools(retrieval and code executor)
- This cause 2 main problem
	- 1) ReAct based trajectory often lies out of distribution relative to pre-training and instruction tuning distribution of both teacher and student models
	- 2) sLM struggle to produce functional code during inference
- To prevent those problem this paper propose 2 techniques
	- 1) FTP : Let teacher model generate model native reasoning trajectory with prefix. distillation trajectory only after prefix
		- Prior studies have shown that the initial reasoning step critically determines the final conclusion of LLMs
	- 2) SAG : Instead of using greedy decoding, sample multiple N thought-action sequences for each step through nucleus sampling.

### Experiments & Results

**Setting**

- Model
	- Teacher :  Qwen2.5-32B-Instruct
	- Student : Qwen2.5-Instruct(0.5B/ 1.5B/ 3B/ 7B)
- Task
	- Factual reasoning
	    - In-domain: HotpotQA
	    - OOD: Bamboogle, MuSiQue, 2WikiMultiHopQA
	- Math reasoning
	    - In-domain: MATH500
	    - OOD: GSM-Hard, AIME, OlymMATH
- Tool
	- Retrieval (Wikipedia 2018, e5-base-v2) 
	- Code execution (CodeAct-style)
**Result**
- Outperforms CoT distillation across all model sizes, with particularly strong gains on OOD tasks  
- Enables small models (≤3B) to match or exceed much larger CoT-distilled models  
- First-thought prefix improves robustness on complex reasoning tasks  
- Self-consistent action generation significantly reduces invalid tool actions

---

## 💭 Critical Analysis / Thoughts

- **Pros**:
	- Propose a tailored way to distill agentic behavior into sLM.
	- Demonstrate strong OOD generalization
- **Cons**:
	- The evaluation is limited to a narrow tool set, which may underestimate challenges in scaling agent distillation to richer, multi-tool environments.
	- FTP occasionally increases hallucination by biasing the agent toward internal reasoning; it is not discussed whether simpler CoT prompting could provide a safer alternative in such scenarios.


---

## 🔗 References & Links
- [Link to Paper](https://openreview.net/forum?id=VkicTqszOn)
- [Code Repository](https://github.com/Nardien/agent-distillation)
