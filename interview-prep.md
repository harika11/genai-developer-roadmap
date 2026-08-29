# Interview Prep

What GenAI / AI Engineer interviews actually test, and how to prepare with 2 years of software
experience behind you.

---

## The loop, typically

| Round | What they test | How to prep |
| --- | --- | --- |
| Recruiter screen | Can you tell a coherent story about your transition? | Rehearse a 90-second narrative |
| Coding | Normal software engineering — often Python, sometimes an LLM API task | LeetCode-easy/medium + one live API exercise |
| LLM fundamentals | Do you understand what's under the hood? | Phase 1 of the roadmap |
| **System design: "design a RAG system"** | The core round. Almost always asked. | Practice out loud, 5+ times |
| Project deep-dive | Is your portfolio real? | Know your own numbers cold |
| Behavioral | Judgment, collaboration, handling ambiguity | STAR stories from your 2 years |

Your existing engineering experience is an advantage in rounds 1, 2, and 6. Most career-changers
from data science or bootcamps are weaker exactly there.

---

## Questions you should be able to answer cold

**Fundamentals**
- What is a token, and why doesn't token count match word count?
- Explain attention to a senior engineer who has never used an LLM.
- Why do LLMs hallucinate? What actually reduces it?
- Temperature vs top-p — when would you change each?
- What's the difference between a base model and an instruction-tuned model?
- What does the context window actually cost you — in money and in quality?

**RAG** *(expect the most questions here)*
- Walk me through a RAG pipeline end to end.
- How do you choose a chunk size? What breaks when it's wrong?
- Vector search vs keyword search — why is hybrid usually better?
- What is reranking and when is it worth the latency?
- How do you evaluate retrieval *separately* from generation?
- Your RAG returns irrelevant chunks. Walk me through your debugging.
- Long context windows are getting cheap. Is RAG dead? *(Answer: no — cost, latency, scale,
  freshness, citations, access control. Say why.)*

**Agents**
- What makes an agent different from a chatbot with tools?
- How do you stop an agent from looping forever or burning $500?
- How do you design a good tool description?
- When is a single well-prompted call better than an agent? *(Usually.)*

**Evaluation** *(where senior candidates separate themselves)*
- How do you know a prompt change made things better?
- What is LLM-as-judge, and what are its failure modes?
- How do you build an eval set for a feature that has no ground truth?
- How do you regression-test prompts in CI?

**Production**
- How do you handle a provider outage?
- How would you cut inference costs by 50%?
- What's your latency budget and where does the time go?
- Fine-tune vs RAG vs prompt engineering — how do you decide?

**Security**
- What is prompt injection? Direct vs indirect?
- Your agent reads web pages and can send email. What's the attack, and the mitigation?
- How do you handle PII in prompts and logs?

---

## The system design round: "Design a RAG system for X"

Have a repeatable structure. Practice saying it out loud until it's fluent.

1. **Clarify** — Corpus size? Update frequency? Users? Latency budget? Accuracy bar? Access control?
   Cost ceiling? *(Asking these is half the score.)*
2. **Ingestion** — Parsing, chunking strategy, metadata, handling updates and deletes
3. **Indexing** — Embedding model choice, vector store, hybrid index, sharding
4. **Retrieval** — Query rewriting, hybrid search, metadata filters, reranking, top-k
5. **Generation** — Prompt structure, citations, refusal behavior, streaming
6. **Evaluation** — Gold set, retrieval metrics, generation metrics, online feedback
7. **Production** — Caching, fallback models, rate limits, monitoring, cost per query
8. **Tradeoffs** — Name at least three you deliberately made, and why

The candidates who get offers are the ones who bring up **evaluation and cost unprompted**.

---

## Your narrative

Do not say: *"I'm transitioning into AI"* or *"I'm still learning."*

Say: *"I'm a software engineer with two years of production experience who now builds LLM-powered
systems. I've shipped a RAG service where I took retrieval recall from 0.61 to 0.88 with hybrid
search and reranking, and an agent that's run 400+ times with a measured 91% success rate at
$0.03 per run."*

Same facts. Completely different signal. **Numbers from your own projects are what make it
credible** — which is why the roadmap insists you measure things.

---

## Practical prep plan (4 weeks, alongside job applications)

| Week | Focus |
| --- | --- |
| 1 | Write your narrative. Rehearse your 3 project deep-dives with numbers. |
| 2 | RAG system design out loud, 5 times. Record yourself once — it's uncomfortable and useful. |
| 3 | Fundamentals flashcards. Mock interview with a friend or an LLM. |
| 4 | Coding practice (Python, medium difficulty) + behavioral STAR stories. |

---

## Where these jobs are

- Titles to search: **AI Engineer**, **GenAI Engineer**, **LLM Engineer**, **Applied AI Engineer**,
  **ML Engineer (LLM)**, **Forward Deployed Engineer**
- Companies building on top of models (far more hiring than the labs themselves)
- **Your current employer.** Genuinely the highest-probability path: propose an internal GenAI
  project, ship it, and become the person who does this. An internal transfer with a shipped system
  beats a cold application every time.
