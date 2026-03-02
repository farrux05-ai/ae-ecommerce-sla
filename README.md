# 🔁 Repeat GMV Growth Analytics — Olist E-Commerce

> **North Star:** Repeat GMV & Repeat Share (Repeat GMV / Total GMV)  
> **Question:** What drives repeat purchases — and how do we grow that share?

![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15-blue?logo=postgresql)
![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-yellow?logo=powerbi)
![Status](https://img.shields.io/badge/status-completed-brightgreen)
![Dataset](https://img.shields.io/badge/dataset-Olist%20Brazil-green)

---

## 📌 Project Overview

End-to-end analytics project on the **Olist Brazilian e-commerce** dataset.  
Focus: understand how much revenue comes from **returning customers** and identify the key **drivers (category, state)** of repeat GMV.

> 🔗 Related project: [ae-ecommerce-warehouse](https://github.com/farrux05-ai/ae-ecommerce-warehouse) — delivery delay & CSAT analysis on the same dataset.

---

## 🏗️ Data Pipeline
```
CSV Files
   └── Staging          — type casting, null handling, trimming
        └── Star Schema  — facts & dimensions
             └── Marts   — BI-ready aggregations
                  └── Power BI Dashboard
```

### Data Model

| Layer | Tables |
|-------|--------|
| **Facts** | `fact_orders` (grain: order), `fact_order_items` (grain: order item) |
| **Dims** | `dim_customer`, `dim_product`, `dim_seller`, `dim_date`, `dim_month` |
| **Marts** | `mart_monthly_repeat_gmv`, `mart_repeat_gmv_by_state_month`, `mart_repeat_gmv_by_category_month` |

### Metric Definitions

| Metric | Definition |
|--------|-----------|
| **GMV** | `price + freight_value` |
| **Repeat Order** | `order_rank >= 2` per `customer_unique_id` |
| **Repeat GMV** | GMV from repeat orders only |
| **Repeat Share** | Repeat GMV / Total GMV |

---

## 🔑 Key Findings

| Finding | Result |
|---------|--------|
| Peak repeat share | **~4% (Feb 2018)** — current benchmark |
| Top repeat states | **SP, RJ, MG, RS, PR** |
| Best repeat category | **bed_bath_table (~5% repeat share)** |
| Underperforming | **health_beauty (~2%)** — growth opportunity |

**Top categories by repeat share:**

| Category | Repeat Share |
|----------|-------------|
| bed_bath_table | ~5% |
| computers_accessories | ~4% |
| furniture_decor | ~4% |
| sports_leisure | ~4% |
| health_beauty | ~2% ⚠️ |

---

## 💡 Recommendations

1. **Beat the 4% benchmark** — post-purchase triggers (7/14/30-day coupons, free shipping)
2. **Double down on bed_bath_table** — bundles + returning-customer incentives
3. **Cross-sell for computers & furniture** — accessories to drive 2nd purchase
4. **A/B test health_beauty** — free shipping vs 2nd purchase coupon
5. **Geo-prioritize SP/RJ/MG** — highest repeat GMV states → retention campaigns first

---

## 📊 Dashboard (Power BI)

| Page | Content |
|------|---------|
| Page 1 | Repeat GMV trend + Repeat Share over time |
| Page 2 | New vs Repeat GMV comparison |
| Page 3 | Top repeat categories & states |

📁 Screenshots: [`/powerbi/screenshots/`](./powerbi/screenshots/)

---

## ⚙️ How to Run

### Prerequisites
- PostgreSQL 13+
- psql or DBeaver

### Setup
```bash
# 1. Clone the repo
git clone https://github.com/farrux05-ai/ae-ecommerce-sla
cd ae-ecommerce-sla

# 2. Load data into PostgreSQL
# Import Olist CSV files into your database

# 3. Run SQL files in order
psql -U your_user -d your_db -f sql/01_staging.sql
psql -U your_user -d your_db -f sql/02_star_schema.sql
psql -U your_user -d your_db -f sql/mart.sql
psql -U your_user -d your_db -f sql/99_final_checks.sql
```

---

## 📁 Project Structure
```
ae-ecommerce-sla/
├── sql/
│   ├── 01_staging.sql        # staging tables & cleaning
│   ├── 02_star_schema.sql    # facts & dimensions
│   ├── mart.sql              # BI-ready marts
│   └── 99_final_checks.sql   # validation tests
├── powerbi/
│   ├── olist.pbix            # dashboard file
│   └── screenshots/          # dashboard images
└── README.md
```

---

## ⚠️ Limitations

- Repeat detection uses `customer_unique_id` (Olist recommended approach)
- Analysis limited to **delivered orders** only
- Some products have missing category labels

---

## 👤 Author

**Farruxbek Valijonov** — Analytics Engineer  
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?logo=linkedin)](www.linkedin.com/in/farrux-valijonov-341975322)
[![GitHub](https://img.shields.io/badge/GitHub-farrux05--ai-black?logo=github)](https://github.com/farrux05-ai)
