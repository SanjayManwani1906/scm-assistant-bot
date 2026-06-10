# SCM Assistant — Trinamix Hiring Task (TX-JrAI-003)

**Submitted by:** Sanjay Manwani  
**Role Applied For:** Junior AI Engineer, Trinamix Inc.

---

## Public Chatbot URL

https://cloud.flowiseai.com/chatbot/5ef2a9bf-e96a-46dd-a917-62407a95adba

---

## Tech Stack

- **LLM:** Groq — `llama-3.3-70b-versatile` / `openai/gpt-oss-120b`
- **Embeddings:** Hugging Face Inference — `sentence-transformers/all-MiniLM-L6-v2` (384 dimensions)
- **Vector Store:** Qdrant Cloud (Free Tier)
- **Framework:** Flowise Cloud

---

## Chunking Configurations Evaluated

### Configuration 1 — Chunk Size: 1000, Overlap: 200 ✅ (Final Choice)

| File | Chunks |
|------|--------|
| SupplyChain_Governance_Policy_v3.2.pdf | 19 |
| supplier_performance_data.csv | 2000 |

### Configuration 2 — Chunk Size: 600, Overlap: 100

| File | Chunks |
|------|--------|
| SupplyChain_Governance_Policy_v3.2.pdf | 30 |
| supplier_performance_data.csv | 3999
|

### Why Configuration 1 Was Selected

Larger chunks preserved complete policy clauses, multi-sentence explanations, and full CSV row context. During testing, the smaller chunk configuration generated more chunks but frequently split policy sections mid-sentence, reducing retrieval quality for section-specific questions such as disruption response procedures and compliance requirements.

---

## Sample Q&A (Verbatim Chatbot Responses)

### Q1. Which Tier-3 suppliers have an active disruption flag, and what response level applies per policy?

> Tier‑3 supplier with an active disruption flag:
>
> **SUP‑080 — Maghreb Castworks**  
> Contract Tier: Tier‑3  
> Active Disruption: Regulatory enforcement pending  
> Risk Level: High
>
> The disruption category “regulatory enforcement” is listed in the policy as a mandatory Level 3 trigger regardless of risk level.
>
> Since the supplier is also classified as High Risk, a **Level 3 – Activate Response** applies, including:
>
> - Immediate escalation to the Chief Procurement Officer (CPO)
> - Alternate supplier activation for at least 40% of volume within 10 business days
> - Safety stock adjustment of +50% for affected SKUs
> - Root Cause Analysis (RCA) within 15 business days
>
> No other Tier‑3 suppliers in the provided data have an active disruption flag.

### Q2. Which suppliers qualify for the annual Volume Rebate Program and how many are there?

> Suppliers qualifying for the Volume Rebate Program:
>
> - **SUP‑107 — Cascade Pack Corp (Tier‑1)**
>
> Only **one supplier** qualifies because the policy requires Tier‑1 status, and SUP‑107 is the only Tier‑1 supplier represented in the provided data.

### Q3. Which region has the highest total PO value, and does it breach the concentration limit?

> Region spend summary:
>
> | Region | Total PO Value (USD) | Approx. Share |
> |---------|---------------------|--------------|
> | APAC | $556,195.50 | ~64% |
> | NA | $165,555.59 | ~19% |
> | EMEA | $144,655.36 | ~17% |
>
> **APAC** has the highest total PO value.
>
> The Supplier Governance & Compliance Policy states that no single region may account for more than 45% of annual procurement spend.
>
> Since APAC represents approximately 64% of total spend, the concentration limit is breached and a diversification plan is required.

### Q4. Which suppliers are on Supplier Watch List (SWL) status and what does it restrict?

> Hmm, I'm not sure.

### Q5. Which product category has the highest average defect rate and does it exceed the Tier-2 limit?

> Average defect rate by category:
>
> | Category | Average Defect Rate |
> |----------|-------------------|
> | Packaging Materials (PM) | 1.15% |
> | Electronic Components (EC) | 3.47% |
> | Raw Materials (RM) | 1.05% |
>
> **Electronic Components (EC)** has the highest average defect rate at **3.47%**.
>
> The Tier‑2 defect-rate threshold defined in the policy is **2.5%**.
>
> Therefore, the category average exceeds the Tier‑2 limit.

---

## Challenges and Limitations Encountered

During development, several platform and resource limitations affected experimentation and final response quality:

- I initially wanted to use **OpenAI Embeddings**, but free credits were unavailable.
- I also tested **Upstash Vector Store**, but quickly encountered daily request limits.
- Some LLM models exhausted their available token quotas during testing, limiting further experimentation.
- Due to these constraints, not every response produced by the chatbot is perfectly accurate.
- With additional iterations, higher limits, and more extensive tuning, answer quality can be improved further.

---

## Future Improvements

If more time and resources were available, I would focus on:

1. Adding a structured data-processing layer (SQL/Pandas) for accurate calculations instead of relying entirely on RAG retrieval.
2. Improving document chunking and retrieval settings through systematic evaluation.
3. Using metadata filtering (supplier, region, tier, etc.) to improve retrieval precision.
4. Adding a reranking step to improve the relevance of retrieved context before sending it to the LLM.
5. Implementing automated testing against benchmark questions to compare outputs after configuration changes.

---

## Notes

This submission demonstrates a Retrieval-Augmented Generation (RAG) workflow built in Flowise using policy documents and supplier performance data. The chatbot successfully answers several policy and analytics questions, while also highlighting areas where structured data processing and additional optimization would further improve reliability and accuracy.
