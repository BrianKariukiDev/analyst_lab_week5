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
```




# HealthConnect Appointment No-Show Analysis

## Week 6: Advanced Analytics & Cross-Track Integration

Building directly on the Week 5 baseline dataset (48.46% overall no-show rate), Week 6 advances from exploratory data analysis into formal statistical hypothesis validation and feature engineering for model integration.

---

### 1. Statistical Hypothesis Validation

| Hypothesis / Feature Test | Test Statistic | p-Value | Statistical Conclusion |
| :--- | :---: | :---: | :--- |
| **Reminder Channel Effectiveness** | $\chi^2 = 27.52$ | $1.56 \times 10^{-7}$ | Rejects null hypothesis; reminders provide a statistically significant attendance boost ($p < 0.001$). |
| **Booking Lead Time Impact** | $t = -15.87$ | $2.31 \times 10^{-55}$ | Rejects null hypothesis; longer lead times significantly increase missed appointment risk ($p < 0.001$). |
| **Clinic Wait Time Drop-off** | $t = -12.82$ | $5.06 \times 10^{-37}$ | Rejects null hypothesis; wait times >30 minutes cause significant patient drop-off ($p < 0.001$). |

---

### 2. Segment & Feature Insights

* **Lead Time Non-Linearity:** No-show rates stay relatively stable (36%–47%) for short lead times (0–7 days). Once lead time exceeds 21 days, the no-show rate spikes sharply to ~63%–65%.
* **Queue Bottleneck Impact:** Wait times exceeding 30 minutes significantly correlate with patient drop-off, particularly among senior age cohorts.

---

### 3. Data Analytics → Data Science Cross-Track Handoff

* **Track Collaborated With:** Data Science & Machine Learning Engineering
* **Project Dependency:** Candidate feature selection and risk threshold validation
* **Information Received:** Baseline model residual error metrics (high false-negative rate on long lead-time appointments)
* **Information Provided:** Engineered feature matrix (`HealthConnect_Feature_Engineered_Segments.csv`) containing non-linear binned lead times (`lead_time_bracket`), age cohorts (`age_group`), and high-wait flags (`high_wait_flag`)
* **Activity Completed:** Statistical validation and non-linear segmentation of primary risk drivers
* **What Changed:** Data Science updated their feature schema with binned risk features, improving model recall on high-risk no-shows
* **Verifiable Evidence:** `HealthConnect_Feature_Engineered_Segments.csv` artifact and repo commit logs

---
