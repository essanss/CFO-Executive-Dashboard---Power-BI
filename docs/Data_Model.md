# Data Model — CFO Executive Dashboard

## Tables & Relationships

### FACT TABLES
| Table | Description | Primary Key |
|-------|-------------|-------------|
| financials | Monthly P&L by Region/BU | Date + Region + Business_Unit |
| cashflow_workingcapital | Monthly cash & WC metrics | Date |
| budget_vs_actual | Budget vs Actual by Region/BU | Date + Region + Business_Unit |

### DIMENSION TABLES (Create in Power Query)
| Table | Description |
|-------|-------------|
| DimDate | Full date table (auto-generated) |
| DimRegion | Region lookup |
| DimBusinessUnit | Business Unit lookup |

---

## DimDate — Power Query M Code
```
let
    StartDate = #date(2024, 1, 1),
    EndDate = #date(2024, 12, 31),
    Duration = Duration.Days(EndDate - StartDate) + 1,
    DateList = List.Dates(StartDate, Duration, #duration(1, 0, 0, 0)),
    DateTable = Table.FromList(DateList, Splitter.SplitByNothing(), {"Date"}),
    ChangedType = Table.TransformColumnTypes(DateTable, {{"Date", type date}}),
    AddYear = Table.AddColumn(ChangedType, "Year", each Date.Year([Date]), Int64.Type),
    AddMonth = Table.AddColumn(AddYear, "Month", each Date.MonthName([Date]), type text),
    AddMonthNo = Table.AddColumn(AddMonth, "MonthNo", each Date.Month([Date]), Int64.Type),
    AddQuarter = Table.AddColumn(AddMonthNo, "Quarter", each "Q" & Text.From(Date.QuarterOfYear([Date])), type text),
    AddWeekday = Table.AddColumn(AddQuarter, "Weekday", each Date.DayOfWeekName([Date]), type text),
    AddYearMonth = Table.AddColumn(AddWeekday, "YearMonth", each Text.From([Year]) & "-" & Text.PadStart(Text.From([MonthNo]), 2, "0"), type text),
    AddIsWeekend = Table.AddColumn(AddYearMonth, "IsWeekend", each Date.DayOfWeek([Date]) >= 5, type logical)
in
    AddIsWeekend
```

---

## Relationships (Star Schema)

```
DimDate[Date]  ──────────────────► financials[Date]
DimDate[Date]  ──────────────────► cashflow_workingcapital[Date]
DimDate[Date]  ──────────────────► budget_vs_actual[Date]
```

### Cardinality:
- DimDate → financials: **1 to Many**
- DimDate → cashflow_workingcapital: **1 to Many**
- DimDate → budget_vs_actual: **1 to Many**
- Cross-filter direction: **Single (DimDate → Fact tables)**

---

## Column Data Types

### financials table
| Column | Type |
|--------|------|
| Date | Date |
| Month | Text |
| Quarter | Text |
| Year | Whole Number |
| Region | Text |
| Business_Unit | Text |
| Revenue | Decimal Number |
| COGS | Decimal Number |
| Gross_Profit | Decimal Number |
| Operating_Expenses | Decimal Number |
| EBITDA | Decimal Number |
| Depreciation | Decimal Number |
| EBIT | Decimal Number |
| Interest_Expense | Decimal Number |
| Tax | Decimal Number |
| Net_Profit | Decimal Number |
| Budget_Revenue | Decimal Number |
| Budget_EBITDA | Decimal Number |
| Budget_Net_Profit | Decimal Number |

### cashflow_workingcapital table
| Column | Type |
|--------|------|
| Date | Date |
| Operating_Cash_Flow | Decimal Number |
| Investing_Cash_Flow | Decimal Number |
| Financing_Cash_Flow | Decimal Number |
| Net_Cash_Flow | Decimal Number |
| Accounts_Receivable | Decimal Number |
| Accounts_Payable | Decimal Number |
| Inventory | Decimal Number |
| Current_Assets | Decimal Number |
| Current_Liabilities | Decimal Number |
| Working_Capital | Decimal Number |
| AR_Days | Whole Number |
| AP_Days | Whole Number |
| Inventory_Days | Whole Number |

---

## Calculated Columns (Add in Power BI)

### In financials table:
```dax
Gross Margin % = DIVIDE([Gross_Profit], [Revenue], 0)
EBITDA Margin % = DIVIDE([EBITDA], [Revenue], 0)
Net Margin % = DIVIDE([Net_Profit], [Revenue], 0)
P&L Period = [Month] & " " & TEXT([Year], "0")
```