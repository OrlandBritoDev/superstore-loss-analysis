# Superstore Loss Analysis: From "Which Category?" to "How Far Does It Spread?"

A two-part formula-based diagnostic analysis of a 10,000-row retail dataset, built and verified entirely in Excel.

## Part 1: Which category loses the most, and why?

**The "Binders" sub-category has the largest accumulated loss of any product line: -$38,504.26, an 18.9% loss rate against its own total sales.**

The cause is traceable, not speculative: transactions in Binders that lost money carried an average discount of 73.79% — the second-highest of any category, and combined with Binders' high sales volume, the most costly in absolute dollar terms.

## Part 2: Does the same pattern repeat elsewhere — and where does it hit hardest?

Starting from the Part 1 finding, this second analysis asks a broader question: **if high discounts are quietly driving losses in Binders, is the same pattern happening in other categories and regions — and if so, how much of the company's total loss does it explain?**

**The Central region loses the most of any region: -$56,308.65, a 31.91% loss rate, with an average 54.91% discount on its losing transactions.**

A Box & Whisker comparison of profit distribution across all four regions was used to first identify Central as worth investigating — its spread of outcomes stood out visually before any calculation confirmed it numerically.

Digging into *why* Central specifically underperforms: three sub-categories — **Furnishings, Binders, and Appliances** — combine to generate $36,477.46 of Central's loss, **64.78% of the region's total**, with an average discount rate reaching up to 80% on their failed transactions.

**In short: the discount-driven loss pattern first found in Binders isn't isolated — it recurs across categories and concentrates geographically, most severely in the Central region.**

## Business Questions

> Part 1: Which product sub-category accumulates the greatest economic loss, and what explains it?

> Part 2: If the discount pattern seen in Binders repeats in other categories, what percentage of the company's total earnings is being lost to this same phenomenon — and does it concentrate in any particular region?

## Data

[Sample Superstore dataset](https://www.kaggle.com/datasets/bravehart101/sample-supermarket-dataset) (Kaggle) — 9,994 retail order records.

## Data Cleaning (Part 1, reused for Part 2)

- **Missing values** — audited across all 13 columns. None found.
- **Duplicate records** — found and removed 17 exact duplicate rows.
- **Text inconsistency** — checked `Category`, `Sub-Category`, and `Region` with `UNIQUE()`. None found.
- **Data type errors** — Sales, Discount, and Profit imported as text due to a regional decimal-separator mismatch. Fixed via Power Query's locale-aware type conversion.

## Method

- **Part 1:** `SUMIFS` (loss and sales per category), `AVERAGEIFS` (discount rate isolated to loss-making transactions)
- **Part 2:** Box & Whisker chart (regional profit distribution — used to generate a hypothesis, not as the final answer), `COUNTIFS` (loss frequency by region), `SUMIFS`/`AVERAGEIFS` (loss and discount rate by sub-category within each region)
- Every regional sub-category breakdown reconciles exactly to the dataset-wide total loss (-$156,112.99) — cross-checked, not assumed.

All formulas are visible in the workbook — no pasted values.

## Files

- `superstore_loss_analysis.xlsx` — Part 1: category-level analysis
- `binders_discount_pattern_impact_analysis.xlsx` — Part 2: regional analysis
- Source data: linked above (not redistributed here per Kaggle's terms)

## Tools

Excel (formulas, Power Query, Box & Whisker charts)

---

*Part of a structured data analytics learning path — [see my LinkedIn profile](https://www.linkedin.com/in/orland-brito-19185639a/) for more.*
