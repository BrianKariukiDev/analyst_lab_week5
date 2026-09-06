# HealthConnect Appointment No-Show Analysis

## Executive Summary
This repository contains the Week 5 data cleaning, exploratory data analysis (EDA), and baseline KPI evaluation for the **HealthConnect** clinical appointment dataset. The goal of this analysis is to identify operational bottlenecks driving patient no-shows and evaluate intervention strategies (such as automated appointment reminders and queue management).

---

## Dataset Overview & Data Engineering

The raw dataset comprises 5,000 clinical appointment records. A data cleaning pipeline was executed to resolve missingness, type mismatches, and structural inconsistencies prior to analysis.

### Data Cleaning & Audit Log

| Field Name | Initial Data Type | Quality / Integrity Issue Identified | Resolution & Imputation Strategy |
| :--- | :---: | :--- | :--- |
| `distance_to_clinic_km` | `Float64` | 90 missing values | Imputed using clinic location subgroup medians to preserve spatial distribution. |
| `waiting_time_minutes` | `Float64` | 60 missing values | Imputed using service type subgroup medians to account for care complexity. |
| `reminder_channel` | `Categorical` | 1,366 missing values | Explicitly encoded as `'No Reminder Sent'` categorical level. |
| `appointment_date` | `Object` / `String` | Non-standard string format | Standardized to ISO `Datetime64` objects for temporal indexing. |

*Cleaned output saved as:* `HealthConnect_Appointment_Data_Cleaned.csv`

---

## Key Performance Indicators (KPIs)

Below are the key metrics computed from the cleaned dataset:

| KPI Metric | Baseline Value | Key Operational Takeaway |
| :--- | :---: | :--- |
| **Overall No-Show Rate** | **48.46%** | 2,423 missed visits out of 5,000 total scheduled appointments. |
| **Reminder Attendance Uplift** | **+4.95%** | Attendance rate of **47.63%** (Reminder Sent) vs **42.68%** (No Reminder Sent). |
| **Average Booking Lead Time Gap** | **24.52 vs 34.53 Days** | Attended visits average **24.52 days** lead time; No-Show visits average **34.53 days**. |
| **High Wait-Time (>30m) Drop-off** | **47.67%** | Appointments experiencing >30 min clinic wait times show an elevated no-show/drop-off rate. |

---

## Key Insights & Recommendations

1. **Lead Time Interventions:**  
   Appointments scheduled over 20+ days in advance experience significantly higher failure-to-attend rates (+10 days lead time gap). Implement mandatory 72-hour re-confirmation workflows for long-lead bookings.

2. **Multi-Channel Reminders:**  
   Automated reminders deliver a demonstrable **+4.95% uplift** in patient attendance. Expand active SMS and WhatsApp confirmation integrations across all clinic branches.

3. **Queue & Scheduling Optimization:**  
   Excessive in-clinic waiting times (>30 minutes) correlate with higher patient churn and missed follow-ups (**47.67%** no-show rate). Re-align appointment scheduling slots by service type to maintain queue times under 20 minutes.

---

## Project Structure

```text
.
├── HealthConnect_Appointment_Data_Cleaned.csv   # Cleaned primary dataset
├── HealthConnect_Week5_Initial_Analysis_Report.pdf # Final executive PDF summary
├── eda_analysis.py                              # Data processing & visualization script
└── README.md                                    # Project documentation