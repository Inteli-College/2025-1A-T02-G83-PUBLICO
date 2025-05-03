# Vision
*Sprint 1 – Planning & Structuring*

> **Context**  
> During Module 1 we built **Lexun**, an AI‑powered knowledge‑management platform for the legal sector.  
> The underlying capability—ingesting unstructured content, transforming it into useful data, and creating value from that data—remains intact.  
> We are now **adjusting our domain focus**: from legal documents to **cooking‑recipe videos**.  
> All technical assets and lessons learned carry forward, while the new domain unlocks a rich source of consumption data for future products.

---

## Module 2 Overview

1. **Raw Experience First**  
   Deliver a minimal web interface and API where users paste a video link (YouTube, TikTok, Reels) or upload a file.  
   The system will  
   – fetch the video  
   – run automatic transcription (initially Whisper‑large or similar)  
   – extract a structured recipe (ingredients, steps, timings, utensils)  
   – store meta‑data (source, duration, category, post date, language)

2. **Demographic Consumption Dataset**  
   Persist each recipe alongside engagement metrics (views, likes, comments) obtained through public platform APIs and any available author profile data.  
   These records are the seed for later recommendation engines, trend dashboards, and B2B insight products for food‑industry stakeholders.

3. **Unchanged Value Chain**  
   *Ingestion → Transformation → Indexing → Application* — we reuse the existing stack (FastAPI, PostgreSQL, vector DB), reducing ramp‑up time and technical risk.

---

## Sprint Roadmap for Module 2

| Sprint | Core Focus | Key Deliverables |
|--------|------------|------------------|
| **1** | **Detailed Planning & Setup** | • Sprint‑by‑sprint delivery plan (this document)<br/>• Mapping of discontinued legal‑domain features<br/>• Initial risk matrix & success criteria<br/>• Technical kick‑off: repo branch, CI/CD, base schemas |
| **2** | PoC – **Video & Data Summarisation Agent** | • Functional transcription + parsing pipeline<br/>• Prototype agent that outputs recipe TL;DR + meta‑data<br/>• Quality metrics (WER, extraction F1) |
| **3** | **App Proposal** powered by PoC data | • Wireframes & flow diagrams<br/>• UX & API requirements<br/>• v1 architecture document |
| **4** | **Alpha Implementation** of the App | • Minimal frontend for upload/link<br/>• Scalable backend ingest → index<br/>• Cloud deployment<br/>• Basic logging & observability |
| **5** | **Results Synthesis** & Market Validation | • Analytical report on culinary‑consumption patterns<br/>• Beta‑user interviews (chefs, food creators, companies)<br/>• Positioning adjustments & next‑step plan |

---

## Sprint 1 – Activity Breakdown

### 1. Sprint‑by‑Sprint Delivery Plan  
* Formalise the table above in the chosen project‑management tool (Linear / Jira).  
* Define **Definition of Done** and acceptance metrics for each sprint.

### 2. Original‑Plan Adjustments  
* Catalogue legal‑sector features that will **no longer** be pursued (e.g., iManage integration, contract generator).  
* Mark corresponding issues as *on‑hold* for traceability—**do not delete code** at this stage.

### 3. Infrastructure & Repository  
* Create branch `module2/` inside the monorepo with a clear timeline.  
* Update CI/CD to include video‑processing dependencies (`ffmpeg`, Whisper).  
* Establish initial database schema (`recipe`, `video`, `source_metrics`).

### 4. Rapid Technical Research  
* Benchmark transcription providers (Whisper API, AssemblyAI, Deepgram).  
* Evaluate public‑data APIs (YouTube Data v3, compliant TikTok scraping).  
* List licences, rate limits, and cost estimates.

### 5. Governance & Metrics  
* Set KPIs for ingestion (avg processing time per video, cost/transcription, parsing success rate).  
* Prepare a sprint‑review template focused on *domain* (culinary) vs. *technology* lessons.

---

### Sprint 1 Success Criteria

| Dimension   | Target |
|-------------|--------|
| Planning    | Roadmap validated by the full team and stakeholders |
| Technical   | Hello‑video pipeline completes transcription and DB write in &lt; 5 minutes |
| Organisation| 100 % of obsolete legal features identified and frozen |
| Risk        | Top‑5 risks plus mitigation actions documented |

---

**Sprint 1 Closure**  
We conclude with a review showcasing the initial pipeline and a formal sign‑off of the roadmap. Only then will we move to the summarisation PoC in Sprint 2.

---