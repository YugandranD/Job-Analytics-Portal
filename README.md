# 📊 Job Portal Analysis — Tableau Data Visualization Project

## Project Overview

| Field | Details |
|---|---|
| **Project Name** | Job Portal Analysis |
| **Tool** | Tableau Desktop 2026 |
| **Dataset** | Job Description Dataset — Kaggle |
| **Dataset Author** | Ravindra Singh Rana |
| **Dataset URL** | https://www.kaggle.com/datasets/ravindrasinghrana/job-description-dataset |
| **Total Tasks** | 6 Visualizations |
| **Submission Date** | 14 May 2026 |
| **Output File** | Job_Portal_Analysis.twbx |

---

## 📁 Project Files

```
Job_Portal_Analysis/
│
├── Job_Portal_Analysis.twbx        ← Main Tableau packaged workbook
├── Job_Portal_Analysis_Report.docx ← Full project report
├── README.md                       ← This file
└── job_descriptions.csv            ← Source dataset (from Kaggle)
```

---

## 📋 Tasks Summary

| Task | Chart Type | Key Filter | Display Time |
|---|---|---|---|
| Task 1 | Bar Chart | Work Type = Intern | 3–5 PM IST |
| Task 2 | Scatter Plot | Job Title = Mechanical Engineer | 3–5 PM IST |
| Task 3 | Tree Map | Role = Data Engineer, Top 10 | 3–5 PM IST |
| Task 4 | Map + Drilldown | Africa, Qualification = B.Tech/M.Tech/PhD | 3–6 PM IST |
| Task 5 | Stacked Bar | India vs Germany, Data Scientist/Art Teacher/Aerospace Engineer | 3–5 PM IST |
| Task 6 | Box Plot | Work Type = Intern, Salary Distribution | 3–5 PM IST |

---

## 📌 Task Details

### Task 1 — Preference vs Work Type (Bar Chart)
- **Chart:** Bar Chart sorted descending by count
- **Columns:** Preference
- **Rows:** CNT(Job Id)
- **Filters:**
  - Work Type = Intern
  - Latitude < 10
  - Country not starting with A, B, C, D
  - Job Title = single word, < 10 characters
  - Company Size < 50,000
  - Salary > $9,000
  - Experience = even number
  - Job Posting Month = odd (Jan, Mar, May, Jul, Sep, Nov)
  - Time: 3 PM – 5 PM IST

---

### Task 2 — Company Size vs Company Name (Scatter Plot)
- **Chart:** Scatter Plot
- **Columns:** Company Name
- **Rows:** Company Size
- **Filters:**
  - Job Title = exactly "Mechanical Engineer"
  - Company Size < 50,000
  - Experience > 5 years
  - Country = Asia, not starting with "I"
  - Salary > $50,000
  - Work Type = Full-Time or Part-Time
  - Preference = Male
  - Job Portal = Idealist
  - Company Name has at least 2 vowels
  - Time: 3 PM – 5 PM IST

---

### Task 3 — Top 10 Companies (Tree Map)
- **Chart:** Tree Map
- **Size:** Count of postings
- **Color:** Company Name
- **Filters:**
  - Role = Data Engineer
  - Job Title = Data Scientist
  - Exclude Asian countries
  - Exclude countries starting with "C"
  - Latitude < 10
  - Preference = Female
  - Qualification = B.Tech
  - Job Posting Date: 01/01/2023 – 06/01/2023
  - Job Portal = LinkedIn
  - Company Size ≥ 10,000
  - Contact Person name ends with a vowel
  - Top 10 by count
  - Time: 3 PM – 5 PM IST

---

### Task 4 — Qualification Drilldown Map (Map with Click)
- **Chart:** Geographic Map with Dashboard Drilldown Action
- **Plot:** Latitude & Longitude
- **Color:** Qualifications
- **Filters:**
  - Qualification = B.Tech, M.Tech, or PhD
  - Work Type = Full-Time
  - Country = Africa only
  - Job Title starts with "D"
  - Preference = Male
  - Company Size > 80,000
  - Contact Person starts with "A"
  - Job Portal = Indeed
  - Salary > $20,000
  - Time: 3 PM – 6 PM IST
- **Drilldown:** Click on map point → filters Detail Map sheet to exact location

---

### Task 5 — India vs Germany Comparison (Stacked Bar)
- **Chart:** Stacked Bar Chart
- **Columns:** Job Title
- **Rows:** CNT(Job Id)
- **Color:** Country (India = Orange #E07B39, Germany = Green #2E8B57)
- **Filters:**
  - Country = India, Germany
  - Qualification = B.Tech
  - Work Type = Full-Time
  - Experience > 2 years
  - Job Title = Data Scientist, Art Teacher, Aerospace Engineer
  - Salary > $10,000
  - Job Portal = Indeed
  - Preference = Female
  - Job Posting Date before 08/01/2023
  - Location not blank
  - Company Name > 8 characters
  - Time: 3 PM – 5 PM IST

---

### Task 6 — Work Type Salary Distribution (Box Plot)
- **Chart:** Box-and-Whisker Plot
- **Columns:** Work Type
- **Rows:** AVG(Salary Min)
- **Detail:** Job Id
- **Filters:**
  - Work Type = Intern
  - Latitude < 10
  - Country not starting with A, B, C, D
  - Job Title = single word, < 10 characters
  - Company Size < 50,000
  - Salary > $8,000
  - Experience = even number
  - Job Posting Date year = 2021, 2022, or 2023
  - Contact Person name contains at least one "e"
  - Time: 3 PM – 5 PM IST

---

## 🧮 Calculated Fields

| Field Name | Formula | Tasks |
|---|---|---|
| Salary Min | `FLOAT(REPLACE(REPLACE(TRIM(SPLIT([Salary Range],'-',1)),'$',''),'K',''))*1000` | All |
| Experience Min | `INT(SPLIT([Experience],' ',1))` | 1,2,5,6 |
| Even Experience | `INT(SPLIT([Experience],' ',1)) % 2 = 0` | 1,6 |
| Odd Posting Month | `MONTH([Job Posting Date]) % 2 = 1` | 1 |
| Single-word Job Title | `FIND([Job Title],' ')=0 AND LEN([Job Title])<10` | 1,6 |
| Country Filter (not ABCD) | `LEFT(UPPER([Country]),1) != 'A' AND != 'B' AND != 'C' AND != 'D'` | 1,6 |
| Company Name Vowels ≥ 2 | Vowel count using LEN-REPLACE method | 2 |
| Asian Country not I | Country IN Asian list AND LEFT != 'I' | 2 |
| Exclude Asia & C | Country not in Asian list AND LEFT != 'C' | 3 |
| Contact Ends Vowel | `RIGHT(LOWER(TRIM([Contact Person])),1) IN ('a','e','i','o','u')` | 3 |
| Job Title Starts D | `LEFT(UPPER([Job Title]),1) = 'D'` | 4 |
| Contact Starts A | `LEFT(UPPER([Contact Person]),1) = 'A'` | 4 |
| Company Name > 8 | `LEN(TRIM([Company Name])) > 8` | 5 |
| Location Not Blank | `NOT ISNULL([Location]) AND TRIM([Location]) != ''` | 5 |
| Contact Contains E | `CONTAINS(LOWER([Contact Person]),'e')` | 6 |
| Posting Year 2021-23 | `YEAR([Job Posting Date])>=2021 AND YEAR([Job Posting Date])<=2023` | 6 |
| Time Restriction 3-5 PM | `DATEPART('hour',NOW())>=15 AND DATEPART('hour',NOW())<17` | 1,2,3,5,6 |
| Time Restriction 3-6 PM | `DATEPART('hour',NOW())>=15 AND DATEPART('hour',NOW())<18` | 4 |

---

## 🗺️ Dashboard Setup

The single dashboard **"Job Portal Analysis Dashboard"** contains all 6 sheets:

```
┌──────────────────┬──────────────────┬──────────────────┐
│   Task 1         │   Task 2         │   Task 3         │
│   Bar Chart      │   Scatter Plot   │   Tree Map       │
├──────────────────┼──────────────────┼──────────────────┤
│   Task 4         │   Task 4         │   Task 5  Task 6 │
│   Main Map       │   Detail Map     │   Stacked  Box   │
│                  │   (Drilldown)    │   Bar      Plot  │
└──────────────────┴──────────────────┴──────────────────┘
```

### Dashboard Action (Task 4 Drilldown):
- **Type:** Filter
- **Source:** Main map sheet
- **Target:** Detail map sheet
- **Run on:** Select (click)
- **Filter Field:** Job Id
- **Clear selection:** Show all values

---

## ⏰ Time Restriction

All charts are restricted to display only during specific IST time windows.

> ⚠️ If viewing outside 3–5 PM IST, the charts will show no data. This is expected behavior as per project requirements.

| Tasks | Window |
|---|---|
| Tasks 1, 2, 3, 5, 6 | 3:00 PM – 5:00 PM IST |
| Task 4 | 3:00 PM – 6:00 PM IST |

---

## 🔧 How to Open

1. Download `Job_Portal_Analysis.twbx`
2. Double-click to open in **Tableau Desktop**
3. All data is embedded — no separate CSV needed
4. Open between **3 PM and 5 PM IST** to see all charts
5. Navigate to the **Dashboard** tab to see all 6 visualizations

---

## ⚠️ Known Limitations

- The dataset has limited rows satisfying all filter conditions simultaneously for some tasks — this is expected
- Salary Range is stored as text (e.g. $55K–$80K); Salary Min calculated field extracts the numeric lower bound
- Experience is stored as text (e.g. "2 to 5 Years"); Experience Min extracts the numeric value
- No Continent column in dataset — Asian and African countries are filtered using manual country lists
- Time restriction uses system clock — ensure Tableau is running in IST timezone

---

## 👤 Project Information

- **Project:** Job Portal Analysis
- **Tool:** Tableau Desktop 2026
- **Dataset:** Kaggle — Job Description Dataset by Ravindra Singh Rana
- **Submission:** 14 May 2026
