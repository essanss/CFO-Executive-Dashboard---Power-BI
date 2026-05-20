# CFO Executive Dashboard — Screenshot Gallery

## Dashboard Pages Overview

This folder contains documentation and visual references for the CFO Executive Dashboard — a production-grade Power BI reporting solution for financial leadership teams.

### 📊 Dashboard Pages

#### [1️⃣ Executive Summary](./01_Executive_Summary.md)
- **Purpose:** High-level financial KPI overview and regional performance
- **Key Visuals:** KPI cards, revenue trend, regional breakdown, YoY growth, status matrix
- **Audience:** CFO, Finance Leadership, Board reporting
- **Refresh Frequency:** Daily

#### [2️⃣ P&L Deep Dive](./02_PL_Deep_Dive.md)
- **Purpose:** Detailed Profit & Loss analysis with margin trends
- **Key Visuals:** Income statement matrix, margin trends, business unit breakdown, rolling averages
- **Audience:** CFO, Controller, Financial Planning team
- **Refresh Frequency:** Monthly (Post close)

#### [3️⃣ Cash Flow & Working Capital](./03_Cash_Flow_Working_Capital.md)
- **Purpose:** Liquidity and operational efficiency monitoring
- **Key Visuals:** Cash flow waterfall, working capital trend, AR/AP analysis, DSO/DPO metrics
- **Audience:** Treasurer, CFO, Finance Operations
- **Refresh Frequency:** Weekly

#### [4️⃣ Budget vs Actual Variance](./04_Budget_vs_Actual.md)
- **Purpose:** Execution tracking and variance analysis
- **Key Visuals:** Variance heatmap, budget trend, YTD performance gauges
- **Audience:** CFO, FP&A Team, Business Unit Leaders
- **Refresh Frequency:** Monthly (Post close)

---

## Dashboard Features

✅ **Advanced DAX Calculations**
- 60+ measures covering all financial metrics
- Time intelligence (YTD, MTD, YoY, MoM)
- Rolling averages and trend analysis
- Budget variance calculations

✅ **Interactive Filtering**
- Fiscal Year selector
- Multi-quarter selection
- Regional drill-down (North, South, East, West)
- Business unit filtering (Product A, Product B)

✅ **Executive Design**
- Dark theme (Navy + Gold) for professional presentation
- Mobile-optimized layouts
- Consistent color coding (Green/Yellow/Red status flags)
- KPI status indicators with emojis

✅ **Financial Analytics**
- Full P&L waterfall analysis
- Cash conversion cycle tracking
- Working capital management
- Financial ratio analysis
- Variance analysis with drill-through

---

## Data Structure

### Source Tables (CSV)
- **financials.csv** — Monthly P&L by region & business unit (48 rows)
- **cashflow_workingcapital.csv** — Monthly cash flow & WC metrics (12 rows)
- **budget_vs_actual.csv** — Budget vs actual by region & BU (48 rows)

### Dimension Table (Generated in Power Query)
- **DimDate** — Auto-generated date table with year, month, quarter, weekday attributes

### Measure Table
- **_Measures** — 60+ DAX measures for all calculations and KPIs

---

## Theme & Color Palette

### Primary Colors
- **Background:** Dark Navy #0D1B2A
- **Accent:** Gold #F5A623
- **Text:** White #FFFFFF

### Status Colors
- 🟢 **Exceeded:** Green #27AE60 (≥+5% variance)
- 🟡 **On Track:** Yellow #F1C40F (0-5% variance)
- 🟠 **At Risk:** Orange #E67E22 (-5-0% variance)
- 🔴 **Behind:** Red #E74C3C (<-5% variance)

### Chart Colors
- Orange #F5A623 — Primary metric (Revenue)
- Green #2ECC71 — Positive indicator
- Blue #3498DB — Secondary metric
- Red #E74C3C — Negative/Outflow

---

## How to Use These Screenshots

1. **Page Documentation** — Each MD file describes the page layout, visuals, and use cases
2. **Visual Reference** — Use alongside Power BI to understand expected layout
3. **KPI Definitions** — Clear explanation of each metric and status indicator
4. **Business Context** — Understand the financial story each page tells

---

## Setup Instructions

For detailed setup and build instructions, see: [`docs/Setup_Guide.md`](../docs/Setup_Guide.md)

For data model specifications, see: [`docs/Data_Model.md`](../docs/Data_Model.md)

For design guidelines, see: [`docs/Dashboard_Design_Guide.md`](../docs/Dashboard_Design_Guide.md)