<img width="1886" height="1100" alt="Screenshot 2026-03-25 171946" src="https://github.com/user-attachments/assets/b1096739-891b-4dfe-ae20-04a17513b7f5" />
# 📊 Ecommerce Performance Analysis — Google Analytics 4 × BigQuery

> **"77% of visitors never saw a single product. The problem wasn't checkout — it was discovery."**

---

## 🔍 Project Overview

A full end-to-end ecommerce analytics project built using real Google 
Analytics 4 data queried directly from BigQuery. This project identifies 
where revenue is being lost across the customer journey — from session to 
purchase — and delivers actionable business recommendations, not just 
data outputs.

**Business Question:**
> Which customer behaviours are driving the most revenue — and where are 
> we losing customers in the funnel?

---

## 🛠 Tools & Stack

| Tool | Purpose |
|------|---------|
| **BigQuery** | SQL querying on GA4 public dataset at scale |
| **Python (pandas)** | Data cleaning, transformation, enrichment |
| **Python (matplotlib)** | Data visualisation and chart generation |
| **Power BI** | Interactive dashboard and business reporting |
| **Google Colab** | Notebook environment for reproducible analysis |

---

## 📦 Dataset

**Source:** bigquery-public-data.ga4_obfuscated_sample_ecommerce

Google's official obfuscated GA4 ecommerce sample dataset, available 
publicly via BigQuery. Contains real ecommerce event data including 
sessions, product views, add-to-cart events, checkout steps and purchases.

**Period:** November 2020 — January 2021  
**Scale:** 267,116 sessions across 3 months

---

## 🔢 Key Metrics

| Metric | Value |
|--------|-------|
| Total Revenue | £250,391 |
| Total Orders | 4,466 |
| Average Order Value | £56.07 |
| Overall Conversion Rate | 1.65% |
| Total Sessions | 267,116 |
| Dec to Jan Revenue Drop | -62% |

---

## 🔄 The Conversion Funnel

| Stage | Users | % of Sessions |
|-------|-------|---------------|
| Sessions | 267,116 | 100% |
| Product Views | 61,252 | 22.9% |
| Add to Cart | 12,545 | 4.7% |
| Checkout Started | 9,715 | 3.6% |
| Purchases | 4,419 | 1.65% |

---

## 💡 Key Business Insights

### 1. 📉 The Discovery Problem

77.1% of sessions never reached a product page.

This is not a conversion problem — it is a discovery and merchandising 
problem. Optimising checkout will not move the needle when the majority 
of visitors leave before seeing a single product.

Imagine 100 people walk into your store. 77 of them turn around and 
leave before they even reach the shelves. They never see a single product.

Would you spend money redesigning the checkout counter? No. You would 
fix the store entrance, the layout, and the signs that guide people to 
what they want. That is exactly what the data showed.

**Recommendation:** Homepage redesign, improved navigation and search 
optimisation should be the number one priority before any investment 
in checkout or cart improvements.

---

### 2. 📉 Post-Holiday Revenue Cliff

Revenue dropped 62% from December (£110,042) to January (£41,630).

This is a predictable seasonal pattern but unmanaged. The data suggests 
no retention strategy was in place to capture December buyers before 
they went cold.

**Recommendation:** Implement a January win-back campaign targeting 
December buyers within 7 days of their last purchase, before the 
drop-off window closes.

---

### 3. 🏆 Apparel Category Dominance

9 of the top 10 revenue-generating products are Apparel. The top product 
(Google Zip Hoodie F/C) alone drove £13,692 in revenue.

**Recommendation:** Expand the Apparel range to capture more of this 
demonstrated demand rather than diversifying into underperforming 
categories.

---

## 📊 SQL Queries

### Monthly Revenue Trend
SELECT
  FORMAT_DATE('%Y-%m', PARSE_DATE('%Y%m%d', event_date)) AS month,
  COUNT(DISTINCT user_pseudo_id) AS unique_users,
  COUNTIF(event_name = 'purchase') AS total_purchases,
  ROUND(SUM(
    (SELECT value.double_value
     FROM UNNEST(event_params)
     WHERE key = 'value')), 2) AS total_revenue
FROM bigquery-public-data.ga4_obfuscated_sample_ecommerce.events_*
WHERE event_name = 'purchase'
GROUP BY month
ORDER BY month;

### Conversion Funnel
SELECT
  COUNT(DISTINCT CASE WHEN event_name = 'session_start'
    THEN user_pseudo_id END) AS sessions,
  COUNT(DISTINCT CASE WHEN event_name = 'view_item'
    THEN user_pseudo_id END) AS product_views,
  COUNT(DISTINCT CASE WHEN event_name = 'add_to_cart'
    THEN user_pseudo_id END) AS add_to_cart,
  COUNT(DISTINCT CASE WHEN event_name = 'begin_checkout'
    THEN user_pseudo_id END) AS checkout_started,
  COUNT(DISTINCT CASE WHEN event_name = 'purchase'
    THEN user_pseudo_id END) AS purchases
FROM bigquery-public-data.ga4_obfuscated_sample_ecommerce.events_*;

---

## 🚀 How to Reproduce This Project

**Step 1 — Run SQL queries in BigQuery**
1. Open console.cloud.google.com
2. Navigate to BigQuery
3. Run each SQL query above
4. Export results as CSV

**Step 2 — Run Python analysis in Google Colab**
1. Open the notebook file in Google Colab
2. Upload your 4 CSV files when prompted
3. Run all cells top to bottom
4. Charts save automatically as PNG files

**Step 3 — View the dashboard**
1. Open ecommerce_dashboard.html in any browser
2. All charts render instantly — no installation needed

---

## 📈 What I Learned

This project taught me to think like a business analyst, not just a 
data analyst. The most important skill was not writing the SQL or 
cleaning the data — it was knowing which question to ask.

The conversion rate of 1.65% looks like the problem. But the funnel 
tells you it is not. Without the funnel, you would optimise the wrong 
thing entirely.

That is the difference between a data report and a business 
recommendation.

---

## 👩‍💻 About

**Sanduni** — Data Analyst specialising in Ecommerce & Retail Analytics

LinkedIn: [www.linkedin.com/in/sanduni-kaushalya-pathiraja-a39392392]
Tools: BigQuery · Python · Power BI · SQL · pandas · matplotlib
Open to: Ecommerce Data Analyst | Retail Analytics | Product Analyst

---

## 📄 Licence

This project uses publicly available data from Google's BigQuery public 
dataset programme. Free to use for educational and portfolio purposes.
