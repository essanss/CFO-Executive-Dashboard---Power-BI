# Step-by-Step Power BI Setup Guide

## Prerequisites
- Power BI Desktop (latest version from Microsoft Store or powerbi.microsoft.com)
- The 3 CSV files from the `/data` folder

---

## STEP 1 — Load Data into Power BI

1. Open Power BI Desktop
2. Click **Home → Get Data → Text/CSV**
3. Load these 3 files one by one:
   - `financials.csv`
   - `cashflow_workingcapital.csv`
   - `budget_vs_actual.csv`
4. For each file, click **Transform Data** instead of Load

---

## STEP 2 — Transform in Power Query

### For `financials` table:
1. Select the `Date` column → **Change Type → Date**
2. Select `Year` column → **Change Type → Whole Number**
3. Select all numeric columns (Revenue through Budget_Net_Profit) → **Change Type → Decimal Number**
4. Click **Close & Apply**

### Repeat the same steps for:
- `cashflow_workingcapital` table
- `budget_vs_actual` table

### Create DimDate table:
1. **Home → Transform Data → (Power Query opens)**
2. **Home → New Source → Blank Query**
3. Paste the M Code from `docs/Data_Model.md`
4. Name the query: `DimDate`
5. Close & Apply

---

## STEP 3 — Build the Data Model

1. Go to **Model view** (left sidebar icon)
2. Drag `DimDate[Date]` → `financials[Date]` (1-to-Many)
3. Drag `DimDate[Date]` → `cashflow_workingcapital[Date]` (1-to-Many)
4. Drag `DimDate[Date]` → `budget_vs_actual[Date]` (1-to-Many)
5. Verify all relationships show a **"1 → *"** symbol

---

## STEP 4 — Create the Measures Table

1. **Home → Enter Data**
2. Create a table named `_Measures` with one column, one blank row
3. Click **Load**
4. This is where all DAX measures will live (keeps model clean)

---

## STEP 5 — Add DAX Measures

1. Click the `_Measures` table in the Fields pane
2. **Home → New Measure**
3. Copy-paste each measure from `dax/DAX_Measures.dax`

**Order to create (dependencies matter):**
1. Base measures (Revenue, EBITDA, Net Profit, etc.)
2. Margin % measures
3. YTD / MTD measures
4. PY / Prior Month measures
5. Budget vs Actual measures
6. Rolling averages
7. Ratios
8. Status flags

---

## STEP 6 — Format Measures

For each measure, set the format in the Properties pane:

| Measure Group | Format |
|---------------|--------|
| Revenue, EBITDA, Net Profit | Currency, 2 decimals, $ |
| Margin %, Variance %, Growth % | Percentage, 1 decimal |
| AR/AP Turnover | Fixed decimal, 1 place |
| DSO / DPO | Whole number |
| Rolling Averages | Currency, $#,##0,,M |

---

## STEP 7 — Apply Theme

1. **View → Themes → Browse for themes**
2. Paste the JSON from `docs/Dashboard_Design_Guide.md` into a `.json` file
3. Browse and apply

Or manually set:
- Canvas background: `#0D1B2A`
- Font: Segoe UI throughout

---

## STEP 8 — Build Page 1 (Executive Summary)

### Add Slicers:
1. Insert Slicer visual → Field: `DimDate[Year]`
   - Format: Horizontal, single select, style = Buttons
2. Insert Slicer → `DimDate[Quarter]`
   - Format: Dropdown, multi-select
3. Insert Slicer → `financials[Region]`
   - Format: List, multi-select
4. Insert Slicer → `financials[Business_Unit]`
   - Format: Buttons, single select

### Add KPI Cards:
1. Insert **Card** visual
2. Field: `[Total Revenue]`
3. Format:
   - Title: "💰 Total Revenue"
   - Display unit: Millions
   - Background: #1A2F47
   - Font: White, Segoe UI Semibold 24px
4. Repeat for EBITDA, Net Profit, Cash Flow, Working Capital, EBITDA Margin %

### Add Revenue Trend (Line + Column Combo):
1. Insert **Line and stacked column chart**
2. X-axis: `DimDate[Month]` (sort by MonthNo)
3. Column Y: `[Total Revenue]`
4. Line Y: `[Budget Revenue]`
5. Legend: None
6. Enable data labels on line only

### Add Donut Chart:
1. Insert **Donut chart**
2. Legend: `financials[Region]`
3. Values: `[Total Revenue]`
4. Data colors: use theme palette
5. Enable % data labels

### Add Waterfall:
1. Insert **Waterfall chart**
2. Category: Static breakdown (use a custom table or calculated table)
3. Breakdowns: Revenue → COGS → OpEx → EBITDA

---

## STEP 9 — Build Remaining Pages

Follow the same pattern using the layout in `Dashboard_Design_Guide.md` for:
- Page 2: P&L Deep Dive
- Page 3: Cash Flow & Working Capital
- Page 4: Budget vs Actual

---

## STEP 10 — Add Navigation Buttons

1. Insert **Button → Navigator → Page Navigator**
2. Or manually insert 4 buttons and use Action → Page Navigation
3. Format buttons to match theme

---

## STEP 11 — Add Conditional Formatting

### For KPI Status column in Matrix:
1. Select the matrix visual
2. Right-click the status value → Conditional Formatting → Background Color
3. Use **Field value** and point to `[Revenue Status]` measure

### For Variance % cells:
1. Format → Conditional Formatting → Font color
2. Rules:
   - Value >= 0.05 → Green (#27AE60)
   - Value >= 0 → Yellow (#F1C40F)
   - Value >= -0.05 → Orange (#E67E22)
   - Value < -0.05 → Red (#E74C3C)

---

## STEP 12 — Final Checks Before Publishing

- [ ] All 4 pages load without errors
- [ ] Slicers cross-filter all visuals correctly
- [ ] YTD/MTD measures show correct values
- [ ] Budget vs Actual variance % has conditional formatting
- [ ] All KPI cards have sparklines or trend indicators
- [ ] Page navigation buttons work
- [ ] Mobile layout configured (View → Mobile Layout)
- [ ] Report title and page names are set