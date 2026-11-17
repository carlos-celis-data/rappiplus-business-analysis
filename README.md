# RappiPlus: From Data to Business Decisions

End-to-end analysis of the **RappiPlus** e-commerce service: data quality, profitability, conversion funnel, cohort retention, A/B testing and an interactive Tableau dashboard.

**Live dashboard:** [Tableau Public](https://public.tableau.com/app/profile/carlos.celis6323/viz/RappyPlusProyectobyCarlosCelis/Story1)

## Business questions

1. Can we trust the data?
2. Is the business profitable?
3. Where do users drop off in the funnel?
4. Do users come back?
5. Does the new checkout UI improve conversion?
6. How do we communicate the results to stakeholders?

## Tech stack

Python (pandas, statsmodels) · SQL (PostgreSQL via SQLAlchemy) · Tableau · Jupyter

## Key findings

| Area | Result |
|---|---|
| Data quality | 100 exact duplicate orders and 50 rows with missing quantity/price removed; negative quantities kept as legitimate returns |
| Outliers | 10 anomalous `Laptop-Gaming-16GB` orders (10,000–20,000 units each) accounted for **81.5% of reported revenue** |
| Profitability | Revenue falls from $51.97M to **$9.62M** after isolating the outliers; net profit from $5.97M to **$2.92M** (still positive) |
| Marketing | $2.87M total spend, evenly split across organic, paid search and social |
| Funnel | **49.47%** end-to-end conversion (first visit → purchase); biggest drops at *begin checkout → add payment info* (78.05% retained) and *add payment info → purchase* (77.65%) |
| Retention | Period-specific retention is stable at ~41–43% per week; rolling retention decays from ~85% (week 1) to ~64% (week 3) |
| A/B test | Control 15.69% vs. treatment 16.29% conversion; z = −0.81, p = 0.416 → **not statistically significant**, so the UI change is not recommended for rollout on this metric alone |

**Main insight:** the raw accounting overstated revenue by more than 5x because of 10 anomalous transactions. Detecting them changes demand and inventory projections completely.

## Project structure

```
rappiplus-business-analysis/
├── RappiPlus_Business_Analysis.ipynb   # full analysis
├── data/                               # cleaned datasets used in Tableau
│   ├── orders_clean.csv
│   ├── catalog_clean.csv
│   └── marketing_clean.csv
├── requirements.txt
├── .env.example
└── README.md
```

## How to run

```bash
git clone https://github.com/carlos-celis-data/rappiplus-business-analysis.git
cd rappiplus-business-analysis
pip install -r requirements.txt
cp .env.example .env      # then fill in your database credentials
jupyter notebook RappiPlus_Business_Analysis.ipynb
```

The notebook loads the CSV datasets from public URLs. Steps 3 and 4 query a PostgreSQL database, so they require the credentials in `.env`.

Note: source column names are in Spanish (e.g. `cantidad` = quantity); the notebook includes a translation table.

## Author

**Carlos Celis** · [GitHub](https://github.com/carlos-celis-data)
