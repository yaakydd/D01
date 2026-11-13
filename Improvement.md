# Deliverable 5: One Improvement Beyond the Brief

## Improvement: Monday Reporting Control Pack

### 1. What I am proposing

I will create a Monday Reporting Control Pack to help Nana check whether the weekly business figures are reliable before using them.

The pack will contain:

- A metric guide defining important figures such as revenue, completed orders, cancelled orders and daily sales.
- A reporting checklist for checking missing data, duplicate orders and unexpected changes.
- A report status showing when the report was last updated and whether it passed its checks.
- An exception section highlighting problems that need investigation.
- Clear responsibilities stating who investigates reporting problems and who confirms that the report is ready to use.

This improvement will work alongside the recommended data warehouse and automated reporting process. It will not replace them.

### 2. Why this improvement is valuable to Nana

Nana currently rebuilds Monday business figures from CSV files. Finance also produces figures that do not always agree with hers.

This creates extra work and makes it difficult for management to know which figures to trust.

The Monday Reporting Control Pack will help Nana:

- Spend less time rebuilding and checking spreadsheets.
- Use the same agreed definitions as Finance.
- Identify reporting problems before presenting figures to management.
- Know when a report is ready to use and when it needs investigation.

The value is not simply that the report arrives automatically. It is that Nana can understand whether the figures are reliable enough to use.

### 3. What the improvement will contain

| Component | What it will do |
|---|---|
| Metric guide | Define how important business figures are calculated so Nana and Finance use the same definitions. |
| Reporting checklist | Check for missing records, duplicate orders and unexpected changes in figures. |
| Report status | Show when the report was last updated and whether its checks passed. |
| Exception section | Highlight problems that require investigation instead of expecting Nana to inspect large CSV files. |
| Responsibility guide | Identify who investigates failed checks and who confirms that the report is ready to use. |

### 4. Undercurrents addressed

| Undercurrent | How the improvement addresses it |
|---|---|
| Data management | Establishes shared definitions for important business figures. |
| DataOps | Introduces checks that make reporting problems visible. |
| Orchestration | Supports a repeatable Monday reporting process instead of relying on Nana to rebuild figures manually. |
| Software engineering | Makes reporting checks repeatable rather than relying on undocumented spreadsheet formulas. |

This improvement makes progress on these undercurrents. It does not claim to solve all of them completely.

### 5. How I will know it has worked

The improvement will be considered successful when:

- Nana and Finance use the same agreed definitions for the selected business figures.
- The Monday report displays its last update time.
- The reporting checks identify missing or duplicate records in test data.
- Failed checks are visible and have an assigned person responsible for investigating them.
- Nana can use the report without manually rebuilding the figures from CSV files.

### 6. Why this is realistic

Kloud Kart has only two approved data hires, and the team has limited experience with data engineering.

The control pack will use the SQL checks and reporting processes already included in the main recommendation. It will not require a separate data platform or another hire.

This keeps the improvement practical while giving Nana something useful beyond the automated report itself.