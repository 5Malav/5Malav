# Malav Joshi
**I build ML systems that don't die.**

ML Infrastructure & Reliability — statistician by training (B.Sc. + two data Master's), operations engineer by experience (3 years at TD Insurance: 45→90% automation completion, $60K saved annually), ML infrastructure builder by choice. Now shipping production-grade ML pipelines in public.

> **How I work:** ship small · tag everything · automate the boring checks · write the runbook before the incident.

---

## Work — the dots are honest
🟢 shipped · 🟡 in progress · ⚪ planned

### 🟡 [llm-reliability-platform](https://github.com/5Malav/llm-reliability-platform) — current build
**A RAG system optimized for calibrated honesty, not just accuracy.** It answers Supabase documentation questions with citations — and refuses, with measured justification, when it shouldn't answer. The observability layer is the product; the assistant is the workload being monitored.

- 🟢 **Reproducible corpus** — 811 source docs → 792 cleaned → 2,654 chunks, pinned to a commit SHA (not scraped)
- 🟢 **Postgres + pgvector** — 1536d embeddings, idempotent upserts, no separate vector DB
- 🟢 **Grounded answers with citations** — every claim carries a source; the model answers from retrieved context, not training memory
- 🟢 **Calibrated refusal** — answerable questions retrieve at 0.28–0.48 cosine distance, out-of-scope at 0.72+. A 0.65 gate refuses **before** the LLM is called: $0.00 and sub-second instead of 3,000 tokens
- 🟢 **Multi-provider failover** — Claude → OpenAI via LiteLLM; a single provider is a single point of failure
- 🟢 **Telemetry from commit one** — per-query cost, retrieval-vs-generation latency split, refusal reason, all logged
- 🟡 **Next:** hybrid retrieval · golden eval set · public dashboards · CI that blocks deploys on quality regression

**$0.0047 per answered query. $0.00 per refused one.** Six incidents found and fixed so far — [every one caught by cross-checking numbers, not by an error message](https://github.com/5Malav/llm-reliability-platform/blob/main/INCIDENTS.md).

### 🟢 [churn-mlops](https://github.com/5Malav/churn-mlops) — flagship · [**live demo →**](https://churn-api-215271667398.asia-south1.run.app/docs)
An end-to-end churn classifier treated like software, not a notebook. **Ten tagged releases (v1.0 → v2.0)** — each documented, reproducible, and rollback-able. It's deployed, monitored, and load-tested; the whole system is live at the URL above.

- 🟢 **LightGBM + Optuna** — tuned model, ROC AUC 0.91, ~500× faster training than the baseline
- 🟢 **Pandera** schemas + **Pydantic** validation — data contracts on every batch and every request
- 🟢 **MLflow** experiment tracking · **DVC** data & model versioning (remote on **GCS**)
- 🟢 **Dockerized** serving (lean 816MB image, no train/serve dependency drift)
- 🟢 **CI on every push** — pytest · ruff · black via GitHub Actions
- 🟢 **Prefect** orchestration with automatic task retries (self-healing pipeline)
- 🟢 **Live on GCP Cloud Run** — serverless, scale-to-zero, public HTTPS endpoint
- 🟢 **Terraform** — the bucket, the Cloud Run service, and IAM defined as code
- 🟢 **Prometheus + Grafana** — request-rate, latency and error dashboards (RED method)
- 🟢 **Evidently** drift detection — catches when incoming data diverges from training
- 🟢 **Locust** load tested — ~80 req/s single-instance ceiling, graceful degradation, zero failures

### 🟢 [Local-RAG](https://github.com/5Malav/Local-RAG) — retrieval that never phones home
A fully local RAG system — no cloud, no API keys, total privacy. Ingests PDF, DOCX and TXT documents, chunks and embeds them with sentence-transformers, stores vectors in **FAISS**, and answers questions with **Mistral 7B via Ollama**, wrapped in a Gradio UI. Built for documents that can't leave the machine.

### 🟢 SQL systems — [Enterprise SQL Analytics](https://github.com/5Malav/Enterprise-SQL-Analytics-Project) · [Business Reporting](https://github.com/5Malav/Relational-Business-Reporting-System)
Two normalized schemas designed from scratch and 88 production-style queries across them — window functions, recursive CTEs, cohort analysis, revenue trends, query optimization. The boring fundamentals every reliable data system stands on.

---

## The path: ops → ML infra

For three years I was the person developers called before shipping an automation — and the person operations called when it broke. The vocabulary changes; the job doesn't.

| What I did at TD Insurance | What it's called in ML infra |
| --- | --- |
| Owned SLA compliance across underwriting operations | SLOs & error budgets |
| UAT + post-deployment validation on every release | CI gates, smoke tests, tagged releases |
| Monitored production bots, triaged failures, root-caused errors | Observability, incident response, runbooks |
| Escalation paths for failures I couldn't resolve alone | Graceful degradation & human-in-the-loop |

---

## Stack

- 🟢 **Daily:** Python · SQL / PostgreSQL · pgvector · scikit-learn · PyTorch · Pandas · Pandera · Docker · MLflow · DVC · Prefect · FastAPI · Git / GitHub Actions · FAISS · Sentence Transformers · Ollama · LiteLLM
- 🟢 **Shipped to production with:** GCP (Cloud Run, GCS, Artifact Registry) · Terraform · Prometheus · Grafana · Evidently · Locust

---

## Find me

**[Portfolio](https://5malav.github.io)** · **[LinkedIn](https://linkedin.com/in/malavjoshi5)** · **malavmjoshi@gmail.com**

Ahmedabad, India (IST) · open to remote & relocation · **open to ML Infrastructure / MLOps / Platform roles**

Always happy to talk production ML, observability, and why every deploy needs an undo.
