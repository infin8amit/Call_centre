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

---<img width="959" height="553" alt="call_cente_ss1" src="https://github.com/user-attachments/assets/abe2cf25-3669-47cc-8c8f-c8a80b4e0e5a" />
<img width="930" height="551" alt="call_cente_ss2" src="https://github.com/user-attachments/assets/3f191580-7825-4255-bee5-1d8218f1e7e7" />



## 🏗️ Data Model & Schema

![Data Model](assets/data_model.png)

* **Fact Table**: `Call Center_Call Center` (Contains interaction metrics, timestamps, CSAT scores, duration, channel, and sentiment).
* **Dimension Table**: `Date Table` (Custom date dimension linking `Date` to `Call Timestamp`).
* **Relationship**: One-to-Many (`1:*`), single direction filtering from `Date Table` to `Call Center`.

---
<img width="689" height="459" alt="Call_center_ss3" src="https://github.com/user-attachments/assets/2ed28954-69cb-4809-a9e7-5c9b67702037" />


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

<img width="760" height="306" alt="image" src="https://github.com/user-attachments/assets/4da6ff68-7e86-42bc-8aa3-d891528797d6" />

