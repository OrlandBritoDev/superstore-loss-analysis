# Superstore Loss Analysis: Why Does the "Binders" Category Lose Money?

A formula-based diagnostic analysis of a 10,000-row retail dataset — built and verified entirely in Excel.

## The Finding

**The "Binders" sub-category has the largest accumulated loss of any product line: -$38,504.26, an 18.9% loss rate against its own total sales.**

The cause is traceable, not speculative: transactions in Binders that lost money carried an average discount of **73.79%** — the second-highest of any category, and combined with Binders' high sales volume, the most costly in absolute dollar terms.

## Business Question

> Which product sub-category accumulates the greatest economic loss, and what explains it?

This started as a narrower question (which single transaction lost the most?), then was deliberately reframed to the aggregate, decision-relevant version above — a transaction-level answer tells you about one outlier; a category-level answer tells you whether to fix or drop a product line.

## Data

[Sample Superstore dataset](https://www.kaggle.com/datasets/bravehart101/sample-supermarket-dataset) (Kaggle) — 9,994 retail order records: Ship Mode, Segment, Region, Category, Sub-Category, Sales, Quantity, Discount, Profit.

## Data Cleaning

Before any analysis, the dataset was audited for:
- **Missing values** — checked across all 13 columns (`COUNTA` vs. total row count). None found.
- **Duplicate records** — found and removed **17 exact duplicate rows** (identical across all 13 fields, including Sales/Profit matching to 4 decimal places). Verified 0 duplicates remain.
- **Text inconsistency** — checked `Category`, `Sub-Category`, and `Region` with `UNIQUE()` for spelling/spacing variants. None found.
- **Data type errors** — Sales, Discount, and Profit imported as text instead of numbers due to a regional decimal-separator mismatch in the CSV import. Fixed via Power Query's locale-aware type conversion (not a formula patch — the import step itself was the source).
- **Zero-profit edge case** — 65 transactions have exactly $0 profit; documented decision to include them in total sales but exclude them from the "loss" calculation, since a $0 result is not itself a loss.

## Method

- `SUMIFS` — total sales and total loss per sub-category
- `AVERAGEIFS` (with `IFERROR`) — average discount rate, isolated to loss-making transactions only, per sub-category
- Cross-checked the total of all 17 category-level losses against the dataset-wide sum of negative-profit transactions — they reconcile exactly.

All formulas are visible in the workbook — no pasted values.

## Files

- `superstore_analysis.xlsx` — full workbook: raw data, cleaning audit, formulas, and answer
- Source data: linked above (not redistributed here due to Kaggle's terms)

## Tools

Excel (formulas + Power Query for import correction)

---

*Part of a structured data analytics learning path — [see my LinkedIn profile](https://www.linkedin.com/in/orland-brito-19185639a/) for more.*
