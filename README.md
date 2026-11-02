# AI Output Quality Evaluation Dashboard (Python)

Streamlit + SQLite + Plotly app that scores AI responses on Relevance, Completeness, Clarity and Factual Support (0-10 each).
Overall = average x 10 (0-100): 90+ Excellent, 75-89 Good, 60-74 Average, below 60 Needs Improvement.

## Run

```bash
python -m venv .venv && source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install -r requirements.txt
streamlit run app.py
```
Opens at http://localhost:8501. The SQLite file `evaluations.db` is created on first run with 30 labelled sample records.

## Pages
Overview (KPIs, trend, status mix, recent-evaluation selector) · New Evaluation (validated form, edit support) ·
Evaluation History (search, filters, click a row to open it; edit, delete, CSV and PDF export) ·
Analytics (7/30/90 days or all time) · Compare Responses (new prompt + two responses, or two saved evaluations) ·
Reports (CSV and detailed PDF) · Settings.

## Scoring modes
- **Demo mode (default):** deterministic text heuristic (keyword overlap, length, sentence structure). It is NOT an AI judge.
  Factual Support stays low and is flagged "unverified" unless sources or an expected answer are given; nothing is ever marked verified.
- **AI judge (optional):** get a key at console.anthropic.com, then either copy `.env.example` to `.env` and paste it there, or paste it on the Settings page (kept in memory only). Never commit `.env`. If the call fails, the app falls back to demo mode and records that.

## Files
`app.py` UI · `core.py` scoring, feedback, SQLite, CSV/PDF · `requirements.txt`

Environment variables: `EVAL_DB` (database path), `EVAL_NO_SEED=1` (start empty).
