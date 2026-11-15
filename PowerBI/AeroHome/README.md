# AeroHome Manufacturing — Operations & Downtime Intelligence

![AeroHome Dashboard](Images/Aero%20Home%20Dashboard.png)

## Executive Summary
**AeroHome Manufacturing** is a premier home appliance manufacturer producing washing machines, air conditioners, refrigerators, microwave ovens, and dishwashers across multi-city factory plants.

This project delivers an enterprise-grade operational intelligence dashboard developed in **Microsoft Power BI**. The dashboard tracks manufacturing attainment, plant throughput, machine downtime root causes, product defect rates, and supply chain vendor reliability with a modern, futuristic dark neon-purple glassmorphic interface.

---

## Key Performance Indicators (KPIs)
* **Total Machine Downtime:** `122,329 minutes` (~2,039 hours)
* **Production Attainment %:** `96.26%` (Against planned capacity targets)
* **Product Defect Rate %:** `1.71%` (Well within industry benchmark thresholds)
* **Production Shortfall:** `-41,425 units` (Cumulative gap between target & actual production)
* **Supplier Delay Rate %:** `16.55%` (Share of delayed component purchase orders)

---

## Dashboard Architecture & Visualizations

```
+-------------------------------------------------------------------------------------------------------------------+
|                                            AEROHOME MANUFACTURING                                                 |
|                               Manufacturing Performance & Operations Intelligence                                 |
+-------------------------------------------------------------------------------------------------------------------+
|  [FILTERS]       | Total Downtime   Production Attain %   Defect Rate %   Production Shortfall   Supplier Delay % |
|  - Plant Name    |    122,329             96.26%              1.71%             -41,425               16.55%      |
|  - Product Name  +------------------------------------------------------------------------------------------------+
|  - Supplier Name | Production Attainment Trend   | Downtime by Reason (mins)     | Supplier Delay Analysis        |
|  - Period        | 94% - 98% trajectory across   | - Material Shortage: 23K      | Area & combo chart analyzing   |
|                  | Jan 2024 - Dec 2024           | - Preventive Maint:  22K      | on-time vs delayed POs by      |
|                  |                               | - Machine Breakdown: 21K      | vendor (Precision, Electra,    |
|                  |                               | - Changeover:        19K      | CoolTech, Prime, Global...)    |
|                  |                               | - Operator Absence:  19K      |                                |
|                  |                               | - Electrical Issues: 18K      |                                |
|                  +-------------------------------+-------------------------------+--------------------------------+
|                  | Defect Rate by Product        | Production Shortfall by Plant | Machine Performance Analysis   |
|                  | AeroCool, AeroFrost, AeroDry  | Hyderabad (-8K) -> Pune (-9.6K| Assembly Line 1 (96.37%)       |
|                  | ranges between 1.5% - 2.0%    | -> Coimbatore (-11K) ->       | Assembly Line 2 (94.17%)       |
|                  |                               | Chennai (-12.2K)              | Compressor Station (97.28%)    |
+-------------------------------------------------------------------------------------------------------------------+
```

### Visual Breakdown
1. **Production Attainment Trend (Line Chart):** Illustrates monthly attainment consistency, hovering between 94% and 98%, highlighting dip periods (July/August) and post-maintenance recovery.
2. **Downtime by Reason (Ranked Bar Chart):**
   * **Material Shortage:** `23,000 mins` (Primary driver of plant idle time)
   * **Preventive Maintenance:** `22,000 mins`
   * **Machine Breakdown:** `21,000 mins`
   * **Changeover Time:** `19,000 mins`
   * **Operator Absence:** `19,000 mins`
   * **Electrical Issues:** `18,000 mins`
3. **Supplier Delay Analysis (Multi-Metric Visual):** Evaluates vendor reliability across component suppliers, identifying critical bottleneck partners (`Precision Parts`, `Electra Supplies`, `CoolTech`).
4. **Defect Rate by Product:** Benchmarks defect percentages across product lines (*AeroCool Refrigerators*, *AeroFrost Freezers*, *AeroDry Dishwashers*, *AeroClean Washers*), highlighting lines requiring stricter QA tolerances.
5. **Production Shortfall by Plant:** Evaluates geographic variance across manufacturing facilities: *AeroHome Hyderabad*, *Pune Plant*, *Coimbatore*, and *Chennai Plant*, identifying plants with the steepest production deficits.
6. **Machine Performance Analysis (Data Matrix):** Deep-dive matrix inspecting machine uptime, line attainment percentages, and cumulative downtime hours across assembly lines.

---

## Data Model & DAX Architecture

### Star Schema Design
The data model connects 6 dimension & bridge tables to 4 core fact tables:
* **Dimensions:** `dim_plants`, `dim_products`, `dim_machines`, `dim_operators`, `dim_suppliers`, `dim_materials`
* **Bridge Table:** `bridge_bill_of_materials` (Mapping product assemblies to raw materials)
* **Fact Tables:** `fact_production`, `fact_quality`, `fact_downtime`, `fact_purchase_orders`

### Key DAX Measures
```dax
// Production Attainment %
Production Attainment % = 
DIVIDE(
    SUM(fact_production[actual_units]), 
    SUM(fact_production[planned_units]), 
    0
)

// Production Shortfall
Production Shortfall = 
SUM(fact_production[actual_units]) - SUM(fact_production[planned_units])

// Defect Rate %
Defect Rate % = 
DIVIDE(
    SUM(fact_quality[defect_units]), 
    SUM(fact_production[actual_units]), 
    0
)

// Supplier Delay %
Supplier Delay % = 
DIVIDE(
    CALCULATE(COUNTROWS(fact_purchase_orders), fact_purchase_orders[is_delayed] = TRUE()),
    COUNTROWS(fact_purchase_orders),
    0
)

// Total Downtime Minutes
Total Downtime Minutes = 
SUM(fact_downtime[downtime_minutes])
```

---

## Directory Organization
```
PowerBI/AeroHome/
├── README.md
├── Dashboard/
│   └── Aero_home.pbix                    # Power BI master analytical report
├── Images/
│   └── Aero Home Dashboard.png           # High-resolution dashboard capture
└── Raw/
    └── AeroHome_Manufacturing_Dataset.xlsx
```

---

## Operational Recommendations
1. **Material Shortage Mitigation:** Material shortages represent `23,000 minutes` of lost machine capacity. Re-evaluating reorder points with high-delay suppliers (`16.55%` delay rate) will substantially reduce factory line stoppages.
2. **Plant Support for Chennai & Coimbatore:** Chennai and Coimbatore exhibit the largest production shortfalls (`-12.2K` and `-11.1K` units). Prioritize predictive maintenance and shift balance in these units.
3. **Line 2 Optimization:** Assembly Line 2 records `94.17%` attainment compared to `97.28%` at the Compressor Station. Operator cross-training and faster tooling changeover can close this gap.
