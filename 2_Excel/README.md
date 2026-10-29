# 📊 Retail Business Intelligence & Profitability Leakage Analytics (Microsoft Excel)

[![Excel](https://img.shields.io/badge/Microsoft_Excel-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)](https://www.microsoft.com/en-us/microsoft-365/excel)
[![Portfolio](https://img.shields.io/badge/Portfolio-Data_Analytics-blue?style=for-the-badge)](https://github.com/)
[![Author](https://img.shields.io/badge/Author-Mohammed_Afraan-orange?style=for-the-badge)](https://github.com/)

This repository houses two end-to-end commercial retail analytics projects developed in Microsoft Excel by **Mohammed Afraan**. Both projects simulate real-world enterprise retail environments—investigating supply chain dynamics, pricing elasticity, promotional discounts, returns, customer segmentation, and margin leakage.

---

## 🗂️ Project Directory & Quick Links

| Project | Domain | Revenue Analyzed | Profit Margin | Core Focus | Link |
| :--- | :--- | :---: | :---: | :--- | :---: |
| **🛒 FreshMart** | FMCG & Grocery Supermarket | **₹ 28.68 Lakhs** | **25.71%** | Category margin disparity, store target recalibration & afternoon sales optimization | [View FreshMart README](./Project/Freshmart/README.md) |
| **👗 TrendMart (Trendkart)** | Fashion & Apparel Enterprise | **₹ 92.07 Lakhs** | **19.53%** | Discount vs. profitability curve, 4.79% returns leakage & digital e-commerce expansion | [View TrendMart README](./Project/Trendkart/README.md) |

---

## 📌 Comparative Project Overview

```mermaid
graph TD
    A[Excel Data Analytics Portfolio] --> B[FreshMart: FMCG Supermarket]
    A --> C[TrendMart: Fashion Enterprise]

    B --> B1[2,500 Orders | 9,823 Units]
    B --> B2[Key Hero: Bakery 38.9% Margin]
    B --> B3[Leakage: Staples Margin Dilution]
    B --> B4[Core Finding: Unrealistic Store Quotas in ERP]

    C --> C1[2,943 Orders | 6,100 Units]
    C --> C2[Key Issue: Uncontrolled Markdowns >15%]
    C --> C3[Leakage: 4.79% Return Rate = ₹5.75L Loss]
    C --> C4[Core Finding: Offline 93.8% vs Online 6.3%]
```

---

## 🛠️ Advanced Excel Competencies Applied

- **Multi-Table Relational Modeling**: Star-schema architecture connecting transactional fact tables with customer, product, store, employee, and supplier dimensions.
- **Lookup & Reference Functions**: `XLOOKUP`, `VLOOKUP`, `INDEX`, `MATCH`.
- **Date & Time Intelligence**: `HOUR()`, `WEEKDAY()`, and nested `IF()` time slot categorization (`Morning`, `Afternoon`, `Evening`, `Night`).
- **Data Cleansing & Transformation**: Deduplication, whitespace trimming, casing normalization, error-checking, and automated data quality audits.
- **Dynamic Pivot Tables & Slicers**: Multi-pivot caching, synchronized slicers, calculated fields, and conditional formatting data bars.
- **Executive UI/UX Dashboard Design**: Polished corporate color schemes, stat KPI summary cards, donut charts, scatter plots, combo charts, and actionable recommendation panels.

---

## 📂 Repository Structure

```text
2_Excel/
│
├── README.md                                             # Portfolio index (this file)
│
└── Project/
    │
    ├── Freshmart/
    │   ├── Final DashBoard Sheet/
    │   │   └── Mohammed Afraan fresh mart.xlsx           # Interactive dashboard workbook
    │   ├── FreshMart (Cleaned DataSet)/
    │   │   └── FreshMart_ALL_CLEANED.xlsx                # Cleaned relational dataset
    │   ├── FreshMart (Raw DataSet)/                      # Raw multi-table CSV/XLSX sources
    │   ├── freshmart_dashboard.png                       # Dashboard visualization screenshot
    │   └── README.md                                     # In-depth FreshMart project report
    │
    └── Trendkart/
        ├── TrendMart FinalDashboard/
        │   └── Mohammed Afraan trend mart(Final DashBoard).xlsx  # Interactive dashboard workbook
        ├── TrendMart (Cleaned Dataset)/
        │   └── Mohammed Afraan trend mart(cleaned).xlsx          # Cleaned dataset with calculated fields
        ├── TrendMart (Raw Dataset)/                              # Raw dataset with Data Quality Log
        ├── trendmart_dashboard.png                               # Dashboard visualization screenshot
        └── README.md                                             # In-depth TrendMart project report
```

---

## 👨‍💻 Author

**Mohammed Afraan**  
*Data Analyst | Retail Business Intelligence Specialist*
