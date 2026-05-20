# 📊 CFO Executive Dashboard — Power BI

> **A production-grade, multi-page CFO Executive Dashboard built in Power BI showcasing advanced DAX, financial KPIs, budget analysis, and time-intelligence calculations.**

---


| Page | Description |
|------|-------------|
| 🏠 Executive Summary | Top-line KPIs, revenue trend, regional breakdown |
| 📄 P&L Deep Dive | Full income statement, margin analysis, EBITDA bridge |
| 💧 Cash Flow & Working Capital | Cash waterfall, AR/AP analysis, working capital trend |
| 📋 Budget vs Actual | Variance heatmap, YTD gauges, region-level drill-through |

---

## 🎯 Business Context

This dashboard is designed for a **CFO or Finance Leadership team** to monitor:
- **Financial health** across regions and business units
- **Profitability trends** from Revenue to Net Profit
- **Liquidity position** via cash flow and working capital
- **Execution vs plan** using budget variance analysis

---

## 📐 Technical Skills Demonstrated

### ✅ DAX Skills
| Skill | Measures |
|-------|----------|
| **YTD Calculations** | `Revenue YTD`, `EBITDA YTD`, `Net Profit YTD`, `Cash Flow YTD` |
| **MTD Calculations** | `Revenue MTD`, `EBITDA MTD`, `Net Profit MTD` |
| **Prior Year (PY)** | `Revenue PY`, `EBITDA PY`, `YoY Growth %` |
| **Prior Month (PM)** | `Revenue Prior Month`, `MoM Growth %` |
| **Rolling Averages** | `Revenue 3M Rolling Avg`, `Revenue 6M Rolling Avg`, `EBITDA 3M Rolling Avg` |
| **Variance %** | `Revenue Variance %`, `EBITDA Variance %`, `Net Profit Variance %`, `OpEx Variance %` |
| **Financial Ratios** | `Current Ratio`, `AR Turnover`, `AP Turnover`, `DSO`, `DPO`, `Cash Conversion Cycle` |
| **Dynamic Titles** | `Selected Period Title`, `YTD vs PY Label` |
| **KPI Status Flags** | `Revenue Status`, `EBITDA Status`, `Cash Flow Status` |
| **DIVIDE Safety** | All division uses `DIVIDE()` with 0 as alternate result |

### ✅ Power Query (M)
- Custom `DimDate` table generated from M code
- Data type transformations and column formatting
- Consistent schema across all 3 fact tables

### ✅ Data Modeling
- **Star Schema** — 3 fact tables connected through `DimDate`
- Proper **1-to-Many** relationships with single cross-filter direction
- Dedicated `_Measures` table for clean DAX organisation

### ✅ Visualisations
- Line + Stacked Column Combo (Revenue vs Budget)
- Waterfall Chart (EBITDA Bridge, Cash Flow Breakdown)
- KPI Cards with trend indicators
- Donut Chart (Revenue by Region)
- Gauge Charts (YTD performance vs target)
- Matrix with conditional formatting (Variance Heatmap)
- Page Navigator buttons

### ✅ UX / Design
- Dark executive theme (Navy + Gold)
- 4-page navigation structure
- Consistent color-coding: 🟢 🟡 🟠 🔴
- Mobile layout configured
- Slicers: Year, Quarter, Region, Business Unit

---

## 📁 Repository Structure

```
CFO-Executive-Dashboard/
│
├── 📂 data/
│   ├── financials.csv                 # Monthly P&L by Region & Business Unit
│   ├── cashflow_workingcapital.csv    # Monthly Cash Flow & Working Capital
│   └── budget_vs_actual.csv          # Budget vs Actual by Region & Business Unit
│
├── 📂 dax/
│   └── DAX_Measures.dax              # All 40+ DAX measures with comments
│
├── 📂 docs/
│   ├── Data_Model.md                 # Schema, relationships & Power Query M code
│   ├── Dashboard_Design_Guide.md     # Page layout, visuals, theme JSON
│   └── Setup_Guide.md               # Step-by-step Power BI build guide
│
├── 📂 screenshots/
│   └── (Add your dashboard screenshots here after building)
│
└── README.md
```

---

## 📊 Key KPIs Covered

| KPI | Measure | Time Intelligence |
|-----|---------|------------------|
| **Revenue** | Total, YTD, MTD, PY, MoM | ✅ |
| **EBITDA** | Total, Margin %, YTD, Rolling 3M | ✅ |
| **Net Profit** | Total, Margin %, YTD, PY | ✅ |
| **Gross Profit** | Total, Margin % | — |
| **Cash Flow** | Operating, Investing, Financing, Net | ✅ |
| **Working Capital** | Total, Current Ratio | — |
| **AR Turnover** | Ratio, DSO (Days Sales Outstanding) | — |
| **AP Turnover** | Ratio, DPO (Days Payable Outstanding) | — |
| **Cash Conversion Cycle** | DSO − DPO + Inventory Days | — |
| **Budget vs Actual** | Variance $, Variance % | ✅ YTD |

---

---

## 🗂️ Data Dictionary

### `financials.csv`
| Column | Type | Description |
|--------|------|-------------|
| Date | Date | Month-end date |
| Month | Text | Month name |
| Quarter | Text | Q1–Q4 |
| Year | Integer | Fiscal year |
| Region | Text | North / South / East / West |
| Business_Unit | Text | Product A / Product B |
| Revenue | Decimal | Gross Revenue ($) |
| COGS | Decimal | Cost of Goods Sold ($) |
| Gross_Profit | Decimal | Revenue − COGS ($) |
| Operating_Expenses | Decimal | SG&A and operating costs ($) |
| EBITDA | Decimal | Earnings before Interest, Tax, D&A ($) |
| Depreciation | Decimal | D&A expense ($) |
| EBIT | Decimal | Earnings before Interest & Tax ($) |
| Interest_Expense | Decimal | Debt service cost ($) |
| Tax | Decimal | Income tax ($) |
| Net_Profit | Decimal | Bottom-line profit ($) |
| Budget_Revenue | Decimal | Revenue budget ($) |
| Budget_EBITDA | Decimal | EBITDA budget ($) |
| Budget_Net_Profit | Decimal | Net Profit budget ($) |

### `cashflow_workingcapital.csv`
| Column | Type | Description |
|--------|------|-------------|
| Operating_Cash_Flow | Decimal | Cash from operations ($) |
| Investing_Cash_Flow | Decimal | Cash used in investments ($) |
| Financing_Cash_Flow | Decimal | Cash from financing ($) |
| Net_Cash_Flow | Decimal | Total net cash movement ($) |
| Accounts_Receivable | Decimal | Outstanding customer receivables ($) |
| Accounts_Payable | Decimal | Outstanding vendor payables ($) |
| Inventory | Decimal | Inventory on hand ($) |
| Current_Assets | Decimal | Total current assets ($) |
| Current_Liabilities | Decimal | Total current liabilities ($) |
| Working_Capital | Decimal | Current Assets − Current Liabilities ($) |
| AR_Days | Integer | Days Sales Outstanding |
| AP_Days | Integer | Days Payable Outstanding |
| Inventory_Days | Integer | Days of Inventory Outstanding |

---

## 📌 DAX Highlights

### YTD with DATESYTD
```dax
Revenue YTD =
CALCULATE(
    [Total Revenue],
    DATESYTD(DimDate[Date])
)
```

### Rolling 3-Month Average
```dax
Revenue 3M Rolling Avg =
CALCULATE(
    [Total Revenue],
    DATESINPERIOD(
        DimDate[Date],
        LASTDATE(DimDate[Date]),
        -3, MONTH
    )
) / 3
```

### Budget Variance %
```dax
Revenue Variance % =
DIVIDE(
    [Total Revenue] - [Budget Revenue],
    [Budget Revenue],
    0
)
```

### Dynamic KPI Status
```dax
Revenue Status =
SWITCH(
    TRUE(),
    [Revenue Variance %] >= 0.05,  "🟢 Exceeded",
    [Revenue Variance %] >= 0,     "🟡 On Track",
    [Revenue Variance %] >= -0.05, "🟠 At Risk",
    "🔴 Behind"
)
```

---

## 🛠️ Tools & Technologies

| Tool | Version | Purpose |
|------|---------|---------|
| Power BI Desktop | Latest | Report development |
| DAX | — | All measures & calculations |
| Power Query (M) | — | Data transformation & DimDate |
| CSV | — | Sample data source |

---

