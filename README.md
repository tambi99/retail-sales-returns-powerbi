# Retail Sales and Returns | Power BI

**Terrence Tambinaka Enow - Power BI portfolio project**

A two-page interactive report for Harbor Home & Office, a fictional US retailer. This project uses Power BI modeling, DAX measures, and interactive visuals to explain sales performance and identify where returns are concentrated. The underlying retail dataset is synthetic; amounts are USD.

## KPI definitions and results

These are the unfiltered results for **2025 order cohorts**, including recorded returns against those orders. Sales and return measures select completed orders. Exact totals were independently recalculated from the report's Excel source using the extracted formulas and checked against the rounded dashboard cards and visible matrix totals.

| KPI | Definition in this report | Result |
|---|---|---:|
| Sales Before Return | Gross sales less discounts on completed orders | $1,976,441.70 |
| Refund Amount | Returned quantity multiplied by the original unit price, before discounts | $110,775.00 |
| Net Sales After Refunds | Sales Before Return less Refund Amount | $1,865,666.70 |
| Returned Units | Sum of returned quantities for completed orders | 648 |
| Returned Orders | Distinct completed order IDs with at least one return | 302 |
| Return Rate | Returned units divided by 12,354 units sold | 5.25% |
| Return Order Rate | Returned orders divided by 1,661 completed orders | 18.18% |
| Average Refund per Returned Order | Refund Amount divided by Returned Orders | $366.80 |
| Top Return Reason | Reason with the highest Refund Amount | Wrong item |

**Calculation basis:** Refunds use prices before discounts, while sales before returns already deduct discounts. Net sales therefore reflects that saved valuation choice. Monthly refund trends follow the original order date, rather than the date of the return. The [measure documentation](docs/model-and-measures.md) explains these choices and the model's filter behavior.

## Project objectives

- Summarize sales before returns, refund value, and sales remaining after refunds.
- Identify the categories, products, regions, and return reasons that deserve investigation.
- Let users explore results by month, category, region, customer segment, and sales channel.

## Open the report

Download [Retail_Sales_Returns_Analytics.pbix](powerbi/Retail_Sales_Returns_Analytics.pbix) and open it in Power BI Desktop. GitHub displays the previews below; the PBIX contains the interactive report and its saved imported data.

The supplied report is preserved unchanged, with its filename simplified. To refresh it, update the local Excel source path in Power Query to a compatible workbook. The source workbook is not included in this repository. See [model, source requirements, and exact DAX measures](docs/model-and-measures.md).

## Dashboard pages

### 1. Executive Overview

Summarizes the financial impact of returns through KPI cards, monthly net sales, net sales by category, the top 10 products by refund value, and refund value by reason.

![Executive Overview dashboard](images/executive-overview.png)

### 2. Returns Analysis

Explores category return rates, monthly refunds, returned orders by region, return-reason share, and product-level detail. Both pages include Month Year, Category, Region, Segment, and Channel slicers.

![Returns Analysis dashboard](images/returns-analysis.png)

The page previews were rendered from the report's native PDF export. The [original Executive Overview desktop screenshot](images/executive-overview-desktop.png) is also preserved.

## Business insights

- **Wrong item leads refund value:** $44,134, or 39.84% of total refunds. Reviewing fulfillment accuracy and product labeling would be a useful next investigation; the dashboard does not establish the cause.
- **Storage has the highest category unit return rate:** 5.78%, compared with Lighting at 5.45% and Furniture at 4.88%. Compare product and reason detail before deciding where to intervene.
- **West has the largest number of returned orders:** 95, followed by North and South at 73 each, and East at 61. This ranks return volume; a regional risk comparison also needs sales or order denominators.
- **Lamp 017 has the highest product refund value:** $9,000. Use the product matrix to compare refund value, returned units, and return rate when prioritizing product reviews.

## Skills demonstrated

- Power BI data modeling across customers, products, orders, order lines, returns, and a Calendar table.
- DAX measures using `CALCULATE`, `SUMX`, `DIVIDE`, `DISTINCTCOUNT`, `RELATED`, and `TOPN`.
- Chronological month sorting, interactive slicers, Top N filtering, and product-level matrix analysis.
- Separate executive and diagnostic report pages, supported by documented metric definitions.

## Scope and limitations

The report describes the supplied synthetic dataset. It does not establish causes or forecast future performance. Net sales is not profit; costs, taxes, and shipping are outside the measures. Distinct returned-order counts can overlap across products and categories.

The saved model uses bidirectional filtering between returns and order lines. Product/category filters do not flow back to the completed-orders denominator, so interpret Return Order Rate under those selections with the [documented filter behavior](docs/model-and-measures.md#relationships). The PBIX and its calculations have been preserved, rather than redesigned during publication.

This is a separate Power BI project with its own reporting objectives. The [Excel and SQL portfolio project](https://github.com/tambi99/terrence-retail-analytics) remains separate and unchanged; its discounted refund valuation differs from this report.

## Repository layout

```text
powerbi/   Original Power BI report, with a simplified filename
images/    Two report-page previews and the supplied desktop screenshot
docs/      Verified DAX, model relationships, and refresh requirements
```
