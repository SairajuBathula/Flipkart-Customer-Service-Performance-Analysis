# Flipkart Customer Service Performance — Power BI Project

> **Status:** Production-ready • **Last updated:** 2025-08-22

This repository/documentation explains a Power BI report that analyzes **Flipkart's customer service performance**.  
It is structured similar to the Coffee Quality project README but tailored for **customer experience and service quality KPIs**.

---

## 📌 Business Goal

Provide a decision-support dashboard for Flipkart’s customer service team to:
- Monitor **customer satisfaction (CSAT) and Net Promoter Score (NPS)**.  
- Analyze **service response times** and **resolution rates**.  
- Identify **top pain points** in customer interactions.  
- Improve operational efficiency through **data-driven insights**.  

---

## 🧰 Tech Stack & Power BI Features

- **Power BI Desktop** (latest version).  
- **Data preparation** with Power Query (M) – data cleaning, transformation, handling nulls.  
- **DAX Measures** for KPIs: CSAT, First Response Time (FRT), Average Handling Time (AHT), Resolution Rate.  
- **Visuals**: Cards, Line/Area Charts, Clustered Bar/Column, Matrix, Funnel, Scatter with trendlines.  
- **Interactions**: slicers for Time, Category, Region; cross-filtering enabled.  
- **Performance optimization**: only measures, no redundant calculated columns.  

---

## 📊 Report Pages & Insights

### 0) **Overview Dashboard**
"https://image2url.com/images/1755846535485-43f7461e-7f93-4d8d-be63-93bd96b15738.png"

- KPIs: **Avg CSAT**, **Avg Resolution Rate**, **Avg First Response Time (FRT)**, **Avg Handling Time (AHT)**.  
- Trendline of **customer satisfaction over time**.  
- **Bar chart**: Complaints by Category (Delivery, Payment, Returns, etc.).  
- **Funnel chart**: Customer complaint lifecycle (Received → Assigned → Resolved → Escalated).  

### 1) **Customer Satisfaction (CSAT) & NPS**
- Line chart: **CSAT trend over months**.  
- Bar chart: **NPS by region/city**.  
- Matrix: breakdown by **customer type (new vs repeat)**.  

### 2) **Response & Resolution Times**
- Card visuals: **Avg First Response Time (FRT)** and **Avg Resolution Time**.  
- Clustered column: response time benchmarks vs actuals.  
- Scatter: correlation between **response time and CSAT**.  

### 3) **Complaint Analysis**
- Bar chart: number of complaints by category (Delivery, Payment, Returns, Support).  
- TreeMap: complaints by **region/warehouse hub**.  
- Line chart: complaints trend over time.  

### 4) **Agent Performance**
- Table: **Top performing agents** by resolution rate.  
- Column chart: Avg Handling Time (AHT) per agent.  
- KPI Cards: escalation rate by agent group.  

### 5) **Escalations & Root Cause**
- Funnel: % of complaints escalated through service hierarchy.  
- Bar chart: root causes of escalations (delay, defective product, miscommunication).  
- Heatmap/Matrix: escalation rate by **region vs category**.  

---

## 🧱 Data Model

**Fact table**: `FactCustomerService`  
Columns:  
`[TicketID]`, `[CustomerID]`, `[Category]`, `[SubCategory]`, `[CreatedDate]`, `[ResolvedDate]`, `[AgentID]`, `[Region]`, `[Status]`, `[ResponseTimeHrs]`, `[ResolutionTimeHrs]`, `[CSATScore]`, `[NPSScore]`  

**Dimensions**:  
- `DimCustomer` (New/Repeat, Segment)  
- `DimAgent` (Agent details, Team, Tenure)  
- `DimDate` (Calendar table for time intelligence)  
- `DimRegion` (Region, City, State)  

---

## 🧮 DAX Measures

```DAX
-- Core KPIs
[Total Tickets] = COUNTROWS(FactCustomerService)
[Resolved Tickets] = CALCULATE(COUNTROWS(FactCustomerService), FactCustomerService[Status] = "Resolved")
[Resolution Rate] = DIVIDE([Resolved Tickets], [Total Tickets])

[Avg CSAT] = AVERAGE(FactCustomerService[CSATScore])
[Avg NPS] = AVERAGE(FactCustomerService[NPSScore])

[Avg Response Time (hrs)] = AVERAGE(FactCustomerService[ResponseTimeHrs])
[Avg Resolution Time (hrs)] = AVERAGE(FactCustomerService[ResolutionTimeHrs])

-- Escalation Rate
[Escalated Tickets] = CALCULATE(COUNTROWS(FactCustomerService), FactCustomerService[Status] = "Escalated")
[Escalation Rate] = DIVIDE([Escalated Tickets], [Total Tickets])

-- Agent Efficiency
[Avg Handling Time] = AVERAGE(FactCustomerService[ResolutionTimeHrs])
```

---

## 🧼 Power Query (M) Checklist

- Convert dates to proper **Date/DateTime** type.  
- Standardize **Region/City** names.  
- Handle nulls for CSAT/NPS where feedback not given.  
- Calculate derived columns (if needed): ResponseTimeHrs = ResolvedDate - CreatedDate.  
- Remove duplicate ticket IDs.  

---

## 🔎 How to Use the Report

1. Open the `.pbix` file in **Power BI Desktop**.  
2. Start at **Overview Dashboard**: check KPIs.  
3. Use slicers for **Time Period, Region, Category**.  
4. Drill into **Customer Satisfaction** for trend insights.  
5. Explore **Agent Performance** for operational efficiency.  
6. Check **Escalations** page for improvement areas.  

---

