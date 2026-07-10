# Malav Joshi
**I build ML systems that don't die.**

ML Infrastructure & Reliability — statistician by training (B.Sc. + two data Master's), operations engineer by experience (3 years at TD Insurance: 45→90% automation completion, $60K saved annually), ML infrastructure builder by choice. Now shipping production-grade ML pipelines in public.

> **How I work:** ship small · tag everything · automate the boring checks · write the runbook before the incident.

---

## Work — the dots are honest
🟢 shipped · 🟡 in progress · ⚪ planned

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
<!-- TODO: record a 10–15s GIF of the Gradio UI answering a question and embed it here -->

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

---

## Stack
- 🟢 **Daily:** Python · SQL / PostgreSQL · scikit-learn · PyTorch · Pandas · Pandera · Docker · MLflow · DVC · Prefect · FastAPI · Git / GitHub Actions · FAISS · Sentence Transformers · Ollama · LangChain · Gradio
- 🟢 **Shipped to production with:** GCP (Cloud Run, GCS, Artifact Registry) · Terraform · Prometheus · Grafana · Evidently · Locust

---

## Find me
**[Portfolio](https://5malav.github.io)** · **[LinkedIn](https://linkedin.com/in/malavjoshi5)** · **malavmjoshi@gmail.com**

Ahmedabad, India (IST) · open to remote & relocation · **open to ML Infrastructure / MLOps / Platform roles**

Always happy to talk production ML, observability, and why every deploy needs an undo.
