# Call_centre
# 📞 Call Centre Performance & Operations Dashboard (Power BI)

An interactive Power BI report analyzing call centre operations, workload distribution, customer sentiment, and SLA response rates across multiple channels and US regions.

---

## 📌 Business Problem & Objectives
Call centre managers need end-to-end visibility into call volumes, service-level compliance, agent utilization across locations, and customer drivers to optimize staffing and reduce churn.

### Key Deliverables:
1. **Total Calls by Day**: Identify peak volume weekdays for capacity planning.
2. **Geographic Distribution**: Filled map showcasing call origin across US states.
3. **Reason Breakdown**: Tree map categorizing primary customer inquiries.
4. **Channel Share**: Donut chart tracking communication channels (Call-Center, Chatbot, Email, Web).
5. **Sentiment Analysis**: Bar chart monitoring customer sentiment distribution.
6. **Centre Performance**: Call volumes handled across individual call centre cities.

---

## 📊 Dashboard Views

### 1. Executive Summary (`Home`)
![Home Dashboard](assets/home_dashboard.png)

* **Top KPIs**:
  * Total Calls: **32.94K**
  * Total Call Duration: **13.74K hrs** (~824.22K min)
  * Average Call Duration: **25.02 min**
  * Response Time SLA Compliance: **75.26%**
* **Operational Visuals**:
  * Call volume trends by day of week (peaking on Thursday and Friday).
  * State-level call volume distribution map.
  * Inflow breakdown by Channel, Reason, and Sentiment.
  * Call distribution by site (Los Angeles, Baltimore, Chicago, Denver).

---

### 2. Tabular Data View (`grid_page`)
![Grid Dashboard](assets/grid_dashboard.png)

* Detailed record-level table with interactive cross-filtering by **Date Range**, **Channel**, and **City**.
* Tracks individual customer interactions, reasons (e.g., Billing Question, Service Outage, Payments), SLA adherence, and specific durations.

---

## 🏗️ Data Model & Schema

![Data Model](assets/data_model.png)

* **Fact Table**: `Call Center_Call Center` (Contains interaction metrics, timestamps, CSAT scores, duration, channel, and sentiment).
* **Dimension Table**: `Date Table` (Custom date dimension linking `Date` to `Call Timestamp`).
* **Relationship**: One-to-Many (`1:*`), single direction filtering from `Date Table` to `Call Center`.

---

## 🧮 Key DAX Measures

```dax
// Total Calls
Total Calls = COUNTROWS('Call Center_Call Center')

// Total Duration (Hours)
Total Duration (Hrs) = DIVIDE(SUM('Call Center_Call Center'[Call Duration In Minutes]), 60, 0)

// Average Duration (Minutes)
Avg Call Duration (Min) = AVERAGE('Call Center_Call Center'[Call Duration In Minutes])

// SLA Response Time %
Response Time % = 
DIVIDE(
    CALCULATE(COUNTROWS('Call Center_Call Center'), 'Call Center_Call Center'[Response Time] = "Within SLA"),
    COUNTROWS('Call Center_Call Center'),
    0
)
