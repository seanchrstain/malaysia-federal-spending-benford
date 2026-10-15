# Malaysian Federal Operating Expenditure: Benford's Law Test (1980–2025)

An audit style analysis of Malaysia's federal operating expenditure using open government data. The project cleans and reconciles the data, explores spending trends with SQL, and applies Benford's Law, a screening technique used in forensic accounting and auditing.

## Data

- **Source:** [Annual Federal Government Operating Expenditure by Object](https://data.gov.my/data-catalogue/federal_finance_year_oe), data.gov.my (Accountant-General's Department)
- **Licence:** CC BY 4.0
- **Coverage:** 1979–2025, annual, RM million (nominal)

## Tools

Python (Pandas, NumPy, Matplotlib), SQLite, Jupyter Notebook

## Method

1. **Clean:** removed the `total` row and the `debt_service` subtotal (which equals domestic + external debt service) to avoid double-counting, and dropped zero values.
2. **Reconcile:** rebuilt each year's total from the detailed rows and compared it with the official total.
   - 1980–2025 reconcile within ±2 (RM mil), explained by rounding.
   - 1979 showed a 1,271 difference because debt service was not split into domestic/external that year, so 1979 was excluded.
   - Final dataset: 414 values across 9 expenditure categories.
3. **Explore (SQL):** ranked categories by total spending and compared 2000 vs 2025 growth.
4. **Benford test:** compared the first-digit distribution of all 414 values with Benford's expected distribution, using Mean Absolute Deviation (MAD) and Nigrini's first-digit thresholds.

## Key findings

**Spending trends**
- Emoluments (salaries) are the largest category, about 31% of operating expenditure from 1980–2025.
- Between 2000 and 2025, subsidies grew the fastest of all operating expenditure categories (11.5×), roughly double the growth of total operating spending (5.8×).
- Retirement charges were the second-fastest (9.2×), rising from RM11.5 billion in 2010 to RM34.1 billion in 2023 in this dataset. This is broadly consistent with Fulcrum's (2024) reported pension spending of RM11 billion and RM32 billion; the difference likely reflects broader category definitions.
- Debt service has shifted towards domestic borrowing: domestic debt service grew 6.8×, while external debt service halved.

**Benford's Law**
- The first-digit distribution broadly follows Benford's Law.
- MAD = 0.0122, which is marginally acceptable conformity under Nigrini's thresholds.
- No individual digit shows a spike of the kind that would suggest manipulation.

## Limitations

- **Small sample:** Benford benchmarks are designed for thousands of transactions; 414 values naturally vary more by chance.
- **Aggregated data:** the values are annual category totals, not individual transactions, so they are not the ideal data type for a Benford test. This analysis is an illustrative demonstration, not an audit finding.
- **Nominal figures:** amounts are not adjusted for inflation.
- **No causal claims:** the data shows what changed, not why.

## Reference

Fulcrum (2024). *Malaysia's Public Service Pensions: Will to Reform, Without A Roadmap.* ISEAS – Yusof Ishak Institute. https://fulcrum.sg/article/commentaries/malaysias-public-service-pensions-will-to-reform-without-a-roadmap/

## Author

Sean Christain Badai, Bachelor of Accounting (Hons) student, Universiti Malaysia Sabah
