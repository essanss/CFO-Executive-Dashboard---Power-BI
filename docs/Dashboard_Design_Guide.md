# Dashboard Design Guide — CFO Executive Dashboard

## Page Layout (4 Report Pages)

---

## PAGE 1 — Executive Summary (Home)
**Theme:** Dark navy (#0D1B2A) | Accent: Gold (#F5A623) | Text: White

### KPI Cards (Top Row — 6 cards)
| Card | Measure | Format | Trend |
|------|---------|--------|-------|
| 💰 Revenue | Total Revenue | $#,##0,,M | MoM Arrow |
| 📈 EBITDA | Total EBITDA | $#,##0,,M | MoM Arrow |
| 🟢 Net Profit | Total Net Profit | $#,##0,,M | MoM Arrow |
| 💧 Cash Flow | Operating Cash Flow | $#,##0,,M | MoM Arrow |
| 🔄 Working Capital | Working Capital | $#,##0,,M | Static |
| 📊 EBITDA Margin | EBITDA Margin % | 0.0% | vs PY |

### Visuals (Middle Row)
| Visual | Type | X-Axis | Y-Axis | Legend |
|--------|------|--------|--------|--------|
| Revenue Trend | Line + Column Combo | Month | Revenue / Budget Revenue | — |
| Revenue by Region | Donut Chart | Region | Total Revenue | Region |
| Budget vs Actual | Clustered Bar | KPI Name | Actual / Budget | — |

### Visuals (Bottom Row)
| Visual | Type | Details |
|--------|------|----------|
| Revenue YoY Growth | Line Chart | Month vs Revenue YoY Growth % |
| EBITDA Waterfall | Waterfall Chart | Revenue → COGS → OpEx → EBITDA |
| KPI Status Table | Matrix | Region × KPI Status flags |

### Slicers
- Year (single select, horizontal buttons)
- Quarter (multi-select, dropdown)
- Region (multi-select, list)
- Business Unit (single select, buttons)

---

## PAGE 2 — P&L Deep Dive

### Visuals
| Visual | Type | Details |
|--------|------|----------|
| P&L Statement | Matrix | Rows: P&L Lines | Cols: Months | Values: $ |
| Revenue Decomposition | Stacked Column | By Region + Business Unit |
| EBITDA Bridge | Waterfall | Month-over-Month EBITDA changes |
| Margin Trends | Multi-Line Chart | Gross / EBITDA / Net Margin % |
| Rolling 3M Averages | Line Chart | Revenue + EBITDA 3M rolling |

---

## PAGE 3 — Cash Flow & Working Capital

### KPI Cards
- Operating Cash Flow
- Net Cash Flow
- Working Capital
- Current Ratio
- DSO / DPO

### Visuals
| Visual | Type | Details |
|--------|------|----------|
| Cash Flow Waterfall | Waterfall | Op / Inv / Fin → Net |
| AR vs AP Trend | Line (dual axis) | Month vs AR / AP |
| Working Capital Trend | Area Chart | Month vs Working Capital |
| Cash Conversion Cycle | Gauge | CCC vs Target (45 days) |
| AR/AP Turnover | Clustered Column | Monthly AR Turnover + AP Turnover |

---

## PAGE 4 — Budget vs Actual Variance

### KPI Cards
- Revenue Variance %
- EBITDA Variance %
- Net Profit Variance %
- OpEx Variance %

### Visuals
| Visual | Type | Details |
|--------|------|----------|
| Variance Table | Matrix | Region × Month × Variance % |
| Budget vs Actual Trend | Line (combo) | Actual vs Budget by Month |
| Variance Heatmap | Matrix with CF | Green/Amber/Red cells |
| YTD Performance | Gauge × 3 | Revenue / EBITDA / Net Profit |
| Variance by Region | Bar Chart | Horizontal, sorted by variance |

---

## Color Coding Rules (Conditional Formatting)

| Condition | Color |
|-----------|-------|
| Variance % >= 5% (Exceeded) | 🟢 #27AE60 |
| Variance % 0–5% (On Track) | 🟡 #F1C40F |
| Variance % -5% to 0% (At Risk) | 🟠 #E67E22 |
| Variance % < -5% (Behind) | 🔴 #E74C3C |

---

## Theme JSON (Paste in Power BI → View → Themes → Customize)

```json
{
  "name": "CFO Executive",
  "dataColors": ["#F5A623", "#2ECC71", "#3498DB", "#E74C3C", "#9B59B6", "#1ABC9C"],
  "background": "#0D1B2A",
  "foreground": "#FFFFFF",
  "tableAccent": "#F5A623",
  "visualStyles": {
    "*": {
      "*": {
        "fontFamily": [{"value": "Segoe UI"}],
        "fontSize": [{"value": 11}]
      }
    }
  }
}
```

---

## Visual Formatting Standards

- **Title Font:** Segoe UI Semibold, 14px
- **Data Labels:** Show on KPI cards and donut chart only
- **Gridlines:** Subtle, 30% opacity
- **Borders:** 1px, color #1E3A5F
- **Card Background:** #1A2F47 (slightly lighter than page bg)
- **Chart Background:** Transparent
- **Legend Position:** Bottom, 10px font