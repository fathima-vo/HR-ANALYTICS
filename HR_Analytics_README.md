# 👥 HR Analytics Dashboard – Power BI

An interactive Power BI dashboard that analyzes workforce headcount, hiring, attrition, compensation, performance and employee satisfaction for **2,000 employees** across **8 departments**, **29 job roles** and **7 cities** (Jan 2023 – Dec 2026).

## 💡 Project Purpose
This dashboard helps HR teams and management make **data-driven people decisions**. It turns raw HR records into clear insights so they can:
- Track headcount, hiring and attrition trends over time
- Find high-attrition departments and the main reasons employees leave
- Plan retention strategies around career growth, pay and work-life balance
- Monitor workforce health through performance, satisfaction, overtime and training data

**Who can use it:** HR managers, department heads, leadership and recruiters.

## 🎯 Business Questions Answered
- What is the total headcount and overall attrition rate?
- How many employees joined and left in a given period?
- Which departments, roles, age groups and locations have the highest attrition?
- Why do employees leave (exit reason, voluntary vs. involuntary)?
- How do salary, job satisfaction, work-life balance, overtime and training relate to retention?
- Who are the most and least experienced employees?

## 🗂️ Data Model (Star Schema)

```
                 ┌──────────────┐
                 │   Dim_Date   │
                 └──────┬───────┘
                        │
┌──────────────┐  ┌─────┴────────────┐  ┌──────────────┐
│   Dim_Job    ├──┤  Fact_HR_Monthly ├──┤ Dim_Employee │
└──────────────┘  └──────────────────┘  └──────────────┘
```

| Table | Description |
|---|---|
| **Fact_HR_Monthly** | Monthly employee records: headcount, joiner/leaver flags, annual CTC, monthly income, performance rating, job satisfaction, work-life balance, overtime flag, training hours |
| **Dim_Employee** | Gender, age & age group, marital status, education, city, state, hire/exit date, experience, distance from home, status, exit reason & type |
| **Dim_Job** | Department, job role, job level |
| **Dim_Date** | Year, quarter, month, fiscal year & fiscal quarter |

Relationships are one-to-many from each dimension to the fact table using `Date_Key`, `Employee_Key` and `Job_Key`.

## 📐 Key DAX Measures

| Measure | Purpose |
|---|---|
| `total_employee` | Distinct count of all employees |
| `active_employees` | Employees currently active |
| `attrition` | Total employees − active employees |
| `attrition_rate` | Attrition ÷ total employees |
| `new_hires` | Total joiners in the selected period |
| `leavers` | Total leavers in the selected period |
| `employee_count` | Distinct employees in the selected period |
| `top_bottom` | Dynamic Top/Bottom N employees by experience |

## ⚙️ Main Concepts Used
- **Star schema modeling** – one fact table connected to dimension tables
- **Power Query transformations** – data type fixes, conditional column for active/exited status, combined name-ID label
- **Dedicated measure table** – all KPIs kept in one place
- **Dynamic Top/Bottom N** – a slicer to pick *Top* or *Bottom* plus a parameter (1–20), using `RANKX` and `ALLSELECTED`
- **Date dimension with fiscal calendar** – for time-based analysis by year, quarter and month

## 📊 Key Insights
- Overall attrition rate is **~32.55%** (651 of 2,000 employees have exited)
- **Engineering** (166) and **Sales** (141) have the most leavers, together about **47%** of all exits
- **Career Growth** (150) and **Better Compensation** (143) are the top exit reasons, together about **45%** of all exits, so growth paths and pay are the main retention levers
