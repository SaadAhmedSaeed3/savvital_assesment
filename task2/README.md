# Operations KPI Dashboard – Write-up

## Metric Choices

I selected all five KPIs because together they tell the complete pipeline story. Volume shows throughput across every stage of the order lifecycle. Delivery conversion rate reveals how many orders successfully reach the customer. Time per stage identifies where operational bottlenecks occur — whether at approval, shipping handoff, or last-mile delivery. Revenue trend over time shows the business impact of growth month by month. Finally, category breakdown exposes the top product channels driving order volume and revenue, which is essential for prioritising fulfilment resources.

-Note: Dataset contains 9 CSV's but I used only 7 as two of were not relating with our KPI's Measures.

## Data Story

The Olist dataset reveals that Brazilian e-commerce grew sharply from early 2017 through mid-2018. Health & beauty and bed, bath & table emerged as the highest-volume categories, while watches & gifts led on revenue per order. The average total delivery time of approximately 12.5 days masks significant variance across stages — the carrier-to-customer leg is the longest and most variable, pointing to last-mile logistics as the primary improvement opportunity. Delivery conversion rates remain consistently above 97%, indicating a healthy and mature fulfilment pipeline with minimal cancellations. (Copied from kaggle Dataset Information)

## Dataset Limitation

- Most of the order volume represent a single marketplace which does not provide capability to draw competitive analysis.
- Most of data shows positive results so it is difficults to get operational negatives from the analysis.
