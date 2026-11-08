# Malav Joshi
**I build ML systems that don't die.**

ML Infrastructure & Reliability — statistician by training (B.Sc. + two data Master's), operations engineer by experience (3 years at TD Insurance: 45→90% automation completion, $60K saved annually), ML infrastructure builder by choice. Now shipping production-grade ML systems in public.

> **How I work:** ship small · tag everything · automate the boring checks · write the runbook before the incident · test the alarm by setting it off.

---

## Work — the dots are honest
🟢 shipped · 🟡 in progress · ⚪ planned

### 🟡 [llm-reliability-platform](https://github.com/5Malav/llm-reliability-platform) — current build · `v1.5`
**A RAG system where the monitoring is the product.** It answers Supabase documentation questions with citations, refuses when it shouldn't answer — and every answer is traced, scored and graphed, so a wrong answer can't hide behind a confident tone.

![Grafana dashboard: errors, grounding score, fallback-model share, fake citations](https://raw.githubusercontent.com/5Malav/llm-reliability-platform/main/docs/images/dashboard-quality.png)

**Measured against 120 hand-written questions:**

| | |
|---|---|
| Unanswerable questions correctly declined | **35 / 35 — zero hallucinated answers** |
| Retrieval: right document in the top 5 | **70 / 85** · bare error codes & function names **20 / 20** |
| Answers with sources on their claims | **58%** of claim sentences, scored on every answer |
| Cost per question | **$0.0040** — agrees across 4 independent sources |

- 🟢 **Reproducible corpus** — 811 source docs → 2,654 chunks, pinned to a commit SHA (not scraped) · Postgres + pgvector
- 🟢 **Hybrid retrieval** — vector + BM25 fused with weighted RRF. Keyword weight chosen by a measured sweep, not a guess: +7 correct documents over vector search alone
- 🟢 **Calibrated refusal** — a distance gate refuses out-of-scope questions **before** the LLM is called: $0.00 and sub-second
- 🟢 **Multi-provider failover** — Claude → OpenAI via LiteLLM
- 🟢 **Golden eval set** — 120 questions written by hand, 29% deliberately unanswerable
- 🟢 **Tracing** — every query a Langfuse trace (OpenTelemetry underneath): retrieval, LLM call, tokens, cost, outcome
- 🟢 **Metrics + dashboard** — Prometheus + a 10-panel Grafana dashboard **provisioned as code**; deleted and rebuilt from the repo to prove it
- 🟢 **Grounding score on every answer** — free, instant, runs on 100% of traffic; flags citations to sources that don't exist
- 🟡 **Next:** deploy to Cloud Run with a public dashboard · CI that blocks deploys when eval quality drops · LangGraph · guardrails

**The incident I'm proudest of catching:** my primary model's API key expired. The fallback took over — every request succeeded, latency normal, zero errors. But the grounding score on the same question fell from **62% to 25%**, because the backup model cited far less. *Failover protected uptime, not quality* — and only the quality score showed it.

**13 incidents and 5 observations logged so far** — [almost every one caught by cross-checking numbers, not by an error message](https://github.com/5Malav/llm-reliability-platform/blob/main/INCIDENTS.md). Four were bugs in my own measurement, including a dashboard panel that couldn't see the first fallback until I tested it by breaking the API key on purpose.

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
- 🟢 **LLM reliability:** Langfuse · OpenTelemetry · hybrid retrieval (BM25 + vector, RRF) · golden-set evaluation · grounding checks
- 🟢 **Shipped to production with:** GCP (Cloud Run, GCS, Artifact Registry) · Terraform · Prometheus · Grafana · Evidently · Locust
- ⚪ **Next up:** LangGraph · Guardrails · eval-gated CI/CD

---

## Find me

**[Portfolio](https://5malav.github.io)** · **[LinkedIn](https://linkedin.com/in/malavjoshi5)** · **malavmjoshi@gmail.com**

Ahmedabad, India (IST) · open to remote & relocation · **open to ML Infrastructure / MLOps / Platform roles**

Always happy to talk production ML, observability, and why every deploy needs an undo.
