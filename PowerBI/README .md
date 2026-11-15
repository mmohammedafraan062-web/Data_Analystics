# Power BI Business Intelligence Portfolio

This directory contains advanced industrial intelligence and operational performance analytics dashboards created in **Microsoft Power BI**. The solutions feature end-to-end star schema data modeling, complex DAX measure engineering, custom time-intelligence calculations, and modern, executive-level glassmorphic UI design systems.

---

## Projects Overview

| Project | Industry / Domain | Focus Areas | Key Output / Scale | Dashboard Preview |
| :--- | :--- | :--- | :--- | :--- |
| **[AeroHome](AeroHome/)** | Home Appliance Manufacturing | Downtime Root Causes, Production Attainment, Defect Rates, Supplier Delays | 122K Downtime mins, 96.26% Attainment | [View Details](AeroHome/) |
| **[Nova_Tech](Nova_Tech/)** | High-Tech & Precision Engineering | MoM Output Fluctuations, Plant Bottlenecks, Quality Assurance, Global Supply Chain | 1.03M Units Produced, -16.9% Production Drop Diagnostic | [View Details](Nova_Tech/) |

---

## 1. AeroHome Manufacturing — Operations & Downtime Intelligence

![AeroHome Dashboard](AeroHome/Images/Aero%20Home%20Dashboard.png)

* **Directory:** [`PowerBI/AeroHome/`](AeroHome/)
* **Report File:** [`AeroHome/Dashboard/Aero_home.pbix`](AeroHome/Dashboard/Aero_home.pbix)
* **Design Aesthetic:** Deep Neon Purple Cyber-Industrial UI with illuminated glassmorphism cards and KPI iconography.
* **Core Metrics:**
  * **Total Machine Downtime:** `122,329 minutes`
  * **Production Attainment:** `96.26%`
  * **Defect Rate:** `1.71%`
  * **Production Shortfall:** `-41,425 units`
  * **Supplier Delay Rate:** `16.55%`
* **Key Analytical Highlights:**
  * **Downtime Root-Cause Attribution:** Quantifies non-productive hours across material shortages (23K mins), preventive maintenance (22K mins), and machine breakdowns (21K mins).
  * **Geographic Plant Variance:** Diagnostic tracking of production shortfalls across Hyderabad, Pune, Coimbatore, and Chennai.
  * **Machine Health Audit:** Table matrix comparing assembly lines and compressor station efficiencies.

---

## 2. Nova Tech Manufacturing — Plant & Supply Chain Performance

![Nova Tech Dashboard](Nova_Tech/Images/Nova%20Tech%20Dashboard.png)

* **Directory:** [`PowerBI/Nova_Tech/`](Nova_Tech/)
* **Report File:** [`Nova_Tech/Dashboard/NovaTech.pbix`](Nova_Tech/Dashboard/NovaTech.pbix)
* **Design Aesthetic:** Vivid Crimson Red Glow Glassmorphic UI with dynamic alert tiles and period variance indicators.
* **Core Metrics:**
  * **Total Finished Production:** `1,029,692 units`
  * **Quality Defect Rate:** `1.71%`
  * **MoM Production Change:** `-16.92%`
  * **Supplier Delay Rate:** `10.69%`
* **Key Analytical Highlights:**
  * **Decline Decomposition:** Uncovers that Munich Electronics (-13K units) and Monterrey Stamping (-7K units) were the primary contributors to the mid-year production deceleration.
  * **Product Quality Risk:** Identifies Avionics Control Systems as carrying a 4.02% defect rate compared to zero defects in Wind Generators.
  * **Supply Chain Bottlenecks:** Pinpoints Global Parts (18.63% delay) and MexiStamp (18.23% delay) as the main supplier risk factors.

---

## Technical Competencies in Power BI
* **Star Schema Dimensional Modeling:** Implemented 1-to-many relationship structures connecting dimension tables (`dim_plants`, `dim_products`, `dim_operators`, `dim_suppliers`) to event/fact tables via integer surrogate keys.
* **DAX Formulas & Time Intelligence:** Developed dynamic KPI measures utilizing `DIVIDE`, `CALCULATE`, `FILTER`, `DATEADD`, `SAMEPERIODLASTYEAR`, and custom conditional formatting flags.
* **Power Query ETL Pipelines:** Ingested multi-format raw data (Excel workbooks and multi-table CSV files), replaced invalid entries, standardized column types, and established audit logs.
* **Visual Storytelling & UI/UX:** Built high-contrast executive visual layouts featuring custom SVG card icons, neon glass borders, coordinated color palettes, synchronized slicer sync panes, and cross-visual interaction filters.

---

## Directory Organization
```
PowerBI/
├── README.md
├── AeroHome/
│   ├── README.md
│   ├── Dashboard/
│   │   └── Aero_home.pbix
│   ├── Images/
│   │   └── Aero Home Dashboard.png
│   └── Raw/
│       └── AeroHome_Manufacturing_Dataset.xlsx
└── Nova_Tech/
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
    │   └── NovaTech.pbix
    └── Images/
        └── Nova Tech Dashboard.png
```
