# Portfolio Projects

Three excellent, deployed, documented projects beat twelve tutorial forks. These are the three the
[roadmap](README.md) builds toward, plus alternatives if a domain doesn't suit you.

## What makes a portfolio project actually work

Hiring managers skim. In 60 seconds they want to see:

1. **A README with a GIF or 60-second demo video at the top.** Not a wall of setup instructions.
2. **A problem statement** — what real thing does this solve, for whom?
3. **Numbers.** Latency, cost per request, accuracy, retrieval recall. Anything measured.
4. **A "what I'd do differently" section.** Signals engineering judgment more than a clean repo does.
5. **Tests, CI, and a deploy.** You're a software engineer applying to an AI role — lead with that
   advantage. Most applicants can't do this part.

What does *not* work: a fork of a tutorial, a Streamlit chatbot over a PDF with no evaluation, or
"AI-powered" anything that's a single API call.

---

## Project 1 — Structured Extraction Service (Phase 2)

**Build after Week 9.**

An API service that takes messy input (invoices, resumes, emails, support tickets, medical
referrals — pick a domain) and returns validated, typed JSON.

**Requirements**
- Pydantic schema, tool-forced / structured output — never regex over free text
- Retry with backoff on malformed output, and a repair loop that feeds the validation error back
- Streaming endpoint
- Cost + token logging per request
- Test suite running against **recorded** responses (so CI is free and deterministic)
- README section on your prompt design decisions and what you tried that failed

**Stretch:** model routing — try a small cheap model first, escalate to a larger one only when
validation fails. Report the cost saving.

**What it proves:** you can make a non-deterministic component behave like a reliable service.

---

## Project 2 — RAG System with a Real Evaluation (Phase 3)

**Build after Week 13. This is your flagship project.**

Retrieval-augmented Q&A over a corpus you have a genuine reason to care about — your company's
internal docs, a body of regulation, tax law, a game's rulebook, a large open-source codebase, your
own note archive.

**Requirements**
- Ingestion pipeline handling real messiness: PDFs, tables, headers, code blocks
- A hand-written gold set of **≥50 question/answer pairs** — you write these yourself, by hand
- **Baseline first:** naive chunking + pure vector search. Measure recall@k and answer quality.
- **Then improve:** hybrid search (BM25 + dense), a cross-encoder reranker, query rewriting
- A before/after metrics table in the README
- Inline citations on every answer, and honest "I don't know" when retrieval fails
- A written failure analysis: the 10 questions it still gets wrong, and why

**The before/after table is the single most valuable artifact in your whole portfolio.** It shows
you can measure and improve a system, not just wire one together.

**What it proves:** you can do the job that most GenAI job postings are literally describing.

---

## Project 3 — An Agent That Does Real Work (Phase 4)

**Build after Week 17.**

An agent with genuine tool access that does something useful and mildly consequential.

**Good ideas**
- A repo maintenance agent: triages issues, labels them, proposes fix PRs
- An on-call assistant: reads logs and dashboards, drafts an incident summary
- A research agent: given a question, searches, reads, and produces a cited report
- A database analyst: natural language → SQL → chart, with a read-only connection

**Non-negotiable requirements**
- Hard step limit and a spend cap that actually halts the run
- Full audit log of every tool call and its result
- Human approval gate before any write/destructive action
- Traces from 100+ real runs, with a measured success rate and cost per run

**Stretch:** expose the tools over **MCP** so the agent also works inside Claude Desktop / Claude
Code. This is a strong current signal.

**What it proves:** you understand agent failure modes — which is the thing separating people who
have shipped agents from people who have watched a demo.

---

## Alternative / stretch projects

| Project | Phase | Skills shown |
| --- | --- | --- |
| Local-first assistant (Ollama + small model, no cloud) | 6 | Quantization, serving, privacy constraints |
| Fine-tune vs prompt bake-off, with honest results | 6 | LoRA, dataset building, evaluation rigor |
| Prompt injection test harness for your own RAG app | 5 | Security, red teaming |
| Semantic search over your own 5 years of notes/email | 3 | Embeddings, ingestion, personal utility |
| Multimodal: doc + image understanding pipeline | 2–3 | Vision models, OCR alternatives |
| An eval harness others can use for their app | 5 | LLM-as-judge, open-source contribution |
| A useful MCP server published to the registry | 4 | MCP, tool design, ecosystem visibility |

---

## Publishing checklist

For each project, before you call it done:

- [ ] Demo GIF or video at the top of the README
- [ ] One-paragraph problem statement
- [ ] Architecture diagram (a simple mermaid diagram is fine)
- [ ] Setup that works from a cold clone — test it in a fresh container
- [ ] `.env.example`, and **no secrets in git history**
- [ ] Tests + CI badge
- [ ] Deployed somewhere with a live link (Render, Fly.io, Vercel, HF Spaces, Railway)
- [ ] Metrics section: cost, latency, quality
- [ ] "What I'd do differently" section
- [ ] A blog post linking to it
