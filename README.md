Ops Tech Builder Challenge – Python + AI Integration

This repository contains a technical implementation of all four parts of the Ops Tech Builder coding task:
---

## Part 1: LLM API Endpoint

- Built with **FastAPI**
- Exposes one endpoint: `POST /summarize`
- Accepts JSON: `{ "text": "..." }`
- Calls **OpenAI or Claude** (switchable via `"provider"` key)
- Returns JSON: `{ "summary": "..." }`

File: `api/main.py`

---

## Part 2: Excel/CSV Parser

- Accepts `.csv` or `.xlsx` file upload via `/upload_file`
- Extracts key fields: `order_id`, `vendor`, `amount` (handles messy data)
- Returns clean JSON list

File: `parser/file_parser.py`

Dependencies: `pandas`, `openpyxl`, `python-multipart`

---

## Part 3: Prompt Comparison

- Designed prompts to extract: **names**, **dates**, **locations**
- Ran the same input on GPT & Claude
- Documented output differences and normalization strategy

Folder: `prompts/`

---

Part 4: SQL Query

> Find top 5 vendors by total paid amount over the last 30 days

File: `sql/top_vendors_last_30_days.sql`

### Example:

```sql
SELECT
    vendor,
    SUM(amount) AS total_amount
FROM
    invoices
WHERE
    created_at >= NOW() - INTERVAL '30 days'
    AND status = 'paid'
GROUP BY
    vendor
ORDER BY
    total_amount DESC
LIMIT 5;
```
---
Setup Instructions
# 1. Create venv and install dependencies
python -m venv venv
venv\Scripts\activate
pip install -r requirements.txt

# 2. Run FastAPI server
uvicorn api.main:app --reload
