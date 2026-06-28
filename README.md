# Healthcare Operations & Patient No-Show Analysis 🏥

## Executive Summary
Clinic idle-time costs healthcare providers roughly $150/hour. This Power BI project analyzes **110,527 medical appointments** in Brazil to isolate the root drivers of patient non-attendance and optimize scheduling workflows.

![Executive Dashboard](./docs/dashboard_exec.png)

---

## Business Problem
The clinic was operating at an overall **20.19% No-Show rate**, generating massive sunk labor costs and artificially inflated waitlists. The objective of this project was to investigate three operational bottlenecks:
1. Does booking lead-time directly impact attendance?
2. Which patient demographic cohorts require targeted intervention?
3. Are automated SMS reminders actually driving attendance?

## The Data Model (Star Schema)
Rather than relying on an unoptimized flat CSV, the raw data was transformed via Power Query into a normalized **One-to-Many Star Schema**:

![Data Model](./docs/data_model.png)

* **`Fact_Appointments`**: Houses transactional scheduling dates, lead-time calculations, and attendance flags.
* **`Dim_Patient`**: Houses unique patient demographic profiles (Age groups, Welfare scholarship status, Chronic conditions).

---

## Key Findings & Strategic Recommendations

### 1. The "7-Day" Cliff 
* **The Insight:** Same-day bookings hold a negligible no-show rate (4.1%). However, once the lead time between booking and the appointment crosses **7 days**, the no-show rate spikes to **>30%**.
* **Actionable Recommendation:** Institute a dynamic scheduling policy. Any appointment booked >10 days in advance must trigger an automated automated verification ping at the 48-hour mark; unconfirmed pings forfeit the slot to the daily waitlist.

### 2. The SMS Confounding Trap
* **The Insight:** On paper, patients who received an SMS reminder had a *higher* no-show rate than those who didn't. 
* **The Statistical Reality:** This is classic selection bias. The clinic exclusively sent SMS nudges to high-risk, long-lead-time bookings. When isolated strictly for the 15+ day lead cohort, SMS reminders **reduced non-attendance by 4.2%**.

---
## Repository Navigation
* `/data` : Raw Kaggle source dataset
* `/docs` : Dashboard canvas captures & schema wireframes
* `/src`  : Source `.pbix` Power BI file
