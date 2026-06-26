<div align="center">
 
# 📊 Student Performance Dashboard

### Academic Performance & Attendance Analysis — Power BI

<br>


[![Typing SVG](https://readme-typing-svg.demolab.com?font=Fira+Code&size=22&pause=1000&color=0B3D91&center=true&vCenter=true&width=600&lines=Turning+Raw+Student+Data+into+Insights...;Built+with+Power+BI+%2B+DAX+%2B+Power+Query;Welcome+to+the+Student+Performance+Dashboard!)](https://git.io/typing-svg)

</div>

---

## 🗂️ Table of Contents

- [Overview](#-overview)
- [Dataset](#-dataset)
- [Data Model](#-data-model)
- [Dashboard Preview](#-dashboard-preview)
- [DAX Measures](#-dax-measures)
- [Visualizations](#-visualizations)
- [Interactivity Features](#-interactivity-features)
- [Steps Performed (.pbix Build Process)](#-steps-performed-pbix-build-process)
- [Project Structure](#-project-structure)
- [Tools & Tech Stack](#-tools--tech-stack)
- [Author](#-author)

---

## 📌 Overview

The **Student Performance Dashboard** is an interactive **Power BI** report that analyzes the **academic performance, attendance, and behavior** of 1,000 students across multiple classes, subjects, and exam terms. It was built as a practical exam project to demonstrate skills in **data modeling, DAX, visualization, and storytelling**.

The dashboard helps teachers and administrators quickly identify:
- 🎯 Which subjects or classes are underperforming
- 📅 Attendance trends and irregularities
- 🧠 Behavioral patterns across students
- 📈 Performance trends term over term

---


## 📁 Dataset

The report is built on four relational CSV datasets:

| File | Columns | Records |
|------|----------|---------|
| `Students.csv` | `StudentID`, `Name`, `Gender`, `Class`, `Section` | 1,000 |
| `Scores.csv` | `StudentID`, `Subject`, `ExamType`, `Score`, `MaxScore`, `Term` | 30,000 |
| `Attendance.csv` | `StudentID`, `Date`, `Status` (Present/Absent), `Reason` | 100,000 |
| `Behavior.csv` | `StudentID`, `Date`, `BehaviorType`, `Notes` | 6,500 |

> 💡 `StudentID` is the common key linking all four tables together.

---

## 🧩 Data Model

A **star-schema** style model was created in Power BI, with `Students` as the central dimension table connected to three fact tables (`Scores`, `Attendance`, `Behavior`) via one-to-many relationships on `StudentID`.

<img width="860" height="682" alt="Model View" src="https://github.com/user-attachments/assets/13e6d8cc-91b7-4169-b89e-7aeb6eadd7d2" />


**Relationships:**
- `Students[StudentID]` → `Scores[StudentID]` (1 → *)
- `Students[StudentID]` → `Attendance[StudentID]` (1 → *)
- `Students[StudentID]` → `Behavior[StudentID]` (1 → *)

---

## 🖥️ Dashboard Preview

<img width="1323" height="746" alt="Dashboard Preview" src="https://github.com/user-attachments/assets/c2dc3bd7-43e4-4886-8a39-181dd283be6f" />


The main **Academic Dashboard** page includes KPI cards, subject/class-wise performance bars, attendance status donut chart, performance trend line, and a detailed student-level score table with conditional formatting.

The report also includes **Behavioural Insights** and **Student Profile** drillthrough pages, accessible from the left navigation pane.

---

## 🧮 DAX Measures

The following calculated fields and measures were created to power the visuals:

```dax
Score % = DIVIDE(SUM(Scores[Score]), SUM(Scores[MaxScore]))

Average Score per Subject =
AVERAGEX(VALUES(Scores[Subject]), [Score %])

Attendance % =
DIVIDE(
    CALCULATE(COUNTROWS(Attendance), Attendance[Status] = "Present"),
    COUNTROWS(Attendance)
)

Behavior Count per Type =
CALCULATE(COUNTROWS(Behavior), ALLEXCEPT(Behavior, Behavior[BehaviorType]))

Performance Category =
SWITCH(
    TRUE(),
    [Score %] >= 0.8, "High",
    [Score %] >= 0.4, "Medium",
    "Low"
)
```

---

## 📊 Visualizations

| Visual Type | Purpose |
|---|---|
| 📶 **Bar Chart** | Average scores by Subject and Class |
| 📈 **Line Chart** | Performance trend across Terms |
| 🍩 **Donut Chart** | Attendance status & Behavior type distribution |
| 📋 **Table** | Student-wise scores with conditional formatting (green ≥ 80%, red < 40%) |
| 🧾 **Card Visuals** | KPIs — Total Students, Average Attendance, Average Score, Total Behavioural Records, Total Subjects |

---

## 🎛️ Interactivity Features

- 🔍 **Slicers** for Class, Section, Subject, and Term
- 🔗 **Drillthrough page** for individual student profiles
- 🧭 **Bookmark navigation** to switch between Academic and Behavioral views
- 🖱️ **Tooltips** with mini charts and metrics on hover

---

## 🛠️ Steps Performed (.pbix Build Process)

The dashboard was built end-to-end in Power BI Desktop following this workflow:

1. **Data Collection** — Organized the four source files (`Students.csv`, `Scores.csv`, `Attendance.csv`, `Behavior.csv`) inside a dedicated `Datasets` folder.
2. **Data Import** — Loaded all CSV files into Power BI using **Get Data → Text/CSV**.
3. **Data Cleaning (Power Query)** — Renamed columns consistently, corrected data types (dates, numbers, text), and handled null/missing values where appropriate.
4. **Data Modeling** — Built relationships between `Students` (1) and `Scores`, `Attendance`, `Behavior` (each *) using `StudentID` as the key, forming a star schema.
5. **DAX Measures** — Created calculated measures: `% Score`, `Average Score per Subject`, `Attendance %`, `Behavior Count per Type`, and `Performance Category` (using `SWITCH`/`IF`).
6. **Report Page 1 – Academic Dashboard** — Added KPI cards, bar charts (score by subject/class), donut chart (attendance status), and line chart (performance trend by term).
7. **Report Page 2 – Behavioural Insights** — Visualized behavior type distribution and trends using donut/bar charts.
8. **Report Page 3 – Student Profile (Drillthrough)** — Configured a drillthrough page to view individual student details on click.
9. **Conditional Formatting** — Applied color rules to the score table (green for high scores, red for low scores).
10. **Slicers & Filters** — Added slicers for Class, Section, Subject, and Term to enable dynamic filtering.
11. **Bookmarks & Navigation** — Set up bookmarks and a navigation pane to toggle between report views.
12. **Tooltips** — Designed custom tooltip pages with mini visuals for richer hover details.
13. **Testing & Validation** — Verified that all visuals interacted correctly with slicers and drillthroughs.
14. **Export & Save** — Saved the final report as `Student_Performance_Dashboard.pbix` and exported a PDF snapshot (`Student_Performance_Report.pdf`).

---

## 📦 Project Structure

```
Power BI/Exam/
│
├── Assets/
│   └──All Icons
│
├── Datasets/
│   ├── Students.csv
│   ├── Scores.csv
│   ├── Attendance.csv
│   └── Behavior.csv
│
├── Screenshots/
│   ├── Dashboard Preview.png
│   ├── Drill-Through Effect.png
│   └── Model View.png
│
├── README.md
│
├── Student_Performance_Dashboard.pbix
└── Student_Performance_Report.pdf
```

---

## ⚙️ Tools & Tech Stack

[![Power BI](https://img.shields.io/badge/Power%20BI%20Desktop-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)](https://powerbi.microsoft.com/)
[![Power Query](https://img.shields.io/badge/Power%20Query-217346?style=for-the-badge&logo=microsoftexcel&logoColor=white)](https://learn.microsoft.com/en-us/power-query/)
[![DAX](https://img.shields.io/badge/DAX-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)](https://learn.microsoft.com/en-us/dax/)
[![CSV](https://img.shields.io/badge/CSV-Data%20Source-4CAF50?style=for-the-badge&logo=googlesheets&logoColor=white)]()

---

<div align="center">

## 👤 Author

[![Author](https://img.shields.io/badge/Author-RENSEE%20GAJIPARA-blueviolet?style=for-the-badge)]()
[![LinkedIn](https://img.shields.io/badge/LinkedIn-rensee--gajipara-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/rensee-gajipara)

</div>
