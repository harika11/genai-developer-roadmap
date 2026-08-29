# Tools & Libraries

The landscape churns fast. Categories are stable; specific tools are not. Learn the category first,
then pick a tool.

**Rule:** learn one tool per category deeply rather than five superficially. And write raw API calls
before you adopt a framework — otherwise you learn the framework, not the concept.

---

## Model providers

| | Notes |
| --- | --- |
| **Anthropic (Claude)** | Strong at long context, code, tool use, and following complex instructions. `anthropic` SDK. |
| **OpenAI** | Largest ecosystem, most tutorials written against it. |
| **Google (Gemini)** | Very long context windows, competitive pricing. |
| **Open weights** — Llama, Mistral, Qwen, Gemma, DeepSeek | Self-hosting, privacy, fine-tuning, cost control. |
| **Aggregators** — OpenRouter, Together, Groq, Fireworks | One API across many models; useful for benchmarking and fallback routing. |

Build against **at least two** providers. Provider lock-in is a real risk in this field, and swapping
models is a routine production requirement.

---

## Orchestration frameworks

| Tool | Use when |
| --- | --- |
| **Raw SDK calls** | Always start here. Most production systems need less framework than you think. |
| **LangChain / LangGraph** | Largest ecosystem; LangGraph is the better part — explicit graph-based agent control flow. |
| **LlamaIndex** | Strongest for RAG-heavy and document-centric work. |
| **PydanticAI** | Type-safe, minimal, familiar if you like Pydantic. |
| **OpenAI Agents SDK / Claude Agent SDK** | Provider-native agent loops with less abstraction. |
| **CrewAI / AutoGen** | Multi-agent role-based orchestration. |
| **Instructor / Outlines** | Structured output and constrained generation. |

---

## Vector stores & retrieval

| Tool | Use when |
| --- | --- |
| **pgvector** | You already run Postgres. Usually the right default — one less system to operate. |
| **Qdrant** | Excellent filtering, self-hostable, good defaults. |
| **Chroma** | Fastest path to a local prototype. |
| **Weaviate** | Built-in hybrid search, module ecosystem. |
| **Pinecone** | Fully managed, scales without you thinking about it. |
| **FAISS** | In-process, library-not-service, great for experiments. |
| **Elasticsearch / OpenSearch** | You need BM25 and mature filtering alongside vectors. |

**Embeddings:** OpenAI `text-embedding-3`, Cohere Embed, Voyage AI, or open models via
`sentence-transformers` (BGE, E5, GTE). Check the [MTEB leaderboard](https://huggingface.co/spaces/mteb/leaderboard)
— but test on *your* data, since leaderboard rank rarely survives a domain shift.

**Reranking:** Cohere Rerank, Voyage rerank, or an open cross-encoder (`bge-reranker`). Usually the
single highest-ROI upgrade to a RAG pipeline.

---

## Document processing

`unstructured`, `LlamaParse`, `Docling`, `PyMuPDF`, `pdfplumber`, `Marker`, `Tesseract`.

Reality check: **PDF parsing is the hardest unglamorous part of most RAG projects.** Budget real
time for it. Tables and multi-column layouts break naive extraction.

---

## Evaluation & observability

| Tool | Notes |
| --- | --- |
| **Langfuse** | Open-source tracing + evals; self-hostable. Great default. |
| **LangSmith** | Deeply integrated with LangChain. |
| **Braintrust** | Evals-first workflow. |
| **Phoenix / Arize** | Open-source observability, strong on RAG-specific analysis. |
| **W&B Weave** | If your org already uses Weights & Biases. |
| **Ragas** | RAG-specific metrics (faithfulness, answer relevance, context precision). |
| **DeepEval / promptfoo** | Pytest-style LLM assertions; promptfoo is great in CI. |
| **OpenTelemetry + GenAI semantic conventions** | The vendor-neutral path. |

---

## Fine-tuning & serving

**Fine-tuning:** Hugging Face `transformers` + `peft` + `trl`, Axolotl, Unsloth (fast, low-VRAM),
Torchtune. Provider-hosted fine-tuning APIs when you don't want infra.

**Serving:** vLLM (the throughput standard), TGI, SGLang, Ollama (local dev), llama.cpp / GGUF
(CPU and edge), LM Studio (GUI).

**Compute:** Colab / Kaggle (free T4s — enough for LoRA on a 7B), Modal, RunPod, Lambda Labs,
Vast.ai. You do not need to buy a GPU to complete this roadmap.

---

## Agent infrastructure

- **MCP (Model Context Protocol)** — standard for exposing tools and data to models
- **Sandboxing** — E2B, Modal, Docker, Firecracker for running model-generated code
- **Browser automation** — Playwright, Browserbase
- **Queues** — Temporal, Celery, or plain Redis for long-running agent jobs

---

## Local dev setup

```bash
# Recommended: uv for env + package management
uv init my-genai-app && cd my-genai-app
uv add anthropic openai pydantic python-dotenv
uv add --dev pytest ruff mypy

# Local models
# https://ollama.com  →  ollama run llama3.2
```

**Habits worth forming from day one**
- Secrets in `.env`, `.env` in `.gitignore`, an `.env.example` committed
- Log every request's model, tokens, latency, and cost — from your very first project
- Cache responses during development (`diskcache` or a simple JSON cache); your API bill and your
  iteration speed will both thank you
- Pin model versions explicitly — never rely on a floating alias in production
- Set a hard monthly spend limit in every provider dashboard before you write a line of code
