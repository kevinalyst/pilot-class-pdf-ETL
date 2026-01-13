# Classroom Pilot ETL + Equity Analysis (PDF → OCR → Lakehouse → BI)

End-to-end pipeline to extract handwritten Chinese questionnaire responses from PDFs, validate/clean them, load into Databricks, and analyze **experience lift** and **equity gap reduction** between under-resourced and resourced schools.

## Architecture

Google Drive (PDFs) → **n8n Cloud** (batch + dedupe) → **Azure Document Intelligence (prebuilt-layout)** → n8n parsing (Q1–Q17 + confidence) + AI agent for **Q18** cleanup/translation → Google Sheets (staging) → **Databricks** (`fact_questionnaire_long`) → Power BI + Databricks Python stats.

## Study groups

* **Under-resourced:** `school_b`, `school_e`
* **Resourced:** `school_c`, `school_d`

## Data outputs

* **Q1–Q12:** learning/experience (1–5) for AI vs baseline
* **Q13–Q17:** AI tool experience (AI only)
* **Q18:** free-text feedback (AI only; cleaned + EN translation)

## Databricks model

**`workspace.pilot_class_data.fact_questionnaire_long`** (long format)

* `respondent_key`, `school_id`, `ai_used` (Y/N)
* `question_num`, `question_code`, `score`, `confidence`
* `text_answer` (Q18), lineage fields (`drive_file_id`, `file_name`)

## Metrics

* **Experience Lift (Q1–Q12):** Avg(AI) − Avg(Baseline)
* **Equity Gap:** Avg(Resourced) − Avg(Under)
* **Gap Reduction:** Gap(Baseline) − Gap(AI)
* **Gap Reduction (%):** Gap Reduction / Gap(Baseline)

## Statistical tests (Databricks Python)

* Respondent-level mean Q1–Q12 (avoid pseudo-replication)
* Welch t-test for **Experience Lift**
* Welch-style linear-contrast test for **Gap Reduction / Equity DiD**
* 95% CI + optional bootstrap sensitivity

## Notes

* Batch + throttle n8n (POST + poll) to avoid 429s
* Dedupe Drive files by `drive_file_id` already in Sheets/Delta
* Q18 agent returns strict JSON: `{Islegit: Y/N, content: ""|EN_text}`
