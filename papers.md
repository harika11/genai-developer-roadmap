# Papers Worth Reading

You do not need to read papers to be a good AI Engineer. But reading ~15 of them makes you notably
better at debugging, at design discussions, and at interviews.

**How to read one:** abstract → figures → conclusion → introduction. Only read the method section if
you're implementing it. 30 minutes per paper is plenty. Do not try to follow every derivation.

Pace: **one paper per week** alongside the roadmap. Write three sentences about each in your notes.

---

## Tier 1 — read these (foundations)

| Paper | Year | Why |
| --- | --- | --- |
| [Attention Is All You Need](https://arxiv.org/abs/1706.03762) | 2017 | The transformer. Everything descends from this. |
| [BERT](https://arxiv.org/abs/1810.04805) | 2018 | Encoders, and why embedding models look the way they do. |
| [Language Models are Few-Shot Learners (GPT-3)](https://arxiv.org/abs/2005.14165) | 2020 | In-context learning — why prompting works at all. |
| [Training language models to follow instructions (InstructGPT)](https://arxiv.org/abs/2203.02155) | 2022 | RLHF. Why a base model and a chat model behave so differently. |
| [Retrieval-Augmented Generation (RAG)](https://arxiv.org/abs/2005.11401) | 2020 | The original RAG paper. |
| [Chain-of-Thought Prompting](https://arxiv.org/abs/2201.11903) | 2022 | Reasoning via prompting. |
| [ReAct: Synergizing Reasoning and Acting](https://arxiv.org/abs/2210.03629) | 2022 | The pattern underneath nearly every agent framework. |
| [LoRA: Low-Rank Adaptation](https://arxiv.org/abs/2106.09685) | 2021 | How practical fine-tuning is actually done. |

---

## Tier 2 — read when the topic becomes relevant

| Paper | Topic |
| --- | --- |
| [QLoRA](https://arxiv.org/abs/2305.14314) | Fine-tuning on one consumer GPU |
| [Direct Preference Optimization (DPO)](https://arxiv.org/abs/2305.18290) | Preference tuning without RL |
| [FlashAttention](https://arxiv.org/abs/2205.14135) | Why modern inference is fast |
| [Constitutional AI](https://arxiv.org/abs/2212.08073) | AI feedback for alignment |
| [Toolformer](https://arxiv.org/abs/2302.04761) | Models learning to call tools |
| [Self-Consistency](https://arxiv.org/abs/2203.11171) | Sampling multiple paths to improve reasoning |
| [Lost in the Middle](https://arxiv.org/abs/2307.03172) | Why long context ≠ good retrieval. **Very practical.** |
| [HyDE](https://arxiv.org/abs/2212.10496) | Hypothetical document embeddings for retrieval |
| [Mixtral / Mixture of Experts](https://arxiv.org/abs/2401.04088) | Sparse models |
| [Scaling Laws](https://arxiv.org/abs/2001.08361) & [Chinchilla](https://arxiv.org/abs/2203.15556) | Why models are the sizes they are |
| [Tree of Thoughts](https://arxiv.org/abs/2305.10601) | Deliberate search over reasoning |
| [Universal and Transferable Adversarial Attacks](https://arxiv.org/abs/2307.15043) | Jailbreaks; pairs with the security phase |

---

## Engineering writeups (often more useful than papers)

- [Building Effective Agents](https://www.anthropic.com/engineering/building-effective-agents) — Anthropic
- [Contextual Retrieval](https://www.anthropic.com/news/contextual-retrieval) — Anthropic; a concrete, big RAG improvement
- [Prompt Engineering Guide](https://www.promptingguide.ai/) — DAIR.AI
- [Agents](https://lilianweng.github.io/posts/2023-06-23-agent/) — Lilian Weng
- [Prompt Engineering](https://lilianweng.github.io/posts/2023-03-15-prompt-engineering/) — Lilian Weng
- [What We Learned from a Year of Building with LLMs](https://applied-llms.org/) — an unusually honest field report
- [Patterns for Building LLM-based Systems](https://eugeneyan.com/writing/llm-patterns/) — Eugene Yan
- [Evaluating LLM Applications](https://hamel.dev/blog/posts/evals/) — Hamel Husain

---

## Keeping up without drowning

- [arXiv cs.CL](https://arxiv.org/list/cs.CL/recent) and [cs.AI](https://arxiv.org/list/cs.AI/recent) — skim titles weekly, nothing more
- [Papers with Code](https://paperswithcode.com/) / [Hugging Face Papers](https://huggingface.co/papers) — daily trending
- [AI Explained](https://www.youtube.com/@aiexplained-official) and [Yannic Kilcher](https://www.youtube.com/@YannicKilcher) — video paper reviews

**Do not** try to read everything published. The field puts out hundreds of papers a week. The Tier
1 list has been stable for years — that's the signal about what's worth your time.
