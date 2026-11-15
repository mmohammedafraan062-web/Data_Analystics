# Nova Tech Manufacturing — Plant & Supply Chain Performance

![Nova Tech Dashboard](Images/Nova%20Tech%20Dashboard.png)

## Executive Summary
**Nova Tech Manufacturing** is a multinational industrial producer specializing in high-precision engineering components across Aerospace, Avionics, Electric Motors, Renewable Energy (Solar & Wind), and Home Automation systems.

This project delivers an executive manufacturing performance and supply chain intelligence dashboard built in **Microsoft Power BI**. Styled with a high-contrast crimson glassmorphic aesthetic, the dashboard provides granular visibility into plant-level output fluctuations, downtime correlations, component defect variations, and global supplier on-time delivery metrics.

---

## Key Performance Indicators (KPIs)
* **Total Production Output:** `1,029,692 units` (>1.02M finished components)
* **Defect Rate:** `1.71%` (Average QA defect percentage across manufacturing runs)
* **Month-over-Month Production Change:** `-16.92%` (Alerting executive leadership to mid-year production deceleration)
* **Supplier Delay Rate:** `10.69%` (Share of delayed component procurements)

---

## Dashboard Architecture & Visualizations

```
+-------------------------------------------------------------------------------------------------------------------+
|                                             NOVA TECH MANUFACTURING                                               |
+-------------------------------------------------------------------------------------------------------------------+
|  [FILTERS]       | Total Production     Defect Rate        Production Change      Supplier Delay Rate             |
|  - Plant Name    |    1,029,692            1.71%                -16.92%                  10.69%                   |
|  - Product Name  +------------------------------------------------------------------------------------------------+
|  - Supplier Name | Monthly Production Trend      | Production Decline by Plant    | Production Decline by Product |
|  - Period        | 40K - 50K units monthly range | May 2025 vs Jun 2025           | Jun 2025 variance analysis:   |
|                  | Jan 2025 - Jan 2026           | - Detroit Engine Plant:  -5K   | - Avionics Control:  +1.0K    |
|                  | High: Apr/Aug (49K)           | - Monterrey Stamping:    -7K   | - Aerospace Turbines: +0.1K   |
|                  | Low:  Nov/Jun (40K)           | - Munich Electronics:   -13K   | - Electric Motors:   -0.2K    |
|                  +-------------------------------+--------------------------------+-------------------------------+
|                  | Downtime Impact on Production | Defect Rate by Product Line    | Supplier Delay Rate by Vendor |
|                  | May vs Jun comparison across  | - Avionics Control:     4.02%  | - Global Parts:        18.63% |
|                  | major industrial facilities   | - Aerospace Turbines:   2.11%  | - MexiStamp Industries: 18.23%|
|                  |                               | - Solar Inverters:      2.02%  | - Shanghai Electronics: 14.87%|
|                  |                               | - Home Automation:      1.91%  | - Bosch Electrical:     7.89% |
|                  |                               | - EV Battery Packs:     0.99%  +-------------------------------+
|                  |                               | - Wind Generators:      0.00%  | Plant-Product Matrix Analysis |
+-------------------------------------------------------------------------------------------------------------------+
```

### Visual Breakdown
1. **Monthly Production Trend (Area / Line Chart):** Tracks cumulative production volume across 13 months (Jan 2025 – Jan 2026), highlighting consistent baselines between 41K and 49K units, with sharp seasonal volatility in May-June.
2. **Production Decline by Plant (Variance Visualizer):** Direct period-over-period comparative diagnostic isolating the -16.92% production drop:
   * **Munich Electronics Plant:** `-13,000 units drop` (Critical bottleneck)
   * **Monterrey Stamping Plant:** `-7,000 units drop`
   * **Detroit Engine Plant:** `-5,000 units drop`
3. **Production Decline by Product (Diverging Waterfall / Bar):** Isolates specific product assembly shortfalls during the downturn window.
4. **Downtime Impact on Production:** Multi-plant downtime correlation chart comparing machine stoppage hours between May and June.
5. **Defect Rate by Product Line:**
   * **Avionics Control Systems:** `4.02%` (Highest defect rate; requires calibration)
   * **Aerospace Turbines:** `2.11%`
   * **Solar Inverters:** `2.02%`
   * **Home Automation:** `1.91%`
   * **EV Battery Packs:** `0.99%`
   * **Wind Turbine Generators:** `0.00%` (Zero defects observed)
6. **Supplier Delay Rate by Vendor:**
   * **Global Parts Inc:** `18.63%` delay
   * **MexiStamp Industries:** `18.23%` delay
   * **Shanghai Electronics:** `14.87%` delay
   * **Bosch Electrical:** `7.89%` delay
7. **Plant-Product Matrix Analysis:** Hierarchical multi-level grid allowing operational leaders to drill from Plant -> Product Line -> Workstation.

---

## Data Model & DAX Architecture

### Star Schema Design
The data model connects 5 normalized dimension tables and 1 bridge table to 2 core transaction fact tables:
* **Dimension Tables:**
  * `dim_plants.csv`: Plant locations (Detroit, Monterrey, Munich, Shanghai), capacities, and operational dates.
  * `dim_products.csv`: Product catalog, engineering categories, unit costs, target prices, and weights.
  * `dim_operators.csv`: Workforce IDs, shift assignments (Morning, Afternoon, Night), hourly rates, experience.
  * `dim_suppliers.csv`: Vendor catalog, rating scores, and headquarters countries.
  * `dim_raw_materials.csv`: Bill-of-materials components, unit measures, and standard costs.
* **Bridge Table:** `bridge_bill_of_materials.csv` (Multi-part subassembly mapping).
* **Fact Tables:**
  * `fact_production_runs.csv`: Granular production run batches, units produced, defect quantities, downtime minutes, energy consumption.
  * `fact_purchase_orders.csv`: Procurement purchase orders, order quantities, delivery lead times, and delay status flags.

### Key DAX Measures
```dax
// Total Production
Total Production = 
SUM(fact_production_runs[quantity_produced])

// Defect Rate %
Defect Rate % = 
DIVIDE(
    SUM(fact_production_runs[quantity_defective]), 
    SUM(fact_production_runs[quantity_produced]), 
    0
)

// MoM Production Change %
Production Change % = 
VAR CurrentProd = [Total Production]
VAR PriorProd = CALCULATE([Total Production], DATEADD('dim_calendar'[Date], -1, MONTH))
RETURN
DIVIDE(CurrentProd - PriorProd, PriorProd, 0)

// Supplier Delay Rate %
Supplier Delay Rate % = 
DIVIDE(
    CALCULATE(COUNTROWS(fact_purchase_orders), fact_purchase_orders[is_delayed] = 1),
    COUNTROWS(fact_purchase_orders),
    0
)
```

---

## Directory Organization
```
PowerBI/Nova_Tech/
├── README.md
├── CSV/
│   ├── bridge_bill_of_materials.csv
│   ├── dim_operators.csv
│   ├── dim_plants.csv
│   ├── dim_products.csv
│   ├── dim_raw_materials.csv
│   ├── dim_suppliers.csv
│   ├── fact_production_runs.csv
│   └── fact_purchase_orders.csv
├── Dashboard/
│   └── NovaTech.pbix                     # Master Power BI analytical report
└── Images/
    └── Nova Tech Dashboard.png           # High-resolution dashboard capture
```

---

## Operational Recommendations
1. **Munich Electronics Intervention:** The Munich plant accounts for 52% of the mid-year production deficit (-13K units). Engineering teams should investigate sensor and PCB fabrication lines.
2. **Avionics Quality Control:** Avionics components record an unacceptable `4.02%` defect rate. Implement automated optical inspection (AOI) stations prior to final assembly.
3. **Vendor SLA Enforcement:** Both Global Parts (`18.63%`) and MexiStamp (`18.23%`) exceed permissible delay contracts. Introduce vendor penalty clauses or split order volumes with secondary suppliers.
