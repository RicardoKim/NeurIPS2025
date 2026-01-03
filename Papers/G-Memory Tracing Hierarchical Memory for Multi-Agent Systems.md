---
tags:
  - paper
  - research
status: 🟧 To Read
authors:
conference: NeurIPS
year: 2025
link: https://openreview.net/pdf?id=mmIAp3cVS0
priority: ⭐⭐⭐⭐⭐
created: 2026-01-02
---

# G-Memory Tracing Hierarchical Memory for Multi-Agent Systems

> [!abstract] Abstract
>  Lack of Memory Architecture in MAS(Multi Agent system) works as bottle neck in their self-evolving capabilities. We Propose G-Memory, a hierarchical agentic memory architecture for MAS. Experiments across five benchmarks show that G-Memory achieves SOTA MAS on embodied action and Knowledge QA tasks and maintaining even lower token usage than mainstream memory design

---

## 🔑 Key Contributions
- Bottleneck Identification of self evolving MAS System
- Propose solution of memory problem of MAS
- Achieve SOTA in several benchmarks with lower token usage

## 📝 Summary
> [!summary] TL;DR
> Design sophisticated Memory Design based on graph to elevate self evolving multi agent system
### Background & Motivation
- Existing MAS lack self-evolving capability (the ability to improve continuously by learning from past collaborative experiences)
- The root cause of this limitation lies in oversimplified memory mechanisms.
	- Solely rely on inside-trial memory
	- Store compressed artifacts rather than collaboration trajectories
	- Mainly focused on single agent system which doesn't have complex interaction trajectory, role-specific memory
- Design Memory architecture explicitly designed for multi-agent collaboration and long term self evolution

### Methodology
- Design memory to organize multi-agent experience at multiple abstraction levels.
- Graph Design
	- Interaction Graph : Stores utterance level collaboration traces within single task
		- Node :
			- Agent Information
			- Agent's output
		- Edge : linked based on the sequence utterances
	- Query Graph : Task level memory links to its interaction graph. Graph Edge encode semantic and experiential relationships between tasks
		- Node 
			- Task(Query)
			- Task Result(Success, Failed)
			- Interaction Graph about the task
		- Edge
			- linked based on the semantic similarity with query of other tasks
	- Insight Graph : Abstracted insights distilled from multiple tasks.
		- Node 
			- Lessons learn from tasks
			- Tasks that this lesson works
		- Edge
			- Encode context-conditioned relationships
			- How one high level insight effects a specific task
- Memory Retrieval
	- 1) Gathering tasks in Query Graph using semantic similarity 
	- 2) Hop Expansion(1-hop)
	- 3) Retrieving insight nodes which is connected to task node
	- 4) Retrieving interaction subgraph which is filtered by llm
	- 5) An operator evaluates retrieved information concerning the agent's role and task
- Memory Update
	- After task execution, all three layers are updated
### Experiments & Results

**Experiment**
- 5 benchmarks : Knowledge reasoning, Embodied action, Game
- 3 agent frameworks : AutoGen, DyLAN, MacNet
- 3 LLM backbone : Qwen 2.5 - 7b, 14b, gpt-4o-mini
**Result**
- Consistent performance gains
- Single Agent memory mechanisms often degrade MAS performance
- G-Memory maintains comparable or lower token consumption than baseline


---

## 💭 Critical Analysis / Thoughts

- **Pros**: 
	- Highlights the necessity of memory architectures specifically designed for the unique characteristics of MAS
- **Cons**:
	- Although MAS should ideally benefit from scalable and distributed architectures, the proposed design relies on tightly coupled, centralized graph structure, which limits its ability to scale with increasing agent counts or task diversity

---
