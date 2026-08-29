# GenAI Developer Roadmap

A 6-month, week-by-week plan to go from **~2 years of general software engineering experience** to a
confident **Generative AI / AI Engineer**.

Here's the good news: you already have the hard part. You know how to ship software, debug things
that break in weird ways, and work with requirements that aren't fully spelled out — that's most of
the job, right there. This roadmap fills in the specific, learnable gap: how large language models
work, and how to build good products on top of them. It doesn't require a math background or a
research pedigree — just a plan and some consistent hours.

---

## Who this is for

You should already have most of these — and it's fine if a couple are missing. Phase 0 exists to
close exactly those gaps before the real climb starts.

> 🧭 **[Open the interactive tracker →](https://claude.ai/code/artifact/f9f63870-8f38-4efc-9d54-72d272208be1)**
> The same plan as a day-by-day checklist — set a start date, check off tasks, and it pins a "you are here" marker on today's task automatically. Progress saves in your browser.

| You have | Why it matters |
| --- | --- |
| 1–3 years writing production code | You already know Git, testing, code review, debugging |
| Comfortable in **Python** (or willing to get there in 2 weeks) | The entire GenAI ecosystem is Python-first |
| Can build and call a REST API | 80% of GenAI work is API orchestration |
| Basic SQL + one datastore | RAG needs a vector store; everything needs persistence |
| Docker basics | Deployment, reproducible envs |

You do need to be comfortable reading a paper's abstract and not panicking at a summation symbol.

---

## The honest framing: three different jobs

"GenAI developer" means three very different roles. Pick one as your primary target — the roadmap
below aims at **AI Engineer**, which is by far the most accessible from a software background.

| Role | What you actually do | Math required | Reachable in 6 months from SWE? |
| --- | --- | --- | --- |
| **AI Engineer / GenAI App Developer** ← *this roadmap* | Build RAG systems, agents, and LLM features into products. Prompting, evals, orchestration, deployment. | Low | ✅ Yes |
| **ML Engineer (LLM)** | Fine-tuning, distillation, serving optimization, inference infra | Medium | ⚠️ ~12 months |
| **Research Scientist** | Novel architectures, training runs, publishing | High | A different path — not this roadmap |

---

## Time commitment

The plan assumes **10–12 hours/week for 24 weeks** (~250–300 hours total). Roughly:

- 4 hrs — courses / reading
- 6 hrs — building the phase project
- 1 hr — writing up what you learned (blog post, README, or notes)

If you can only do 5 hrs/week, double the calendar time. Do not skip the building hours — that is
the part that gets you hired.

---

## The roadmap at a glance

```
Week  1 ──┬── Phase 0: Foundations           Python, ML mental model
Week  3 ──┼── Phase 1: How LLMs Work         Transformers, tokens, embeddings
Week  6 ──┼── Phase 2: LLM App Development   APIs, prompting, structured output, tools
Week 10 ──┼── Phase 3: RAG                   Chunking, embeddings, vector DBs, retrieval quality
Week 14 ──┼── Phase 4: Agents                Tool use, planning, multi-agent, MCP
Week 18 ──┼── Phase 5: Evaluation & Safety   Evals, observability, guardrails, red teaming
Week 21 ──┼── Phase 6: Fine-tuning & Serving LoRA, quantization, inference optimization
Week 24 ──┴── Phase 7: Ship & Get Hired      LLMOps, portfolio, interviews
```

📚 **[Full course list with links →](courses.md)**
🛠️ **[Portfolio projects →](projects.md)**
🧰 **[Tools & libraries →](tools.md)**
📄 **[Papers worth reading →](papers.md)**
💼 **[Interview prep →](interview-prep.md)**
✅ **[Progress tracker →](progress-tracker.md)**

---

## Phase 0 — Foundations (Weeks 1–2)

**Goal:** Be fluent enough in Python and ML vocabulary that nothing later feels like magic.

Skip this phase entirely if you already write Python daily *and* know what a gradient, a loss
function, and an embedding are.

### Learn
- Python for real: type hints, `async`/`await`, virtual envs (`uv` or `poetry`), `pydantic`
- NumPy + pandas basics — you'll read a lot of code that uses them
- ML vocabulary only: training vs inference, loss, gradient descent, overfitting, train/val/test

### Courses
| Course | Provider | Time | Cost |
| --- | --- | --- | --- |
| [Practical Deep Learning for Coders — Part 1, lessons 1–4](https://course.fast.ai/) | fast.ai | 12h | Free |
| [Python for Everybody](https://www.coursera.org/specializations/python) *(only if Python is new)* | Coursera | 15h | Free to audit |

### Build
A CLI tool that calls any LLM API and streams the response to your terminal. ~100 lines. This is
your "hello world" and you'll reuse it constantly.

### Done when
You can explain to a colleague what a neural network is doing during training, in 3 sentences,
without hand-waving.

---

## Phase 1 — How LLMs Actually Work (Weeks 3–5)

**Goal:** Kill the magic. You should be able to draw a transformer block on a whiteboard and
explain why an LLM hallucinates.

This phase feels like a detour when you're eager to build. It isn't. Every debugging session later
— "why is my RAG returning garbage", "why does it ignore my system prompt", "why did my token bill
triple" — resolves faster when you know what's under the hood.

### Learn
- Tokenization (BPE) and why token counts ≠ word counts
- Embeddings: what a vector actually represents, cosine similarity
- Attention and the transformer block
- Pretraining → instruction tuning → RLHF/DPO: the three stages that make a chatbot
- Sampling: temperature, top-p, top-k, and why "deterministic" is a lie
- Context windows, KV cache, and why long prompts cost more than long outputs

### Courses
| Course | Provider | Time | Cost |
| --- | --- | --- | --- |
| [Neural Networks: Zero to Hero](https://karpathy.ai/zero-to-hero.html) — **the single highest-value resource here** | Andrej Karpathy | 20h | Free |
| ↳ Especially *Let's build GPT: from scratch* and *Let's build the GPT Tokenizer* | | | |
| [Generative AI with LLMs](https://www.coursera.org/learn/generative-ai-with-llms) | DeepLearning.AI + AWS | 16h | Free to audit |
| [Hugging Face LLM Course](https://huggingface.co/learn/llm-course) | Hugging Face | 15h | Free |
| [The Illustrated Transformer](https://jalammar.github.io/illustrated-transformer/) *(read, don't skim)* | Jay Alammar | 1h | Free |

### Build
Follow along with Karpathy and train a tiny GPT on a text file you care about (your own chat logs,
a book, your codebase). It will produce nonsense. That's the point — you'll understand *why*.

### Done when
You can answer: *"Why does an LLM confidently make up a citation?"* in terms of next-token
prediction, not "because it's an AI."

---

## Phase 2 — LLM Application Development (Weeks 6–9)

**Goal:** This is your actual job. Build reliable software on an unreliable, non-deterministic
component.

### Learn
- Provider APIs: Anthropic (Claude), OpenAI, Google Gemini — the request/response shape is similar
- Prompt engineering that survives production: role prompting, few-shot, chain-of-thought,
  XML/delimiter structuring, prompt templating
- **Structured output** — JSON schema / tool-forced output. This is what turns an LLM from a chatbot
  into a component you can `if`-statement on
- Function calling / tool use
- Streaming, retries, timeouts, rate limits, exponential backoff
- Cost and latency: prompt caching, batching, choosing a small model when a small model suffices
- Orchestration frameworks — learn one, but write raw API calls first so you know what it's hiding

### Courses
| Course | Provider | Time | Cost |
| --- | --- | --- | --- |
| [Anthropic Prompt Engineering Interactive Tutorial](https://github.com/anthropics/prompt-eng-interactive-tutorial) | Anthropic | 6h | Free |
| [Anthropic Academy — Claude API development](https://www.anthropic.com/learn) | Anthropic | 8h | Free |
| [ChatGPT Prompt Engineering for Developers](https://www.deeplearning.ai/short-courses/chatgpt-prompt-engineering-for-developers/) | DeepLearning.AI | 2h | Free |
| [Building Systems with the ChatGPT API](https://www.deeplearning.ai/short-courses/building-systems-with-chatgpt/) | DeepLearning.AI | 2h | Free |
| [Functions, Tools and Agents with LangChain](https://www.deeplearning.ai/short-courses/functions-tools-agents-langchain/) | DeepLearning.AI | 2h | Free |
| [LLM Bootcamp](https://fullstackdeeplearning.com/llm-bootcamp/) | Full Stack Deep Learning | 8h | Free |

### Build
**Project 1 (portfolio):** A production-shaped LLM feature — e.g. a service that takes a messy
document and returns validated, typed JSON. Must have: retries, streaming, cost logging, a test
suite that runs against recorded responses, and a `README` explaining your prompt design choices.

### Done when
Your app doesn't crash when the model returns malformed JSON, and you know what that request cost.

---

## Phase 3 — Retrieval-Augmented Generation (Weeks 10–13)

**Goal:** RAG is still the #1 thing companies hire GenAI developers to build. Get good at it —
including the unglamorous parts.

Naive RAG is a weekend project. *Good* RAG is a career skill. The gap between them is where the job
is.

### Learn
- Document ingestion: PDFs, HTML, tables, code — the messy reality
- Chunking strategies: fixed, recursive, semantic, and why chunk size ruins retrieval
- Embedding models: choosing one, dimensions, domain fit, and when to fine-tune
- Vector stores: pgvector, Qdrant, Weaviate, Pinecone, Chroma, FAISS
- **Hybrid search**: BM25 + dense vectors. Almost always beats pure vector search
- Reranking (cross-encoders) — the highest-ROI single upgrade to most RAG systems
- Query transformation: rewriting, decomposition, HyDE
- Retrieval evaluation: recall@k, MRR, NDCG — measure retrieval separately from generation
- Citations and grounding; handling "I don't know"
- Long-context vs RAG: when to just paste the whole document in

### Courses
| Course | Provider | Time | Cost |
| --- | --- | --- | --- |
| [Building and Evaluating Advanced RAG](https://www.deeplearning.ai/short-courses/building-evaluating-advanced-rag/) | DeepLearning.AI | 2h | Free |
| [Vector Databases: from Embeddings to Applications](https://www.deeplearning.ai/short-courses/vector-databases-embeddings-applications/) | DeepLearning.AI | 2h | Free |
| [Preprocessing Unstructured Data for LLM Applications](https://www.deeplearning.ai/short-courses/preprocessing-unstructured-data-for-llm-applications/) | DeepLearning.AI | 2h | Free |
| [Building Applications with Vector Databases](https://www.deeplearning.ai/short-courses/building-applications-vector-databases/) | DeepLearning.AI | 1h | Free |
| [Advanced RAG techniques](https://github.com/NirDiamant/RAG_Techniques) *(repo — work through it)* | Nir Diamant | 10h | Free |

### Build
**Project 2 (portfolio):** A RAG system over a corpus that *you* have a reason to care about — your
company's docs, a regulation, a game's rules, a codebase. Requirements:

1. A gold set of ≥50 question/answer pairs you wrote by hand
2. Retrieval metrics reported *before* and *after* adding hybrid search + reranking
3. Inline citations in every answer
4. A written analysis of the failure cases

That evaluation table is the single most impressive thing you can put in a portfolio.

### Done when
You can say "our retrieval recall@10 went from 0.61 to 0.88 by adding BM25 and a cross-encoder
reranker" about your own project.

---

## Phase 4 — Agents & Tool Use (Weeks 14–17)

**Goal:** Build systems where the model decides what to do next — and doesn't spiral.

### Learn
- The agent loop: reason → act → observe → repeat
- Tool/function design: how tool descriptions are prompts, and bad ones cause bad behavior
- ReAct, plan-and-execute, reflection patterns
- Memory: short-term (conversation), long-term (vector), episodic
- Multi-agent: supervisor/worker, handoffs — and when a single agent with better tools is simpler
- **Model Context Protocol (MCP)** — the emerging standard for connecting models to tools and data
- Failure modes: infinite loops, cost explosions, tool-call hallucination, prompt injection via
  tool output
- Guardrails: step limits, budget caps, human-in-the-loop approval for destructive actions
- Frameworks: LangGraph, CrewAI, OpenAI Agents SDK, Claude Agent SDK, PydanticAI

### Courses
| Course | Provider | Time | Cost |
| --- | --- | --- | --- |
| [MCP: Build Rich-Context AI Apps with Anthropic](https://www.deeplearning.ai/short-courses/mcp-build-rich-context-ai-apps-with-anthropic/) | DeepLearning.AI | 2h | Free |
| [Hugging Face Agents Course](https://huggingface.co/learn/agents-course) | Hugging Face | 12h | Free |
| [AI Agents in LangGraph](https://www.deeplearning.ai/short-courses/ai-agents-in-langgraph/) | DeepLearning.AI | 2h | Free |
| [Multi AI Agent Systems with crewAI](https://www.deeplearning.ai/short-courses/multi-ai-agent-systems-with-crewai/) | DeepLearning.AI | 2h | Free |
| [Building Effective Agents](https://www.anthropic.com/engineering/building-effective-agents) *(essay — read it twice)* | Anthropic | 1h | Free |

### Build
**Project 3 (portfolio):** An agent that does something genuinely useful and slightly dangerous —
files PRs, triages issues, queries a real database, books something. Requirements: a hard step
limit, a spend cap, an audit log of every tool call, and human approval before any write.

Bonus: expose your tools over MCP so the agent works in Claude Desktop / Claude Code too.

### Done when
Your agent has run 100+ times and you can show the traces, the cost per run, and the failure rate.

---

## Phase 5 — Evaluation, Observability & Safety (Weeks 18–20)

**Goal:** The skill that separates a demo builder from an engineer. Most people skip this. Don't —
it's disproportionately what senior interviewers probe.

### Learn
- Why you cannot ship LLM features on vibes
- Building an eval set: golden datasets, from real production traffic
- Eval types: exact match, similarity, **LLM-as-judge** (and its biases), human review
- Regression testing prompts — treat prompts as versioned artifacts
- Observability: tracing, token accounting, latency percentiles, per-feature cost
- Tools: LangSmith, Langfuse, Braintrust, Phoenix/Arize, Weights & Biases Weave
- Guardrails: input validation, output filtering, PII redaction, refusal handling
- **Prompt injection** — direct and indirect. This is *the* security topic in GenAI
- OWASP Top 10 for LLM Applications
- Responsible AI: bias, transparency, EU AI Act awareness

### Courses
| Course | Provider | Time | Cost |
| --- | --- | --- | --- |
| [Evaluating AI Agents](https://www.deeplearning.ai/short-courses/evaluating-ai-agents/) | DeepLearning.AI | 2h | Free |
| [Automated Testing for LLMOps](https://www.deeplearning.ai/short-courses/automated-testing-llmops/) | DeepLearning.AI | 2h | Free |
| [Quality and Safety for LLM Applications](https://www.deeplearning.ai/short-courses/quality-safety-llm-applications/) | DeepLearning.AI | 2h | Free |
| [Red Teaming LLM Applications](https://www.deeplearning.ai/short-courses/red-teaming-llm-applications/) | DeepLearning.AI | 1h | Free |
| [OWASP Top 10 for LLM Applications](https://genai.owasp.org/) | OWASP | 3h | Free |

### Build
Go back to **Projects 1–3** and add: an eval suite in CI, tracing with Langfuse or LangSmith, and a
dashboard showing cost/latency/quality over time. Write a blog post: *"What I learned evaluating my
own RAG system."*

### Done when
You can prove — with numbers — that a prompt change made your system better rather than just
different.

---

## Phase 6 — Fine-tuning & Serving (Weeks 21–23)

**Goal:** Know when *not* to fine-tune, and be able to do it when the answer is yes.

Fine-tuning is the most over-requested and least-often-correct solution. Learn it so you can push
back credibly — and execute when it's genuinely the right call.

### Learn
- The decision tree: prompt → few-shot → RAG → fine-tune. Try in that order
- What fine-tuning *does* fix (format, tone, domain style, latency via smaller model) and what it
  *doesn't* (adding facts — that's RAG)
- PEFT: **LoRA** and QLoRA
- Dataset construction — the actual hard part. Quality over quantity
- Preference tuning: DPO
- Quantization: GPTQ, AWQ, GGUF, and the quality/speed tradeoff
- Serving: vLLM, TGI, Ollama, llama.cpp; batching, KV cache, throughput vs latency
- Open-weight models: Llama, Mistral, Qwen, Gemma, DeepSeek — and licensing

### Courses
| Course | Provider | Time | Cost |
| --- | --- | --- | --- |
| [Finetuning Large Language Models](https://www.deeplearning.ai/short-courses/finetuning-large-language-models/) | DeepLearning.AI | 2h | Free |
| [Quantization Fundamentals](https://www.deeplearning.ai/short-courses/quantization-fundamentals-with-hugging-face/) | DeepLearning.AI | 2h | Free |
| [Efficiently Serving LLMs](https://www.deeplearning.ai/short-courses/efficiently-serving-llms/) | DeepLearning.AI | 2h | Free |
| [Hugging Face — Fine-tuning chapters](https://huggingface.co/learn/llm-course) | Hugging Face | 6h | Free |

### Build
Fine-tune a small open model (7B or under) with LoRA on a narrow task, on a free Colab/Kaggle GPU.
Then **prove with an eval** whether it beat a well-prompted frontier model. Publish the honest
result either way — "I fine-tuned and it lost to a good prompt" is a great, credible blog post.

### Done when
You can give a one-minute answer to *"should we fine-tune?"* that starts with "what have you tried
first?"

---

## Phase 7 — Ship, Portfolio & Get Hired (Week 24+)

**Goal:** Convert 6 months of learning into offers.

### Learn
- Deployment: containerize, deploy to a cloud, add a real frontend
- LLMOps: prompt versioning, model version pinning, canary rollouts, fallback models
- Cost engineering: caching, model routing (small model first, escalate on failure), batch APIs
- Reading the field: keep up without drowning

### Do
1. **Polish 3 projects.** Deployed, documented, with a demo video or GIF in the README.
   Depth > breadth — three excellent repos beat twelve tutorials.
2. **Write.** 3–5 technical blog posts about problems you actually hit. This is how strangers find
   you.
3. **Contribute.** One meaningful PR to an open-source GenAI library.
4. **Optional certification** — see [courses.md](courses.md#certifications). Certs rarely get you
   hired on their own, but they pass HR filters and give structure. Best ROI: the cloud one
   matching your target employers' stack.
5. **Reframe your resume.** You are not "learning AI" — you are a software engineer who ships
   LLM-powered systems. Lead with shipped systems and measured results.
6. **Interview prep** — see [interview-prep.md](interview-prep.md).

### Done when
You're getting technical screens. Then keep building while you interview.

---

## Rules that make this work

1. **Build > watch.** A course you watched and didn't build from is entertainment. Cap yourself at
   2 hours of video per 6 hours of coding.
2. **Write raw API calls before frameworks.** Frameworks hide the thing you're trying to learn.
   Learn LangChain *after* you've hand-rolled the loop it abstracts.
3. **Ship something ugly in week 3.** Not week 20.
4. **Learn in public.** A README, a blog post, a LinkedIn post per phase. The compounding effect on
   your job search is larger than the extra content you'd have consumed instead.
5. **Don't chase every new model.** The fundamentals in Phases 1–5 have been stable for years. The
   model names change every quarter; the engineering doesn't.
6. **Set a monthly API budget** ($20–50 is plenty) and use small/cheap models while developing.

---

## Why this is a realistic goal, not a stretch

Six months of steady, part-time effort is genuinely enough to become a credible, hireable GenAI
engineer — **especially with 2 years of software experience already behind you.** That experience
is your biggest advantage here, not a gap you're behind on. Most people entering this field can get
a chatbot to say something clever; very few can ship, test, and operate software that depends on
one. You already know how to do that part. This roadmap teaches you the rest.

This plan points squarely at the **AI Engineer** role, and that's also where almost all of the
current hiring is happening — companies building products on top of models, not research labs. The
goal and the opportunity line up, which is exactly what makes this worth the six months.

---

## Contributing

Found a dead link, a better course, or a phase that's out of date? Open an issue or a PR.

## License

[MIT](LICENSE) — use it, fork it, adapt it.
