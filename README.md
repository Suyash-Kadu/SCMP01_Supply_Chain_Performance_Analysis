# 🌐 Supply Chain Operations Center: End-to-End Analytics

## 📖 Introduction
This project provides a comprehensive, data-driven visualization of the complete Supply Chain Cycle. By tracking the flow of materials and goods through sequential stages (Supplier ➡️ Manufacturer ➡️ Distributor ➡️ Retailer ➡️ Customer), this Power BI suite offers granular visibility into operational efficiency, cost management, and quality control. Currently, the project features deep-dive analytical dashboards for the first three critical stages: The Supplier, The Manufacturer, and The Distributor.

## 💼 Business Problem
Without end-to-end visibility, leadership teams struggle to identify root causes of margin erosion and delays.
1. Procurement cannot accurately identify which suppliers have the highest rejection rates or longest lead times.
2. Manufacturing lacks real-time insight into machine utilization and raw material waste (scrap).
3. Logistics cannot easily correlate shipping costs with specific transportation modes or identify over-reliance on a single distributor.
4. This project solves these blind spots by providing centralized, interactive business intelligence.

## 🛠️ Tech Stack Used

1. Data Storage: Google Sheets (serving as a live, highly accessible primary database).
2. BI & Visualization: Power BI (used as the primary engine for data modeling and visual UI).
3. Data Generation & Scripting: Python / pandas (used to generate realistic, linked mock data and batch numbers across the supply chain).
4. Logic Engine: DAX (Data Analysis Expressions) for dynamic aggregations and time intelligence.

## 🗄️ Data Gathering & Modelling
To build a highly analytical data model, I established a strict "chain of custody" data lineage rather than relying on isolated tables.
1. The Blueprint: The data model relies on a relational structure where tables interact via 1:N relationships to ensure accurate cross-filtering.
2. Inheritance Logic: Using Python, I structured the data so that a Customer's Batch No. matches the exact Batch No. of the Retailer, which maps perfectly up to the Distributor and back to the Manufacturer.
3. The Result: If a user clicks on a specific Batch No. in the Manufacturer view, the model accurately filters down the entire pipeline to show exactly which distributors and customers received products from that specific production run.

## 🧮 DAX Queries
The dashboards rely heavily on custom DAX measures to aggregate raw data into actionable KPIs. Here are a few core examples from the project:

#### 1. Scrap Percentage (Manufacturing Efficiency)
Calculates the ratio of wasted material to total consumed material.
scrap_percentage = (SUM('Manufacturer'[Scrap Qty]) * 100) / SUM('Manufacturer'[Qty Consumed])

#### 2. Top Consumer Percentage (Material Usage)
Evaluates how much of a specific product code was consumed relative to the maximum consumption across all selected products.
top_% = (SUM('Manufacturer'[Qty Consumed]) / MAXX(ALLSELECTED('Manufacturer'[Product Code]), CALCULATE(SUM('Manufacturer'[Qty Consumed]))))*100

#### 3. Average Lead Time (Logistics Tracking)
Calculates the internal warehouse processing time by finding the difference between when an order is placed and when it is physically dispatched.
avg_lead_time = DATEDIFF('Distributor'[Order Date], 'Distributor'[Distribution Date], DAY)

## 🏭 Stage 1: Supplier Performance Dashboard
Focused entirely on procurement metrics and raw material intake.
1. Quality Control Insights: Tracks the total volume of products received versus the amount rejected to monitor overall supplier reliability.
2. Delivery Volume: A dynamic Pie Chart visualizes the total quantity delivered by individual suppliers to identify highest-volume partners.
3. Cost Analysis: Evaluates the average unit cost of products across various suppliers.
Lead Time Tracking: A detailed matrix visually highlights the core lead time (in days) per supplier using conditional formatting.

## ⚙️ Stage 2: Manufacturer Performance Dashboard
Focused on the factory floor, tracking the conversion of raw materials (RM) to finished goods (FG).
1. RM Consumption: A Funnel Chart dynamically tracks material usage percentages, allowing for a quick scan of utilization rates.
2. Production Breakdown: A Tree Map illustrates Category Wise Production across Engine Parts, Electronics, and Fasteners.
3. Material Efficiency: Donut Charts compare the Sum of Required Qty vs Consumed Qty to pinpoint potential waste.
4. Machine Allocation: Tracks Total Machine Usage based on specific Finished Goods to monitor facility distribution.

## 🚚 Stage 3: Distributor Performance Dashboard
Focused on outbound logistics, shipping costs, and demand projection.
1. Demand Forecasting: A line chart plotting historical order volume with predictive, curved forecasting to anticipate future geographic demand.
2. Cost-to-Serve Analysis: A Combo Chart (Line and Clustered Column) plotting Total Shipping Cost against Grand Total Revenue by Mode of Transportation (Truck, Container, Rail) to evaluate margin erosion.
3. Concentration Risk: A Treemap visualizes Revenue Share by Distributor. This answers the critical executive question: How much of our total revenue relies on our top 3 distributors?

## 🎯 Conclusion
This project demonstrates a complete end-to-end understanding of Supply Chain Analytics. By combining robust data modeling techniques, realistic data generation, advanced DAX logic, and UX-focused dashboard design, it bridges the gap between raw database tables and strategic business decisions. From monitoring raw material defects to projecting regional demand, these dashboards provide the actionable intelligence required to run a lean, profitable supply chain operation.
