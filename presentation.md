---
marp: true
theme: default
class: lead
paginate: true
title: Quarterly Earnings — Technical Documentation
description: Technical documentation for data sources, metrics, and analysis behind the quarterly earnings.
---

# Quarterly Earnings — Technical Documentation
**Version:** Q2 FY25 • **Author:** Shiva Varshney  
**Email:** 22f3001416@ds.study.iitm.ac.in

<!-- presenter: Introduce scope, audience (finance & data teams), and expected outcomes. -->

---

## Introduction
This document explains the data pipeline, metrics, and methodology used to prepare the quarterly earnings report.

- Goals: Accuracy, reproducibility, auditability
- Deliverables: KPIs, tables, reconciliations, and sensitivity analysis
- Tooling: Python, Pandas, SQL, dbt, CI/CD

<!-- presenter: Emphasize traceability and version control best practices. -->

---

## Data Sources
| Source | Type | Refresh | Purpose |
|---|---|---:|---|
| Data Warehouse (Snowflake) | Fact/Dim | Hourly | Revenue, bookings, margin |
| Billing System | App events | Daily | Invoices, refunds, credits |
| Finance Ledger | CSV/S3 | Monthly | GL entries, reconciliation |
| CRM | API | Daily | Pipeline, churn, ARR |

> Data quality checks run via dbt tests & Great Expectations.

<!-- presenter: Explain SLAs and lineage. -->

---

## Financial Metrics
**Core KPIs**
- Revenue (IFRS), Gross Margin, Opex, EBITDA
- EPS (basic/diluted), Free Cash Flow, Net Retention

**Formulas**
- ROI: \\( \mathrm{ROI} = \frac{\mathrm{Gain}-\mathrm{Cost}}{\mathrm{Cost}} \\)
- NPV: \\( \mathrm{NPV} = \sum_{t=0}^{T} \frac{C_t}{(1+r)^t} \\)

<!-- presenter: Mention consistent FX rates and holiday calendars. -->

---

## Example: EPS Surprise (Code)
```python
import pandas as pd

df = pd.DataFrame({
    "quarter": ["Q2 FY24", "Q1 FY25", "Q2 FY25"],
    "eps_actual": [5.26, 5.72, 6.12],
    "eps_consensus": [5.20, 5.60, 5.70]
})
df["surprise_pct"] = (df["eps_actual"] - df["eps_consensus"]) / df["eps_consensus"] * 100
df
```

<!-- presenter: Show output table and how we validate against StreetAccount. -->

---

## Key Insights
- Subscription share improved → margin expansion
- Opex discipline → leverage on revenue growth
- FX tailwinds aided EPS beat

**Risks**
- Macro slowdown, regulatory changes, currency volatility

<!-- presenter: Keep a balanced tone for stakeholders. -->

---

## Future Outlook
- FY25 guidance raised by 2%
- Capex prioritized for data & AI capabilities
- Target net retention > 115%

**Appendix**
- Data dictionary
- Reconciliation steps
- Runbook links

<!-- presenter: Invite questions and share repository link. -->
