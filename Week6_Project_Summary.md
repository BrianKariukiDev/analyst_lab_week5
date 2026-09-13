# AnalystLab Africa Week 6 Project Summary
**Track:** Data Analytics  
**Intern:** Brian Kariuki  
**Project:** HealthConnect Clinic Experience Lab  

---

### 1. Objectives & Achievements
* **Planned:** Validate Week 5 baseline KPIs statistically, perform cohort segment analysis, and engineer non-linear features for cross-track handoff.
* **Completed:** Executed Chi-Square and T-test statistical validations, completed lead-time vs. age cohort interactions, and generated `HealthConnect_Feature_Engineered_Segments.csv`.

### 2. Week 5 → Week 6 Progress & Integration
* **Improvements:** Shifted from basic EDA to formal hypothesis validation and non-linear risk feature extraction.
* **Cross-Track Collaboration:** Partnered with Data Science and ML Engineering to address baseline model misclassifications.
* **Handoff Artifacts:** Shared binned lead-time brackets (`0-7d`, `8-21d`, `22-45d`, `45d+`) and high-wait binary flags (`>30m`), improving model prediction recall for long-lead appointments.

### 3. Key Findings & Next Steps
* **Statistical Validation:** All core risk drivers (lead times, wait times, reminder channels) were validated with $p < 0.001$.
* **Week 7 Plan:** Support end-to-end testing of model predictions against analytical segment thresholds and refine decision-support dashboards.