# 📦 NHS Pharma Supply Chain & Logistics Performance Dashboard  
### Power BI | SQL | Power Query | DAX | Data Storytelling | Procurement Analytics

---

## 📌 **Project Description**

This project presents an end-to-end **interactive Supply Chain & Logistics Analytics Dashboard** for NHS Pharma suppliers.  
It analyses **order fulfilment, delivery reliability, storage compliance, cost impact, and supplier performance**, enabling Supply Chain, Procurement, and Operations teams to make informed, data-driven decisions.

The report consists of **four dashboards**:

1. **Order Fulfilment & Delivery Efficiency Overview**  
2. **Delivery Performance & Cost Imapact Analysis**  
3. **Medicine Storage Efficiency & Cost Imapact Analysis**  
4. **Summary & Strategic Recommendations**

This project demonstrates capabilities in **ETL, data cleaning, modelling, KPI development, root-cause analysis, procurement insight generation, and professional BI report design**.

---

## 🧩 **Problem Statement**

The NHS pharma supply chain handles thousands of orders across multiple suppliers, but leadership lacked:

- A **centralised view** of supplier fulfilment and delivery performance  
- Visibility into the **financial impact of delays**  
- Insight into **wastage drivers and poor storage compliance**  
- A clear understanding of **which suppliers contribute most to inefficiencies**  
- A structured summary to support **SLA negotiation and supplier performance management**

This dashboard solves these problems by integrating multiple datasets, transforming them, and presenting **clear, actionable performance intelligence**.

---

## 🏥 **Business Context**

Efficient delivery and correct product storage are critical to NHS operations because delays or incorrect handling:

- Affect patient care  
- Disrupt pharmacy workflows  
- Increase operational costs  
- Reduce supply chain reliability  
- Generate avoidable waste  

This dashboard was built to support:  
- **Procurement category reviews**  
- **Supplier performance meetings**  
- **SLA revisions**  
- **Quarterly business reviews (QBRs)**  
- **Cost-saving and waste-reduction initiatives**

---

## 📥 **Dataset & ETL Overview**

### **Data Sources**
- CSV extracts from NHS pharma order systems  
- Excel files for additional cleaning  
- SQL used for exploratory analysis and validation  

### **ETL Process (End-to-End)**  
1. **Extraction**  
   - Imported CSV files into Power BI using Power Query  
   - Validated raw data in SQL (NULL checks, duplicates, datatypes)

2. **Transformation (SQL,Powerbi)**  
   - Removed duplicates  (SQL)
   - Standardised date formats  (SQL)
   - Fixed inconsistent supplier names  (SQL)
    - Handled missing or invalid values (SQL)
   - Ensured correct data types (SQL)
   - Created calculated columns (delivery status, storage accuracy)  (Powerbi)
   

3. **Loading**  
   - Loaded the transformed tables into Power BI Model  
   - Built relationships and star-schema style modelling  


---

Upload your files into these folders when building your GitHub repo.

---

## 📥 **Dataset & ETL Overview**

### **Data Sources**
- CSV extracts from NHS pharma order systems  
- Excel files for additional cleaning  
- SQL used for exploratory analysis and validation  

### **ETL Process (End-to-End)**  
1. **Extraction**  
   - Imported CSV files into Power BI using Power Query  
   - Validated raw data in SQL (NULL checks, duplicates, datatypes)

2. **Transformation (Power Query)**  
   - Removed duplicates  
   - Standardised date formats  
   - Fixed inconsistent supplier names  
   - Created calculated columns (delivery status, storage accuracy)  
   - Handled missing or invalid values  
   - Ensured correct data types

3. **Loading**  
   - Loaded the transformed tables into Power BI Model  
   - Built relationships and star-schema style modelling  

This satisfies ETL/ELT requirements expected in professional analytics roles.

---

## 🛠️ **Data Cleaning & Transformation (Details)**

See `/Documentation/data_transformation.md` and `/Documentation/data_cleaning.md` for full steps, but summary:

### **Power Query Tasks**
- Trim & clean supplier names  
- Split delivery timestamp into date & time  
- Create Flags like additional columns of storage_temp like ambient&room_temp into ambient ,cold_chain & refrigerated into refrigerated
  - On-Time / Late  
  - Created calculated column and set Set storage _temp into the ideal_storage and storage_match for  Correct / Incorrect Storage  
- Remove unused columns  
- Merge lookup tables  
- Create parameterised queries for reusability  

### **SQL Checks Used**
```sql
SELECT supplier_name, COUNT(*) 
FROM orders
GROUP BY supplier_name;

SELECT *
FROM orders
WHERE delivery_date IS NULL;

Excel Checks

VLOOKUP validation

Pivot exploration

Missing value comparisons


📐 DAX Measures Used
See full list in /Documentation/dax_measures.md.

Key measures include:

DAX
Fulfilment Rate = DIVIDE([Completed Orders], [Total Orders])

On Time Delivery % = DIVIDE([On Time Orders], [Total Orders])

Delayed Delivery % = DIVIDE([Delayed Orders], [Total Orders])

Incorrect Storage % = DIVIDE([Incorrect Storage], [Total Orders])

Total Delay Cost = SUM(Orders[Delayed_Cost])

Total Waste Cost = SUM(Orders[Wastage_Cost])


📊 Dashboard Walkthrough
## 📊 Dashboard 1 – Fulfilment Overview
![dashaboard1](https://github.com/ibromacy/NHS-pharmacy-delivery-Cost-impact-analysis/blob/main/Screenshot_dashaboard1.png?raw=true)

1️⃣ Fulfilment, On-Time Delivery & Storage Accuracy Overview
Key Findings:

Overall fulfilment rate appears strong at 95.41%

But deeper analysis shows:

On-time delivery fell by 0.3% YoY

26.65% of all orders were delayed

32.70% of orders recorded incorrect storage handling

The high fulfilment KPI masked hidden inefficiencies

2️⃣ Delayed Delivery Cost Impact & Supplier Breakdown
Key Findings:

Total delayed delivery cost: £1.73M

Supplier Healquick:

Responsible for 33.33% of all delayed deliveries

£0.47M of delay-related costs

60 delayed orders → major SLA breach

Immediate supplier performance intervention required

3️⃣ Wastage Cost & Storage Compliance Analysis

![Screenshot_dashboard3](https://github.com/ibromacy/NHS-pharmacy-delivery-Cost-impact-analysis/blob/main/Screenshot_dashboard3.png?raw=true)
![dashboard 3](https://raw.githubusercontent.com/ibromacy/NHS-pharmacy-delivery-Cost-impact-analysis/refs/heads/main/Screenshot_dashboard3.png)
Key Findings:

Total wastage cost: £4.83M

Wastage breakdown:

Returned/Cancelled — unavoidable in some cases

Incorrect storage — fully preventable

Correct storage rate declined 0.9% YoY

Major contributors:

UKPharma: £1.22M (incorrect storage)

NHS Supply Chain: £1.07M

Storage practices are declining and driving multi-million-pound losses.

4️⃣ Summary & Recommendations Dashboard

This page consolidates all insights into an executive summary.

🧠 Cross-Page Insight: Q3 Operational Spike

Across fulfilment, delays, and wastage datasets, Q3 consistently shows peaks.

Possible causes:

Seasonal demand

Staff shortages

Supplier capacity bottlenecks

Logistics congestion

This pattern requires proactive pre-Q3 planning and risk mitigation.

📝 Strategic Recommendations
1. Supplier SLA Re-Alignment

Renegotiate with Healquick, UKPharma, and NHS Supply Chain

Introduce:

On-time delivery penalty clauses

Storage compliance KPIs

Mandatory quarterly performance reviews

2. Strengthen Supplier Relationship Management (SRM)

Conduct root-cause sessions

Implement supplier scorecards

Agree on monthly forecasting meetings

3. Storage Process Improvement

Introduce cold-chain temperature monitoring

Mandatory storage compliance certification

Quarterly audits

Introduce QR-code scanning for storage verification

4. Reduce Wastage Through Sustainability

Introduce recycling partnerships for damaged packaging

Redirect safe unused medicines to approved redistribution channels

Use supplier penalty recoveries to fund sustainability projects

Convert recyclables into revenue (cardboard, plastic, pallets)

5. Q3 Risk Management Plan

Increase safety stock

Lock in supplier capacity early

Implement predictive forecasting models

Deploy temporary warehousing if needed

🚀 What This Project Demonstrates

This portfolio project showcases:

End-to-end ETL

Complex Power Query transformations

Robust DAX modelling

Professional dashboard storytelling

Supplier performance analytics

Procurement-focused insights

Cost-saving and sustainability thinking

Executive-level recommendations

